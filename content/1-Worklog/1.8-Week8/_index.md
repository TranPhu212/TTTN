---
title: "Week 8 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.8. </b> "
---

### Week 8 Objectives:

* Learn and practice NoSQL database management with Amazon DynamoDB
* Deploy and manage a shared file storage system using Amazon FSx
* Analyze AWS costs and resource utilization with AWS Glue and Amazon Athena
* Build a Data Lake and explore end-to-end data analytics workflows on AWS
* Refactor and enhance the SOC Dashboard UI while preparing for real-time integration

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
|  6  | - Amazon DynamoDB - Managing and Querying NoSQL Databases | 05/06/2026 | 05/06/2026 | <https://000060.awsstudygroup.com/> |
|  2  | - Deploying Amazon FSx for Windows File Server | 08/06/2026 | 08/06/2026 | <https://000025.awsstudygroup.com/>> |
|  3  | - Preparing Data with AWS Glue and Analyzing Cost & Resource Utilization Using Amazon Athena | 09/06/2026 | 09/06/2026 | <https://000040.awsstudygroup.com/> |
|  4  | - AWS Analytics Lab: Data Lake, ETL and Data Analytics | 10/06/2026 | 10/06/2026 | <https://000072.awsstudygroup.com/> |
|  5  | - SOC Dashboard Refactoring & UI Enhancement | 11/06/2026 | 11/06/2026 |


### Week 8 Achievements:

## Friday: Friday: Building and Managing NoSQL Solutions with Amazon DynamoDB
* **Working with Amazon DynamoDB**
  * **Introduction**
    * Amazon DynamoDB is a fully managed NoSQL database service that delivers fast and predictable performance with seamless scalability. DynamoDB relieves the administrative burden of operating and scaling a distributed database, providing hardware provisioning, setup and configuration, replication, software patching, or cluster scaling. DynamoDB also provides encryption at rest.
    * DynamoDB creates database tables that can store and retrieve any amount of data and serve any level of request traffic. You can scale up or down the throughput capacity of your table without downtime or performance degradation.
    * DynamoDB provides on-demand backup capability. It allows you to create full backups of your tables for long-term retention and archival for regulatory compliance needs.
    * You can create on-demand backups and enable point-in-time recovery for Amazon DynamoDB tables. Point-in-time recovery helps protect your tables from accidental write or delete operations. With point-in-time recovery, you can restore a table to any point in the last 35 days.
    * DynamoDB allows you to automatically delete expired items from your table, helping reduce storage usage and costs for data that is no longer relevant.

    * **Core Components of Amazon DynamoDB**
      * Table: Similar to other database systems, DynamoDB stores data in tables. A table is a collection of data.
      * Item: Each table contains zero or more items. Items in DynamoDB are similar to the concept of rows in a relational database, records, or datasets in other database systems. In DynamoDB, there is no limit to the number of items you can store in a table.
      * Attribute: Each item consists of one or more attributes. An attribute is a basic data element that does not need to be further subdivided. Attributes in DynamoDB are similar in many ways to columns in other database systems.

      * **Primary Key**
        * When you create a table, in addition to the table name, you must specify the table's primary key.
        * The primary key uniquely identifies each item in the table, so no two items can have the same key.
        * DynamoDB supports two types of primary keys:
          * Partition key
          * Composite primary key

      * **Partition Key**
        * A simple primary key consisting of a single attribute called the Partition key.
        * DynamoDB uses the value of the partition key as input to an internal hash function. The output from the hash function determines the partition (physical storage inside DynamoDB) where the item will be stored.
        * In a table with only a partition key, no two items can have the same Partition key value.

      * **Composite Primary Key**
        * The first attribute is the partition key and the second attribute is the sort key.
        * DynamoDB uses the value of the partition key as input to an internal hash function. The output from the hash function determines the partition (physical storage inside DynamoDB) where the item will be stored.
        * All items with the same partition key value are stored together, sorted by the sort key value.
        * In a table with a partition key and sort key, multiple items can have the same partition key value. However, those items must have different sort key values.
        * Composite primary keys give you more flexibility when querying data.

    * **Secondary Index**
      * You can create one or more Secondary Indexes on a table.
      * Secondary Indexes allow you to query data in the table using keys different from the table's original partition and sort keys. With DynamoDB, querying data using indexes is much faster and more cost-effective than Scan operations.

      * **DynamoDB supports two types of indexes:**
        * Global Secondary Index: An index with a partition key and sort key that can be different from the table's keys.
        * 
        * Local Secondary Index: An index with the same partition key as the table but a different sort key.

      * Each table in DynamoDB can have up to 20 Global Secondary Indexes (default limit) and 5 Local Secondary Indexes.

    * **Naming Rules and Data Types**
      * **Naming Rules**
        * Tables, attributes, and other objects in DynamoDB must have names.
        * All names must be encoded in UTF-8 and are case-sensitive.
        * Table names and index names must be between 3 and 255 characters long and can only contain the following characters: a-z, A-Z, 0-9, _, -, and .
        * Attribute names must be at least one character long, but no longer than 64 KB.
        * Some exceptions allow attribute names up to 255 characters.

      * **Data Types**
        * DynamoDB supports many data types:
          * Scalar types: number, string, binary, Boolean, and null.
          * Document types: list and map.
          * Set types: string sets, number sets, and binary sets.

    * **Read Consistency**
      * **Eventually Consistent Reads**
        * When you read data from a DynamoDB table, the response might not reflect the results of a recently completed write operation.
        * The response might include some stale data.
        * If you repeat your read request after a short time, the response will return the latest data.

      * **Strongly Consistent Reads**
        * When you request Strongly Consistent Reads, DynamoDB returns a response with the most up-to-date data. However:
          * It might not be available in the event of a network issue.
          * It has higher latency.
          * It is not supported for Global Secondary Indexes.
          * It consumes twice the read capacity.

    * **Read/Write Capacity Mode**
      * **On-Demand Mode**
        * Pay-per-use flexible billing.
        * Suitable for unpredictable or unknown workloads.

      * **Provisioned Mode**
        * Specify the number of reads/writes per second.
        * Can use auto scaling.
        * Suitable for predictable traffic.

  * **Preparation Steps**
    * You need to create an Access key in advance to configure the AWS CLI.
    * You can access AWS DynamoDB via the AWS Management Console or AWS CLI / CloudShell.

    * **Using the AWS Management Console**
      * You can access it at https://console.aws.amazon.com/dynamodb/home
      * Main features: create tables, manage items, query/scan, indexes, monitoring, backups, etc.

    * **Creating Access Keys**
      * Create IAM Access Keys through the IAM console.

    * **Creating a Table**
      * Create a table named Music with Partition key: Artist, Sort key: SongTitle.

    * **Writing Data**
      * Add sample items to the Music table (e.g., Artist: No One You Know, Acme Band...).

    * **Reading Data**
      * Use Query or Explore items to read data.

    * **Querying Data**
      * Perform Query using Partition key and Sort key.

    * **Creating a Global Secondary Index**
      * Create a GSI on AlbumTitle.

    * **Querying the Global Secondary Index**
      * Query using the newly created index.

    * **Using AWS CloudShell**
      * AWS CloudShell is a browser-based command-line environment with AWS CLI pre-installed.

    * **Creating a Table**
      * Launch AWS CloudShell at: https://console.aws.amazon.com/cloudshell/home
      * Configure AWS CLI: `aws configure`
      * Enter Access Key, Secret Key, region (e.g., us-east-1), output format (json).
      * Create the Music table:
        bash aws dynamodb create-table \
            --table-name Music \
            --attribute-definitions \
                AttributeName=Artist,AttributeType=S \
                AttributeName=SongTitle,AttributeType=S \
            --key-schema \
                AttributeName=Artist,KeyType=HASH \
                AttributeName=SongTitle,KeyType=RANGE \
            --provisioned-throughput \
                ReadCapacityUnits=10,WriteCapacityUnits=5 \
            --table-class STANDARD

      * Check table status: aws dynamodb describe-table --table-name Music | grep TableStatus
      * Wait until TableStatus is ACTIVE.
      * Writing Data
      * Use the put-item command to add sample data:
        Bash aws dynamodb put-item \
            --table-name Music \
            --item \
                '{"Artist": {"S": "No One You Know"}, "SongTitle": {"S": "Call Me Today"}, "AlbumTitle": {"S": "Somewhat Famous"}, "Awards": {"N": "1"}}'

        aws dynamodb put-item \
            --table-name Music \
            --item \
                '{"Artist": {"S": "No One You Know"}, "SongTitle": {"S": "Howdy"}, "AlbumTitle": {"S": "Somewhat Famous"}, "Awards": {"N": "2"}}'

        aws dynamodb put-item \
            --table-name Music \
            --item \
                '{"Artist": {"S": "Acme Band"}, "SongTitle": {"S": "Happy Day"}, "AlbumTitle": {"S": "Songs About Life"}, "Awards": {"N": "10"} }'

        aws dynamodb put-item \
            --table-name Music \
            --item \
                '{"Artist": {"S": "Acme Band"}, "SongTitle": {"S": "PartiQL Rocks"}, "AlbumTitle": {"S": "Another Album Title"}, "Awards": {"N": "8"} }'

      * Reading Data
      * Use the get-item command (you can use --consistent-read for strongly consistent reads):
        Bash aws dynamodb get-item --consistent-read \
            --table-name Music \
            --key '{ "Artist": {"S": "Acme Band"}, "SongTitle": {"S": "Happy Day"}}'
      * Updating Data
      * Use the update-item command:
        Bash aws dynamodb update-item \
            --table-name Music \
            --key '{ "Artist": {"S": "Acme Band"}, "SongTitle": {"S": "Happy Day"}}' \
            --update-expression "SET AlbumTitle = :newval" \
            --expression-attribute-values '{":newval":{"S":"Updated Album Title"}}' \
            --return-values ALL_NEW
      * Querying Data
      * Use the query command by Partition Key:
        Bash aws dynamodb query \
            --table-name Music \
            --key-condition-expression "Artist = :name" \
            --expression-attribute-values  '{":name":{"S":"Acme Band"}}'

      * Creating a Global Secondary Index
        Bash aws dynamodb update-table \
            --table-name Music \
            --attribute-definitions AttributeName=AlbumTitle,AttributeType=S \
            --global-secondary-index-updates \
                "[{\"Create\":{\"IndexName\": \"AlbumTitle-index\",\"KeySchema\":[{\"AttributeName\":\"AlbumTitle\",\"KeyType\":\"HASH\"}], \
                \"ProvisionedThroughput\": {\"ReadCapacityUnits\": 10, \"WriteCapacityUnits\": 5      },\"Projection\":{\"ProjectionType\":\"ALL\"}}}]"

      * Wait for the index to become ACTIVE (check with describe-table).
      * Querying the Global Secondary Index
        Bash aws dynamodb query \
            --table-name Music \
            --index-name AlbumTitle-index \
            --key-condition-expression "AlbumTitle = :name" \
            --expression-attribute-values  '{":name":{"S":"Somewhat Famous"}}'

  * **Getting Started with AWS SDK**
    * **Configure AWS CLI**
      * Use aws configure with Access Key.

    * **Getting Started with Python and DynamoDB (Boto3)**
      * Use Boto3 Client or Resource.
      * Operations:
        * Create table
        * Write data (put_item)
        * Read data (get_item)
        * Update data
        * Delete data
        * Load sample data
        * Query data (query)
        * Scan data (scan)
        * Delete table

  * **Cleaning Up Resources**
    * Delete the table and related resources to avoid incurring costs.

## Tuesday: Building Shared File Storage Solutions with Amazon FSx
* **Implementing FSx on Windows**
  * **General Introduction**
    * Amazon FSx for Windows File Server provides fully managed shared file storage, fully integrated with Windows Server and supporting numerous administrative and data management features.
    * Main architecture:
      * File servers: EC2 instances running Windows File Server, accessed via the SMB protocol
      * Storage: Data is stored on Amazon S3 (object storage)
      * VPC: Deployed within a VPC for security
      * Networking: Uses ENI and VPC
      * Data replication: Automatic multi-AZ replication
      * Management: Fully managed by AWS (backup, patching, monitoring)

  * **Introduction**
    * Amazon FSx for Windows File Server provides fully managed shared file storage, integrated with Windows Server and offering a wide range of administrative, data management, and data access features.
    * In this hands-on lab, we will set up a shared data storage system for the Windows infrastructure.

  * **Preparation Steps**
    * To prepare for Amazon FSx for Windows File Server, you should consider the following steps:
      * Determine storage requirements: Choose appropriate capacity and performance
      * Create VPC and configure networking (subnets, security groups)
      * Set up Windows Active Directory (if integration is needed)
      * Configure Security Group for FSx
      * Plan data transfer (if applicable)
      * Create Amazon FSx file system via Console, CLI or SDK
      * Verify connectivity and access

  * **Create File Share**
    * **Connect to EC2 Windows Instance 0**
      * Open the Amazon EC2 Console
      * Select the running Windows Instance 0
      * Copy the Public DNS (IPv4)
      * Use Remote Desktop (RDP) to connect to the instance
      * Retrieve username/password from AWS Secrets Manager (Secret name containing "Password-<GUID>")

    * **Map the Default File Share**
      * In File Explorer on the Windows Instance:
        * Right-click This PC → Map network drive
        * Drive: Z:
        * Folder: UNC path of the default file share (e.g.: \\fs-0123456789abcdef.example.com\share)
          * Copy DNS Name from the Network & security tab of the FSx file system
          * Check Reconnect at sign-in

      * Create some test files on drive Z:

      * Download sample data from NASA NEX (using PowerShell):  
        powershell Read-S3Object -BucketName nasanex -KeyPrefix /AVHRR -Folder Z:/nasanex/AVHRR (The download process takes approximately 20 minutes).

  * **Create New File Share**
        * Open the Amazon FSx Console → Select the file system → Network & security tab → Copy DNS Name.
        * On the Windows Instance: Start → type `fsmgmt.msc`.
        * Action → Connect to another computer → Paste DNS Name.
        * In Shares → Action → New Share….
        * Create the following shares (on drive D:):

          | Folder path     | Share name   | Create new path | Shared folder permissions      |
          |-----------------|--------------|-----------------|--------------------------------|
          | D:\application  | application  | Yes             | Everyone - Full Control        |
          | D:\data         | data         | Yes             | Everyone - Full Control        |

        * Experiment with creating additional shares on drive D:

      * **Manage File Shares via PowerShell Remote**
        * Get the Windows Remote PowerShell Endpoint from the Network & security tab of FSx.
        * Run the script to connect remotely:
          ```powershell
          $WindowsRemotePowerShellEndpoint = "fs-0123456789abcdef.example.com"
          Enter-PSSession -ComputerName ${WindowsRemotePowerShellEndpoint} -ConfigurationName FsxRemoteAdmin

      * Check the following commands:
        PowerShell  Get-Command
                    Get-FSxSmbShare
                    Get-FSxSmbSession
                    Get-FSxSmbServerConfiguration
                    Get-FSxSmbShareAccess

  * **Performance Testing**
      * **Performance Testing**
        * This section will test the performance of STG326 - SAZ
        * There are many disk performance testing tools. The lab has pre-installed DiskSpd and fio on Windows Instance 0.
      
      * **DiskSpd Read Tests**
        * RDP into Windows Instance 0
        * Open Windows PowerShell
        * Create a 100GB test file:
          ```powershell
          $random = $(Get-Random)
          fsutil file createnew Z:\${env:computername}-$random.dat 100000000000
        * Run the read test: C:\Tools\DiskSpd-2.0.21a\amd64\DiskSpd.exe -d120 -w0 -r -t1 -o32 -b64K -Su -L Z:\${env:computername}-$random.dat
        * While running, open Task Manager → Performance → Ethernet to monitor

    * **Questions:**
      * What is the highest read throughput achieved?
      * P99 latency?
      * Total IO MiB/s?
      * IOPS?
      * AvgLat?
      * Why is the actual throughput higher than the baseline?
      * Experiment with different parameters (-b, -o, -t, -Su, etc.)

    * **DiskSpd Write Tests**
      * Run the write test:
        ```powershell
        $random = $(Get-Random)
        C:\Tools\DiskSpd-2.0.21a\AMD64\DiskSpd.exe -d120 -c2G -s64K -w100 -t1 -o32 -b64K -Sh -L Z:\${env:computername}-$random.dat
      * Monitor similarly and answer the questions about write performance.

    * **fio Read / Write Tests**
      * Use fio to test:
        ```powershell
        # Read test
        $random = $(Get-Random)
        C:\Tools\fio-3.16-x64\fio --randrepeat=1 --direct=1 --name="Z:\${env:computername}-$random.dat" --numjobs=1 --bs=64K --iodepth=32 --size=1024M --readwrite=read --rwmixread=100 --thread --time_based --runtime=120

  * **Performance Monitoring**
    * This section will monitor the performance of STG326 - SAZ

    * **CloudWatch Dashboard**
      * Open the CloudWatch Console
      * Select Dashboards from the left menu
      * Select the pre-created dashboard (name usually region-fs-id, e.g.: us-east-2-fs-0123456789abcdef)
      * Explore the widgets, zoom in/out, and observe time synchronization between metrics

    * **CloudWatch Alarm**
      * Copy the FSx File System ID from the dashboard
      * Maximize the Throughput (Bytes per second) widget → View in metrics
      * Find the Total Data Throughput (B/s) metric → Create alarm
      * Set threshold > 200000000 (200 MB/s)
      * Create a new SNS topic and subscribe your email
      * Name the alarm and create it
      * Confirm subscription via email
      * Re-run the performance tests (read/write) for at least 2 minutes to trigger the alarm
      * Check your email for the notification

  * **Enable Data Deduplication**
    * Use the Windows Remote PowerShell Endpoint from the Network & security tab of FSx
    * Connect via Remote PowerShell:
      ```powershell
      $WindowsRemotePowerShellEndpoint = "fs-..."
      Enter-PSSession -ComputerName $WindowsRemotePowerShellEndpoint -ConfigurationName FsxRemoteAdmin
    * View commands:  
        ```powershell
        Get-Command *-FSxDedup*
    * Enable: Enable-FSxDedup
    * Check status:
        Get-FSxDedupConfiguration
        Get-FSxDedupStatus
        Get-FSxDedupJob
    
    * **Create Optimization Schedule**
      * Create DailyOptimization schedule
      * Update `MinimumFileAgeDays = 0`
      * Run the job and monitor with `Get-FSxDedupStatus` to see saved capacity

    * **Enable Shadow Copies**
      * Connect to Remote PowerShell as above
      * View commands:  
        ```powershell
        Get-Command *-FSxShadow*
        ```
      * Set defaults: Set-FsxShadowStorage -Default
                      Set-FsxShadowCopySchedule -Default
      * Check:  Get-FSxShadowCopies
                Get-FSxShadowCopySchedule
                Get-FSxShadowStorage

    * **Modify and Create Shadow Copy**
      * Set max size 20%: `Set-FSxShadowStorage -maxsize "20%"`
      * Create new Shadow Copy: `New-FSxShadowCopy`
      * Test restoring previous versions via File Explorer

  * **Manage User Sessions and Open Files**
    * **Via GUI (fsmgmt.msc)**
      * Connect to the FSx DNS Name
      * View Sessions and Open Files
      * Run DiskSpd test and observe open file → Close Open File

    * **Via PowerShell Remote**
      * Connect to Remote PowerShell.
      * View commands: `Get-Command *SmbSession*`, `Get-Command *Open*`
      * Run test and use:  
        ```powershell
        Get-FSxSmbOpenFile
        Close-FSxSmbOpenFile

  * **Enable User Storage Quotas**
    * Connect to Remote PowerShell.
    * View commands: `Get-Command *-FSxUserQuota*`
    * Enable quota:  
      ```powershell
      Enable-FSxUserQuotas -Track -DefaultLimit 200000000000 -DefaultWarningLimit 100000000000
    * Create a large file exceeding the limit → Check with `Get-FSxUserQuotaEntries`
    * Switch to Enforce mode and test.
    * Disable: `Disable-FSxUserQuotas`

  * **Enable Continuously Available Share**
    * Use Multi-AZ file system.
    * Create folder D:\sql
    * Create CA Share:  
      ```powershell
      New-FSxSmbShare -Name "SQL CA Share" -Path "D:\sql" -Description "SQL CA share" -ContinuouslyAvailable $True -FolderEnumerationMode AccessBased -EncryptData $true

  * **Scale Throughput Capacity**
    * Go to FSx Console → Select MAZ file system → Update Throughput capacity to 64 MB/s
    * Monitor the Updates tab
    * The process will perform failover (Multi-AZ) or short downtime (Single-AZ)

  * **Scale Storage Capacity**
    * Go to FSx Console → Select file system → Update Storage capacity by increasing 10%
    * Monitor the Updates tab and Free storage capacity widget
    * The optimization process runs in the background (may take several hours/days)

  * **Resource Cleanup**
    * Delete manual backups (if any)
    * Delete Multi-AZ file system
    * Delete the CloudFormation stack to clean up the entire environment

## Tuesday: AWS Cost and Performance Analysis with Glue and Athena
* **Introduction**
  * This section provides foundational knowledge about the two core services used in this lab:
    * **AWS Glue:** A data preparation service that supports the ETL (Extract - Transform - Load) process. The material explains the basic workflow of Glue, from extracting raw data from sources such as Amazon S3, transforming it into optimized formats (e.g., Parquet), and loading it into a data warehouse.
    * **Amazon Athena:** An interactive query service that enables users to analyze data directly in Amazon S3 using standard SQL.
    * **Operational Model:** The documentation outlines a standard seven-step workflow, starting with uploading data to S3, using a Glue Crawler to scan the data, performing ETL transformations, storing the results in Parquet format, and finally querying the data with Athena. However, to simplify the lab, the initial transformation step will be skipped, and participants will work directly with pre-existing Parquet files.

* **Preparation Steps**
  * This section guides learners through preparing the database environment for analysis and is divided into three sub-steps:
  * **Database Preparation:** Initial setup tasks, including IAM access configuration, service permissions, and preparing an S3 bucket to store input data.
  * **Database Construction:** Creating the data structure, configuring an AWS Glue Crawler to scan the provided sample Parquet files, and automatically generating tables in the Glue Data Catalog.
  * **Database Validation:** Verifying that the data has been loaded correctly and that the structure is ready for analysis.

* **Usage and Cost Performance Analysis**
  * This is the core hands-on section where learners write SQL queries in Amazon Athena to analyze reporting data:
  * **Table Data Exploration:** Examine the overall structure of the crawled dataset and understand the meaning of fields related to costs and resource usage.
  * **Cost Analysis:** Execute SQL queries to identify cost distribution, determine which services generate the highest expenses, and analyze cost growth trends over time.
  * **Tagging and Cost Allocation:** Learn how to analyze costs based on resource tags (e.g., by Dev/Prod environment, department, or project).
  * **Utilization Analysis:** Compare costs against actual resource utilization metrics (CPU usage, storage consumption, request volume, etc.) to identify idle or underutilized resources and potential cost-saving opportunities.

* **Resource Cleanup**
  * The final section explains how to remove all AWS resources created during the lab, such as deleting result S3 buckets, removing Glue databases and crawlers, and clearing Athena query history. This step is extremely important to ensure that learners' AWS accounts do not incur unexpected charges after completing the lab.

## Wednesday: Building an End-to-End Data Lake and Analytics Platform on AWS
* **Introduction & Preparation**
  * **Introduction:** Overview of services within the AWS Analytics portfolio. Core learning objectives include building a Data Lake with Amazon S3, processing real-time data, managing metadata, and optimizing query performance.
  * **Preparation Steps:** Instructions for setting up the lab environment and initializing a sample data source using Amazon RDS.

* **Data Ingestion & Storage**
  * **Creating Kinesis Firehose:** Configure Amazon Kinesis Data Firehose to continuously collect and deliver streaming data into a data lake stored on Amazon S3.
  * **Generate Dummy Data:** Provide methods or scripts to generate simulated streaming data for testing the system’s ingestion pipeline.

* **Data Discovery & Cataloging**
  * **Create IAM Role:** Configure AWS IAM permissions to allow AWS services to securely interact with one another.
  * **Creating AWS Glue Crawlers:** Set up AWS Glue Crawlers to automatically scan raw data stored in Amazon S3, discover data schemas, and register metadata in the AWS Glue Data Catalog.
  * **Verify Tables:** Validate and verify the tables automatically created in the Data Catalog.

* **Data Transformation**
  * This section guides users through performing ETL (Extract, Transform, Load) using multiple AWS tools and approaches:
  * **AWS Glue Interactive Sessions:** Run and test Spark ETL code interactively through a Jupyter Notebook environment.
  * **AWS Glue Studio:** Use a graphical drag-and-drop interface to design, execute, and monitor ETL workflows with minimal coding.
  * **AWS Glue DataBrew:** Utilize a visual data preparation tool to quickly clean, transform, and standardize data.
  * **Amazon EMR (Elastic MapReduce):** Perform large-scale data transformations by running Spark jobs on Amazon EMR clusters.

* **Data Analysis & Consumption**
  * **Analysis with Athena:** Use Amazon Athena to query and analyze data directly on Amazon S3 using standard SQL without managing infrastructure.
  * **Analysis with Kinesis Data Analytics:** Perform real-time analytics and compute metrics on streaming data as it flows through the system.
  * **Serve with Lambda:** Use AWS Lambda functions to process and serve data to downstream applications and services.
  * **Warehouse on Redshift:** Load processed data from AWS Glue/Amazon S3 into Amazon Redshift, while learning best practices and architectural patterns for optimizing data warehouse performance.

* **Visualization & Cleanup**
  * **Visualize in QuickSight:** Connect Amazon QuickSight to Athena or Redshift data sources to create dashboards, charts, and business intelligence reports.
  * **Clean Up:** Detailed instructions for removing all deployed resources, including Amazon S3, Amazon Redshift, Amazon EMR, AWS Glue, Amazon RDS, and related services.

## Thursday: Frontend Consolidation and Real-Time Integration Preparation
* **Weekly Progress Summary**
  * This week focused heavily on **refactoring and enhancing the UI of the main SOC Dashboard pages**.
    * Completed refactoring of several critical modules: Settings, Reports, Dashboard, Cloud, Threat Intel, Attack Surface, and more.
    * Resolved merge conflicts and synchronized routing and sidebar navigation.
    * Improved UI/UX consistency, especially for **Light/Dark mode**.
    * Branch `devphu` is currently **16 commits ahead** of `main`.
  * **Weekly Goal**: Build a solid frontend foundation that is ready for real-time integration with the Track A backend.

* **Commits**
  * **fix conflic** (`556d881c7e07e03edc64e9f6d9d72782fb894b93`)
    Fixed merge conflicts after integrating changes from other branches.
    **Key Changes**:
    * Updated routing configuration in `App.tsx`.
    * Imported new pages (CloudPage, ThreatIntelPage, etc.).
    * Adjusted Sidebar logic and `AppView` type definitions.
  * **refactor settings** (`660438543037e5d5ad1d9951e1bdf2273e3b8334`)
    Refactored the entire **Settings** page.
    **Highlights**:
    * Added the `zod` library for form validation.
    * Created and optimized multiple tabs: General, Appearance, AWS, AccessControl, UserManagement, AiEngineSettingsTab, Integrations, Monitoring, Backup, Dataset, Reporting, Fusion, and more.
    * Improved permission management grid, toast notifications, and dark/light mode support.
  * **refactor reports** (`1d95e6e6f193645d032472422a0cde8ff7d55754`)
    Refactored the Reports page.
  * **refactor dashboard** (`5a0ee2d71cd33cde4818639b4348884384ca48ff`)
  * **refactor cloud** (`62d0307ffd30131ad117538dc462c9d8014b5631`)
  * **refactor threat intel** (`85d2434f3ad2626c5514e955787c9e28d0f277ea`)
  * **refactor attack surface, integrations, mitre att&ck, playbooks** (`e731649666c89b2789be1a858fab5a3c05518993`)
  * Refactored AI Threat Detection, Alerts, Case Management, Endpoint, and Network modules.
  * Added new Cloud and Threat Intelligence pages.
  * Updated Attack Surface, Playbooks, and Geomap.
  * Fixed Light/Dark mode issues across multiple pages (Dashboard, Network, Alerts, Integrations, etc.).
  * Merged pull requests from feature branches.

* **Detailed Work Completed**
  * Frontend Improvements
    * **Routing & Navigation**: Synchronized React Router, Sidebar, and AppView type definitions.
    * **Settings Module**: Completed a comprehensive configuration system with robust validation.
    * **Reports**: Enhanced the reporting interface and user experience.
    * **Core Pages**: Dashboard, Cloud Security, Threat Intelligence, Attack Surface, MITRE ATT&CK, Playbooks, AI Threat Detection, Alerts, Network, and Endpoint.
    * **UI/UX Consistency**:
      * Stable Light/Dark mode implementation across the entire application.
      * Improved KPI cards, MITRE matrix, alert feed, and event detail modal.
      * Enhanced toast notifications, permission management, and responsive design.
  * Technologies & Dependencies
    * Added `zod` for schema validation.
    * Continued using React + Vite + Tailwind CSS.
    * Prepared mock data and groundwork for WebSocket integration.

* **Challenges & Solutions**
  * **Merge Conflicts**: Fully resolved through the `fix conflic` commit.
  * **UI Consistency**: Fixed Light/Dark mode issues across multiple pages.
  * **Settings Complexity**: Split into multiple dedicated components with validation support.

* **Overall Project Status**
  * **Frontend (Track B)**: In excellent condition; the SOC Dashboard UI is now largely complete and professional.
  * **Integration Readiness**: Ready to connect with Track A (API + WebSocket).
  * **Demo**: Can be demonstrated immediately by running `pnpm dev` inside the `frontend` directory.
