---
title: "Week 6 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.6. </b> "
---

### Week 6 Objectives:

* Enhance the Frontend Dashboard with new features and functional pages
* Practice deploying AWS Storage Gateway and File Shares
* Learn virtual machine migration using AWS VM Import/Export
* Manage AWS resources using Tags and Resource Groups
* Deploy and evaluate security controls with AWS Security Hub

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
|  6  | - Frontend Dashboard | 11/08/2025 | 11/08/2025 | <https://cloudjourney.awsstudygroup.com/> |
|  2  | - AWS Storage Gateway and File Shares Hands-on Lab | 12/08/2025 | 12/08/2025 | <https://cloudjourney.awsstudygroup.com/> |
|  3  | - Virtual Machine Migration Guide | 13/08/2025 | 13/08/2025 | <https://cloudjourney.awsstudygroup.com/> |
|  4  | - AWS Tags and Resource Group | 14/08/2025 | 15/08/2025 | <https://cloudjourney.awsstudygroup.com/> |
|  5  | - Hands-on AWS Security Hub: Enable, Evaluate Security Standards, and Resource Cleanup | 15/08/2025 | 15/08/2025 | <https://cloudjourney.awsstudygroup.com/> |

### Week 6 Achievements:

## Friday: Frontend Dashboard (Track B)
  * **Overview of the devphu branch**
    * The devphu branch is the main development branch for Track B (Real-time & UX Dashboard). This week focused heavily on UI/UX polishing, feature expansion, user experience improvements, and adding new pages
    * The frontend has now moved into the advanced implementation + refinement phase, still using high-quality mock data while being well-prepared for future backend integration

  * **Changes & NEW Features Added**
    * Major updates:
      * Fully fixed Light/Dark Mode: Resolved theme toggle bugs, improved smooth transition animations, and synchronized color consistency across the entire application
      * Improved Animation & Lists: Optimized animations for new alerts, smoother sort/filter behavior, enhanced loading states, and better transitions
      * Refactored component structure: Reorganized components more clearly by module (dashboard, network, reports, playbooks, integrations...)

    * Newly added features:
      * Network Monitoring Page:
        * NetworkChart.tsx (real-time line chart)
        * NetworkStreamTable.tsx
        * NetworkStats.tsx
        * useNetworkStream hook
        * NetworkGenerator & NetworkConfig (mock data)
      * Playbooks Page: PlaybookList, PlaybookCard, PlaybookModal, PlaybookFilters
      * Reports Page: ExecutiveSummaryTab, ThreatIntelTab, AIPerformanceTab, InfrastructureTab, ReportFilters
      * Integrations Page: IntegrationGrid, IntegrationCard, IntegrationFormModal, IntegrationTabs
      * Settings Page
      * New shared components: FloatingPanel, BottomWidgets, SecondaryWidgets, AnalyticsZone
      * New hooks:
        * useRealtimeBuffer.ts
        * useThreatAnalytics.ts
        * useNetworkStream.ts
      * Mock data optimization: Updated securityData.ts and generators (networkGenerator, syslogGenerator)

  * **Frontend Structure - Latest Update**
Bash
frontend/src/
├── components/
│   ├── common/              # EventModal, FloatingPanel...
│   ├── dashboard/           # KPIOverview, AnalyticsZone, BottomWidgets...
│   ├── network/             # NetworkChart, NetworkStreamTable... (NEW)
│   ├── playbooks/           # PlaybookList, PlaybookModal... (NEW)
│   ├── reports/             # Report tabs (NEW)
│   ├── integrations/        # Integration components (NEW)
│   └── layout/              # Sidebar, Header...
├── pages/
│   ├── Dashboard.tsx
│   ├── NetworkMonitoringPage.tsx   (NEW)
│   ├── PlaybooksPage.tsx           (NEW)
│   ├── ReportsPage.tsx             (NEW)
│   ├── IntegrationsPage.tsx        (NEW)
│   └── SettingsPage.tsx            (NEW)
├── hooks/                   # useSocket, useRealtimeBuffer, useNetworkStream...
├── mocks/
├── utils/
├── types/
└── App.tsx

  * **Core Features - Current Progress**
    * Completed successfully:
      * Smooth Dark/Light mode + animations
      * KPI Overview
      * Realtime Alert Feed (improved lists & animations)
      * Event Detail Modal (detailed view, MITRE, Evidence, AI Analysis)
      * Header (WebSocket status, AI Engine, User)
      * Network Activity Page (new)
      * Playbooks & Reports sections
    * Ready for integration:
      * WebSocket client (useSocket.ts)
      * Contract data (snake_case ↔ camelCase)
      * Action buttons (Block IP, Export, Create Ticket)

  * **Local Setup Guide**
Bash
cd frontend
pnpm install
cp .env.example .env
pnpm dev

## Monday: AWS Storage Gateway and File Shares Hands-on Lab
* **Overview**
  * This workshop helps learners understand and practice:
    * How to initialize Storage Gateway
    * How to create File Shares
    * How to connect/mount File Sharing drives to an On-premises server

* **Detailed Step Structure**
  * **Preparation**
    * Create an S3 Bucket: Create an Amazon S3 storage bucket in the cloud where the actual data will be synchronized and stored
    * Create an EC2 Instance for Storage Gateway: Configure an Amazon EC2 virtual machine to act as or simulate the Storage Gateway in the lab environment

  * **Using AWS Storage Gateway**
    * Create Storage Gateway: Configure and activate the Storage Gateway to establish connectivity between local infrastructure and the cloud
    * Create File Shares: Configure shared folders based on the previously created S3 bucket
    * Mount File Shares on an On-premises Machine: Provide commands or instructions for a local server to recognize and use the network drive like a normal disk

  * **Clean Up Resources**
    * Instructions for deleting created resources (S3 Bucket, EC2, Storage Gateway, etc.) after completing the lab to avoid unexpected charges on your AWS account

* **Create an S3 Bucket**
  * Access the S3 service management console
    * Click Create bucket
  * Set the S3 bucket name to `s3-instancestoragegw-2023`
  * Scroll down and click Create bucket
  * Ensure the bucket is successfully created as shown below before proceeding to the next steps

* **Create an EC2 Instance for Storage Gateway**
  * Access the Storage Gateway service management console
    * Use the Singapore Region (`ap-southeast-1`) if the region has changed
    * Click Create gateway

  * Scroll down to the Platform options section and select Amazon EC2
    * Click Customize your settings
    * Select Launch instance

  * AWS will automatically choose the AMI for the deployment

  * Scroll down to the Instance type section and select `m4.large`

  * Scroll down to the Key pair section and select Create new key pair
    * Set the Key pair name to `storagegw-key`
    * Select RSA in the Key pair type section
    * Select `.pem` in the Key pair file format section
    * Click Create key pair
    * Then select `storagegw-key` in the required Key pair name field

  * Scroll down to the Network settings section and select Edit

  * Scroll down to the Firewall (security groups) section
    * In the Security group name field, enter `storagegw-instance-sg`
    * In the Description field, enter `storagegw-instance-sg`

  * Scroll down to the Inbound security group rules section
    * Click Add security group rule to add a new rule
    * In the Type field, select Custom TCP
    * In the Port range field, enter `111`
    * In the Source type field, select Custom
    * In the Source field, enter `0.0.0.0/0`
    * Repeat similarly for the remaining rules
    * Rule 3, 4
    * Rule 5, 6
    * Rule 7, 8
    * Rule 9, 10
    * Rule 11, 12
    * Rule 13, 14
  
  * Scroll down to the Configure storage section
    * Click Add new volume
    * Enter `150` for the volume size

  * Click Launch instance

  * Click View all instances, select the Public IP of the instance, and save it for use in the next step

* **Create Storage Gateway**
  * **Create Storage Gateway**
    * Access the Storage Gateway service management console
      * Use the Singapore Region (`ap-southeast-1`) if the region has changed
      * Click Create gateway

    * In the Gateway settings section
      * In the Gateway name field, enter `filesgw`

    * Scroll down to the Platform options section and select Amazon EC2
      * Click Customize your settings

    * Scroll down and select I completed all the steps above and launched the EC2 instance
      * Click Next

    * In the Gateway settings section
      * In the Gateway name field, enter `54.179.17.167` (the Public IP of the instance created in step 1.2)
      * Click Next

    * On the Review and activate page, click Next

    * In the Configure cache storage section, set Allocated to to Cache
      * In the CloudWatch log group section, select Deactivate logging

    * In the CloudWatch alarms section
      * Click No alarm
      * Then select Configure
      * Complete the Gateway creation process

  * **Configure SMB Settings**
    * When using SMB File Shares for Windows machines, authentication for SMB must be configured:
      * Access the Storage Gateway service management console
        * Click Gateways
        * Select the Gateway created previously
        * Click Actions
        * Click Edit SMB settings
        * Click Guest access settings

      * In the Guest password field, enter a password of your choice and remember it for later use
        * Click Save changes

* **Create File Shares**
  * Access the Storage Gateway service management console
    * Click File Shares
    * Click Create file share

  * In the Gateway field, select `filesgw`
    * In the File share type field, select SMB
    * In the Amazon S3 bucket name field, select `s3-instancestoragegw-2023` (the S3 bucket created earlier)
    * In the User Authentication field, select Guest access
    * Then click Configure
    * Enter the password created earlier and click Save

  * Scroll down and click Create file share
    * File Shares creation is now complete

* **Mount File Shares on an On-premises Machine**
  * Access the Storage Gateway service management console
    * Click File Shares
    * Click the File Share you created
  
  * In the information section of the created File Share, AWS will display a command that you can use to mount the file share
  * On your Windows On-premises machine, use Command Prompt to run the command
  * Enter the Guest password configured earlier and press Enter
  * Check Windows File Explorer and you should see a new Z drive appear
  * Create a file in this drive and check the S3 bucket again — the file will be synchronized to the S3 bucket
    * Access the previously created S3 bucket to verify the synchronized file

* **Clean Up Resources**
  * **Delete Storage Gateway**
    * Access the Storage Gateway service management console
      * Select the Singapore Region
      * Click Gateways
      * Select the Gateway created earlier
      * Click Actions
      * Click Delete gateway
      * Delete Storage Gateway
      * Type `delete`
      * Click Delete to confirm deletion

  * **Delete EC2 Instance**
    * Access the Amazon EC2 console
      * In the left navigation pane, select Instances
      * Select the EC2 instance created for the lab
      * Click Instance state
      * Click Terminate instance
      * Click Terminate

  * **Delete S3 Bucket**
    * Access the S3 service management console
      * Select the S3 bucket `s3-instancestoragegw-2023`
      * Click Empty

    * Enter `permanently delete` to confirm, then click Empty to remove all data in the S3 bucket
      * Click Exit to return to the S3 interface

    * Select the S3 bucket `s3-instancestoragegw-2023`, then click Delete

    * Enter the bucket name and click Delete bucket to remove the S3 bucket

## Tuesday: Virtual Machine Migration Guide (AWS VM Import/Export)
* **Overview**
  * **Core Concepts:**
    * **VM Import/Export:** A feature that allows you to migrate virtual machine images from your on-premises environment to Amazon EC2, and vice versa (exporting from EC2 back to on-premises). This feature helps you to:
      * Migrate existing applications and workloads to Amazon EC2
      * Create backups of on-premises virtual machines on Amazon EC2
      * Support disaster recovery scenarios
      * Cost: This feature is available at no additional service charge (you only pay for the actual EC2 resources and Amazon S3 storage used)

    * **Amazon S3:** An object storage service used in this lab to store virtual machine files before importing or after exporting. Each bucket can store objects up to 5 TB in size, with no limit on the total number of files.

* **Detailed Step-by-Step Lab Structure**
  * The navigation menu of the website divides the practical roadmap into the following specific chapters:
    * **VMWare Workstation**
      * Instructions on preparing and configuring the virtual machine environment on VMware Workstation software at your local machine/on-premises to act as the sample resource for the lab exercise.

    * **Import virtual machine to AWS**
      * This process is broken down into 4 steps:
        * Export Virtual Machine from On-premises: Export the virtual machine file from the local virtualization environment (VMware) into formats supported by AWS (such as OVA, VMDK, VHD, etc.).
        * Upload virtual machine to AWS: Use the AWS CLI or AWS Console to upload the exported virtual machine file to an Amazon S3 bucket.
        * Import virtual machine to AWS: Execute the command/configure the VM Import service to convert the virtual machine file stored in S3 into an Amazon Machine Image (AMI) or Snapshot.
        * Deploy Instance from AMI: Proceed to launch (deploy) a new EC2 Instance from the successfully imported AMI file to verify its operation.

    * **Export instance from AWS**
      * The process of bringing a virtual machine from the cloud back to a local machine includes:
        * Setting up S3 bucket ACL: Configure Access Control List (ACL) permissions for the S3 bucket to grant the VM Export service permission to write the virtual machine configuration files into it.
        * Export virtual machine from Instance: Instructions on how to directly export a running EC2 Instance into a downloadable virtual machine file.
        * Export virtual machine from AMI: Instructions on how to export an AMI backup into a virtual machine file.

    * **Additional Content**
      * **Reference video:** Provides visual instructional videos to help learners easily follow along with each practical step.
      * **Resource Cleanup on AWS Cloud:** Instructions on cleaning up resources after completing the lab (Deleting EC2 instances, deleting AMIs, deleting S3 buckets) to avoid unexpected costs on your AWS Cloud account.

* **Virtual Machine Preparation**
  * Start by installing VMware Workstation Pro from here.
  * Next, download the Ubuntu operating system.
  * Open VMware Workstation and select **Create a New Virtual Machine**.
  * On the **Welcome to the New Virtual Machine Wizard** screen, select **Typical (recommended)**.
  * On the **Guest Operating System Installation** screen, select the **Installer disc image file (.iso)** of the latest Ubuntu Desktop version. You can download this file from Ubuntu Releases.
  * On the **Easy Install Information** screen, enter the Username as `awsstudent` and set a corresponding password.
  * Name the instance on the **Name the Virtual Machine** screen, for example: `Ubuntu`.
  * Configure the storage capacity on the **Specify Disk Capacity** screen, enter a value of `20GB`.
  * Review the specifications and select **Finish** to begin the installation process.
  * Complete the installation process of the Ubuntu operating system on VMware.
  * Perform configuration for the user.
  * Once the installation and configuration are complete, you need to install OpenSSH Server to connect via SSH to the instance using the following commands:
    ```bash
    sudo apt install openssh-server
    sudo systemctl start ssh
    sudo systemctl enable ssh
    ```

* **Export Virtual Machine from On-premises**
  * This step guides you on how to export the virtual machine from VMware Workstation to prepare for migration to the AWS platform.
    * Open the VMware Workstation application, select the virtual machine you want to export, then click on **File** and select **Export to OVF…**
    * Select the destination path to save the exported virtual machine files.
    * Wait about 5 minutes for the export process to complete.
    * Navigate to the folder where you chose to save the exported virtual machine. The crucial file we will use is the `.vmdk` file.

* **Upload Virtual Machine to AWS**
  * **Create an S3 bucket to store the virtual machine**
    * To create an S3 bucket, perform the following steps:
      * Access the Amazon S3 console.
        * In the navigation pane, select **Buckets**.
        * Select **Create bucket** to create a new S3 bucket.

      * On the **Create bucket** page, configure the parameters for the S3 bucket:
        * **Bucket name:** Enter a name for your bucket. This name must be globally unique. (Example: `import-bucket-2023`)
        * **AWS Region:** Select the Region for the bucket.

      * Uncheck the **Block all public access** option to allow public access. AWS will display a warning; select **I acknowledge that the current settings might result in this bucket and the objects within becoming public**.

      * Select **Create bucket**.

      * The bucket is successfully created.

  * **Upload the virtual machine to the S3 bucket**
    * After creating the bucket, we will next upload the virtual machine files exported from the on-premises virtualization environment.
      * Access the newly created S3 bucket. (Example: `import-bucket-2023`)
      * In the **Objects** section, select **Upload**.

    * Drag and drop the virtual machine files into this window or select **Add files** to choose the virtual machine files. Then, click **Upload**. In this example, since we created the virtual machine using VMware Workstation, the virtual machine file is `Ubuntu-disk1.vmdk`.

    * The process of uploading the file to the S3 bucket will take a certain amount of time.

* **Import Virtual Machine to AWS**
  * Before performing the virtual machine import into AWS, you need to create the required IAM role.
    * Access the AWS IAM console.
    * In the navigation pane, select **Roles**.
    * If the `vmimport` role does not exist, proceed to create it.
    * Create a file named `trust-policy.json` to allow the VM Import/Export service to assume the `vmimport` role.
    * Use the AWS CLI command `create-role` to create the `vmimport` IAM role and attach the trust policy.
    * Verify the created role in the IAM console.
    * View the **Trust relationships** of the role.
    * Create a file named `role-policy.json` containing the required IAM policies.
    * Attach the policy to the `vmimport` role using the AWS CLI command `put-role-policy`.
    * Verify the permissions of the role in the IAM console.

  * **Import the virtual machine as an AMI**
    * Use the AWS CLI to import the virtual machine into an AMI:
      * Run the AWS CLI command `aws ec2 import-image`:
      * The import process may take 5-10 minutes depending on the size of the virtual machine
      * Once completed, the new AMI will appear in the AMIs list with the AMI name set as the task ID
      * Check to ensure that the Amazon EBS volume is not encrypted

* **Deploy an EC2 Instance from the AMI**
  * Below are the detailed instructions to deploy an EC2 instance from the imported AMI:
    * Access the Amazon EC2 console
    * In the navigation pane, select **AMIs**
    * Find and select the AMI you just imported (e.g., `import-ami-08a9efac866dfcb04`) and click the **Launch instance from AMI** button
    * **Name:** Enter a name for the EC2 instance, for example: `Import-Server`
    * **AMI:** Leave the default selected AMI as it is
    * **Instance type:** Keep the default selected instance type and click **Create new key pair**
    * **Key pair name:** Enter a name for the key pair and click **Create key pair**
    * **Network settings:** Keep the default network configurations
    * Click **View all instances**
    * Confirm the information of the newly created instance
    * Establish an SSH connection to the instance
    * Select **SSH client** to get the connection details
    * Complete entering the SSH connection details
    * Enter the password to complete the SSH authentication
    * After the SSH connection is successful, you have finished deploying the EC2 instance from the AMI and can verify connectivity using the `ping` command

* **Configure ACL for S3 Bucket**
  * **Guide to storing the Export file on Amazon S3 Bucket**
    * When exporting an instance from the AWS environment to other virtualization environments, storing them in an S3 bucket is very important

  * **Create an S3 Bucket to store the Export file**
    * Access the Amazon S3 Management Console
    * In the navigation pane, select **Buckets**
    * Click **Create bucket** to create a new S3 bucket
    * On the **Create bucket** page, enter the required information:
      * **Bucket name:** Enter a name for the bucket. The name must be globally unique. Example: `export-bucket-2023`
      * **AWS Region:** Select the region for the bucket

  * **Configure Block Public Access and Permissions**
    * Uncheck **Block all public access** to allow public access. AWS will display a warning; you need to check **I acknowledge that the current settings might result in this bucket and the objects within becoming public**
    * Click **Create bucket**

  * **Configure Access Control List (ACL)**
    * Select **Bucket owner enforced** in the **Object Ownership** section
    * **Enable ACLs**, then click **Save changes**
    * Click **Add grantee**
    * Enter the **Canonical ID** and select **Write Objects** and **Read bucket ACL** permissions, then click **Save changes**

  * Note: The Canonical ID varies depending on the AWS Region. Below is the list of Canonical IDs for the user `vm-import-export@amazon.com` by region

  * **List of Canonical IDs for the user `vm-import-export@amazon.com` by AWS Region:**
    * Africa (Cape Town)
    * `f7744aeebaf91dd60ab135eb1cf908700c8d2bc9133e61261e6c582be6e33ee`
    * Asia Pacific (Hong Kong)
    * `97ee7ab57cc9b5034f31e107741a968e595c0d7a19ec23330eae8d045a46edfb`
    * Europe (Milan)
    * `04636d9a349e458b0c1cbf1421858b9788b4ec28b066148d4907bb15c52b5b9c`
    * Middle East (Bahrain)
    * `aa763f2cf70006650562c62a09433f04353db3cba6ba6aeb3550fdc8065d3d9f`
    * China (Beijing)
    * `834bafd86b15b6ca71074df0fd1f93d234b9d5e848a2cb31f880c149003ce36f`
    * AWS GovCloud (US)
    * `af913ca13efe7a94b88392711f6cfc8aa07c9d1454d4f190a624b126733a5602`
    * Other Regions
    * `c4d8eabf8db69dbe46bfe0e517100c554f01200b104d59cd408e777ba442a322`

* **Export Virtual Machine from EC2 Instance**
  * **Export Virtual Machine from EC2 Instance**
    * Access the Amazon EC2 console to get the Instance ID that needs to be exported

    * Run the command `aws ec2 create-instance-export-task` to initiate the EC2 Instance export task into a format suitable for the target virtualization environment. The following parameters must be entered:
      * `--instance-id`: The Instance ID obtained from the EC2 instances list
      * `--target-environment`: The target virtualization environment (e.g., `vmware`)
      * `--export-to-s3-task`: Specifies the parameters of the exported virtual machine:
        * Format (`vmdk`)
        * Target S3 bucket (`export-bucket-2021`)
        * Prefix in the bucket (`vms/`)
      * To avoid input errors, create a JSON file named `export-task.json` containing the parameters for `--export-to-s3-task`

    * The export process may take some time. Use the following command to check progress:

    * Once completed, the virtual machine file will be stored in the specified S3 bucket

  * **Testing Deployment of the Exported Virtual Machine**
    * After downloading the disk image file (VMDK or VHD) to your on-premises system, you can deploy the virtual machine using this file on the corresponding virtualization platform (VMware or Hyper-V)

* **Export Virtual Machine from AMI**
  * **Export Virtual Machine from Amazon EC2 AMI**
    * To export a virtual machine for deployment on an on-premises virtualization environment, AWS supports exporting from an AMI using the AWS CLI
    * Access the EC2 Management Console to get the AMI ID that needs to be exported

    * Run the command `aws ec2 export-image` to initiate the AMI export process into the desired format for your virtualization environment.
      * `--image-id`: The AMI ID obtained from the EC2 instance list.
      * `--disk-image-format`: The virtual machine/virtual disk file format (e.g., `vmdk` or `vhdx`).
      * `--s3-export-location`: Defines the location where the file will be exported:
        * Target S3 bucket (e.g., `import-bucket-2021`)
        * Storage path prefix within the bucket (e.g., `export/`)

    * The process of exporting an AMI to a VHD file (for deployment on Hyper-V) or VMDK (for VMware) will take some time. You can use the command `aws ec2 describe-export-image-tasks` to check the export progress

    * Once completed, you will have the virtual disk file of the virtual machine stored in the S3 bucket

  * **Testing Deployment of the Exported Virtual Machine**
    * After downloading the VHD virtual disk file to your on-premises system, you can attempt to deploy the virtual machine using this VHD file on the corresponding virtualization platform

## Wednesday:Hands-on Lab – AWS Tags and Resource Groups
* **Overview & Concepts**
  * **Tag:** Labels (entered as Key–Value pairs) assigned to AWS resources to classify them by purpose, owner, or environment, helping users easily search for and manage resources when the number of resources grows large.
  * **AWS Resource Groups:** A feature that helps manage and automate operations across multiple resources at once by grouping them based on Tags (Tag-based) or by CloudFormation stacks.

* **Detailed Hands-on Workshop Steps**
  * The lesson content is divided into clear sections for learners to follow:
    * **Introduction:** Overview of the reasons and benefits of tagging resources and creating resource groups.
    * **Using Tags:**
      * Using tags through the AWS Management Console:
        * **Create an EC2 Instance with tags:** Step-by-step instructions to launch a virtual machine and attach identification tags during creation.
        * **Add or remove tags:** How to modify, add, or delete tags from existing resources.
        * **Filter resources by tags:** How to quickly search for resources using tag-based filters.
      * Using tags through the AWS CLI: Instructions for managing, assigning, and filtering tags using the AWS Command Line Interface (CLI).
    * **Create a Resource Group:** Instructions for creating a Resource Group based on tag conditions (Tag-based) for centralized management.
    * **Clean up resources:** Instructions for removing resources created during the lab to avoid unwanted AWS charges.

* **Create an EC2 Instance with Tags**
  * Access the EC2 Management Console.
    * Click **Launch Instances**.
  * Click **Select** to choose an AMI.
  * On the **Choose an Instance Type** page:
    * Click **Review and Launch**.
  * On the **Review Instance Launch** page:
    * Scroll to the bottom of the page.
    * Click **Edit Tags** to configure tags for the EC2 instance.
  * Click **Add Tag** to add a new tag.
  * Enter the tag values as shown below and click **Review and Launch**.
  * Click **Launch** to create the EC2 instance.
  * Select **Create a new key pair**.
    * Set **Key pair type** to **RSA**.
    * Set **Key pair name** to **TestTagging**.
    * Click **Download Key Pair**.
    * Click **Launch Instances**.
  * Click **View Instances** to view the EC2 instance you just created.
  * Select the EC2 instance you created.
    * Click the **Tags** tab to verify the created tags.
  * Repeat steps 1–10 to create another EC2 instance with the following tags:
    | Key         | Value       |
    | ----------- | ----------- |
    | Owner       | Yourname    |
    | Service     | Yourservice |
    | Environment | UAT         |
  * In the next step, we will add additional tags to our EC2 instances.

* **Add or Remove Tags**
  * **Add or remove tags for individual resources**
    * Access the Amazon EC2 Console.
    * From the top navigation bar, select the Region where you want to perform the operation (currently we are using the Singapore Region).
    * In the left navigation pane, select the resource type you want to tag (for example, **Instances**).
    * Select the target resource from the resource list, open the **Tags** tab, and click **Manage tags**.
    * Click **Add tag**, enter the **Key** and **Value** information as shown below, and click **Save**.
      * We have added a tag to identify the operating system of the EC2 instance.

  * **Add or remove tags for multiple resources**
    * Access the Amazon EC2 Console.
    * In the left navigation pane, select **Tags**.
    * Click **Manage Tags**.
    * On the **Manage Tags** page, select the resource type to filter under **Filter** (for example, **Instances**).
    * To add tags to multiple resources:
      * Select the resources you want to tag.
      * Under **Add Tag**, enter the **Key** and **Value**, then click **Add Tag**.
    * To remove tags from multiple resources:
      * Select the resources whose tags you want to remove.
      * Under **Remove Tag**, enter the **Key** and click **Remove Tag**.

* **Filter Resources by Tags**
  * Click **Instances** to return to the EC2 instance list.
  * Click the **Filter Instances** box.
    * Select the **Owner** tag from the list.
  * Select **Owner: Your Name**.
  * The results will display the resources tagged with the corresponding value.
  * After completion, select **Clear Filters** to remove the applied filters.

* **Using Tags with the AWS CLI**
  * **Add tags to existing resources**
    * Use the CLI command **create-tags** with the parameters `--resources` and `--tags`.
      * `aws ec2 create-tags --resources <ResourceID> --tags Key=<Key>,Value=<Value>`
    * Example: To create a tag `Key=Environment,Value=Test` for an EC2 instance:
      * `aws ec2 create-tags --resources i-01234example56789 --tags Key=Environment,Value=Test`

  * **Add tags when creating new resources**
    * **Add tags to a new EC2 instance**
      * Use the CLI command **run-instances** and specify tags using the `--tag-specifications` parameter as follows:
        ```bash
        aws ec2 run-instances \
        --image-id <image-id> \
        --count 1 \
        --instance-type t2.micro \
        --key-name <YourKeyPair> \
        --subnet-id <YourSubnetID> \
        --tag-specifications ResourceType=instance,Tags=[{Key=Environment,Value=Test}] ResourceType=volume,Tags=[{Key=Environment,Value=Test}]
        # The volume created together with the instance will also have the tag "Key=Environment,Value=Test"
        ```
      * Note: Replace the parameters with values appropriate for your AWS account.

    * **Add tags to a new EBS volume**
      * Use the CLI command **create-volume** and specify tags using the `--tag-specifications` parameter as follows:
        ```bash
        aws ec2 create-volume \
        --availability-zone ap-southeast-1a \
        --volume-type gp2 \
        --size 80 \
        --tag-specifications ResourceType=volume,Tags=[{Key=Environment,Value=Test},{Key=cost-center,Value=cc123}]
        # The created volume will be assigned two tags: "Key=Environment,Value=Test" and "Key=cost-center,Value=cc123"
        ```
      * Note: Replace the parameters with values appropriate for your AWS account.

  * **Describe tagged resources**
    * Use the CLI command **describe-instances** with the `--filters` parameter:
      * `aws ec2 describe-instances --filters Name=tag-key,Values=<SampleTagKey>`

* **Create a Resource Group**
  * In this step, you will create a Resource Group categorized by tags. In this lab example, you may use the tags created earlier.
    * Access the AWS Resource Groups Console.
    * In the left navigation pane, click **Create Resource Group**.
    * On the **Create query-based group** page, under **Group type**, select **Tag-based** to create a Resource Group categorized by tags.
    * Under **Grouping criteria**, perform the following:
      * Select **AWS::EC2::Instance** as the resource type. You can select up to 20 resource types.
    * Under **Tags**, enter the tag `Key=BusinessUnit,Value=Marketing`, then click **Add**. You may also use tags created in previous steps.
    * Click **Preview group resources** to display matching resources under **Group Resources**.
    * Under **Group details**, enter the following:
      * **Group name:** MarketingBU
      * **Group description (optional):** Enter a description for the Resource Group (for example: *Servers of Marketing BU*)
      * Review the configuration and click **Create group**.
    * After the Resource Group has been successfully created:
      * Click **Saved Resource Groups** to view all Resource Groups you have created.
    * Click the **MarketingBU** Resource Group.
    * Scroll down to the **Group resources** section to view all resources belonging to this Resource Group.

* **Clean Up Resources**
  * **Delete EC2 Instances**
    * Access the EC2 Management Console.
    * In the left navigation pane, select **Instances**.
    * Select all EC2 instances related to this lab (you can use tags to filter the instances or refer to the Resource Group created earlier).
    * Click **Actions**.
    * Click **Manage Instance State**.
    * Select **Terminate**.
    * Click **Change State**, then click **Terminate** to confirm.

  * **Delete the Resource Group**
    * Access the AWS Resource Groups Console.
    * Click **Saved Resource Groups** in the left navigation pane.
    * Select the Resource Group related to this lab (**MarketingBU**).
    * Click **Delete**, then click **Delete** again to confirm the deletion.

## Thursday: AWS Security Hub Hands-on Lab
* **Overview of AWS Security Hub**
  * AWS Security Hub is a service that provides you with a comprehensive view of high-priority security alerts and compliance status across all your AWS accounts.
  * Problem it solves: Organizations typically use many different security tools (such as firewalls, endpoint protection solutions, and vulnerability scanners). As a result, security teams often need to switch between multiple tools to manage hundreds or even thousands of alerts every day.
  * Security Hub solution: This service acts as a centralized location to organize and prioritize security alerts and findings from various AWS services (such as Amazon GuardDuty, Amazon Inspector, and Amazon Macie) as well as AWS Partner solutions.
  * Visualization capabilities: Identified security risks are summarized in an integrated dashboard with interactive charts and metrics.
  * Continuous monitoring: You can continuously monitor your environment using automated compliance checks based on AWS best practices and industry standards adopted by your organization.

* **Estimated Cost**
  * Typical cost: For accounts used only for testing, learning, and practice purposes without performing simulated attacks, the monthly cost is generally less than $1.
  * AWS Security Hub pricing details:
    * Security checks:
      * First 100,000 checks: $0.0010 per check
      * 100,001 – 500,000 checks: $0.0008 per check
      * Over 500,001 checks: $0.0005 per check
    * Finding ingestion events:
      * First 10,000 events: Free
      * From event 10,001 onward: $0.00003 per event

* **Workshop Structure**
  * The workshop is divided into the following main sections for step-by-step hands-on practice:
    * Overview – detailed content as described above
    * Security standards
    * Step-by-step guide to enabling AWS Security Hub
    * Viewing and evaluating security scores based on standards
    * Cleaning up resources after completing the workshop to avoid unexpected charges

* **Enable Security Hub**
  * **Overview**
    * To enable Security Hub, AWS provides a graphical user interface that allows users to interact with the service. In this section, we will enable Security Hub through the AWS Management Console.

  * **Enable Security Hub through the Console**
    * To enable Security Hub in a Region, follow these steps:
      * Sign in to the Amazon Management Console. In the search bar, search for the Security Hub CSPM service.
      * On the AWS Security Hub CSPM page, choose **Go to Security Hub CSPM**.
      * On the **Welcome to AWS Security Hub** page, select the security standards you want to enable, such as AWS Foundational Security Best Practices, CIS AWS Foundations Benchmark, and PCI DSS.
      * Choose **Enable Security Hub CSPM**.
      * After enabling the service, wait for Security Hub to evaluate the Security Score of your current AWS account against the selected security standards.
      * Select **Controls** to view the Security Score.

  * **Configure AWS Config**
    * In the AWS Console, search for and select **AWS Config**.
    * Choose **Get started**.
    * Under **Override settings**, select **All globally recorded IAM resource type** and choose **Exclude from recording**.
    * Under **Data governance**, select **Create AWS Config service-linked role**.
    * Under **Delivery channel**, choose **Create a bucket**, keep the default bucket name, and select **Next**.
    * Continue selecting **Next**.
    * Select **Confirm**.
    * AWS Config setup is now complete.

* **Scores for Each Security Standard**
  * After some time, Security Hub will provide evaluations based on security scores and identify existing security risks within your account. To view the detected risks, access each security standard and review its assessment results:
    * Sign in to the Amazon Management Console. In the search bar, search for the Security Hub CSPM service.
    * In the left navigation pane, choose **Security standards** to view an overview of the assessment scores for each security standard.
    * To view detailed evaluation criteria for a specific standard, choose **View results** for that standard.
      * Example: **Foundational Security Best Practices v1.0.0**
    * If there are controls that do not apply to your environment and you want to exclude them from the assessment, select the corresponding control from the standard’s results list.
      * Example: You want to exclude **EC2 instances managed by Systems Manager should have an association compliance status of COMPLIANT** from the **PCI DSS v3.2.1** standard. Choose **View results**.
    * Then select **EC2 instances managed by Systems Manager should have an association compliance status of COMPLIANT**.
      * On the control details page, choose **Disable control**.
      * Enter the reason **Not aligned to risk threshold**, then select **Disable**.

* **Resource Cleanup**
  * In this section, you will disable AWS Security Hub to avoid incurring additional charges on your AWS account (most of the cost associated with Security Hub comes from AWS Config). However, if you are working in a production environment, it is recommended to keep AWS Security Hub enabled to help manage your account security more effectively.

  * **Disable AWS Security Hub**
    * Access **Security Hub CSPM**.
      * In the left navigation pane, choose **Settings > General**.
    * On the Settings page, select the **General** tab.
      * Scroll to the bottom and choose **Disable AWS Security Hub**.
      * In the confirmation prompt, select **Disable AWS Security Hub**.
    * Then choose **Disable AWS Security Hub CSPM**.

  * **Disable AWS Config**
    * Access **AWS Config**, then on the right side select **Settings** and choose **Stop recording**.
    * Select **Confirm** to confirm the action.

  * **Delete the S3 Bucket**
    * Access **Amazon S3**.
    * Select the bucket that was created and choose **Empty**.
    * Enter **permanently delete**, then choose **Empty**.
    * After the deletion process is complete, choose **Exit**.
    * Select the bucket again and choose **Delete**.
    * Enter the bucket name and choose **Delete bucket**.
