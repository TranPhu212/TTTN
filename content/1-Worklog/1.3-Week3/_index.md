---
title: "Week 3 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.3. </b> "
---

### Week 3 Objectives:
* Get familiar with and practice AWS Backup to create automated backup and restore plans for AWS resources (EBS, RDS, DynamoDB, EFS)
* Install and configure AWS CLI v2, then manage core AWS services through command line (S3, SNS, IAM, VPC, Internet Gateway, EC2)
* Deploy and utilize Amazon CloudWatch for monitoring, working with metrics, Logs Insights, Metric Filters, Alarms, and Dashboards

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
|  2  | - * **Practices** <br>&emsp; + Implemented AWS Backup system with CloudFormation deployment <br>&emsp; + Backup plan configuration <br>&emsp; + SNS notifications <br>&emsp; + Backup/restore testing | 04/05/2026 | 04/05/2026 | <https://000013.awsstudygroup.com/> |
|  3  | - Installation of AWS CLI v2, profile configuration, hands-on practice with Amazon S3, SNS, IAM, VPC, Internet Gateway, and launching EC2 instances using CLI <br> - Resource cleanup and basic troubleshooting | 05/05/2026 | 05/05/2026 | <https://000011.awsstudygroup.com/> |
|  4  | - Deploy CloudFormation Stack, explore EC2 Metrics, Search Expressions, Logs, Alarms & Dashboards | 06/05/2026 | 06/05/2026 | <https://000008.awsstudygroup.com/> |

### Week 3 Achievements:

## Monday: Implementing AWS Backup for Systems
* **Deploying AWS Backup for Systems**
  * **Overview of the Lab**
    * This lab introduces users to the AWS Backup service in order to:
      * Create backup plans for common AWS resources such as:
        * EBS Volumes
        * RDS Databases
        * DynamoDB Tables
        * EFS File Systems
      * Learn how to restore data from backups
      * Automate the entire backup and recovery process

  * **Importance of Backups**
    * Data is one of the most valuable assets of any organization
    * Regular backups are critical for long-term operational success
    * In cloud environments, backup and recovery testing are much easier and more flexible compared to traditional on-premises data centers

  * **Specific Objectives**
    * Build automated backup plans
    * Test backup and data recovery workflows
    * Configure notification systems to ensure stakeholders receive updates when backup processes complete successfully or fail

  * **AWS Services Used in This Lab**
    * AWS Backup: A centralized service that automates data protection across AWS services and on-premises environments. It enables users to manage backup policies from a single location
    * AWS Simple Notification Service (SNS): A notification service used to send messages from publishers to subscribers through Topics. In this lab, SNS is used to notify users about backup job statuses

  * **Structure of the Upcoming Steps**
    * The workflow of this lab includes:
      * Introduction (Current Page)
      * Preparation Steps (Creating S3 Bucket and Deploying Infrastructure)
      * Creating a Backup Plan
      * Configuring Notifications
      * Testing the Workflow
      * Cleaning Up Resources

  * **Creating an S3 Bucket**
    * Download the CloudFormation template and Lambda Function
      * After downloading the CloudFormation template and Lambda Function from the provided link:
        * Create an S3 bucket to store the source files
        * Open the AWS Management Console, search for, and select S3
      * ![Search S3](/images/1-Worklog/1.3-Week3/Day2/SearchS3.png)
      * In the S3 interface, select Create bucket
      * ![Create Bucket](/images/1-Worklog/1.3-Week3/Day2/Createbucket.png)
      * In the Create bucket interface:
        * Enter a unique Bucket name. If the bucket name already exists, bucket creation will fail
      * ![Bucket Name](/images/1-Worklog/1.3-Week3/Day2/Bucket%20name.png)
      * Keep the default configurations
      * ![Default Setting](/images/1-Worklog/1.3-Week3/Day2/DefaultSetting.png)
      * In the Default encryption section:
        * Select Disable, then choose Create bucket
      * ![Default Encryption](/images/1-Worklog/1.3-Week3/Day2/Default%20encryption.png)
      * Successfully created the S3 bucket
      * ![Create Bucket Success](/images/1-Worklog/1.3-Week3/Day2/CreateBucketSuccess.png)
      * Create a folder for storing files
      * In the folder creation interface:
        * Enter the Folder name
        * Select Create folder
      * ![Folder Name](/images/1-Worklog/1.3-Week3/Day2/FolderName.png)
      * Successfully created the folder
      * ![Create Folder Success](/images/1-Worklog/1.3-Week3/Day2/CreateFolderSuccess.png)
      * Inside the newly created folder, upload the downloaded and extracted files
      * ![Upload Files](/images/1-Worklog/1.3-Week3/Day2/UploadFile.png)
      * In the Upload section:
        * Select Add files
        * Choose the files to upload
        * Select Upload
      * ![Add Files](/images/1-Worklog/1.3-Week3/Day2/AddFiles.png)
      * Successfully uploaded the files
      * ![Upload Success](/images/1-Worklog/1.3-Week3/Day2/UploadSuccess.png)
      * Configure Permissions for the S3 bucket:
        * For Block public access (bucket settings)
      * ![Upload Success](/images/1-Worklog/1.3-Week3/Day2/UploadSuccess.png)
      * Uncheck Block all public access:
        * Then select Save changes
      * ![Save Changes](/images/1-Worklog/1.3-Week3/Day2/Blockallpublicaccess.png)
      * Confirm the changes by typing confirm and then selecting Confirm
      * ![Confirm Edit Bucket](/images/1-Worklog/1.3-Week3/Day2/ConfirmEditBucket.png)
      * Next, configure the Bucket policy:
        * Select Edit
      * ![Bucket Policy](/images/1-Worklog/1.3-Week3/Day2/BucketPolicy.png)
      * In the Edit bucket policy interface:
        * Paste the following code and replace it with your own Bucket ARN
      * ![Edit Bucket Policy](/images/1-Worklog/1.3-Week3/Day2/Editbucketpolicy.png)
      * Select Save changes
      * ![Save Changes](/images/1-Worklog/1.3-Week3/Day2/Blockallpublicaccess.png)
      * Verify that the Permissions are public
      * ![Permissions Check](/images/1-Worklog/1.3-Week3/Day2/PermissionsCheck.png)
      * Copy the path information of lambda_function.zip
      * ![Copy URL](/images/1-Worklog/1.3-Week3/Day2/CopyURL.png)
      * Copy the Object URL information of the backup-lab.yaml file
    
    * **Deploying Infrastructure**
    * This section explains how to use AWS CloudFormation to automate the initialization and deployment of the infrastructure resources required for the lab exercises
    * Instead of manually creating each service, you will use a predefined template to set everything up quickly
    * Access the AWS Management Console
      * Search for and select CloudFormation
    * ![Search CloudFormation](/images/1-Worklog/1.3-Week3/Day2/SearchCloudFormation.png)
    * Select Create stack
    * ![Create Stack](/images/1-Worklog/1.3-Week3/Day2/CreateStack.png)
    * In the Create stack interface
      * For PREREQUISITE - PREPARE TEMPLATE, select Template is ready
      * For SPECIFY TEMPLATE, select Amazon S3 URL
      * For Amazon S3 URL, enter the URL you created
      * Select Next
    * ![Create Stack Interface](/images/1-Worklog/1.3-Week3/Day2/PerformanceCreate%20stack.png)
    * In the STACK NAME section:
      * Enter Backup-plan (or any name you prefer)
      * Select AvailabilityZone
      * For LatestAmiId, keep the default value
      * For NotificationEmail, enter your email address to receive notifications
      * For S3BucketName, enter the name of the S3 bucket you created
      * For S3KeyLambdaZip, enter the path of lambda_function.zip
    * ![Stack Name](/images/1-Worklog/1.3-Week3/Day2/STACKNAME.png)
    * In the CONFIGURE STACK OPTIONS section:
      * Select I acknowledge that AWS CloudFormation might create IAM resources
      * Select Next
    * ![Configure Stack Options](/images/1-Worklog/1.3-Week3/Day2/CONFIGURESTACK.png)
    * For CAPABILITIES:
      * Select Submit
    * ![Capabilities](/images/1-Worklog/1.3-Week3/Day2/CAPABILITIES.png)
    * Successfully created the CloudFormation stack
    * ![Create Stack Success](/images/1-Worklog/1.3-Week3/Day2/CopyURL.png)
    * Check the Outputs section of the CloudFormation stack
    * ![Check Output](/images/1-Worklog/1.3-Week3/Day2/CheckOutput.png)
    * Select the Value of ApplicationURL
    * ![Application URL](/images/1-Worklog/1.3-Week3/Day2/ApplicationURL.png)
    * Check your email to receive the notification email
    * ![Check Mail](/images/1-Worklog/1.3-Week3/Day2/CheckMail.png)
    * Confirm the email subscription
    * ![Confirm Email](/images/1-Worklog/1.3-Week3/Day2/confirm.png)

  * **Creating a Backup Plan**
    * Before starting, the page emphasizes defining a backup strategy based on two important metrics:
      * RTO (Recovery Time Objective)
      * RPO (Recovery Point Objective)
      * These metrics should be defined specifically for each workload instead of applying a single policy across the entire infrastructure
    * Access the AWS Management Console
      * Open the AWS Management Console
      * Search for and select AWS Backup
    * ![Search AWS Backup](/static/images/1-Worklog/1.3-Week3/Day2/SearchAWSBackup.png)
    * Select AWS Backup Plan
    * ![Create Backup Plan](/static/images/1-Worklog/1.3-Week3/Day2/CreateBackupPlan.png)
    * Create a backup plan
      * In the Create backup plan interface, select Build a new plan
      * For the Backup plan name field, enter BACKUP-LAB
    * ![Backup Plan Interface](/static/images/1-Worklog/1.3-Week3/Day2/BackupPlanPerfomance.png)
    * Configure the backup rule
      * Enter BACKUP-LAB-RULE for RULE NAME
      * In the SCHEDULE section, under FREQUENCY, select Daily
      * Select Use backup window defaults - recommended to use the default backup window settings
      * For BACKUP VAULT, select CREATE NEW BACKUP VAULT
    * ![Backup Rule](/static/images/1-Worklog/1.3-Week3/Day2/BackupRule.png)
    * Set the Backup Vault name
      * Enter BACKUP-LAB-VAULT for BACKUP VAULT NAME
      * Select (default) aws/backup
      * Select CREATE BACKUP VAULT
    * ![Backup Vault](/static/images/1-Worklog/1.3-Week3/Day2/BackupVaultName.png)
    * Add Key and Value pairs for tags
      * Select Create plan
    * ![Create Plan](/static/images/1-Worklog/1.3-Week3/Day2/CreateBackup.png)
    * Successfully created the Backup Plan
      * In the RESOURCE ASSIGNMENTS section, select ASSIGN RESOURCES
    * ![Create Backup Plan Success](/static/images/1-Worklog/1.3-Week3/Day2/ASSIGNRESOURCES.png)
    * Assign resources to the Backup Plan
      * Enter BACKUP-RESOURCES for RESOURCE ASSIGNMENT NAME
      * Select DEFAULT ROLE for IAM ROLE. If the role does not exist, AWS Backup will automatically create a new role with the required permissions
      * Add Tag Key and Tag Value
      * Select ASSIGN RESOURCES
      * ![Assign Resources](/static/images/1-Worklog/1.3-Week3/Day2/ASSIGNRESOURCESname.png)
    * Confirm and continue
      * Confirm by selecting Continue
    * ![Confirm Plan](/static/images/1-Worklog/1.3-Week3/Day2/ConfirmPlan.png)
    * Successfully completed resource assignment
    * ![Complete Plan](/static/images/1-Worklog/1.3-Week3/Day2/CompletePlan.png)

  * **Setting Up Notifications**
    * Configuring notifications helps the operations team monitor the status of backup and restore tasks in a timely manner, allowing rapid response if errors occur
    * Configure AWS CLI
      * Open Terminal and ensure you have access to AWS CLI. Make sure the CLI version is updated and that you have AWS Administrator permissions to execute AWS CLI commands
      * Modify the following AWS CLI command and replace it with the ARN of the SNS TOPIC you created. This ARN can be found in the CloudFormation Stack outputs section
      * After editing the command, execute it. This will trigger notifications through the SNS TOPIC whenever a backup or restore job is completed. This information helps the operations team monitor any failures during backup or restore processes
      * ![AWS CLI Command](/static/images/1-Worklog/1.3-Week3/Day2/CommandAWSCLI.png)
    * Check the SNS interface
    * ![Check SNS](/static/images/1-Worklog/1.3-Week3/Day2/CheckSNS.png)
    * Verify notifications
      * To verify that notifications were successfully enabled, you can use the following command. The output will include a section called SNSTopicArn, followed by the ARN of the created SNS Topic
      * ![SNSTopicArn Command](/static/images/1-Worklog/1.3-Week3/Day2/CommandSNSTopicArn.png)
      * You have now successfully enabled notifications for BACKUP-LAB-VAULT, ensuring that the operations team is informed about the completion of backup and restore activities related to this vault, as well as any associated failures
  
    * **Testing the Workflow**
    * Verify that Recovery Points have been successfully created in the Backup Vault
    * Perform a restore process for a resource from a backup to test availability
    * Learn how to monitor the status of Restore Jobs
    * Access the AWS Management Console:
      * Open the AWS Backup interface
      * Select CREATE AN ON-DEMAND BACKUP
    * ![AWS Backup Dashboard](/static/images/1-Worklog/1.3-Week3/Day2/AWSBackupDashboard.png)
    * In the RESOURCE TYPE section:
      * Select EC2
      * Paste the Instance ID from the Outputs section of the CloudFormation Stack
      * In the BACKUP WINDOW section, select CREATE BACKUP NOW
      * For Backup Vault, select BACKUP-LAB-VAULT
      * Use the default IAM role
      * Select CREATE ON-DEMAND BACKUP
    * ![Create On-Demand Backup](/static/images/1-Worklog/1.3-Week3/Day2/On-demandbackup.png)
    * In Jobs:
      * Select Backup jobs
      * Wait until the status changes to Completed
    * ![Backup Jobs](/static/images/1-Worklog/1.3-Week3/Day2/WaitBackupJobs.png)
    * Click the Backup jobs ID to view details
    * ![Backup Jobs ID](/static/images/1-Worklog/1.3-Week3/Day2/BackupJobsID.png)
    * Check your email to confirm notification delivery
    * Check the email related to Restore Test Status
    * View Restore jobs information and select the Restore jobs ID
    * View the details of the Restore jobs
    * Return to the AWS Management Console:
      * Search for and select CloudWatch
    * ![CloudWatch Interface](/static/images/1-Worklog/1.3-Week3/Day2/SearchCloudWatch.png)
    * In the CloudWatch interface:
      * Select Logs
      * Select the Log group for this lab:
        * (/aws/lambda/RestoreTestFunction-<YOUR CLOUDFORMATION STACK NAME>)
    * ![Logs](/static/images/1-Worklog/1.3-Week3/Day2/Logs.png)
    * In the Logs interface:
      * Select Log streams
      * Select the Log stream for this lab
    * ![Log Streams](/static/images/1-Worklog/1.3-Week3/Day2/LogStreams.png)
    * View detailed Log Events
    * ![Log Events Details](/static/images/1-Worklog/1.3-Week3/Day2/LogEvents.png)

  * **Cleaning Up Resources**
    * **Delete SNS Subscribers**
      * Access the AWS SNS Console
      * Select Subscription from the left sidebar
      * Select and delete the related Subscribers
    * ![SNS Subscriber](/static/images/1-Worklog/1.3-Week3/Day2/SNSSubscriber.png)

    * **Delete SNS Topics**
      * Access the AWS SNS Console
      * Select Topics from the left sidebar
      * Select and delete the related Topic
    * ![SNS Topic](/static/images/1-Worklog/1.3-Week3/Day2/SNSTopic.png)

    * **Delete Backup Vaults**
      * Access the AWS Backup Console
      * Select Backup Vaults from the left sidebar
      * Select the Backup Vault created in this lab
      * ![Backup Vaults](/static/images/1-Worklog/1.3-Week3/Day2/BackupVaults.png)
      * In the Backup Vault details page:
        * In the Recovery points section, select the Recovery points
        * Choose Actions, then select Delete
      * ![Recovery Points](/static/images/1-Worklog/1.3-Week3/Day2/RecoveryPoints.png)
      * Next, in the Backups section, after deleting the Recovery points:
        * Select Delete vault
      * ![Delete Vault](/static/images/1-Worklog/1.3-Week3/Day2/Deletevault.png)

    * **Delete Backup Plans**
      * Access the AWS Backup Console
      * Select Backup plans from the left sidebar
      * Select the Backup plan created in this lab
      * ![Backup Plans](/static/images/1-Worklog/1.3-Week3/Day2/BackupPlans.png)
      * In the Resource assignments section:
        * Select the created resource
        * Select Delete
      * ![Backup Resource](/static/images/1-Worklog/1.3-Week3/Day2/BackupResource.png)
      * In the Backup plan details page:
        * Select Delete
      * ![Backup Lab](/static/images/1-Worklog/1.3-Week3/Day2/BackupLab.png)

    * **Delete the CloudFormation Stack**
      * Access AWS CloudFormation
      * Select the Stack for this lab
      * Select Delete
    * ![Backup Stack](/static/images/1-Worklog/1.3-Week3/Day2/BackupStack.png)

    * **Delete CloudWatch Logs**
      * Access AWS CloudWatch
      * Select Logs
      * Select /aws/lambda/RestoreTestFunction
      * Select Actions, then choose Delete Log Group
      * Select Yes, Delete
    * ![CloudWatch Logs](/static/images/1-Worklog/1.3-Week3/Day2/CloudWatchLogs.png)

## Tuesday: Introduction and Hands-on with AWS CLI
* **Introduction to AWS CLI**
  * **Definition:** AWS Command Line Interface (AWS CLI) is an open-source tool that allows you to interact with AWS services using commands in a command-line shell.
  * **Benefits:** * Provides equivalent functionality to the AWS Management Console.
    * Enables automation of tasks through shell scripts.
    * Direct access to the public APIs of AWS services.
  * **Supported Environments:** * **Linux/macOS:** bash, zsh, tcsh
    * **Windows:** Command Prompt, PowerShell
    * **Remote:** Via SSH/PuTTY connection to Amazon EC2 instances or AWS Systems Manager

* **Configuration and Management**
  * Profiles in AWS CLI
  * **Profile:** A collection of settings and credentials. By default, AWS CLI uses the `default profile`.
  * **Custom Profile:** Use the `--profile` parameter to specify different accounts or configurations.
  * **Storage:** Information is stored locally in the `config` and `credentials` files.
  * **Basic Configuration Command**
    * Use the `aws configure` command to set up 4 important pieces of information:
    * **Access Key ID:** Access identifier
    * **Secret Access Key:** Security key (must be kept confidential)
    * **AWS Region:** Default region to send requests (e.g., `us-west-2`, `ap-southeast-1`).
    * **Default Output Format:** Data return format (`json`, `yaml`, `text`, or `table`)

* **Detailed Practice Content**
  * The workshop provides instructions for interacting with core services:
  * **Amazon S3:** Commands to create buckets, upload/download, and manage objects
  * **Amazon SNS (Simple Notification Service):** Configure topics and send notifications
  * **IAM (Identity and Access Management):** Manage users, groups, and permissions via CLI
  * **VPC (Virtual Private Cloud):** Set up virtual network infrastructure including Subnets, Internet Gateway, and route tables
  * **Amazon EC2:** Launch, manage state (start/stop/terminate), and configure virtual servers

* **Final Steps**
  * **Troubleshooting:** Instructions on how to read logs and handle common errors related to permissions or command syntax
  * **Resource Cleanup:** Instructions to delete created resources (EC2, S3, VPC...) to avoid unexpected charges after finishing the lesson

* **Installing AWS CLI**
  * AWS Command Line Interface (AWS CLI) has two versions. In this guide, we will install AWS CLI v2 on both Windows and Ubuntu, as this version is simpler and has fuller support compared to AWS CLI v1.
    * AWS CLI version 1 (v1): The original version of AWS CLI, still supported by AWS.
    * AWS CLI version 2 (v2): The latest version, supporting all new AWS features. Some features are only available in v2 and not in v1.
    * ![Tạo Key pair](/images/1-Worklog/1.3-Week3/Day3/create-key-pair.png)

  * **Installing AWS CLI**
    * For Windows: `msiexec.exe /i https://awscli.amazonaws.com/AWSCLIV2.msi`
    * ![Cài AWS](/images/1-Worklog/1.3-Week3/Day3/AWSWindows.png)

  * **Checking AWS CLI Installation:**
    * ![Kiểm tra version](/images/1-Worklog/1.3-Week3/Day3/AWSversion.png)

  * **Creating Default Profile**
    * Use the `aws configure` command to set up AWS CLI. This command will prompt you to enter the important information:
      * Access Key ID
      * Secret Access Key
      * AWS Region
      * Output format
    * ![Tạo Default Profile](/images/1-Worklog/1.3-Week3/Day3/AWSconfigure.png)
    * This configuration is saved in the credentials file under the default profile. The default profile will be used by AWS CLI if no other profile is specified.

  * **Configuring Multiple Profiles**
    * To create another profile, for example `devops`, use the following command:
    * ![Tạo Another Profile](/images/1-Worklog/1.3-Week3/Day3/ProfileDevop.png)
    * The profile contains the Access Key ID and Secret Access Key to sign requests sent to AWS.
  
  * **Checking Profile Region**
    * ![Kiểm tra region](/images/1-Worklog/1.3-Week3/Day3/RegionProfile.png)

  * **Listing Configuration**
    * ![Liệt kê danh sách](/images/1-Worklog/1.3-Week3/Day3/AWSlist.png)

  * **Listing Profiles**
    * ![Liệt kê profile](/images/1-Worklog/1.3-Week3/Day3/ListProfiles.png)

* **Checking Resources via CLI**
  * **Checking Number of S3 Buckets for the Profile**
    * To list S3 buckets of the profile, use the command:
    * ![liệt kê bucket S3](/images/1-Worklog/1.3-Week3/Day3/S3bucket.png)
  
  * **Using CLI Auto Prompt**
    * AWS CLI's Auto Prompt helps suggest parameters and commands, very convenient when you don't remember the exact syntax:
    * ![Command Prompt](/images/1-Worklog/1.3-Week3/Day3/CLIAutoPrompt.png)

* **AWS CLI with Amazon S3**
  * **Using AWS CLI to Manage S3 Resources**
    * **Listing S3 Buckets**
      * To view the list of existing buckets in your account:
      * ![Danh sách S3 bucket](/images/1-Worklog/1.3-Week3/Day3/S3list.png)
      * If no buckets are visible, ensure you have access permissions to AWS S3.
  
    * **Checking Objects in an S3 Bucket**
      * To list objects in a specific bucket:
      * ![Liệt kê object](/images/1-Worklog/1.3-Week3/Day3/ObjectS3.png)
    
    * **Deleting an Object in an S3 Bucket**
      * When you need to delete an object from a bucket:
      * ![Xóa object](/images/1-Worklog/1.3-Week3/Day3/RemoveObject.png)

    * **Deleting an S3 Bucket**
      * After deleting all objects in the bucket, you can delete the bucket with the following command:
      * ![Xóa S3](/images/1-Worklog/1.3-Week3/Day3/RemoveS3.png)

* **AWS CLI with Amazon SNS**
  * **Creating an SNS Topic**
    * To create an SNS topic, do the following:
    * This is the command to create an SNS topic named `aws-cli`
    * ![Tạo topic SNS](/images/1-Worklog/1.3-Week3/Day3/SNScreate.png)
  
  * **Creating a Subscriber**
    * After successfully creating the SNS topic, register a subscriber with the following command:
    * ![đăng ký subscriber](/images/1-Worklog/1.3-Week3/Day3/SNSsubscribe.png)

  * **Confirming Subscription**
    * Check the email you used in the previous command. Then select **Confirm subscription** in the email to complete the registration.
    * ![Kiểm tra email](/images/1-Worklog/1.3-Week3/Day3/ConfirmEmail.png)
  
  * **Subscription Completed**
    * Once you have confirmed the subscription, the subscription status will be complete.
    * ![Hoàn tất đăng ký](/images/1-Worklog/1.3-Week3/Day3/Completesubscript.png)
  
  * **Publishing a Test Message**
    * After successful subscription, we will try publishing a message to test:
    * This command sends a message with the content "Hello" to all registered subscribers.
    * ![Push tin nhắn](/images/1-Worklog/1.3-Week3/Day3/SNSpublish.png)
  
  * **Receiving Message via Email**
    * If everything works correctly, you will receive the sent message via email.
    * ![Nhận tin nhắn email](/images/1-Worklog/1.3-Week3/Day3/AWSmessage.png)

* **AWS CLI with IAM**
  * We can quickly create IAM groups, IAM users, and policies using the CLI. The steps are as follows:
  * **Creating an IAM Group**
    * First, create a new IAM group with CLI:
    * ![Tạo Group](/images/1-Worklog/1.3-Week3/Day3/IAMcreate.png)

  * **Creating an IAM User**
    * Next, create a new user named `dev-1`:
    * ![Tạo User](/images/1-Worklog/1.3-Week3/Day3/IAMuser.png)

  * **Adding User to Group**
    * The next step is to add the newly created user to the `dev` group:
    * ![Thêm user vào group](/images/1-Worklog/1.3-Week3/Day3/add-user-to-group.png)

  * **Checking Group and User Details**
    * We can check the details of the group and user with the following command:
    * ![Kiểm tra group](/images/1-Worklog/1.3-Week3/Day3/CheckGroup.png)

  * **Creating Access Key for User**
    * Next, create an Access Key for the `dev-1` user:
    * ![Tạo Access Key](/images/1-Worklog/1.3-Week3/Day3/create-key-pair.png)

  * **Deleting Access Key**
    * Finally, if you want to delete the created Access Key, you can do so with the following command:
    * ![Xóa Access Key](/images/1-Worklog/1.3-Week3/Day3/delete-access-key.png)

* **AWS CLI with VPC**
  * **Creating a VPC**
    * Create a VPC using AWS CLI:
    * ![Tạo VPC](/images/1-Worklog/1.3-Week3/Day3/create-vpc.png)
    
  * **Creating a Subnet**
    * Next, create a subnet based on the created VPC ID:
    * ![Tạo Subnet](/images/1-Worklog/1.3-Week3/Day3/create-subnet.png)
    * Create a second subnet with a different CIDR:
    * ![Tạo Subnet thứ hai](/images/1-Worklog/1.3-Week3/Day3/SecondSubnet.png)

  * **Checking and Managing VPC Resources**
    * Check the result of subnet creation:
    * ![Kiểm tra subnet](/images/1-Worklog/1.3-Week3/Day3/delete-subnet.png)

* **AWS CLI with Internet Gateway**
  * **Creating an Internet Gateway**
    * ![Tạo Internet Gateway](/images/1-Worklog/1.3-Week3/Day3/CreateInternetGateway.png)
    * This is the step to initialize the Internet Gateway.

  * **Confirming Internet Gateway**
    * We will confirm that the Internet Gateway was created successfully and use the Internet Gateway ID for the next steps.
    * ![Xác nhận Internet Gateway](/images/1-Worklog/1.3-Week3/Day3/ConfirmInternetGateway.png)
    * Confirming the Internet Gateway is an important step before proceeding.

  * **Checking VPC**
    * We will check the VPC to use the VPC ID for the next step.
    * ![Kiểm tra VPC](/images/1-Worklog/1.3-Week3/Day3/CheckVPC.png)
    
  * **Attaching Internet Gateway**
    * After checking the Internet Gateway and VPC, we attach the internet gateway as follows:
    * ![Attach Internet Gateway](/images/1-Worklog/1.3-Week3/Day3/attach-internet-gateway.png)
    * We need to use the correct VPC ID and Internet Gateway ID to attach successfully.

  * **Creating a Route Table**
    * Similarly, we create a Route Table for our VPC.
    * ![Tạo Route Table](/images/1-Worklog/1.3-Week3/Day3/create-route-table.png)

  * **Routing the Route Table**
    * Then, we set up routing for the Route Table to connect to the Internet:
    * ![Định tuyến Route Table](/images/1-Worklog/1.3-Week3/Day3/dinh-tuyen-%20Route-Table.png)
    
  * **Checking the Route Table**
    * After creating the route, we check the Route Table configuration again:
    * ![Kiểm tra Route Table](/images/1-Worklog/1.3-Week3/Day3/describe-route-tables.png)

* **Creating EC2 using AWS CLI**
  * **Creating EC2 using AWS CLI**
    * From the network infrastructure created with CLI, we will create an EC2 instance. First, create an AWS Key Pair:
    * ![Tạo Key pair](/images/1-Worklog/1.3-Week3/Day3/create-key-pair.png)
    * Check in the console to confirm the Key Pair was created successfully.
    * ![Kiểm tra Key pair](/images/1-Worklog/1.3-Week3/Day3/ConfirmCreateKeyPair.png)
    * Create a Security Group for EC2:
    * ![Tạo Security Group](/images/1-Worklog/1.3-Week3/Day3/create-security-group.png)
    * Check the Security Group just created.
    * ![Kiểm tra Security Group](/images/1-Worklog/1.3-Week3/Day3/CheckSecuritygroup.png)
    * Grant SSH permission:
    * ![Cấp quyền SSH](/images/1-Worklog/1.3-Week3/Day3/authorize-security-group-ingress.png)

* **Resource Cleanup**
  * **Deleting Security Group**
    * Make sure you have confirmed deletion of all connections related to the Security Group before executing the delete command.
    * ![Xóa Security Group](/images/1-Worklog/1.3-Week3/Day3/delete-security-group.png)
  
  * **Deleting Subnet**
    * ![Xóa Subnet](/images/1-Worklog/1.3-Week3/Day3/delete-subnet.png)

  * **Deleting Route Table**
    * ![Xóa Route Table](/images/1-Worklog/1.3-Week3/Day3/delete-route-table.png)

  * **Detaching Internet Gateway**
    * ![Detach Internet Gateway](/images/1-Worklog/1.3-Week3/Day3/detach-internet-gateway.png)

  * **Deleting Internet Gateway**
    * ![Xóa Internet Gateway](/images/1-Worklog/1.3-Week3/Day3/delete-internet-gateway.png)

  * **Deleting VPC**
    * ![Xóa VPC](/images/1-Worklog/1.3-Week3/Day3/delete-vpc.png)

## Wednesday: Amazon CloudWatch - Monitoring and Managing AWS Resources
* **Introduction to Amazon CloudWatch**
  * CloudWatch is a monitoring and management service that provides data for AWS resources, hybrid applications, and on-premises resources. Key features include:
    * Data collection: Collect logs and metrics on the same platform
    * End-to-End Monitoring: Monitor the entire application, infrastructure, and services
    * Automation: Use alarms and event data to reduce Mean Time To Resolution (MTTR)
    * Storage: Store metrics for up to 15 months

* **Deploy CloudFormation Stack**
  * Access the AWS Management Console
    * Search for CloudFormation service in the search bar
    * Select CloudFormation from the search results
  * ![Seach CloudFormation](/images/1-Worklog/1.3-Week3/Day4/SeachCloudFormation.png)
  * In the CloudFormation interface
    * Choose Create stack
    * Choose With new resources (standard)
  * ![Create stack](/images/1-Worklog/1.3-Week3/Day4/Createstack.png)
  * In the Create stack interface
    * Download the configuration template file to your computer
    * In the Prerequisite - Prepare template section, choose Choose an existing template
    * Then choose Upload a template file
    * Click Choose file to upload the downloaded template file
    * Click Next
  * ![Info stack](/images/1-Worklog/1.3-Week3/Day4/Infostack.png)
  * Configure Stack information
    * Stack name: Enter FCJ-CloudWatch-Workshop (or another easy-to-remember name)
    * RegionId: Select the correct Region ID where you are doing the workshop (e.g., us-east-1 for N. Virginia)
    * Keep the remaining parameters at their default values
    * Click Next
  * ![Stack detail](/images/1-Worklog/1.3-Week3/Day4/Stackdetail.png)
  * Configure Stack options
    * No need to change the default configuration on this page
    * Scroll to the bottom
    * Check I acknowledge that AWS CloudFormation might create IAM resources with custom names
    * Click Next
  * ![Stack setting](/images/1-Worklog/1.3-Week3/Day4/Stacksetting.png)
  * Review and create Stack
    * Review all configuration information
    * Scroll to the bottom and click Submit to start creating the Stack
  * ![Submit stack](/images/1-Worklog/1.3-Week3/Day4/Submitstack.png)
  * Monitor the deployment process
  * ![Watch create](/images/1-Worklog/1.3-Week3/Day4/Watchcreate.png)

* **Viewing Metrics**
  * **Viewing Metrics**
    * Access the AWS Management Console
      * Search for CloudWatch service in the search bar
      * Select CloudWatch from the search results
      * ![Search CloudWatch](/images/1-Worklog/1.3-Week3/Day4/SearchCloudWatch.png)
    * In the CloudWatch interface
      * Expand the Metrics section in the left menu
      * Choose All metrics
      * ![All metrics](/images/1-Worklog/1.3-Week3/Day4/Metrics.png)
    * In the metrics graph interface, enter EC2 in the search box
    * ![Nhập EC2](/images/1-Worklog/1.3-Week3/Day4/TypeEC2.png)
    * From the search results, choose EC2 > Per-Instance Metrics
    * ![Per-Instance Metrics](/images/1-Worklog/1.3-Week3/Day4/Per-InstanceMetrics.png)
    * ![Per-Instance List](/images/1-Worklog/1.3-Week3/Day4/Per-InstanceList.png)
    * In the search bar, enter CPUUtilization and search
    * ![Nhập CPUUtilization](/images/1-Worklog/1.3-Week3/Day4/TypeCPUUtilization.png)
    * ![CPUUtilization List](/images/1-Worklog/1.3-Week3/Day4/CPUUtilizationList.png)
    * Select 2 out of the 5 instances created by the CloudFormation stack to compare CPUUtilization metrics
    * ![Chọn instances](/images/1-Worklog/1.3-Week3/Day4/Choseinstances.png)
    * Next, we will view other metrics of the same Instance
      * Deselect Instance B
      * Clear the CPUUtilization search tag
      * Enter EBSWriteBytes in the search bar
    * ![Nhập EBSWriteBytes](/images/1-Worklog/1.3-Week3/Day4/TypeEBSWriteBytes.png)
    * ![EBSWriteBytes List](/images/1-Worklog/1.3-Week3/Day4/EBSWriteBytesList.png)
    * Scroll down and select Instance A
    * ![Chọn Instance A](/images/1-Worklog/1.3-Week3/Day4/ChoseInstanceA.png)
    * You can hide one of the two metrics to see more details
    * ![Hide metrics](/images/1-Worklog/1.3-Week3/Day4/Hidemetrics.png)
  * **Chart Operations**
    * In the Graphed metrics tab, on the EBSWriteBytes row, in the Y axis column, select > to move this metric to the second Y axis
    * ![Graphed metrics](/images/1-Worklog/1.3-Week3/Day4/Graphedmetrics.png)
    * Add horizontal annotation to the chart
      * Switch to the Options tab
      * Choose Add horizontal annotation
    * ![Options Graphed metrics](/images/1-Worklog/1.3-Week3/Day4/OptionsGraphedmetrics.png)
    * Configure horizontal annotation with the following information:
      * Label: 5% Mark
      * Value: 5
    * ![Horizontal Annotation](/images/1-Worklog/1.3-Week3/Day4/HorizontalAnnotation.png)
    * Create an additional Vertical annotation with the label "Job start"
    * ![Vertical annotation](/images/1-Worklog/1.3-Week3/Day4/Verticalannotation.png)
    * Adjust the time for the vertical annotation
      * Hover the mouse over the start of the line on the chart
      * Observe that the job started around 03:00
    * ![Điều chỉnh thời gian](/images/1-Worklog/1.3-Week3/Day4/Changetime.png)
    * Change the Date of the Job start to 02:40
    * Select Apply to save the changes
    * ![Date của Job](/images/1-Worklog/1.3-Week3/Day4/DateOfJob.png)
    * The Job start line has been moved to the correct position
    * ![Job start](/images/1-Worklog/1.3-Week3/Day4/Jobstart.png)

* **Performing Searches**
  * In the previous section, we viewed metrics manually, but it still has many limitations and requires many operations with different metrics. In this section, we can do this faster with Search Expression
    * Clear all information in the old chart by clicking X or Clear graph
    * ![Clear graph](/images/1-Worklog/1.3-Week3/Day4/Cleargraph.png)
    * Return to the Browse tab
      * Clear the EBSWriteBytes filter
      * Click Graph search
    * ![Xoá EBSWriteBytes](/images/1-Worklog/1.3-Week3/Day4/DeleteEBSWriteBytes.png)
    * ![Press Graph search](/images/1-Worklog/1.3-Week3/Day4/PressGraphsearch.png)
    * Back to the Graphed metrics tab, we can see the Details column has a search expression that just appeared
    * ![Quay trở lại Graphed metrics](/images/1-Worklog/1.3-Week3/Day4/BackGraphedmetrics.png)
    * In the top right corner
      * Expand the Line dropdown
      * Choose Stacked area
    * ![Stacked area](/images/1-Worklog/1.3-Week3/Day4/Stackedarea.png)
    * And our chart becomes easier to read
    * ![Easy look](/images/1-Worklog/1.3-Week3/Day4/Outlook.png)
    * Find the average memory usage by percentage (Disk Used Percent)
    * ![Disk Used Percent](/images/1-Worklog/1.3-Week3/Day4/DiskUsedPercent.png)
    * ![Disk Used Percent Look](/images/1-Worklog/1.3-Week3/Day4/DiskUsedPercentLook.png)
    * Search by the keyword “used”
    * ![Search used](/images/1-Worklog/1.3-Week3/Day4/Searchused.png)
    * You can see the results have changed somewhat
    * ![Search used look](/images/1-Worklog/1.3-Week3/Day4/Searchusedlook.png)

* **Performing Mathematical Operations**
  * First, clean up the previous search expression
  * ![Dọn dẹp biểu thức](/images/1-Worklog/1.3-Week3/Day4/CleanSearch.png)
  * Return to the Browse tab
    * Click Graph search to restore the chart as in the previous step
  * ![Back Browse](/images/1-Worklog/1.3-Week3/Day4/BackBrowse.png)
  * Then expand the Add math section in the top right corner, below the chart
    * Expand Filter
    * Choose Top 10 by sum
  * ![Add math](/images/1-Worklog/1.3-Week3/Day4/Addmath.png)
  * Now we will rearrange the chart based on the first search expression, with the expression as below
  * ![Biểu thức tìm kiếm đầu tiên](/images/1-Worklog/1.3-Week3/Day4/FirstSearch.png)

* **Creating Dynamic Labels**
  * Delete the old expressions from the previous section
  * Clear all Filters and click All to return to the namespaces section
  * ![Xoá Filers](/images/1-Worklog/1.3-Week3/Day4/CleanFilers.png)
  * Then go into the CWAgent namespace
  * ![CWAgent](/images/1-Worklog/1.3-Week3/Day4/CWAgent.png)
  * Continue selecting Dimensions: ImageId, InstanceId, InstanceType, exe, process_name
  * ![Dimension](/images/1-Worklog/1.3-Week3/Day4/Dimension.png)
  * ![Dimension Look](/images/1-Worklog/1.3-Week3/Day4/DimensionLook.png)
  * In the search bar, enter the following 2 pieces of information
    * exe=cloudwatch
    * MetricName=procstat_memory_rss (in this section we specifically need the Metric name)
  * ![Search](/images/1-Worklog/1.3-Week3/Day4/Search.png)
  * Continue clicking Graph search to display the chart
  * ![Graph search](/images/1-Worklog/1.3-Week3/Day4/Graphsearch.png)
  * Switch to the Graphed metrics tab
    * Expand Add dynamic label
    * Expand All labels
    * Choose PROP(‘Dim.DimName’)
  * ![All labels](/images/1-Worklog/1.3-Week3/Day4/Alllabels.png)
  * We can see that the Label on the chart has changed
  * ![Label Change](/images/1-Worklog/1.3-Week3/Day4/LabelChange.png)
  * Edit the label expression to the following format
  * ![Sửa label](/images/1-Worklog/1.3-Week3/Day4/FixLabel.png)
  * The label has changed to the following parts
  * ![Label](/images/1-Worklog/1.3-Week3/Day4/Label.png)

* **CloudWatch Logs**
  * **CloudWatch Logs**
    * In the main CloudWatch page
      * In the left menu, expand the Logs section
    * ![Logs](/images/1-Worklog/1.3-Week3/Day4/Logs.png)
    * In the search bar, enter /ec2 and select /ec2/linux/var/log/messages
    * ![Nhập EC2](/images/1-Worklog/1.3-Week3/Day4/SearchEC2.png)
    * ![EC2 Info](/images/1-Worklog/1.3-Week3/Day4/EC2Info.png)
    * Select any instance to view detailed logs
    * In the logs interface, you can see records from this instance generated from various sources such as: dhclient, NET, ec2net, systemd…
    * ![Logs Event](/images/1-Worklog/1.3-Week3/Day4/LogsEvent.png)
    * Return to the log group information /ec2/linux/var/log/messages. Now we will configure the retention time for log events
      * Expand the Actions menu
      * Choose Edit retention setting
    * ![Edit retention setting](/images/1-Worklog/1.3-Week3/Day4/Editretentionsetting.png)
    * In the Retention setting section, choose 1 week (7 days) for Expire events after
    * ![Retention setting](/images/1-Worklog/1.3-Week3/Day4/Retentionsetting.png)
    * ![Success Setting.](/images/1-Worklog/1.3-Week3/Day4/SuccessSetting..png)

  * **CloudWatch Logs Insights**
    * In this section, we will generate logs from an application, then query these logs in CloudWatch Logs Insights. I will choose one instance as an example
    * In the service search bar
      * Enter EC2
      * Select EC2
    * ![Find EC2](/images/1-Worklog/1.3-Week3/Day4/FindEC2.png)
    * In the EC2 Console Instances page
      * Select any Instance, here I choose Instance-A
      * Click Connect
    * ![Connect](/images/1-Worklog/1.3-Week3/Day4/Connect.png)
    * In the Connect to instance page
      * Choose the Session Manager tab
      * Click Connect
    * ![Session Manager](/images/1-Worklog/1.3-Week3/Day4/SessionManager.png)
    * After a few moments, a Terminal will appear
      * First, go to the tmp directory
      * Then download the py script file
    * ![tmp](/images/1-Worklog/1.3-Week3/Day4/tmp.png)
    * Grant execute permission and run this script file
    * Check the loggers running as processes
    * You can see there are currently 2 processes running, they will run until the end of the lab
    * Use the command to print log lines from the file /var/log/messages, it will print until you cancel it
    * Return to the CloudWatch Console, go to Logs Insights in the left menu. We will query logs here
    * In Selection criteria, find /ec2 and select /ec2/linux/var/log/messages
    * Enter the query below and click Run query
    * And get the result
    * These are the logs we just created in the step above
    * Now try querying ERROR Logs
    * These are also the error logs we created earlier
    * Next are the WARN Logs
    * These are the newly created logs
    * Now try querying the error logs again, we will also see the newly created logs
    * In addition, we can also query by other keywords. Like the query below

  * **Visualizing Log Queries**
    * In addition, we can also view charts of these queries. Switch to the Visualization tab
  
  * **Saving Query Commands**
    * In the future, we may have many queries that we need to reuse or more complex queries that we need to save. Logs Insights supports saving these queries
    * For example, I will save the error query
      * Return to the main Logs Insights screen
      * Paste the query to find Error logs again
      * Click Save
    * In the Save a new query page, fill in the information:
      * Query name: Errors
      * Folder: cloudwatch-workshop, and check Create new
      * Review the information in Query definition details
      * Click Save
  
  * **Query History**
    * Logs Insights also allows us to view previous query history. On the interface, click History (under Query editor)

  * **CloudWatch Metric Filter**
    * Return to the main CloudWatch screen
      * Choose Log groups from the left menu
      * Search for /ec2 in the search bar
      * Select /ec2/linux/var/log/messages
    * In the /ec2/linux/var/log/messages interface
      * Expand the Actions menu
      * Choose Create metric filter
    * ![Create metric filter](/images/1-Worklog/1.3-Week3/Day4/Createmetricfilter.png)
    * In the Define Pattern section, configure the following:
      * Filter pattern: expand the dropdown and choose ERROR
      * Test pattern: expand and choose one instance (should choose the instance where we created the processes earlier)
    * ![Define Pattern](/images/1-Worklog/1.3-Week3/Day4/DefinePattern.png)
    * Click Test pattern to check if the filter works correctly
    * ![Test pattern](/images/1-Worklog/1.3-Week3/Day4/Testpattern.png)
    * In the Create filter name section of Assign metric, enter PythonAppErrors
    * ![Create filter name](/images/1-Worklog/1.3-Week3/Day4/Createfiltername.png)
    * In the Metric details section, configure the following:
      * Metric namespace: ec2-logs
      * Metric name: /var/log/messages - ERROR
      * Metric value: 1
      * Default value: 0
      * Unit: expand dropdown and choose Count
      * Click Next
    * ![Metric details](/images/1-Worklog/1.3-Week3/Day4/Metricdetails.png)
    * Review the configuration and click Create metric filter
    * ![Create metric](/images/1-Worklog/1.3-Week3/Day4/Createmetric.png)
    * ![Create Success](/images/1-Worklog/1.3-Week3/Day4/CreateSuccess.png)
    * Return to Metrics > All metrics
      * Search with the keyword /var/log/messages and ERROR
      * Choose ec2-logs > Metrics with no dimensions
    * ![Metrics with no dimensions](/images/1-Worklog/1.3-Week3/Day4/Metricswithnodimensions.png)
    * ![Metric name](/images/1-Worklog/1.3-Week3/Day4/Metricname.png)

* **CloudWatch Alarms**
  * Return to the main CloudWatch screen
    * Choose Alarms in the left menu
    * Choose All alarms
    * Click Create alarm
  * ![Create alarm](/images/1-Worklog/1.3-Week3/Day4/Createalarm.png)
  * Choose Select metric
  * ![Select metric](/images/1-Worklog/1.3-Week3/Day4/Selectmetric.png)
  * The metrics window appears, in Custom namespaces, choose ec2-logs
  * ![Custom namespaces](/images/1-Worklog/1.3-Week3/Day4/Customnamespaces.png)
  * Then choose Metrics with no dimensions, select /var/log/messages and click Select metric
  * ![Metrics with no dimensions](/images/1-Worklog/1.3-Week3/Day4/Metricsnodimensions.png)
  * In the Specify metric and conditions section, choose Period as 1 minute
  * ![Period](/images/1-Worklog/1.3-Week3/Day4/Period.png)
  * In the Conditions section
    * Threshold type: Static
    * Condition: Greater than 10
  * ![Conditions](/images/1-Worklog/1.3-Week3/Day4/Conditions.png)
  * ![Conditions Look](/images/1-Worklog/1.3-Week3/Day4/ConditionsLook.png)
  * Then click Next to continue
  * Now configure the notification as follows
    * Alarm state trigger: In alarm
    * Choose Create new topic
    * Topic name: Error_logs_reach_10
    * Notification email: enter your email here
    * Click Create topic
  * ![Create topic](/images/1-Worklog/1.3-Week3/Day4/Createtopic.png)
  * ![Topic Info](/images/1-Worklog/1.3-Week3/Day4/TopicInfo.png)
  * Click Next
  * ![Next](/images/1-Worklog/1.3-Week3/Day4/Next.png)
  * In the final step, enter the alarm name as PythonApplicationErrorAlarm and click Next
  * ![PythonApplicationErrorAlarm ](/images/1-Worklog/1.3-Week3/Day4/PythonApplicationErrorAlarm .png)
  * Review the result and click Create alarm
  * ![Info Alarm.](/images/1-Worklog/1.3-Week3/Day4/InfoAlarm..png)
  * ![Create Alarm](/images/1-Worklog/1.3-Week3/Day4/CreateAlarm.png)
  * Result
  * ![Final.](/images/1-Worklog/1.3-Week3/Day4/Final.png)
  * Log in to Gmail or any email service you use. You will see an email sent from AWS Notification
  * Click Confirm subscription
  * ![Confirm subscription](/images/1-Worklog/1.3-Week3/Day4/Confirmsubscription.png)
  * ![Success Subscription](/images/1-Worklog/1.3-Week3/Day4/SuccessSubscription.png)

* **CloudWatch Dashboards**
  * In the final part of this workshop, we will create a simple Dashboard to centrally manage the Metrics and Alarms set up earlier, especially the Error Logs configured in the previous section
  * Add the created alarm to the Dashboard:
    * Select PythonApplicationErrorAlarm
    * Expand the Actions menu
    * Choose Add to dashboard
  * ![Add to dashboard](/images/1-Worklog/1.3-Week3/Day4/Addtodashboard.png)
  * In the Add to dashboard dialog, choose Create new
  * ![Create new](/images/1-Worklog/1.3-Week3/Day4/Createnew.png)
  * Configure the new Dashboard:
    * Enter dashboard name: CloudWatch-Workshop
    * Click Create
    * Click Add to dashboard
  * ![CloudWatch-Workshop](/images/1-Worklog/1.3-Week3/Day4/CloudWatch-Workshop.png)
  * ![Success Create Alarm](/images/1-Worklog/1.3-Week3/Day4/SuccessCreateAlarm.png)
  * Below is the newly created dashboard:
  * ![Dashboard](/images/1-Worklog/1.3-Week3/Day4/dashboard.png)
  * You can perform many customization operations on this widget:
  * ![widget](/images/1-Worklog/1.3-Week3/Day4/widget.png)
  * ![widget look](/images/1-Worklog/1.3-Week3/Day4/widgetlook.png)

* **Resource Cleanup**
  * In the AWS service search bar:
    * Enter CloudFormation
    * Select CloudFormation
  * ![Seach CloudFormation](/images/1-Worklog/1.3-Week3/Day4/SeachCloudFormation.png)
  * In the CloudFormation Console:
    * Select the stack created in this workshop
    * Click Delete
  * ![Delete](/images/1-Worklog/1.3-Week3/Day4/Delete.png)
  * In the confirmation dialog:
    * Click Delete to confirm stack deletion
  * ![Delete stack](/images/1-Worklog/1.3-Week3/Day4/Deletestack.png)
  * Wait for the deletion process to complete:
    * The stack will show “DELETE_IN_PROGRESS” status during deletion
    * After completion, the stack will disappear from the list
  * ![Delete complete](/images/1-Worklog/1.3-Week3/Day4/Deletecomplete.png)