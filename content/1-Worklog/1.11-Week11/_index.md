---
title: "Week 11 Worklog"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 1.11. </b> "
---

### Week 11 Objectives:

* Study and deploy a secure static website hosting architecture on AWS using Amazon S3 and CloudFront, focusing on content delivery optimization, HTTPS enforcement, and secure access control through Origin Access Control (OAC)
* Explore and implement database credential management using AWS Secrets Manager, configure automatic Secret Rotation, and validate secure access to Amazon RDS from AWS Fargate containers following security best practices
* Design and test a serverless order-processing workflow using Amazon SQS, SNS, and DynamoDB, ensuring reliable message handling, notification delivery, data persistence, and scalable system architecture
* Standardize the SOC Console data architecture by separating Demo, Replay, and Live operating modes while improving realtime data processing, connection-state management, and multi-source integration capabilities

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
|  2  | - Secure Static Website Deployment with Amazon S3 and CloudFront | 29/06/2026 | 29/06/2026 | <https://000094.awsstudygroup.com/> |
|  3  | - Managing RDS Credentials with AWS Secrets Manager, Secret Rotation, and RDS Access from AWS Fargate | 30/06/2026 | 30/06/2026 | <https://000096.awsstudygroup.com/> |
|  4  | - Serverless Order Processing with SQS, SNS, and DynamoDB | 01/07/2026 | 01/07/2026 | <https://000083.awsstudygroup.com/> |
|  5  | - Implementing Multi-Mode Data Architecture Demo / Replay / Live for the SOC Console | 02/07/2026 | 02/07/2026 |


### Week 11 Achievements:

### Work completed in the FCAJ Hybrid SOC/AWS project

* Updated the **SOC Console** frontend so that its data source is no longer tied to one fixed flow and can explicitly run in `demo`, `replay`, or `live` mode through the `VITE_DATA_MODE` setting.
* Modified `App.tsx`, `useSocket.ts`, and `RealtimeIncidentStream.tsx` to synchronize connection state, prevent duplicate WebSocket connections, and display the latest alerts first.
* Adjusted the Network Monitoring, AI Threat Detection, and Threat Hunting views to consume Zeek, Suricata, and AI model outputs according to the selected operating mode.
* Added supporting FastAPI backend endpoints (`/api/status`, `/api/events`, `/api/replay/demo`, `/ws/alerts`) and demo users to test authentication, replay, and realtime flows.
* Validated the frontend–backend flow and prepared the SOC Console for demonstrations with mock data, historical replay, or a connection to the Local Security Lab.

The first three days focused on AWS labs that reinforced security, serverless, and data-pipeline knowledge. Thursday's SOC Console work was the direct project contribution for the week.

## Monday: CLOUDFRONT WITH S3 BUCKET ORIGIN
* **Introduction**
  * Learn how to **host static website content** on an **Amazon S3 bucket**, then use **Amazon CloudFront** to secure and accelerate content delivery.

* **Objectives**
  * Learn how to combine S3 + CloudFront
  * Apply security best practices based on the AWS Well-Architected Framework
  * Build a production-ready static website architecture

* **Prerequisites**
  * AWS account (AWS Free Tier or test account)
  * IAM permissions for Amazon S3 and Amazon CloudFront
  * Basic knowledge of the AWS Console

* **Cost**
  * Usually **under $1/month** if used only for learning purposes and properly cleaned up (teardown) afterward

* **Implementation Steps**
* **Create an S3 Bucket and Upload Content**
  * **Go to the S3 Console → Create bucket**
    * Enter a bucket name (for example: `my-static-site-000094` – must be globally unique)
    * Select the appropriate Region
    * **Block all public access** = OFF (or configure later)

  * **Upload files:**
    * Create a simple `index.html` file:
    ```html
    <!DOCTYPE html>
    <html>
    <head><title>My Static Site</title></head>
    <body><h1>Hello from S3 + CloudFront!</h1></body>
    </html>
    ```
    * Upload `index.html` and any additional files (CSS, JS, images)

  * **Enable Static Website Hosting:**
    * Properties → Static website hosting → Enable
    * Index document: `index.html`
    * Save the Website Endpoint URL

* **Create a CloudFront Distribution**
  * Go to the CloudFront Console → Create distribution
  * Origin settings:
    * Origin domain: Select the S3 bucket (or enter it manually)
    * Origin access: Choose Origin Access Control (OAC) (recommended)

  * Create a new OAC if one does not already exist:
    * Signing behavior: Sign requests
    * Update the S3 bucket policy automatically or manually

  * Behavior settings:
    * Viewer protocol policy: Redirect HTTP to HTTPS
    * Cache policy: CachingOptimized
    * Compress objects: Yes

  * Settings:
    * Alternate domain names (if using a custom domain)
    * Custom SSL certificate (ACM)

  * Create the distribution (deployment takes approximately 5–10 minutes)

* **Configure Security (Bucket Policy + OAC)**
  * Update the S3 Bucket Policy to allow access only from CloudFront:
  ```json
  {
      "Version": "2012-10-17",
      "Statement": [
          {
              "Effect": "Allow",
              "Principal": {
                  "AWS": "arn:aws:iam::cloudfront:user/CloudFront Origin Access Identity XXXXX"
              },
              "Action": "s3:GetObject",
              "Resource": "arn:aws:s3:::my-static-site-000094/*"
          }
      ]
  }
  ```
  * (Replace with the ARN associated with your OAC)

* **Testing**
  * Access the CloudFront URL (for example: `https://dxxxxxx.cloudfront.net`)
  * Verify performance, HTTPS functionality, and confirm that direct access to the S3 bucket is blocked

* **Cleanup**
  * Delete the CloudFront Distribution
  * Delete the S3 Bucket and all objects inside it

## Tuesday: Hands-on with AWS Secrets Manager, Secret Rotation, and RDS Access from Fargate
* **Objectives**
  * Access the RDS Database through Secrets Manager
  * Perform **Secret Rotation** (periodically change passwords)
  * Access RDS from an application running on **AWS Fargate**

* **AWS Services Used**
  * Amazon RDS (MySQL)
  * AWS Secrets Manager
  * AWS Fargate + ECS + ECR
  * Amazon EC2 (Bastion Host)
  * Amazon VPC
  * AWS CloudFormation
  * AWS Systems Manager Session Manager

* **Architecture**
  * VPC with 2 Subnets
  * **Bastion Host** (EC2 Amazon Linux 2) for running scripts
  * **Private RDS Instance**
  * **Fargate Tasks** for testing connectivity from containers

* **Hands-on Labs**
  * **Infrastructure Preparation**
    * Use **AWS CloudFormation** to create a stack named `smdemo` in the **us-east-1** region
    * Template URL: `https://s3.amazonaws.com/sa-security-specialist-workshops-us-east-1/secrets-manager-workshop/RDSFargate.yml`
    * Record the following **Stack Outputs**:
      * `BastionIP`
      * `DBInstance`, `DBUser`, `DBPassword`
      * `EC2UserPassword`
      * `ECRRepository`, `ECSCluster`

  * **Using Secrets Manager with RDS**
    * Secure RDS credentials
    * Create a Secret in Secrets Manager and select the RDS database secret type
    * Associate the secret with the RDS Instance

  * **Accessing RDS from the Bastion Host**
    * Connect using **Session Manager**
    * Run the following scripts:
      * `mysql.oldway.sh` (hard-coded password)
      * `mysql.newway.sh` (retrieves the secret dynamically using AWS CLI and jq)

  * **Secret Rotation**
    * Enable automatic rotation (for example, every 30 days)
    * Secrets Manager uses Lambda to rotate the password and update RDS automatically

  * **Validation After Rotation**
    * The old script will fail
    * The new script will continue to access the database successfully

  * **Using Secrets Manager with Fargate**
    * Build and push the Docker image
    * From the Bastion Host, run:
      * `dockerbuild.sh`
      * `dockertagandpush.sh`

  * **Configure Fargate**
    * Edit the Task Definition and add the Secret ARN as an Environment Variable
    * Run the Task on Fargate

  * **Access & Testing**
    * Connect to the Fargate container
    * Run the updated script to connect to the RDS database

* **Clean Up**
  * Run `./cleanup.sh` from the Bastion Host
  * Delete the Secret from Secrets Manager
  * Delete the CloudFormation stacks

## Wednesday: Order Processing and Management with SQS, SNS, and DynamoDB
* **Overview**
  * When a user places an order (Checkout), the system sends the order information to an SQS queue and publishes a notification through an SNS topic to notify the admin.
  * Admins can view the order list, Handle (process) orders (save them to DynamoDB and remove them from the queue), or Delete orders.

* **Main Architecture:**
  * POST /books/order: Place an order → send to SQS queue + publish SNS notification
  * GET /books/order: Admin retrieves the list of orders from DynamoDB
  * POST /books/order/handle: Process an order → save to DynamoDB + remove from queue
  * DELETE /books/order: Delete an order from the queue

* **Main Content Sections**
  * **Preparation:**
    * Download the source code fcj-book-store-sam-ws6.zip
    * Edit template.yaml (replace the domain, uncomment the CloudFront + Certificate section if needed)
    * Deploy SAM (sam build, sam deploy --guided)
    * Clone the FCJ-Serverless-Workshop frontend repository, set isAdmin: true, build, and upload it to S3
    * Configure DNS in Route 53

  * **Create APIs & Lambda Functions:**
    * Create the OrdersTable DynamoDB table (partition key: id, sort key: book_id)
    * Create the following Lambda functions:
      * checkout_order
      * order_management
      * handle_order
      * delete_order
    * Integrate them with API Gateway

  * **Testing the Workflow:**
    * Get the Invoke URL from API Gateway
    * Update the frontend configuration, rebuild, and upload it to S3 again
    * Add sample books, add them to the cart, and perform checkout
    * Verify messages in the SQS queue
    * Receive SNS email notifications
    * Admin views Orders, Handles orders (verify records in DynamoDB), and Deletes orders

  * **Resource Cleanup:**
    * Delete Route 53 records
    * Empty S3 buckets
    * Delete CloudFormation stacks
    * Delete the SQS queue and SNS topic

## Thursday: Standardizing Data Flow and Realtime Operations for the SOC Console
* **Primary Objective:**
  * Improve the SOC console frontend architecture to clearly separate **demo mode**, **replay mode**, and **live mode**, making the system more flexible for demonstrations, historical data testing, and real-time integration with backend/local lab environments.

* **Main Frontend Changes**
  * **Environment Configuration (`.env.example`)**
    * Add detailed comments explaining `VITE_DATA_MODE`
    * Valid values: `demo`, `replay`, `live`
    * Production builds require an explicitly defined value to prevent runtime issues

  * **App.tsx (Core Application Logic)**
    * Integrate `dataMode` from the `useSocket` hook into application state management
    * Improve routing logic and authentication flow when switching between modes
    * Handle post-login/register redirects to the appropriate dashboard based on the current mode
    * Optimize re-renders and state synchronization across child components

  * **Socket & Realtime Handling (`useSocket.ts`, `RealtimeIncidentStream.tsx`)**
    * Extend the `useSocket` hook to support multiple modes:
      * **Demo mode**: Use a mock WebSocket server (`server.ts`)
      * **Live mode**: Connect directly to the FastAPI WebSocket endpoint (`/ws/alerts`)
      * **Replay mode**: Support playback of historical data from the backend
    * Add `socketStatus`, `platformStatus`, and `error` states for clearer visibility
    * Prevent duplicate socket connections when switching modes

  * **Updated Dashboard Components**
    * **NetworkMonitoringPage.tsx**, **AIThreatDetectionPage.tsx**, **ThreatHuntingPanel.tsx**: Support mode-aware data rendering
      * **RealtimeIncidentStream.tsx**: Improve real-time alert streaming with priority on the latest alerts
      * **DatasetMismatchPanel.tsx**, **SuricataCenter.tsx**, **AttackReplayCampaignPanel.tsx**: Integrate mode-aware logic
      * **FlowDetailPanel.tsx**, **ExplainabilityCenter.tsx**: Display event details according to the data source (Zeek, Suricata, AI models)

  * **Auth & User Management**
    * Update `authService.ts` and related forms (`LoginForm.tsx`)
    * Support demo credentials and localStorage-based registration
    * Add mock backend endpoints for `/api/auth/*`

* **Backend Changes (Mode Support)**
  * **main.py**:
    * Add CORS support and demo authentication users
    * Enhance `/api/status`, `/api/events`, and `/api/replay/demo`
    * Add `_encode_demo_token` function for JWT-like demo tokens
  * Support event ingestion from multiple sources (Zeek conn logs, HTTP logs, Suricata)

* **Overall Improvements**
  * **Flexibility**:
    * Easily switch between mock data (quick demos), replay logs (scenario testing), and live data (production-like environments)

  * **UX/UI**:
    * Clearly display connection status (connected/disconnected)
    * Ensure KPI widgets, alert feeds, and MITRE mappings function consistently across all modes

  * **Developer Experience**:
    * Provide detailed frontend setup and execution instructions in the README
    * Clearly separate the mock server (`server.ts`) from the production backend

  * **Multi-Model Integration**:
    * Support visualization of outputs from AI1 (Anomaly Detection), AI2A (Network Classification), AI2B (HTTP Web Attack Detection), and the Fusion Layer

* **Benefits of These Changes**
  * Reduce demo and testing preparation time
  * Simplify frontend-backend debugging
  * Prepare for live integration with Local Lab components (pfSense, Zeek, Suricata) and AWS deployment
  * Establish a solid foundation for future real-time capabilities (WebSocket scaling, CloudWatch monitoring)
