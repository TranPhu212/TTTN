---
title: "Week 10 Worklog"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 1.10. </b> "
---

### Week 10 Objectives:

* Learn how to deploy a web application with Amazon RDS, connect EC2 instances to a managed relational database, and perform backup and recovery operations
* Understand the process of schema conversion and database migration using AWS Schema Conversion Tool (SCT) and AWS Database Migration Service (DMS), including migration monitoring and troubleshooting
* Explore Amazon S3 for object storage, deploy a static website, and practice data management features such as versioning, replication, and CloudFront integration
* Deploy Grafana on AWS, integrate it with Amazon CloudWatch, and build monitoring dashboards to visualize cloud infrastructure metrics
* Learn how to secure web applications using AWS Web Application Firewall (AWS WAF) by configuring managed rules, custom rules, logging, and request filtering

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
|  6  | - Building a Web Application with Amazon RDS on AWS | 19/06/2026 | 19/06/2026 | <https://000005.awsstudygroup.com/> |
|  2  | - Hands-on Schema Conversion, Data Migration, and Troubleshooting with AWS Database Migration Service | 22/06/2026 | 22/06/2026 | <https://000043.awsstudygroup.com/> |
|  3  | - Object Storage and Static Website Hosting with Amazon S3 | 23/06/2026 | 23/06/2026 | <https://000057.awsstudygroup.com/> |
|  4  | - Deploying Grafana and Building AWS CloudWatch Monitoring Dashboards | 24/06/2026 | 24/06/2026 | <https://000029.awsstudygroup.com/> |
|  5  | - Deploying and Configuring AWS Web Application Firewall (AWS WAF) | 25/06/2026 | 25/06/2026 | <https://000026.awsstudygroup.com/> |


### Week 10 Achievements:

## Friday: Building a Web Application with Amazon RDS on AWS
* **Introduction**
  * Explain that Amazon RDS is a managed service that enables users to deploy and manage relational databases on AWS.
  * Suitable for OLTP (Online Transaction Processing) workloads and structured data.
  * Benefits:
    * Automated backups
    * Automatic patching and maintenance
    * Easy scalability
    * Multi-AZ deployment
    * Read Replicas
  * Supported database engines:
    * Amazon Aurora
    * MySQL
    * MariaDB
    * Oracle
    * SQL Server
    * PostgreSQL
  * Compare Amazon RDS with other AWS services (EC2, DynamoDB, Redshift, etc.).
  * Important concepts:
    * DB Instance
    * Endpoint
    * DB Subnet Group
    * Encryption
    * Billing
    * Scalability
    * Multi-AZ vs Read Replicas

* **Preparation Steps**
  * Guide participants through creating:
    * VPC
    * Subnets (Multi-AZ)
    * Security Groups for EC2 and RDS
    * DB Subnet Group
  * Emphasize the requirement of having at least two Availability Zones to support Multi-AZ deployments.

* **Create an EC2 Instance**
  * Detailed instructions for launching a Linux EC2 instance:
    * Amazon Linux 2023
    * t2.micro or t3.micro (Free Tier eligible)
  * Configure:
    * Security Group
    * Key Pair
  * Connect to the instance using MobaXterm via SSH.

* **Create an RDS Instance**
  * Install Git and Node.js on the EC2 instance.
  * Guide participants through creating an RDS instance using the AWS Console (Standard Create):
    * Select a database engine (MySQL, MariaDB, SQL Server, etc.)
    * Configure Storage
    * Configure Multi-AZ
    * Configure Security Group
    * Set database credentials
  * Review:
    * Logs
    * Events
    * Maintenance
    * Backups

* **Deploy the Application**
  * Clone the sample repository from GitHub:
    * AWS-First-Cloud-Journey/AWS-FCJ-Management
  * Install Node.js dependencies and required packages:
    * Express
    * MySQL
    * Other project dependencies
  * Run scripts to:
    * Install the MySQL client
    * Create a database and tables on RDS
  * Insert sample data:
    * A `user` table containing information about UFC fighters
  * Start the application:
    * `npm start`
  * Access the application through a web browser on port 5000.

* **Backup & Restore**
  * Demonstrate how to:
    * View automated backups
    * Create manual snapshots
  * Restore a snapshot to a new RDS instance.
  * Perform monitoring and validation after the restore process.

* **Resource Cleanup**
  * Delete:
    * RDS Instance
    * Snapshots
    * DB Subnet Group
  * Remove:
    * Security Groups
    * NAT Gateway
    * Elastic IP
    * VPC
  * Terminate the EC2 instance.
  * Highlight best practices to avoid unexpected AWS charges.

## Monday: Schema Conversion and Database Migration with AWS DMS
* **Overview**
  * This page provides an overview of the two most important processes involved in heterogeneous database migration and modernization to the AWS Cloud:
    * **Schema Conversion:** Introduces the AWS Schema Conversion Tool (AWS SCT) and the Schema Conversion & Migration feature available directly in the AWS DMS console, announced at AWS re:Invent.
    * This tool automatically assesses and converts database objects such as tables, views, functions, and stored procedures from the source database to a compatible target database, while identifying code segments that require manual remediation.
    * **Database Migration:** Introduces AWS Database Migration Service (AWS DMS), which enables secure data migration from source databases (on-premises, Amazon EC2, or Amazon RDS) to target platforms (Amazon EC2, Amazon RDS, Amazon S3, Apache Kafka, Amazon Kinesis, Amazon DocumentDB, Amazon DynamoDB, and others) with minimal downtime through continuous data synchronization.

* **Content**
  * The workshop menu is divided into seven major sections with detailed hands-on activities:
  * **Getting Started**
  * **Sign in to AWS:** Step-by-step instructions for accessing an AWS account for the workshop.
  * **Create a Key Pair:** Instructions for creating a secure key pair for remote access.
  * **Prepare the Environment:** Set up foundational infrastructure components (VPC networking, IAM permissions, etc.).
  * **Connect to an EC2 Instance and Install Schema Conversion Tool:** Instructions for remotely accessing an Amazon EC2 instance and installing AWS SCT.

* **Select a Source Database for DMS**
  * **Oracle Source**
    * Connect to the Oracle source database.
    * Configure the Oracle source database.

  * **SQL Server Source**
    * Launch SQL Server Management Studio (SSMS).
    * Configure the Microsoft SQL Server source database.

* **Select a Target Database for DM**
  * **Schema Conversion Process**
    * Grant permissions in the target database.
    * Create a project in AWS SCT.
    * Convert the database schema.

  * **Data Migration**
    * **Configure the Target Database:** Configure supported target database types, including:
      * Amazon RDS for Microsoft SQL Server
      * Amazon Aurora (MySQL-Compatible Edition)
      * Amazon Aurora (PostgreSQL-Compatible Edition)
    * **Create a Replication Instance:** Provision an intermediate server that performs data replication for AWS DMS.
    * **Create DMS Source and Target Endpoints:** Define source and target connection endpoints for AWS DMS.
    * **Create a DMS Migration Task:** Create migration tasks for specific data migration workloads.
    * **Inspect the Content of the Target Database:** Verify that data has been successfully migrated to the target database. 
    * Validation examples include:
      * Microsoft SQL Server
      * Aurora MySQL
      * Aurora PostgreSQL
      * Oracle
      * Amazon S3
    * **Replicate Data Changes:** Configure Change Data Capture (CDC) to continuously replicate ongoing changes from the source database.

* **Serverless Replication**
  * **Migrate Data Using DMS Serverless**
    * Create a serverless migration workflow (AWS automatically scales resources instead of requiring a managed Replication Instance).
    * AWS DMS Serverless replication phases.

  * **Test DMS Serverless Scaling Behavior**
    * Generate workload on the source database (simulate load).
    * Monitor scale-up events.
    * Monitor scale-down events.

* **Monitor DMS Migrations**
  * **CloudWatch Metrics:** Monitor resource utilization metrics (CPU, memory, network, etc.).
  * **Event Notifications:** Configure notifications when task events occur.
  * **Table Statistics:** Review detailed statistics, row counts, and status information for individual tables.
  * **Task Logs:** Analyze logs for detailed operational insights.
  * **Task States:** Understand task statuses such as Running, Stopped, and Failed.
  * **RunBook:** Standard operating procedures for managing migration activities.

* **Troubleshoot AWS DMS**
  * **Memory Pressure on a DMS Instance**
    * Create the environment (simulate a memory overload scenario).
    * Troubleshooting steps: Analyze the root cause.
    * Resolution: Apply corrective actions (increase instance size, optimize caching, etc.).

  * **Table Errors in a DMS Task**
    * Create the environment (simulate errors affecting specific tables).
    * Troubleshooting steps.
    * Resolution: Reload failed tables or skip errors to allow the task to continue.

* **Clean Up Environment**
  * Instructions for removing resources after completing the workshop to avoid unexpected charges:
    * Delete Serverless Migration Tasks.
    * Delete Database Migration Tasks.
    * Delete DMS Endpoints.
    * Delete the DMS Replication Instance.
    * Delete the CloudFormation Stack.
    * Delete the Amazon S3 Bucket and IAM Roles.

## Tuesday: Amazon S3 and Static Website Hosting
* **Introduction to Amazon S3**
  * This section explains in detail that Amazon S3 is an object storage service that provides virtually unlimited scalability, high availability, strong security, and excellent performance.
  * Emphasize its durability of **99.999999999% (11 nines)**.
  * Clearly compare **Bucket** (a globally unique container that stores objects and applies common policies) and **Object** (the actual data file stored inside a bucket, identified by a unique key name, containing metadata, and supporting sizes up to 5 TB).
  * Present the available storage classes (Standard, Intelligent-Tiering, Standard-IA, Glacier, etc.), security features (encryption, IAM, bucket policies, ACLs), management features (versioning, lifecycle policies, replication), performance capabilities, and real-world use cases such as static website hosting, backup, data lakes, and media storage.

* **Preparation**
  * Provide step-by-step instructions for the initial setup: create an S3 bucket and upload all website files (including HTML, CSS, JavaScript, images, and other assets) in preparation for hosting a static website.

* **Enable Static Website Hosting**
  * Explain what static website hosting is (serving static content directly from Amazon S3 without requiring a web server). Highlight its advantages, including low cost, scalability, and reliability.
  * Provide detailed instructions: Navigate to the bucket's **Properties** tab → **Static website hosting** → **Enable** → Select **Host a static website** → Set the **Index document** to `index.html` (optionally specify an **Error document**).
  * After enabling, a website endpoint will be generated in the format: `http://bucket-name.s3-website-region.amazonaws.com`.

* **Configure Block Public Access**
  * Explain the purpose of Block Public Access and why it must be temporarily disabled for this lab, while providing a strong security warning.
  * Steps: Open the bucket → **Block public access** → Uncheck **Block all public access** → Save changes and confirm.

* **Configure Public Objects**
  * Explain the S3 permission model, including **Bucket Policies**, **ACLs**, and **IAM**.
  * Provide instructions to enable ACLs by changing **Object Ownership** to **ACLs enabled** and selecting **Bucket owner preferred**.
  * Then select the required objects (or folders) → **Actions** → **Make public using ACL**. Include a sample Bucket Policy JSON for public read access and recommend using CloudFront instead of public access for production environments.

* **Test the Website**
  * Demonstrate how to verify that the website is working: Navigate to **Objects** → Select `index.html` → Copy the **Object URL** → Open it in a web browser to confirm the website is displayed correctly.

* **Accelerate the Website with CloudFront**
  * Introduce the integration of CloudFront to improve website performance, enable HTTPS, and protect the S3 bucket by eliminating the need for direct public access.
  * Include a technical note explaining the difference between the **S3 website endpoint** and **Origin Access Control (OAC)**. Also provide estimated costs and the steps required to configure a CloudFront distribution.

* **Bucket Versioning**
  * Explain that versioning allows multiple versions of the same object to be retained, protecting against accidental deletion or overwriting. Describe how versioning works and its states (**Enabled** and **Suspended**).
  * Hands-on exercise: Enable versioning → Modify the local `index.html` file → Upload it again → Enable **Show versions** to view and restore previous versions. Combine this exercise with CloudFront by adjusting the cache TTL to observe version updates.

* **Move Objects**
  * Demonstrate how to move objects between buckets: Create a destination bucket → Select all objects in the source bucket → **Actions** → **Move** → Choose the destination bucket.
  * Use checksums to verify data integrity after the transfer.

* **Cross-Region Object Replication**
  * Explain that Cross-Region Replication (CRR) automatically replicates objects to another AWS Region for disaster recovery, compliance, and reduced latency. Mention that versioning must be enabled on both the source and destination buckets.
  * Steps: Create a destination bucket in a different Region → Create a replication rule → Configure the required IAM role → Upload a new file to the source bucket and verify that replication completes successfully.

* **Clean Up Resources**
  * Provide instructions for removing all resources after completing the lab: Empty each bucket before deleting it, then disable and delete the CloudFront distribution to avoid unnecessary charges.

## Wednesday: Deploying Grafana and Building AWS CloudWatch Monitoring Dashboards
* **Introduction to Grafana**
  * Grafana is an open-source tool used for data visualization and analysis.
  * It helps collect metrics from multiple data sources, create customizable dashboards, run queries, visualize data, set up alerts, and explore metrics regardless of where the data is stored.
  * Grafana transforms time-series data into beautiful and interactive charts.
  * It supports connections to Graphite, Prometheus, InfluxDB, Elasticsearch, MySQL, PostgreSQL, and many other data sources.
  * In addition to the open-source edition, Grafana also provides Grafana Cloud and Grafana Enterprise for enterprise environments.

* **Key Features**
  * **Visualize:** Create flexible and interactive charts with various visualization options.
  * **Dynamic Dashboards:** Build dynamic dashboards using template variables (dropdown menus).
  * **Explore Metrics:** Explore data with ad-hoc queries and compare multiple time ranges.
  * **Explore Logs:** Navigate from metrics to logs and perform live log searches (best used with Loki).
  * **Alerting:** Define alert rules and send notifications through Slack, PagerDuty, VictorOps, or OpsGenie.
  * **Mixed Data Sources:** Combine multiple data sources within the same panel.
  * **Annotations:** Add event annotations directly to charts.
  * **Ad-hoc Filters:** Create dynamic key/value filters for data exploration.

* **Detailed Implementation Steps**
  * **Create a VPC and Subnet:**
    * Create a VPC named **Grafana-ASG** with the CIDR block **10.0.0.0/16**.
    * Create a public subnet and enable **Auto-assign Public IPv4 Address**.

  * **Create a Security Group (SG-PUB-Grafana-ASG):**
    * Configure inbound rules to allow:
      * SSH
      * All ICMP-IPv4
      * All ICMP-IPv6
      * Custom TCP

  * **Create an EC2 Instance (Grafana-Server):**
    * AMI: Amazon Linux
    * Instance type: Choose an appropriate instance type.
    * Create a Key Pair (**GrafanaKeyPair** - RSA `.pem`).
    * Networking:
      * Select the VPC and public subnet created earlier.
      * Enable **Auto-assign Public IP**.
    * Security Group:
      * Use **SG-PUB-Grafana-ASG**.

  * **Create an IAM User (Grafana-user):**
    * Enable both **Programmatic Access (Access Key)** and **AWS Management Console Access**.
    * Attach the **AdministratorAccess** policy.
    * Download the `.csv` file containing the **Access Key ID** and **Secret Access Key**.

  * **Create an IAM Role (GrafanaAccessRole):**
    * Create a policy named **GrafanaAccessPolicy** with permissions for:
      * **CloudWatch:** DescribeAlarmsForMetric, ListMetrics, GetMetricStatistics, GetMetricData
      * **EC2:** DescribeTags, DescribeInstances, DescribeRegions
      * **Resource Groups Tagging API:** tag:GetResources
    * Create a role for the **EC2** service and attach the policy above.

  * **Attach the IAM Role to the EC2 Instance:**
    * Assign **GrafanaAccessRole** to the **Grafana-Server** instance using **Modify IAM Role**.

  * **Install Grafana on the EC2 Instance**
    * Connect to the instance using **PuTTY** (with the Public IP and key pair) or **MobaXterm**.
    * Update the system:
      * `sudo yum update -y`
    * Create the Grafana repository:
      * `sudo nano /etc/yum.repos.d/grafana.repo`
      * Paste the official Grafana repository configuration.
    * Install Grafana:
      * `sudo yum install grafana`
    * Manage the Grafana service:
      * `sudo systemctl daemon-reload`
      * `sudo systemctl start grafana-server`
      * `sudo systemctl status grafana-server`
      * `sudo systemctl enable grafana-server.service`

  * Access Grafana:
    * Open `http://Public_IP:3000`
    * Log in using the default credentials:
      * Username: **admin**
      * Password: **admin**
    * Change the password when prompted during the first login.

  * **Monitoring with Grafana**
    * Add a **CloudWatch** Data Source:
      * Name: **CloudWatch-Grafana**
      * Authentication:
        * Enter the **Access Key ID** and **Secret Access Key** from the IAM User.
      * Click **Save & Test**.

    * Create a New Dashboard:
      * Add a panel.
      * Namespace: **AWS/EC2**
      * Metric: **CPUUtilization**
      * Statistic: **Average**
      * Dimension: **InstanceId** of **Grafana-Server**
      * Click **Apply**, refresh the dashboard, and save it as **Grafana-Monitoring**.
    * Share the dashboard using its generated link.
    * Use **Explore** to query the same metrics interactively.

  * **Clean Up Resources**
    * Terminate the **Grafana-Server** instance from the **EC2 Console**.
    * Delete the VPC from the **VPC Console**.

## Thursday: Securing Web Applications with AWS Web Application Firewall (AWS WAF)
* **Introduction to AWS Web Application Firewall**
  * AWS WAF (AWS Web Application Firewall) is a web application firewall service.
  * It helps protect your web applications or APIs from common web exploits that could affect availability, compromise security, or consume excessive resources.
  * Using AWS WAF is an excellent way to strengthen your web application's security. It helps mitigate risks from vulnerabilities such as SQL Injection, Cross-Site Scripting (XSS), and other common attacks listed in the OWASP Top 10.
  * AWS WAF allows you to create custom rules to determine whether HTTP requests should be allowed or blocked before they reach your application.

* **Using AWS WAF**
  * Create a Web ACL from the AWS WAF Console.
  * Create rules for AWS WAF.
  * Test the new rules.
  * Log incoming requests.

  * **Web ACLs with Managed Rules**
    * **Scenario**
      * You are the only developer at the Juice Shop startup. Your website is a simple web application running on a SQL database. For some reason, a group known as the "Milkshake Bandits" has started attacking your website.
      * Fortunately, you recently attended an AWS WAF workshop. You decide to deploy AWS WAF to protect your website. Since you are short on time, you choose to deploy two AWS Managed Rule Groups into a Web ACL to protect your website against the common attacks used by the Milkshake Bandits.

    * **Web ACLs with Managed Rules**
      * A Web ACL (Web Access Control List) is the core resource in AWS WAF. It contains the rules that are evaluated for every incoming request. A Web ACL is associated with your web application through Amazon CloudFront, AWS API Gateway, or an AWS Application Load Balancer.
      * Managed Rule Groups are collections of rules created and maintained by AWS or third-party vendors through AWS Marketplace. These rules provide protection against common attack patterns or are designed for specific types of applications.

    * **Steps**
      * Open the AWS WAF Console. This workshop uses the latest version of AWS WAF (not WAF Classic).
      * Click **Create web ACL**.

    * **Under Web ACL details:**
      * Resource type: **CloudFront distributions**
      * Name: **waf-workshop-juice-shop**
      * Description: **Web ACL for the aws-waf-workshop**

    * **Under Associated AWS resources:**
      * Click **Add AWS resources**, select the CloudFront distribution you created (**E24BURECS1O10C - dkievcmqb5kzc.cloudfront.net**), then click **Add**.

    * **Under Rules:**
      * Click **Add rules → Add managed rule groups**.
      * Select **AWS managed rule groups**.
      * Choose **Core Rule Set** and **SQL Database**.
      * Add the rule groups, configure their priority and metrics, then click **Create web ACL**.

  * **Testing**
    * Run the following curl command to simulate an XSS attack (it should be blocked):
      ```bash
      curl -X POST <Your Juice Shop URL> \
      -F "user='<script><alert>(Hello)></alert></script>'"
      ```
    * Run the following curl command to simulate a SQL Injection attack (it should be blocked):
      ```bash
        curl -X POST <Your Juice Shop URL> -F "user='AND 1=1;"
        ```

* **Custom Rule**
  * **Scenario**
    * Just when you thought the Milkshake Bandits had been stopped, more malicious requests started targeting your application. The attacks became more specific. You discovered that all of them contain an unusual header called **X-TomatoAttack**. Blocking requests with this header will stop the attacks.

  * **Creating a Custom Rule**
    * AWS WAF allows you to create your own rules for processing requests. This is useful when you need logic tailored to your specific application. This section also introduces **Request Sampling** and **Web ACL Capacity Units (WCU)**.

  * **Steps**
    * On the Web ACL details page:
      * Click **Rules → Add Rules → Add my own rules and rule groups**.

    * **In the Rule builder:**
      * Name: **MyCustomRule-X-TomatoAttack**

    * **Under Statement:**
      * Inspect: **Single header**
      * Header field name: **X-TomatoAttack**
      * Match type: **Size greater than or equal to**
      * Size in bytes: **0**
    * Action: **Block** → **Add rule** → **Save**

    * **Testing**
      * ```bash
        curl -H "X-TomatoAttack: Red" "<Your Juice Shop URL>"
        ```
      * ```bash
        curl -H "X-TomatoAttack: Green" "<Your Juice Shop URL>"
        ```
    * Check **Sampled requests** in the **Overview** tab to verify that the requests were **BLOCKED**.

* **Advanced Custom Rule**
  * **Scenario**
    * The Milkshake Bandits are back with a new attack strategy. You need to update your rule to block malicious requests while still allowing legitimate customer traffic.

  * **Creating an Advanced Custom Rule**
    * Every AWS WAF rule is defined as a JSON object. For more complex rules, editing the JSON directly is often more efficient.

  * **Original Rule (JSON)**
    * The rule blocks requests that contain either:
      * Header **x-milkshake: chocolate**, or
      * Query parameter **milkshake=banana**.

  * **Updated Rule (Advanced Version)**
    * Update the JSON so that requests are blocked only when the following **AND** conditions are met:
      * Header **x-milkshake: chocolate** **AND** **x-favourite-topping: nuts**
      * **OR**
      * Query parameter **milkshake=banana** **AND** **favourite-topping=sauce**

  * **Testing**
    * Run requests that should be **allowed**.
    * Run requests that should be **blocked** (returning an HTTP 403 HTML response).

* **Testing New Rules**
  * Before deploying a new rule, testing is essential to avoid accidentally blocking legitimate requests.
  * Use the **Count** action, which records matching requests without actually blocking them. The Web ACL will continue evaluating the remaining rules.

  * **Test Rule (JSON)**
    * Create a rule that counts requests containing the query parameter **username**.

  * **Run the test command**
    * ```bash
      curl "<Your Juice Shop URL>?username=admin"
      ```
  * Check the metrics in **CloudWatch → WAFv2 → Rule, WebACL**.

* **Logging Requests**
  * **Scenario**
    * Juice Shop is growing rapidly. As more rules are added, it becomes difficult to determine which rule is responsible for blocking a request. You decide to enable logging. Since the logs contain sensitive information such as the **Cookie** header, you also configure **redaction** to mask this field.

  * **Steps**
    * Create a **Kinesis Data Firehose** (Region: **us-east-1**):
      * Source: **Direct PUT**
      * Destination: **Amazon S3**
      * Name: **aws-waf-logs-workshop-26**
      * Select the S3 bucket **aws-waf-logs-001**

    * In the Web ACL, open **Logging and metrics → Enable**:
      * Select the **Kinesis stream**
      * Redacted fields: **Single header → Cookie**
    * Run several curl test commands.
    * Download the log file from Amazon S3 and verify that the **Cookie** header has been redacted.

  * **Conclusion**
    * AWS WAF can log requests through Kinesis Data Firehose and supports redaction of sensitive information. The logs include request details, actions taken, and the matching rules, making them extremely useful for operating and troubleshooting AWS WAF.

* **Cleaning Up Resources**
  * Clean up the resources in the following order to avoid unnecessary charges:
    * **Delete the sample web application**
      * Go to the **CloudFormation Console** → Select **WAFWorkshopSampleWebApp** → **Delete**

    * **Delete the Web ACL**
      * Go to the **AWS WAF Console** → **Web ACLs** → Select **waf-workshop-juice-shop** → **Delete**

    * **Delete the Kinesis Data Firehose**
      * Go to the **Kinesis Console** → **Delivery streams** → Select **aws-waf-logs-workshop-26** → **Delete**

    * **Delete the S3 bucket**
      * Go to the **Amazon S3 Console** → Select **aws-waf-logs-001** → **Empty** (type **"permanently delete"** to confirm) → **Delete bucket**
