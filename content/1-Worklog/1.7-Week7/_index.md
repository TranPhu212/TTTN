---
title: "Week 7 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.7. </b> "
---

### Week 7 Objectives:

* Study AWS database services and fundamental database concepts.
* Practice access management and permission control using AWS IAM User, IAM Role, and Permission Boundaries.
* Explore data protection solutions on AWS with Amazon S3, AWS KMS, and CloudTrail.
* Strengthen knowledge of cloud security, monitoring, and access control mechanisms.
* Enhance the SOC Dashboard by integrating AI Threat Detection, Attack Surface Management, MITRE ATT&CK, and Case Management modules.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
|  6  | - Database Fundamentals and AWS Database Services Overview | 29/05/2026 | 29/05/2026 | <https://youtu.be/OOD2RwWuLRw> <br> <https://youtu.be/qbrobQZrokY> <br> <https://youtu.be/UvdiRW34aNI> |
|  2  | - Hands-on AWS IAM, EC2 Instance Roles, and secure access control mechanisms | 01/06/2026 | 01/06/2026 | <https://000048.awsstudygroup.com/> <br> <https://000044.awsstudygroup.com/> |
|  3  | - Practiced AWS IAM access management using Permission Boundaries, IAM Roles, and Resource Tags | 02/06/2026 | 02/06/2026 | <https://000030.awsstudygroup.com/> <br> <https://000028.awsstudygroup.com/> |
|  4  | - Building a Secure Data Protection and Cost Optimization Solution on AWS Using KMS, CloudTrail, Athena, and Lambda | 03/06/2026 | 03/06/2026 | <https://000033.awsstudygroup.com/> <br> <https://000022.awsstudygroup.com/> |
|  5  | - Expanded the routing system, updated Sidebar Navigation, and integrated advanced pages (AI Threat Detection, Attack Surface, MITRE ATT&CK, and Case Management) | 04/06/2026 | 04/06/2026 |


### Week 7 Achievements:

## Friday: Database Fundamentals and AWS Database Services Overview
* **Database Concepts**
  * **Database** is a system of structured/semi-structured information stored on storage devices to satisfy the concurrent information access requirements of multiple users or multiple application programs running at the same time for different purposes.
  * **Session** is the period from the time a connection to the database system is established (start time) until the connection is terminated (end time).
  * **Primary Key** is a special column (or combination of columns) in a relational database table designated to uniquely identify each record in the table.
  * **Foreign Key** is a column or group of columns in a relational database table that provides a link between data in two tables. It acts as a cross-reference between tables because it references the primary key of another table, thereby establishing a relationship between them.
  * **Index** is a data structure that improves the speed of data retrieval operations (read) on a database table. However, it increases write costs and storage space requirements to maintain the index structure.
  * Indexes are used to locate data quickly without scanning every row in a database table whenever the table is accessed. Indexes can be created using one or more columns of a database table.
  * **Partitions** refer to the database process in which very large tables are divided and stored as multiple smaller segments. By separating a large table into smaller, individual tables, queries that access only a subset of the data can run faster because there is less data to scan.
  * **Execution Plan / Query Plan** is a sequence of steps used to access data in a relational database management system (SQL). When a query is submitted to the database, the query optimizer evaluates several possible execution strategies and selects what it considers the best option.
  * **Database Log** is a critical component of a highly available database solution because logs enable recovery after failures and help synchronize primary and secondary databases. All databases have a logging system associated with them.
  * **Buffers** are temporary storage areas in main memory. They allow temporary data storage while data moves from one location to another. Database buffers store copies of disk blocks and are commonly used to improve read performance (reading data from buffers) and write performance (writing data to buffers first, then synchronizing them to database storage).
  * **RDBMS (SQL)** is a Database Management System (DBMS) that combines the relational data model and typically includes a Structured Query Language (SQL) programming interface.
  * Data in a relational database is organized and accessed through relationships between data items. In relational databases, these relationships are represented through tables. Dependencies between tables are expressed through data values.
  * **NoSQL** databases ("Not Only SQL") are typically non-tabular and store data differently from relational tables. NoSQL databases come in various types based on their data models.
  * The primary types are **Document**, **Key-Value**, **Wide-Column**, and **Graph** databases. They provide flexible schemas and scale easily for large volumes of data and high user loads.
  * **OLTP (Online Transaction Processing)** systems capture and maintain transactional data in a database. Each transaction involves individual database records composed of multiple fields or columns.
  * Examples include banking operations, credit card processing, and retail checkout transactions. In OLTP systems, the focus is on fast processing because databases are frequently read, written, and updated. If a transaction fails, built-in system logic ensures data integrity.
  * **OLAP (Online Analytical Processing)** applies complex queries to large volumes of historical data aggregated from OLTP databases and other sources for data mining, analytics, and business intelligence projects. In OLAP systems, the focus is on response time for complex queries. Each query typically involves one or more aggregated columns from multiple rows of data.
  * Examples include annual financial performance analysis and marketing lead generation trend analysis. OLAP databases and data warehouses provide analysts with custom reporting tools that transform data into actionable insights.

* **Amazon RDS & Aurora**
  * **Amazon RDS**
    * Amazon RDS is a managed database service on AWS. Users can only access and manage the database at the RDBMS level and cannot access or manage the underlying operating system. Supported engines include Aurora, MySQL, PostgreSQL, Microsoft SQL Server, Oracle, and MariaDB.
    * Amazon RDS provides the following features:
      * Automated backups (both database backups and logs, up to 35 days).
      * Read Replicas for handling read-heavy workloads (e.g., reporting).
      * Read Replicas can be promoted and converted into a Primary node.
      * Automatic failover with a Primary/Standby architecture, also known as **Multi-AZ** deployment.
      * RDS is commonly used for OLTP applications.
      * Data encryption at rest and in transit.
      * Protection through firewall mechanisms similar to EC2 (Security Groups and NACLs).
      * Scaling by changing instance sizes.
      * Storage Auto Scaling.
    * Automatic failover with a Primary/Standby architecture, also known as **Multi-AZ** deployment.

  * **Amazon RDS > Aurora**
    * Amazon Aurora is a relational database engine that re-architects the underlying storage layer to provide high-performance parallel read/write capabilities. Aurora supports MySQL and PostgreSQL compatibility.
    * Since Aurora is part of Amazon RDS, it inherits all RDS features.
    * In addition, Amazon Aurora provides:
      * **Backtrack** – Restore the database to a previous point in time.
      * **Clone** – Create database copies.
      * **Global Database** – One primary database with multiple read replicas across different AWS Regions.
      * **Multi-Master** – Multiple writable master database nodes.

* **Amazon Redshift**
  * Amazon Redshift is a managed Data Warehouse service provided by AWS. It is based on PostgreSQL but optimized for OLAP workloads.
  * Redshift uses a **Massively Parallel Processing (MPP)** database architecture, where data is partitioned and stored across Compute Nodes (including both compute and storage resources). A Leader Node coordinates and aggregates query execution.
  * Redshift stores data using **columnar storage**, making it highly suitable for OLAP applications.
  * Redshift supports SQL and common JDBC/ODBC drivers.
  * It includes features for cost optimization, such as **Transient Clusters** and **Redshift Spectrum**.

* **Amazon ElastiCache**
  * Amazon ElastiCache is a managed AWS service for creating caching clusters. It currently supports two caching engines: **Redis** and **Memcached**.
  * Amazon ElastiCache is responsible for detecting and replacing failed nodes automatically.
  * ElastiCache is commonly deployed in front of the database layer to cache data and reduce database workload.
  * For new workloads and applications, **Redis** is generally recommended due to its richer feature set and better performance.
  * Using ElastiCache requires implementing and managing caching logic within the application.

## Monday: Identity and Access Management (IAM) – User, Group, Role và Access Control trên AWS
* **Overview**
  * The objective of this lesson is to help users:
    * Understand how to grant permissions to an application using Access Key / Secret Access Key and understand why this method should not be used in real-world environments (for security reasons)
    * Learn how to securely grant permissions to an application using an IAM Role attached directly to an EC2 instance

* **Detailed Implementation Steps**
  * **Prepare Resources**
    * Before configuring permissions, you need to set up a test environment including:
      * Launch an EC2 Instance: Create an EC2 virtual server, which will host your application and require permissions to interact with other AWS services
      * Create an S3 Bucket: Create an Amazon S3 storage bucket, which will serve as the target service that the application running on EC2 needs to access for reading and writing data
    * Using Access Key (Use Access Key) – Not Recommended
    * This section demonstrates the traditional but less secure approach:
      * Create an IAM User and Access Key: Create an IAM user, grant it permissions to access S3, and generate an Access Key ID and Secret Access Key pair
      * Use the Access Key: Configure this key pair directly on the EC2 instance so that the application can access data from S3

  * **Using an IAM Role on EC2**
    * This is the core part of the workshop and serves as a replacement for Step 2:
      * Create an IAM Role: Create an IAM Role and attach a policy that allows interaction with the S3 bucket
      * Use the IAM Role: Attach the newly created IAM Role to the EC2 instance. Once attached, applications running on the EC2 instance can securely access S3 without storing any Access Key / Secret Access Key pair in source code or on the server

  * **Clean Up Resources**
    * Guide learners on how to delete all resources created during the lab (EC2, S3 bucket, IAM Role, IAM User) after completion to avoid unexpected AWS charges

* **Create an EC2 Instance**
  * Follow Step 1.1.1 in the Amazon EC2 Introduction Workshop to create an EC2 instance
    * Create an Amazon Linux instance with the free-tier eligible t2.micro configuration for this workshop
  * Use PuTTY to connect to the virtual machine you created by following the instructions in Step 1.1.2
    * Next, we will create an S3 bucket for the application running on our EC2 server to connect to

* **Create an S3 Bucket**
  * Access the S3 Management Console
    * Click Create bucket
  * Set the bucket name to `s3-instancerole-001` (you may add a suffix such as `s3-instancerole-1000` since S3 bucket names must be globally unique)
  * Scroll down and click Create bucket
  * Ensure that the bucket is created successfully before proceeding to the next steps

* **Create an IAM User and Access Key**
  * Access the IAM Management Console
    * Click Users
  * Click Add users
  * Set the User name to `iamaccesskey`
    * Select Programmatic access (This option allows the use of Access Keys and Secret Access Keys with AWS APIs, CLI, and SDKs)
    * Click Next: Permissions
  * Select Attach existing policies directly
    * In the Filter policies field, enter `S3`
    * Select AmazonS3FullAccess to grant full access for uploading and managing files in the S3 bucket created earlier
    * Click Next: Tags
  * Click Next: Review, then click Create user
  * After the user is successfully created, click Show to display the Secret Access Key
    * Save both the Access Key ID and Secret Access Key for use in the following steps of the workshop
    * You may also click Download .csv to download the credentials as a CSV file
  * Next, we will use the Access Key and Secret Access Key to upload a file to the S3 bucket

* **Using Access Key**
  * Return to the EC2 instance terminal
    * Run the following command to install the AWS SDK for Python
  * After the installation is complete, run the following command to create a `test.txt` file for upload testing
  * Run the following command to create a Python application file
    * Note: Replace the placeholder values with your own credentials and bucket information
  * Run the Python application to upload the file to the S3 bucket
  * Access the S3 Management Console
    * Click the `s3-instancerole-001` bucket
    * Verify that the file has been uploaded successfully
  * When using Access Keys, the application runs with the permissions granted to the IAM user `iamaccesskey`, which in this case has full access to S3. This approach is risky because Access Keys can easily be exposed, for example when source code is pushed to public repositories such as GitHub. Embedding Access Keys directly in code is not recommended due to security risks. In the next section, instead of using Access Keys, we will use IAM Roles.

* **Create an IAM Role**
  * Access the IAM Management Console
    * Click Roles
  * Click Create role
  * Under **Choose a use case**, select EC2 to create a role for applications running on EC2
    * Click Next: Permissions
    * In the Filter policies field, enter `S3`
    * Select AmazonS3FullAccess to grant full access to the S3 bucket created earlier
    * Click Next: Tags
  * Click Next: Review
  * Set the Role name to `ec2roles3upload`
    * Click Create role
  * Next, we will attach this role to the EC2 instance so that the application can upload files to S3 without requiring Access Keys or Secret Access Keys in the code

* **Using an IAM Role**
  * Access the EC2 Management Console
    * Select the EC2 instance created earlier
    * Click Actions
    * Click Security
    * Click Modify IAM role
  * Select the role `ec2roles3upload`
    * Click Save
  * Return to the EC2 instance terminal
    * Run the following command to create a Python application file
    * Note: Replace the placeholder values with your own bucket information
  * Run the Python application to upload the file to the S3 bucket
  * Access the S3 Management Console
    * Click the `s3-instancerole-001` bucket
    * Verify that the file has been uploaded successfully
  * We can also inspect the temporary security credentials generated for the IAM role `ec2roles3upload` using the following command. Notice that the credentials have an Expiration time and are automatically refreshed when they expire.
  * Run the following command to list all S3 buckets in the AWS account

* **Clean Up Resources**
  * **Delete the S3 Bucket**
    * Access the S3 Management Console
      * Select the `s3-instancerole-001` bucket
      * Click Empty
    * Enter `permanently delete` to confirm, then click Empty to remove all objects from the bucket
      * Click Exit to return to the S3 dashboard
    * Select the `s3-instancerole-001` bucket, then click Delete
    * Enter the bucket name and click Delete bucket to remove the S3 bucket

  * **Delete the EC2 Instance**
    * Access the EC2 Management Console
      * Select the instance created for this lab
      * Click Instance state
      * Click Terminate instance, then click Terminate to confirm
    * Access the IAM Management Console
      * Click Users
      * Select the user `iamaccesskey`
      * Click Delete. Enter `iamaccesskey` and click Delete to confirm
    * Click Roles
      * Enter `ec2` in the search box to locate the role created earlier
      * Select the role `ec2roles3upload`
      * Click Delete. Enter `ec2roles3upload` and click Delete to remove the IAM Role

* **Overview**
  * This lesson focuses on the principle of least privilege in AWS IAM, instead of granting full Administrator access to users. The content explains how to create Users/Groups with limited administrative permissions for specific AWS services (EC2 and RDS), and then configure IAM Roles with Conditions based on IP addresses and time restrictions to enhance security.

* **Detailed Content Structure**
  * The document is divided into 5 main sections:
    * Introduction to IAM:
      * Request to AWS Service: How requests sent to AWS services are processed.
      * Authenticate Requests: The authentication mechanism for identities.
      * Assume Role Process: How an entity assumes an IAM Role to obtain temporary credentials and permissions.
    * Create IAM Group:
      * Instructions for creating user groups to manage permissions centrally.
    * Create IAM User:
      * Create IAM Users: Provision user accounts.
      * Check Permissions: Verify assigned permissions to ensure they are neither excessive nor insufficient.
    * Configure Role Conditions:
      * Create Admin IAM Role: Create an IAM Role with administrative privileges.
      * Configure Switch Role: Allow users to switch to the role when necessary.
      * Restrict Role Access: Add additional security controls, including:
        * Limit Switch Role by IP: Only allow role switching from specified IP ranges (e.g., corporate network IPs).
        * Limit Switch Role by Time: Restrict when the role can be assumed.
    * Clean Up Resources:
      * Remove created Users, Groups, and Roles after completing the lab to avoid unnecessary costs or security risks.

* **Request to AWS Service**
  * Request: When a principal attempts to perform an action through the AWS Console, AWS API, or AWS CLI, a request is sent to AWS. A request contains:
    * Action or Operation: The action the principal wants to perform.
    * Resource: The resource that will be affected.
    * Principal: Information about the user or application making the request, including attached policies.
    * Environment Data: Information such as IP address, user agent, SSL status, and request timestamp.
    * Resource Data: Information related to the target resource, such as a DynamoDB table name or EC2 instance tag.

* **Authenticating Requests**
  * Authentication: A principal must authenticate before sending requests to AWS.
    * Root User: Requires an email address and password (long-term credentials).
    * IAM User: Requires an account ID or alias, along with a username and password (long-term credentials).
    * To authenticate IAM users through AWS APIs or CLI, you can use Access Keys and Secret Access Keys (long-term credentials) or use IAM Roles and temporary credentials obtained through AWS Security Token Service (AWS STS) after assuming a role.

* **Assume Role Process**
  * In this section, we will learn how an IAM User assumes a role and obtains temporary credentials.
  * The IAM User uses long-term credentials (password or Access Key/Secret Access Key) to send a request to AWS Security Token Service (AWS STS) and perform the `sts:AssumeRole` action.
  * AWS STS verifies whether the IAM User is authorized to perform this action by checking:
    * Trust Relationship (attached to the Role).
    * Identity Policy (attached to the IAM User).
  * If validation succeeds, AWS STS returns temporary security credentials.
  * The IAM User then uses these temporary credentials to make API calls to AWS services. At this point, the user inherits the permissions assigned to the IAM Role that was assumed.

* **Create IAM Group**
  * Access the IAM Console at: https://console.aws.amazon.com/iam/home#/home
  * In the left navigation pane, select **User groups**, then click **Create group**.
  * On the **Create user group** page, enter the following information:
    * User group name: `ec2-rds-admin-group`
    * Scroll down to **Attach permissions policies - Optional**, then search for and select:
      * `AmazonEC2FullAccess`
      * `AmazonRDSFullAccess`
      * `DatabaseAdministrator`
    * Review the configuration and click **Create group**.
    * The IAM Group has now been successfully created.

* **Create IAM Users**
  * Log in to the IAM Console using the following link:
    https://console.aws.amazon.com/iam/home#/home
  * In the left navigation pane, select **Users**, then click **Add User**.
  * On the **Set user details** page, enter the following:
    * User name: `EC2-admin-user`
    * Access type: Select **AWS Management Console access**.
    * Console password: Choose **Custom password** and define a password.
    * Require password reset: Uncheck this option.
    * Review and click **Next: Permissions**.
  * On the **Set permissions** page:
    * Select **Attach existing policies directly**.
    * Search for and select `AmazonEC2FullAccess`.
    * Review and click **Next: Tags**.
  * On the **Add tags (optional)** page:
    * Leave the default settings and click **Next: Review**.
  * On the **Review** page:
    * Review the configuration and click **Create user**.
  * Once the user is created, click **Close** to return to the IAM Console.

  * You have successfully created the first user. To create additional users, repeat the same process with the following modifications:

    * **RDS-admin-user**
      * Step 3:
        * User name: `RDS-admin-user`
      * Step 4:
        * Select **Attach existing policies directly**
        * Choose:
          * `AmazonRDSFullAccess`
          * `DatabaseAdministrator`

    * **Group-user**
      * Step 3:
        * User name: `Group-user`
      * Step 4:
        * Select **Add user to group**
        * Choose the group `ec2-rds-admin-group`

    * **No-permission-user**
      * Step 3:
        * User name: `No-permission-user`
      * Step 4:
        * Skip permission assignment and click **Next: Tags**

* **Check Permissions**
  * Log in to the IAM Console:
    https://console.aws.amazon.com/iam/home#/home
  * In the left navigation pane, select **Users**.
  * Select **EC2-admin-user**.
  * Open the **Security credentials** tab and copy the sign-in URL displayed in the Summary section.
  * Open an incognito/private browser window or another browser and access the copied URL.
  * Sign in using the credentials of `EC2-admin-user`.
  * Repeat steps 1–6 for the remaining users.
  * After successful login, perform the following validation tests:
    * `EC2-admin-user`: Successfully launch an EC2 instance.
    * `RDS-admin-user`: Successfully launch an RDS instance.
    * `Group-user`: Successfully launch both an EC2 instance and an RDS instance.
    * `No-permission-user`: Cannot access or use any AWS services.

* **Create Admin IAM Role**
  * Log in to the IAM Console:
    https://console.aws.amazon.com/iam/home#/home
  * In the left navigation pane, select **Roles**, then click **Create role**.
  * Under **Select type of trusted entity**, choose **AWS Service**.
  * Under **Choose a use case**, select **EC2**.
  * Click **Next: Permissions**.
  * Search for and select the `AdministratorAccess` policy.
  * Click **Next: Tags**.
  * Skip the tagging step and click **Next: Review**.
  * On the Review page:
    * Role name: `lab44-RoleFullAccess`
    * Click **Create role**.

* **Configure Switch Role**
  * Access the IAM Console:
    https://console.aws.amazon.com/iam/home#/home
  * In the left navigation pane, select **Users**.
  * Open the user `No-permission-user` and copy the User ARN.
  * In the left navigation pane, select **Roles**, then open `lab44-RoleFullAccess`.
  * Go to the **Trust relationships** tab and click **Edit trust relationship**.
  * Add the AWS principal using the ARN of `No-permission-user` as shown in the lab instructions.
  * Click **Update Trust Policy**.
  * `No-permission-user` can now assume the role `lab44-RoleFullAccess`.
  * To verify:
    * Log in as `No-permission-user`.
    * Click the username in the upper-right corner and select **Switch Role**.
    * Enter the required information.
    * Click **Switch Role**.
    * Access services such as EC2 or RDS to confirm the role assumption was successful.
    * With the `AdministratorAccess` policy, `No-permission-user` can now use any AWS service.

* **Restrict Access by IP**
  * Log in to the IAM Console using an Admin account.
  * In the left navigation pane, select **Roles**, then choose `lab44-RoleFullAccess`.
  * In the **Trust relationships** tab, click **Edit trust relationship**.
  * Add the required **Condition** based on IP addresses, then click **Update Trust Policy**.
  * After updating the trust policy, the allowed IP addresses will appear in the Condition section.
  * Return to the `No-permission-user` session and attempt to switch roles again.
  * You should receive an error if your current IP address does not match the allowed IP range.

* **Restrict Access by Time**
  * Log in to the IAM Console using an Admin account.
  * In the left navigation pane, select **Roles**, then choose `lab44-RoleFullAccess`.
  * In the **Trust relationships** tab, click **Edit trust relationship**.
  * Add the required **Condition** based on date and time restrictions, then click **Update Trust Policy**.
  * After updating the trust policy, the allowed date and time range will appear in the Condition section.
  * Return to the `No-permission-user` session and attempt to switch roles again.
  * You should receive an error if the role assumption attempt occurs outside the allowed time window.

* **Clean Up Resources**
  * Delete the role `lab44-RoleFullAccess`
    * Open the IAM Console.
    * In the left navigation pane, select **Roles**.
    * Locate and select `lab44-RoleFullAccess`.
    * Click **Delete**.

  * Delete IAM Users:
    * `EC2-admin-user`
    * `RDS-admin-user`
    * `Group-user`
    * `No-permission-user`
    * Open the IAM Console.
    * In the left navigation pane, select **Users**.
    * Select the users created for the lab.
    * Click **Delete user**.

  * Delete the User Group `ec2-rds-admin-group`
    * Open the IAM Console.
    * In the left navigation pane, select **User groups**.
    * Select the user group created for the lab.
    * Click **Delete**

## Tueday: IAM Permission Management with Permission Boundaries and Resource Tags
* **Overview & Concepts**
  * **What is IAM Permission Boundary?** IAM Permission Boundary is an advanced AWS IAM feature that defines the maximum permissions an IAM User or Role can have. Even if the user is attached to a policy granting broader permissions, they cannot exceed the limits defined by the Permission Boundary. The user's effective permissions are the intersection of the Identity-based Policy and the Permission Boundary.
  * **Why use it?** As the number of users grows, managing individual policies becomes more complex and increases the risk of privilege escalation vulnerabilities. Using Permission Boundaries simplifies permission management and provides a quick, centralized way to prevent privilege escalation.

* **Lab Structure**
  * This workshop is designed as a 6-step hands-on lab:
    * **Introduction:** Overview and core concepts of Permission Boundaries.
    * **Preparation:** Set up the required environment for the lab.
    * **Create Restriction Policy:** Configure a policy that defines permission boundaries.
    * **Create IAM Limited User:** Create a new IAM User and apply the Permission Boundary.
    * **Test IAM User Limits:** Verify that the user cannot perform actions beyond the defined boundary, even when granted higher permissions.
    * **Clean Up Resources:** Remove all resources created during the lab to avoid unnecessary AWS charges.

* **Introduction**
  * **What is IAM Permission Boundary?**
    * IAM Permission Boundary is an advanced feature that allows us to define the maximum permissions for a User or Group. For example, if we apply a Permission Boundary that only allows the user **EC2admin** to manage EC2 services, that user will not gain permissions for any other AWS service, even if a policy granting broader access is attached.
    * Therefore, the effective permissions of the **EC2admin** user are limited to the permissions allowed by both the Permission Boundary and the user's Identity-based Policy.

  * **Why Use IAM Permission Boundary?**
    * Normally, when granting permissions to IAM users, you may assume that carefully designing permission policies is sufficient and that Permission Boundaries are unnecessary.
    * However, as the number of users increases and job responsibilities evolve, more permission policies must be created and maintained. This makes permission management increasingly complex and can introduce opportunities for privilege escalation.
    * To simplify permission management, instead of modifying individual policies, you can apply Permission Boundaries centrally and consistently to close privilege escalation gaps.

* **Create Restriction Policy**
  * Sign in to the IAM Management Console.
  * In the left navigation pane, select **Policies** and then choose **Create Policy**.
  * On the **Create Policy** page, select the **JSON** tab and paste the provided JSON policy into the editor. This policy allows all EC2 actions on all resources, provided that the EC2 service is being accessed in the **ap-southeast-1 (Singapore)** region.
    * Review the policy and choose **Next: Tags**.
  * Skip the tagging step and choose **Next: Review**.
  * Name the policy **ec2-admin-restrict-region**. (This policy ensures that the EC2 Admin user can only perform actions within the Singapore region, **ap-southeast-1**.) Then choose **Create Policy**.
  * You have now created the policy that will be used to define the maximum permissions an IAM user can have. In the next step, we will apply this policy as a Permission Boundary.

* **Create a Limited IAM User**
  * Sign in to the IAM Management Console.
  * In the left navigation pane, select **Users**, then choose **Add user**.
  * On the **Set user details** page, enter the following information and choose **Next: Permissions**:
    * **User name:** ec2-admin
    * **Access type:** Select **AWS Management Console access** to allow the user to sign in to the AWS Management Console.
    * Select **Custom Password** and specify a password of your choice.
    * Uncheck **User must create a new password at next sign-in**.
  * In the **Set permissions** section:
    * Select **Attach existing policies directly**.
    * Search for and select **AmazonEC2FullAccess** to grant full EC2 administrative permissions.
  * Then expand the **Set permissions boundary** section:
    * Select **Use a permissions boundary to control the maximum user permissions**.
    * In the search box, enter **ec2-admin-restrict-region** and select the policy you created earlier.
    * Review the configuration and choose **Next: Tags**.
  * On the **Add tags (optional)** page, keep the default settings and choose **Next: Review**.
  * On the **Review** page, verify the configuration and choose **Create user**.
  * The user has now been created successfully. In the next step, you will sign in using the **ec2-admin** user to verify whether it can create EC2 instances outside the permitted region.
  * We will use this IAM user in the following test.

* **Test IAM User Restrictions**
  * In the left navigation pane, select **Users** and choose the **ec2-admin** user you created.
  * Open the **Security credentials** tab, copy the IAM user sign-in URL from the **Summary** section, and launch it in an incognito/private browser window or a different browser.
  * On the **Sign in as IAM user** page, enter the following credentials:
    * **IAM User name:** ec2-admin
    * **Password:** The password you created earlier.
    * Click **Sign in**.
  * Reminder: The **ec2-admin-restrict-region** Permission Boundary only allows access to EC2 services in the **ap-southeast-1 (Singapore)** region.
  * In the AWS Management Console as **ec2-admin**, select the **ap-southeast-1 (Singapore)** region and access the EC2 service using the search bar. You will see that EC2 functions normally.
  * Change the region in the top-right corner to **ap-southeast-2 (Sydney)**. You will notice that, despite having full EC2 administrative permissions, the user cannot perform EC2 actions in Sydney because the Permission Boundary restricts EC2 access to the Singapore region only.

* **Clean Up Resources**
  * **Delete the ec2-admin User**
    * Return to your primary AWS account.
    * Open the IAM Management Console.
    * In the left navigation pane, select **Users**.
    * Select the user associated with this lab.
    * Choose **Delete user**.
    * Confirm by checking the box in the pop-up window and selecting **Yes, delete**.

  * **Delete the IAM Policy**
    * Open the IAM Management Console.
    * In the left navigation pane, select **Policies**.
    * Search for **ec2-admin-restrict-region**.
    * Select the policy and choose **Actions**.
    * Choose **Delete**.
    * In the confirmation dialog, enter the policy name and choose **Delete**.

* **Overview**
  * This lab walks us through the process of managing EC2 service access using Resource Tags through detailed policy configurations and IAM roles with specific permissions. The use of Resource Tags becomes extremely useful as organizations scale and adopt decentralized administration.
  * In this lab, we will create policies and roles that can be used by specific users, such as EC2 Administrators. These policies will only allow EC2 Administrators to create and manage resources when certain requirements are met and specific Resource Tags are applied.

* **Objectives**
  * Apply the principle of least privilege in IAM.
  * Define IAM policies with detailed conditions (IAM Policy Conditions).

* **Create IAM User**
  * **Create an Admin Group**
    * Sign in to the AWS Management Console.
    * Click the account name in the upper-right corner and select **Security Credentials**.
    * In the left navigation pane, select **User Groups**, then choose **Create Group**.
    * Under **Name the group**, enter a group name (for example: **AdminGroup**) and scroll down.
    * In the **Attach permissions policies** section, search for **AdministratorAccess** and press Enter. Select **AdministratorAccess** from the list, then choose **Create Group**.
    * The Admin Group has now been created successfully.

  * **Create an Admin User**
    * In the left navigation pane, select **Users**, then choose **Add User**.
    * On the **Specify user details** page, under **User details**, enter a username in the **User name** field. This will be the AWS sign-in name for the new user. Example: **AdminUser**
      * Select **Provide user access to the AWS Management Console**. This option creates AWS Management Console credentials for the new user.
      * You will be asked whether you want to provide console access for a person. AWS recommends creating users in IAM Identity Center instead of IAM.
      * To switch to creating a user in IAM Identity Center, select **Specify a user in Identity Center**.
      * If IAM Identity Center is not enabled, selecting this option will redirect you to the service page where you can enable it. For more details, see the AWS IAM Identity Center User Guide.
      * If IAM Identity Center is already enabled, selecting this option will redirect you to the **Specify user details** page within IAM Identity Center.
      * If you cannot use IAM Identity Center, select **I want to create an IAM user**.
    * For **Console password**, choose one of the following:
      * **Autogenerated password** – The user receives a randomly generated password that complies with the account password policy. You can view or download the password on the Retrieve Password page.
      * **Custom password** – The user is assigned the password that you enter manually.
      * *(Optional)* **Users must create a new password at next sign-in (recommended)** is selected by default to ensure that users change their password upon first login.
      * Choose **Next**.
    * On the **Set permissions** page, specify how you want to assign permissions to the user. Choose one of the following options:
      * **Add user to group** – Assign the user to one or more existing groups that already have permission policies attached.
      * **Copy permissions** – Copy all group memberships, attached managed policies, inline policies, and existing permission boundaries from another user.
      * **Attach policies directly** – Select AWS-managed or customer-managed policies to attach directly to the user. You can also create a new policy if needed.
    * *(Optional)* On the **Review and create** page, under **Tags**, select **Add new tag** to add metadata as key-value pairs.
      * Review all selections carefully, then choose **Create user**.
    * On the **Retrieve password** page:
      * Select **Show** to view the assigned password.
      * Select **Download.csv** to download the user's credentials and store them securely.
    * Verify that the user has been created successfully.
    * Verify the user’s group membership.
    * Copy the **Console Sign-In URL**.

* **Create IAM Policies**
  * **Steps to Create an IAM Policy**
    * Sign in to the AWS Management Console and navigate to the IAM Management Console.
    * In the left navigation pane, select **Policies** and choose **Create policy**.
    * On the policy creation screen, select **JSON** and enter the policy definition.
      * In this example, we use the **ec2-list-read** policy.
      * Choose **Next: Tags**.
    * Keep the default configuration and choose **Next: Review**.
    * Provide the following details:
      * **Name:** ec2-list-read
      * **Description:** ec2-list-read
      * Choose **Create Policy**.
    * The policy has now been created successfully.

* **Policy - ec2-create-tags**
  * In the left navigation pane, select **Policies** and choose **Create policy**.
  * Select **JSON** and enter the policy definition. In this example, we use the **ec2-create-tags** policy.
  * Choose **Next: Tags**.
  * Keep the default configuration and choose **Next: Review**.
  * Information:
    * **Name:** ec2-create-tags
    * **Description:** ec2-create-tags
    * **Description:** This policy allows the creation of EC2 tags, provided the action occurs during EC2 instance creation.
    * Choose **Create Policy**.
  * The policy has now been created successfully.

* **Policy - ec2-create-tags-existing**
  * Information:
    * **Name:** ec2-create-tags-existing
    * **Description:** ec2-create-tags-existing
    * **Description:** This policy allows users to tag EC2 resources only when all three conditions are met:
      * The EC2 resource tag must contain the key-value pair **Key=Team, Value=Alpha**.
      * The allowed tag keys include **Team** and **Name**.
      * The requested tag assignment must be **Key=Team, Value=Alpha**.

* **Policy - ec2-run-instances**
  * Information:
    * **Name:** ec2-run-instances
    * **Description:** ec2-run-instances
    * **Description:** This policy consists of two parts:
      * The first part allows EC2 instance creation only when the required AWS Region and Resource Tag conditions are satisfied.
      * The second part allows the creation of related resources during EC2 instance provisioning, subject to AWS Region restrictions.

* **Policy - ec2-manage-instances**
  * Information:
    * **Name:** ec2-manage-instances
    * **Description:** ec2-manage-instances
    * **Description:** This policy allows basic EC2 instance management operations (reboot, terminate, start, stop), provided that AWS Region and Resource Tag requirements are satisfied.
  * After completion, you will have a total of five EC2-related policies.

* **Create an IAM Role**
  * Sign in to the AWS Management Console and navigate to the IAM Management Console.
  * In the left navigation pane, select **Roles** and choose **Create role**.
  * On the role creation screen, select **Another AWS account** and enter your Account ID (available under **My Account**). Enable **Require MFA** as a security best practice.
  * Under **Attach permissions policies**, select the following policies:
    * ec2-list-read
    * ec2-create-tags
    * ec2-create-tags-existing
    * ec2-run-instances
    * ec2-manage-instances
  * Choose **Next: Tags**.
  * Keep the default configuration and choose **Next: Review**.
    * Enter a role name (for example: **ec2-admin-team-alpha**) and an appropriate description.
  * Choose **Create role**.
  * After the role is created successfully, select **ec2-admin-team-alpha** from the list of IAM roles and record the following:
    * Role ARN
    * Switch Role URL
  * Use the IAM User ARN to configure the Trust Relationship.
  * Modify the Trust Policy as required.
  * Complete the update.

* **Switch Role**
  * Sign in to the AWS Management Console.
    * Select **Users**.
    * Select the Admin User you created.
    * Choose **Add user**.
  * Select **Security credentials**.
    * Copy the sign-in URL.
  * Open the sign-in URL in a new browser tab.
    * Enter the Account ID, username, and password.
    * Choose **Sign in**.
  * After signing in successfully:
    * Click the username displayed in the upper-right corner.
    * Select **Switch Role**.
    * Alternatively, paste the previously saved Switch Role URL.
  * On the **Switch Role** page:
    * **Account:** `<ACCOUNT_ID_NUMBER>`
    * **Role:** `ec2-admin-team-alpha`
    * **Display Name (Optional):** Enter a friendly name for future use.
    * Choose **Switch Role**.
  * Your browser will be redirected to the new role session.

* **Access the EC2 Console in AWS Region - Tokyo**
  * Sign in to the AWS EC2 Console and access EC2 in **ap-northeast-1 (Tokyo)**:
    * `https://ap-northeast-1.console.aws.amazon.com/ec2/v2/home?region=ap-northeast-1`
  * When accessing the dashboard, you will notice multiple errors containing the phrase **API Error**.
    * This confirms that the first validation test has passed because **ap-northeast-1** is not an allowed AWS Region.

* **Access the EC2 Console in AWS Region - North Virginia**
  * Sign in to the AWS EC2 Console and access EC2 in **us-east-1 (North Virginia)**:
    * `https://us-east-2.console.aws.amazon.com/ec2/v2/home?region=us-east-1`
  * When accessing the dashboard, you will only encounter a single **API Error** related to Load Balancing.
    * This confirms that the first validation test has passed because **us-east-1** is an allowed AWS Region.

## Wednesday: Building a Secure Data Protection and Cost Optimization Solution on AWS Using KMS, CloudTrail, Athena, and Lambda
* **Introduction**
  * Overview of the system architecture and data flow: Encrypt objects on S3 using KMS keys, configure Amazon CloudTrail to record all interaction logs, and use Amazon Athena to query those log files.

* **Preparation Steps**
  * Create Policy and Role: Guide on creating IAM Policies that define permissions and IAM Roles to allow AWS services or entities to securely interact with each other.
  * Create Group and User: Guide on creating IAM Groups and specific IAM Users for permission management in this lab.

* **Create Key Management Service**
  * Steps to configure and create a Customer Managed Key (KMS) to establish a custom data encryption and decryption mechanism.

* **Create Amazon S3**
  * Create Bucket: How to create an S3 Bucket on AWS.
  * Upload data to S3: Guide on uploading data to the bucket and applying server-side encryption (at-rest) using the configured KMS key.

* **Create AWS CloudTrail and Amazon Athena**
  * Create CloudTrail: Configure CloudTrail to log all API calls related to S3 and KMS.
  * Logging to CloudTrail: Monitor and verify the automatic logging process.
  * Create Amazon Athena: Set up Amazon Athena environment (define table structure based on CloudTrail log format).
  * Retrieve data with Athena: Use SQL query statements in Athena to filter and search information from the log files.

* **Verify and Share Encrypted Data on S3**
  * Perform integrity checks on the encrypted data, simulate valid/invalid access scenarios, and guide how to securely share the encrypted data with authorized parties.

* **Clean Up Resources**
  * Guide on deleting all created resources (S3 Bucket, CloudTrail, Athena, KMS Key, IAM Users/Roles) to avoid unexpected charges after completing the lab.

* **Create Policy and Role**
  * **Create Policy**
    * Access the AWS Management Console
      * Search for IAM
      * Select IAM
    * In the IAM interface
      * Select Policies
      * Select Create policy
    * In the Specify permissions section
      * Select JSON, delete the old code and copy the new code below into it
    * After completing the above step, scroll to the bottom of the page and click Next
    * In the Review and create section
      * Policy name: enter `kms-key-policy`
    * After entering the Policy name, scroll to the bottom and click Create policy
    * Policy created successfully notification

  * **Next, we will create the Role**
    * In the IAM interface
      * Select Roles
      * Select Create role
    * In the Select trusted entity section
      * Select AWS service
    * Scroll down to the Use case section
      * For Service or use case, select S3
      * For Use case, select S3
      * Click Next
    * In the Add permissions section
      * Search and find the newly created `kms-key-policy`
      * Check the newly created policy
      * Click Next
    * In the Name, review, and create section
      * Role name: enter `kms-key-role`
    * Scroll down and click Create role
    * Role created successfully notification

* **Create Group and User**
  * **Create Group**
    * Access the AWS Management Console
      * Search for IAM
      * Select IAM
    * In the IAM interface
      * Select User groups
      * Select Create group
    * In the Create user group section
      * User group name: enter `GroupLimit`
    * Scroll down to Attach permissions policies
      * Click the search bar and select S3
      * Check `AmazonS3FullAccess`
      * Click Create group
    * Group created successfully notification

  * **Next, we create the User**
    * In the IAM interface
      * Select Users
      * Select Create user
    * In the Specify user details section
      * User name: enter `User-S3`
      * Check Provide user access to the AWS Management Console
      * Check I want to create an IAM user
    * Scroll down to Console password
      * Enter your Password
      * Uncheck Users must create a new password at next sign-in (We will not require password change on first login)
      * Click Next
    * In the Permissions options section
      * Select Add user to group
      * Check the newly created `GroupLimit`
      * Click Next
    * Scroll down and click Create user
    * User created successfully notification
      * After successful creation, copy the login link and open it in an incognito window or new browser
    * Log in with the credentials you just created
    * Successfully logged in as User-S3

* **Create Key Management Service**
  * Access the AWS Management Console
    * Search for KMS
    * Select Key Management Service
  * In the KMS interface
    * Select Customer managed keys
    * Select Create
  * In the Configure key section
    * In this section we will create a symmetric key to encrypt data. You can refer to symmetric and asymmetric keys in AWS Key Management Service.
    * Key type: select Symmetric
    * Key usage: select Encrypt and decrypt
    * Click Next
  * In the Add labels section
    * Alias: enter `kms-key-encrypt-decrypt`
  * Scroll down and click Next
  * In the Define key administrative permissions section
    * Key administrator: search for `kms`
    * Check `kms-key-role`
    * Key deletion: check Allow key administrators to delete this key
    * Click Next
  * In the Define key usage permissions section
    * Key usage: search for `kms`
    * Check `kms-key-role`
    * Click Next
  * Scroll down and click Finish
  * Key created successfully notification

  * Automatic key rotation in AWS KMS is a feature that automatically changes your encryption key after a certain period (from 90 days up to 2560 days). This enhances the security of your data by reducing the risk of key exposure or compromise. Reference link: Rotating AWS KMS keys
  * Return to the KMS interface
    * Select the newly created Key
  * Next
    * Select Key rotation
    * Select Edit
  * In the Edit automatic key rotation section
    * Select Enable
    * In Rotation period (in days), you can customize how often the encryption key should be automatically rotated

* **Create Bucket**
  * Access the AWS Management Console
    * Search for S3
    * Select S3
  * In the S3 interface
    * Select Buckets
    * Select Create bucket
  * In the Create bucket interface
    * Bucket type: select General purpose
    * Bucket name: enter `kms-key-s3`
  * Scroll down to Object Ownership
    * Select ACLs enabled
    * Object ownership: select Object writer
  * Scroll down to Block Public Access settings for this bucket
    * Uncheck Block all public access
    * Check I acknowledge that the current settings might result in this bucket and the objects within becoming public
  * Scroll down to Default encryption
    * Encryption type: select Server-side encryption with AWS Key Management Service keys (SSE-KMS)
    * AWS KMS Key: select Choose from your AWS KMS keys
    * Available AWS KMS keys: select `kms-key-encrypt-decrypt`
  * Scroll down and click Create bucket
  * Bucket created successfully notification

* **Upload Data to S3**
  * Access the AWS Management Console
    * Search for S3
    * Select S3
  * In the S3 interface
    * Select Buckets
    * Select `kms-key-s3`
  * Click Upload
  * In the Upload section
    * Select Add files
    * Select the downloaded file and click Open
  * Next
    * You will see the file has been uploaded
    * Go to the Properties tab
  * Scroll down to Server-side encryption
    * Server-side encryption: select Specify an encryption key
    * Encryption settings: select Override bucket settings for default encryption
    * Encryption type: select Server-side encryption with AWS Key Management Service keys (SSE-KMS)
  * Scroll down to AWS KMS key
    * Select Choose from your AWS KMS keys
    * Available AWS KMS keys: select `kms-key-encrypt-decrypt`
  * Scroll down and click Upload
  * Data upload successful notification

* **Create CloudTrail**
  * Access the AWS Management Console
    * Search for CloudTrail
    * Select CloudTrail
  * In the CloudTrail interface
    * Select Trails
    * Select Create trail
  * In the Choose trail attributes section
    * Trail name: enter `kms-key-cloudtrail`
    * Storage location: select Use existing S3 bucket
    * Click Browse
  * Next
    * Select `kms-key-s3`
    * Click Choose
  * In the Prefix - optional section
    * Enter `cloudtrail`
  * Scroll down and click Next
  * In the Choose log events section
    * Event type: check Management events
    * Check Data events
  * Scroll down to the Data events section
    * Click on the text "Switch to basic event selector" to change the mode
    * Click Continue
  * In the Data event: S3 section
    * Data event source: select S3
    * For S3 bucket, uncheck Read and Write
    * Under Individual bucket selection, click Browse
  * Next
    * Select `kms-key-s3`
    * Click Choose
  * Click Next
  * Scroll down and click Create trail
  * Trail created successfully notification
  * Go back to S3
  * Select Buckets > `kms-key-s3`
  * You will see a folder named `cloudtrail/` has been created. This folder will contain all logs related to `kms-key-s3`

* **Logging to CloudTrail**
  * Access the AWS Management Console
    * Search for S3
    * Select S3
  * In the S3 interface
    * Select Buckets
    * Select `kms-key-s3`
  * Go to the `cloudtrail/` folder
  * You will see that there are currently no logs recorded in the `cloudtrail/` folder
  * Return to `kms-key-s3`
    * Select Upload
  * In the Upload section
    * Select Add files
    * Select the file downloaded in section 4.2
    * Click Open
  * Next
    * Go to the Properties tab
  * Scroll down to Server-side encryption
    * Server-side encryption: select Specify an encryption key
    * Encryption settings: select Override bucket settings for default encryption
    * Encryption type: select Server-side encryption with AWS Key Management Service keys (SSE-KMS)
    * AWS KMS key: select Choose from your AWS KMS keys
  * Scroll down to Available AWS KMS keys
    * Select `kms-key-encrypt-decrypt`
  * Scroll down and click Upload
  * Upload successful notification
  * Return to the `cloudtrail/` folder
  * You will now see that the log has been recorded in the `cloudtrail/` folder

* **Create Amazon Athena**
  * Access the AWS Management Console
    * Search for CloudTrail
    * Select CloudTrail
  * In the CloudTrail interface
    * Select Event history
    * Select Create Athena table
  * In the Create a table in Amazon Athena section
    * Storage location: select `kms-key-s3/cloudtrail`
  * Click Create table
  * Table created successfully notification

* **Retrieve Data with Athena**
  * Access the AWS Management Console
    * Search for Athena
    * Select Athena
  * In the Athena interface
    * Select Query editor
    * Select Edit settings
  * In the Manage settings section
    * Click Browse S3
  * Next
    * Select `kms-key-s3`
    * Click Choose
  * Click Save
  * Return to the Query editor
    * Select Editor
    * Click the three dots next to the table `cloudtrail-log-kms-key-s3-cloudtrail`
    * Select Preview table
  * Scroll down to see the logs appear
  * Test querying the eventname for `kms-key-s3`
    * Enter the query: `SELECT eventname FROM "default"."cloudtrail_logs_kms_key_s3_cloudtrail" limit 100;`
    * Click Run to execute the query
  * Scroll down to see the eventname retrieved successfully

* **Test and Share Encrypted Data on S3**
  * Access the AWS Management Console
    * Search for S3
    * Select S3
  * In the S3 interface
    * Select Buckets
    * Select `kms-key-s3`
  * In the `kms-key-s3` bucket
    * Check the file `awsstudygroup.jpg`
    * Click Open
  * As you can see, the file opens successfully because you are the owner with full access rights.
  * Next, we will make the object public to test access
  * Return to `kms-key-s3`
    * Check the `awsstudygroup` file
    * Select Actions
    * Select Make public using ACL
  * In the Make public section
    * Click Make public
  * Success notification
  * Return to `kms-key-s3`
    * Check `awsstudygroup`
    * Click Copy URL
  * Paste the URL into a new tab. You will not be able to open the file. AWS requires AWS Signature Version 4 for server-side encryption with KMS-managed keys.
  * Switch to the incognito window and log in with the `User-S3` account created earlier
    * Go to S3
    * Select Buckets > `kms-key-s3`
    * Try to Open the file
  * As User-S3, you will receive an Access Denied message because this user does not have decryption permissions (This demonstrates that only the owner has access).
  * Still in User-S3, return to `kms-key-s3`
    * Check `awsstudygroup`
    * Copy URL
  * Paste the URL into a new tab — Access will still be denied.
  * Return to your main (owner) account
    * Go to S3
    * Check `qrcode_facebook_awsstudygroup`
    * Select Actions
  * Select Share with a presigned URL
  * Next
    * Time interval until the presigned URL expires: select Minutes
    * Number of minutes: enter `2` (for demo purposes)
    * Click Create presigned URL
  * Success notification — Click Copy presigned URL
  * Anyone with this link can access the file for 2 minutes
  * After 2 minutes, attempting to access will show Access Denied (expired)

* **Clean Up Resources**
  * **Delete KMS Resources**
    * Access the AWS Management Console
      * Search for KMS
      * Select KMS
    * In the KMS interface
      * Check `kms-key-encrypt-decrypt`
      * Select Key actions
      * Select Disable
    * Next
      * Check Confirm that you want to disable this key
      * Click Disable key
    * Return to KMS
      * Check `kms-key-encrypt-decrypt`
      * Select Key actions
      * Select Schedule key deletion
    * Next
      * Waiting period (in days): enter `7`
      * Check Confirm that you want to schedule these keys for deletion after a 7 day waiting period
      * Click Schedule deletion
    * Success notification

  * **Delete CloudTrail Resources**
    * Access the AWS Management Console
      * Search for CloudTrail
      * Select CloudTrail
    * In the CloudTrail interface
      * Select Trails
      * Select `kms-key-cloudtrail`
    * Click Stop logging
    * Confirm Stop logging
    * After stopping, click Delete
    * Click Delete again
    * Success notification

  * **Delete S3 Resources**
    * Access the AWS Management Console
      * Search for S3
      * Select S3
    * In the S3 interface
      * Check `aws-athena-query-results-058264191537-us-east-1`
      * Select Empty
    * Next
      * Type `permanently delete`
      * Click Empty
    * Empty successful notification
    * Delete the bucket `aws-athena-query-results-058264191537-us-east-1`
    * Now empty and delete the `kms-key-s3` bucket (repeat Empty and Delete steps)
    * Bucket deleted successfully

  * **Delete User and Group Resources**
    * Access the AWS Management Console
      * Search for IAM
      * Select IAM
    * In the IAM interface
      * Check `User-S3`
      * Select Delete
    * Type `User-S3`
    * Click Delete user
    * Success notification
    * Return to IAM
      * Check `GroupLimit`
      * Select Delete
    * Type `GroupLimit`
    * Click Delete
    * Success notification

* **Optimize EC2 Costs with Lambda**
  * **Create a VPC**
    * Access the AWS Management Console
      * Search for VPC
      * Select VPC
    * In the VPC interface
      * Select Your VPCs
      * Click Create VPC
    * In the Create VPC interface
      * Select **VPC, subnets, etc**
      * Enter **lambda-lab**
    * Click Create VPC
    * Click View VPC
    * Complete the VPC creation process
    * In the VPC interface
      * Select Subnets
      * Select the public subnet
      * Click Actions
      * Select Edit subnet settings
    * Enable **Auto-assign public IPv4 address**, then click Save

  * **Create a Security Group**
    * In the VPC interface:
      * Select Security Groups
      * Click Create security group
      * In the Security group name field, enter **lambda-lab**
      * In the Description field, enter **security group for lambda lab**
      * Select the VPC you created earlier
    * In the Create security group interface:
      * Configure Inbound rules
      * Configure Outbound rules
    * Click Create security group

  * **Create an EC2 Instance**
    * Access the AWS Management Console
      * Search for EC2
      * Select EC2
    * In the EC2 interface
      * Select Instances
      * Click Launch instances
    * In the Launch instance interface
      * Name: **lambda-lab-instance**
      * Select Quick Start
      * Select Amazon Linux
      * Select Amazon Linux 2 AMI
    * Select an Instance type and click Create new key pair
    * In the Create key pair interface
      * Key pair name: **lambda-lab-key**
      * Click Create key pair
    * In the Network settings section
      * Click Edit
    * In the Network settings section
      * Select the VPC created earlier
      * Select the public subnet
      * Enable Auto-assign public IP
      * Select **Select existing security group**
      * Choose the security group created earlier
    * Successfully create the EC2 instance

  * **Using Incoming Webhooks on Slack**
    * First, sign in to Slack through your browser
    * After successfully signing in, you will see the Slack interface
    * Now, navigate to Incoming Webhooks
      * If you did not sign in previously, select **Sign in to install**
    * After signing in successfully, select **Add to Slack**
    * Next, you will be prompted to create another workspace
      * Enter **aws-lambda-labs** and click Next
    * Then enter **aws-lambda** and click Next
    * Complete the Slack workspace creation process
    * In the Slack App Directory interface
      * Select the workspace you just created
      * Click Add to Slack
    * Next, select **Create a new channel**
    * In the Create a Channel interface:
      * Channel name: **notification**
      * Description: **notification for lambda**
      * Click Create
    * After completing the above steps, copy the Webhook URL for later use

  * **Create a Tag for the Instance**
    * In the EC2 interface
      * Select Instances
      * Select **lambda-lab-instance**
      * Click Actions
      * Select Instance settings
      * Select Manage tags
    * In the Manage tags interface
      * Key: **environment_auto**
      * Value: **true**
      * Click Save

  * **Create a Role for Lambda**
    * Access the AWS Management Console
      * Search for IAM
      * Select IAM
    * In the IAM interface
      * Select Roles
      * Click Create role
    * In the Select trusted entity interface
      * Select AWS service
      * Select Lambda
      * Click Next
    * In the Add permissions interface
      * Search for **AmazonEC2FullAccess**
      * Select **AmazonEC2FullAccess**
    * Next, repeat the same process:
      * Search for **CloudWatchFullAccess**
      * Select **CloudWatchFullAccess**
      * Click Next
    * In the Name, review, and create section
      * Role name: **dc-common-lambda-role**
    * Review the configuration and click Create role
    * Successfully create the role for the Lambda function

  * **Create a Lambda Function to Stop Instances**
    * Access the AWS Management Console
      * Search for Lambda
      * Select Lambda
    * In the AWS Lambda interface
      * Select Functions
      * Click Create function
    * In the Create function interface
      * Select Author from scratch
      * Function name: **dc-common-lambda-auto-stop**
      * Runtime: **Python 3.8**
      * Architecture: **x86_64**
    * Continue in the Create function interface
      * Expand Change default execution role
      * Select Use an existing role
      * Choose **dc-common-lambda-role**
      * Click Create function
    * After successfully creating the function
      * Select Configuration
      * Select Environment variables
      * Click Edit
    * In the Edit environment variables interface
      * Click Add environment variable
    * In the Edit environment variables interface
      * Key: **environment_auto**
      * Value: **true**
    * After creating the environment variable
      * Select Code
    * In the Code source section
      * Import the source code. You must modify the **webhook_url** to receive Slack notifications.
    * Save the code and click Deploy

  * **Create a CloudWatch/EventBridge Rule**
    * Access the AWS Management Console
      * Search for CloudWatch
      * Select CloudWatch
    * In the CloudWatch interface
      * Select Events
      * Select Rules
      * Click Go to Amazon EventBridge
    * In the Rules interface
      * Click Create rule
    * In the Create rule interface
      * Name: **dc-common-lambda-auto-stop**
      * Description: **dc-common-lambda-auto-stop**
      * Select Schedule
      * Click Next
    * In Schedule pattern
      * Two schedule options are available:
        * A detailed schedule that runs at a specific time, such as 8:00 AM PST on the first Monday of every month
        * A schedule that runs at a regular interval, such as every 10 minutes
      * Select **A schedule that runs at a regular rate, such as every 10 minutes**
      * Set the rate value to **9 hours**
      * Click Next
    * In the Target interface
      * Select AWS service
      * Select Lambda function
      * Function: **dc-common-lambda-auto-stop**
      * Click Next
    * Click Next again
    * Review and click Create rule
    * Successfully create the rule for stopping instances

  * **Create a Lambda Function to Start Instances**
    * In the Lambda Functions interface
      * Click Create function
    * In the Create function interface
      * Select Author from scratch
      * Function name: **dc-common-lambda-auto-start**
      * Runtime: **Python 3.8**
      * Architecture: **x86_64**
    * In the Create function interface
      * Expand Change default execution role
      * Select Use an existing role
      * Choose **dc-common-lambda-role**
      * Click Create function

  * **Create Environment Variables Before Importing Code**
    * Select Configuration
    * Select Environment variables
    * Click Edit
    * In the Edit environment variables interface
      * Key: **environment_auto**
      * Value: **true**
      * Click Save

  * **Deploy the Function**
    * After creating the environment variable
      * Select Code
      * Import the source code. You must modify the **webhook_url** to receive Slack notifications.
      * Save and click Deploy

  * **Create a CloudWatch/EventBridge Rule**
    * In the Rule details section
      * Name: **dc-common-lambda-auto-start**
      * Description: **dc-common-lambda-auto-start**
      * Select Schedule
      * Click Next
    * In the Schedule pattern interface
      * Two schedule options are available:
        * A detailed schedule that runs at a specific time, such as 8:00 AM PST on the first Monday of every month
        * A schedule that runs at a regular interval, such as every 10 minutes
      * Select **A schedule that runs at a regular rate, such as every 10 minutes**
      * Set the rate value to **8 hours**
      * Click Next
    * In the Target interface
      * Select AWS service
      * Select Lambda function
      * Function: **dc-common-lambda-auto-start**
      * Click Next
    * Click Next again
    * Review and click Create rule

  * **Verify the Results**
    * Check the EC2 interface and the instance status
    * Go to the Lambda function responsible for starting instances
      * Click Test
      * Select Create new event
      * Event name: **instance-start**
      * Click Save
      * Click Test
    * A **Starting instance** notification should appear in the Slack workspace
    * Similarly, for the Lambda function responsible for stopping instances:
      * Click Test
      * Select Create new event
      * Event name: **instance-stop**
      * Click Save
      * Click Test
    * Verify that the instance has changed to the **Stopped** state
    * A **Stopping Instance** notification should appear in the Slack workspace

  * **Clean Up Resources**
    * **Delete Lambda Functions**
      * Access the AWS Lambda page
      * Select the functions related to this lab
      * Click Delete

    * **Delete CloudWatch Events Rules**
      * Access the CloudWatch page
      * Select Rules
      * Select the rules related to this lab
      * Click Actions
      * Click Delete

## Thursday: Routing, Navigation, and New SOC Pages Update
* **Overall Description**
  * Focused on extending and completing routing functionality while integrating new advanced pages into the Frontend SOC Dashboard.
  * This is a critical step toward improving navigation capabilities and preparing for future modules such as AI Threat Intelligence, Attack Surface Management, MITRE ATT&CK Framework, and Case Management.

* **Specific Changes**
  * **Main Routing Update (`src/App.tsx`)**
    * Added imports for 4 new pages:
      * `AIThreatDetectionPage`
      * `AttackSurfacePage`
      * `MitreAttackPage`
      * `CaseManagementPage`

    * Improved the type definition of the `currentView` state:
      * Before: Hardcoded union type (`"dashboard" | "alerts" | ...`)
      * After: Uses `AppView` (defined in `types/views.ts`) — resulting in cleaner, more maintainable, and scalable code.

    * Extended the conditional rendering logic (`AnimatePresence`) to support rendering the new pages based on `currentView`.
    * Updated Sidebar navigation to link to the newly added views.

  * **Mock Server Update (`frontend/server.ts`)**
    * Changed the default port from `3000` to `3001` (or retrieves it from the environment variable `process.env.PORT`).
    * This helps prevent port conflicts when running alongside other services (e.g., FastAPI backend typically runs on port `8000`).

  * **Added / Updated Pages and Configuration Files**
    * Newly added pages:
      * `AIThreatDetectionPage.tsx` — AI-powered threat detection monitoring page.
      * `AttackSurfacePage.tsx` — Attack Surface Management page.
      * `MitreAttackPage.tsx` — MITRE ATT&CK Framework integration page.
      * `CaseManagementPage.tsx` — Case Management page.
      * `EndpointPage.tsx` — Endpoint Management page.

    * Supporting configuration files:
      * `aiThreatDetectionConfig.ts`
      * `attackSurfaceConfig.ts`
      * `caseManagementConfig.ts`
      * `mitreConfig.ts`

    * Updated shared components:
      * `IncidentsFeed.tsx`
      * `MultiColorDonut.tsx`
      * `Sidebar.tsx`
      * `ReportStats.tsx`
      * Updated CSS styles and type definitions (`views.ts`).

* **Detailed Content of New Pages (Mock Data)**
  * **AI Threat Detection Page** includes:
    * KPI cards:
      * Total Detections
      * Avg Accuracy
      * False Positive Rate
      * Active Models
      * Avg Latency
    * Detection Timeline (24h) with mock data.
    * Model Performance Radar Chart (comparison across multiple models).
    * Accuracy Trend Line Chart.
    * Multi-color Donut Chart showing attack-type distribution.
    * Recent Detections list.
    * Active Models status panel.

* **Attack Surface Page**, **MITRE ATT&CK Page**, and **Case Management Page** are also implemented with similar structures, utilizing rich mock datasets to simulate real-world SOC workflows and interfaces.

* **Overall Status of Branch `devphu` After the Update**
  * Frontend has become significantly more complete with multiple advanced pages.
  * Stable Dark/Light mode support.
  * Realtime WebSocket integration (mock server).
  * Fully functional Sidebar navigation.
  * Multiple charts, KPI widgets, alert feeds, and event detail modals.
  * Well-prepared for future backend integration (Track A).
