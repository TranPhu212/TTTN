---
title: "Week 1 Worklog"
date: 2026-04-17
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---


### Week 1 Objectives:

* **Connection & Integration:** Get acquainted with the First Cloud Journey community, master the program's rules and regulations, and complete the workspace setup (AWS Free Tier account)
* **Governance & Basic Security:** Understand and practice setting up AWS Budgets for cost management, alongside AWS IAM for access control (Users, Groups, Roles, and Policies)
* **AWS Infrastructure Foundations:** Gain a comprehensive understanding of the AWS Global Infrastructure and core service categories: Compute, Storage, and Database
* **Networking & Management Tools:** Gain a deep understanding of networking with Amazon VPC and become proficient in interacting with AWS services via the AWS Management Console and AWS CLI

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
| 6 | - Get acquainted with FCJ members <br> - Read and note the internship program rules and regulations <br> - Create an AWS Free Tier account | 17/04/2026 | 17/04/2026 | <https://000001.awsstudygroup.com/> |
| 2 | - Set up AWS Budgets for cost management | 20/04/2026 | 20/04/2026 | <https://000007.awsstudygroup.com/> |
| 3 | - Learn about AWS and service categories: <br>&emsp; + Compute <br>&emsp; + Storage <br>&emsp; + Networking <br>&emsp; + Database <br>&emsp; + ... <br> - Study Access Management with AWS IAM (User, Group, Policy, Role) | 21/04/2026 | 21/04/2026 | <https://000002.awsstudygroup.com/> |
| 4 | - Learn Networking with Amazon VPC | 22/04/2026 | 22/04/2026 | <https://000003.awsstudygroup.com/> |
| 5 | - **Practice:** <br>&emsp; + Practice basic AWS CLI commands | 23/04/2026 | 23/04/2026 | <https://000003.awsstudygroup.com/> |

### Week 1 Achievements:

## Friday: Infrastructure Initialization & Environment Onboarding

* **Environmental Integration:**
    * **Team Connection:** Connect and get acquainted with the members of the First Cloud Journey (FCJ) community
        * Establish communication channels (Whatsapp/Linkedin) and identify technical support Mentors
    * **Rule Research:** Thoroughly read and analyze the internship terms and Worklog reporting procedures (Daily/Weekly)
        * **Commitment:** Ensure data confidentiality and adhere to information security principles when practicing in the Cloud environment

* **AWS Account Administration:**
    * **Initialize AWS Free Tier Account:**
        * Register an account at AWS Free Tier
        * **Technical Requirements:** Use an international payment card (Visa/Mastercard) with at least $1 available for account verification
        * **Region Selection:** Prioritize regions near Vietnam, such as Singapore (ap-southeast-1), to ensure the lowest latency during practice
    ![Proof: AWS account activated successfully](/images/1-Worklog/1.1-Week1/Day6/Create_Account.png)
    * **Root Account Hardening:**
        * **Activate MFA (Multi-Factor Authentication):** This is a mandatory step immediately after account creation. Use applications like Google Authenticator or Authy to create a second layer of security for the Root account
    ![Proof: MFA activated successfully for the account](/images/1-Worklog/1.1-Week1/Day6/MFA_success.png)

* **Identification and Classification of Free Services:**
    * Based on the instructional documentation at https://000001.awsstudygroup.com/, classify the three types of AWS offers:
    * **Always Free:** Services such as AWS Lambda (1 million requests/month), Amazon DynamoDB (25GB storage)
    * **12 Months Free:**
        * **Amazon EC2:** 750 hours/month (t2.micro or t3.micro instance types depending on the region).
        * **Amazon S3:** 5GB of Standard storage capacity
        * **Amazon RDS:** 750 hours/month for micro database instances
    * **Trials:** Premium services with short-term trials ranging from 30-60 days (such as Amazon SageMaker or GuardDuty)

* **Identifying "Credit Killers" (Cost Risk Warnings):**
    * Note services that easily incur unintended charges even during the Free Tier period:
    * **Elastic IP (EIP):** Charges apply if registered but not attached to a running EC2 instance
    * **NAT Gateway:** Not included in the Free Tier. Maintenance fees are approximately $0.045/hour (can quickly drain your account balance if you forget to delete it)
    * **EBS Volumes:** Only a total of 30GB capacity is free. Creating excessive redundant volumes will result in storage charges

## Monday: Cost Management with AWS Budgets

* **Cost Management (AWS Budgets - Knowledge Base)**
    * **Shared Responsibility Model for Cost:** AWS provides the tools, but the user is responsible for monitoring and setting limits to avoid resource wastage
    * **Budget Types:**
        * **Cost Budget:** Tracks based on the actual amount (USD) incurred
        * **Usage Budget:** Tracks based on resource usage metrics (running hours, storage capacity) - extremely important for controlling Free Tier limits
        * **Reservation Budget:** Tracks the efficiency of pre-purchased resources (intended for enterprises).
    * **Alerting Mechanisms:**
        * **Actual:** Alerts when costs have already occurred
        * **Forecasted:** Alerts based on AWS machine learning algorithms, predicting month-end costs based on current usage habits (helps prevent risks early)
    * **Data Latency:** Understand that Billing data is usually delayed by 8 - 12 hours; therefore, it is necessary to set alert thresholds slightly lower than the desired level

* **Cost Management (AWS Budgets - Setup Process)**
    * **Create a Cost Budget**
        * Set up a budget based on actual invoice costs
        * Set the alert threshold at **$0.01** for absolute control over any incurred costs
        * Apply to all AWS services
        * Log in to the AWS Management Console and search for the **Billing and Cost Management** service in the search bar
        * ![Proof: Select AWS Billing and Cost Management service](/images/1-Worklog/1.1-Week1/Day2/AWS_Billing_and_Cost_Management.png)
        * On the management page, select **Budgets** from the left menu. Click the **Create budget** button
        * ![Proof: Create budget](/images/1-Worklog/1.1-Week1/Day2/Create_a_budget.png)
        * Select **Customize**
        * Under **Budget types**, select **Cost budget**.
        * Click **Next**
        * ![Proof: Budget setup section](/images/1-Worklog/1.1-Week1/Day2/Budget_setup_1.png)
        * ![Proof: Budget setup section](/images/1-Worklog/1.1-Week1/Day2/Budget_setup_2.png)
        * In the **Budget name** field, enter **Monthly**
        * ![Proof: Set your budget interface](/images/1-Worklog/1.1-Week1/Day2/Set_your_budget.png)
        * **Period:** Choose the time interval for the Budget:
            * Daily
            * Monthly
            * Quarterly
            * Annually
        * **Budget effective dates:**
            * **Recurring Budget:** If you want the Budget to repeat periodically
            * **Expiring Budget:** If you only want the Budget to apply once
        * **Specify your monthly budget:**
            * **Fixed:** If you want the budget for each period to be the same
            * **Monthly Budget Planning:** If you want to set different budgets for each month
            * **Budgeted amount:** Enter the amount corresponding to your budget
        * ![Proof: Set budget amount](/images/1-Worklog/1.1-Week1/Day2/Set_budget_amount.png)
        * In the **Budget scope** section, select **All AWS services** to apply the budget to all AWS services. For **Aggregate costs by**, select **Unblended costs**. Then click **Next**
        * ![Proof: Budget scope](/images/1-Worklog/1.1-Week1/Day2/Budget_scope.png)
        * Select **Add an alert threshold** to set up a notification threshold
        * ![Proof: Setup alert threshold](/images/1-Worklog/1.1-Week1/Day2/Add_an_alert_threshold.png)
        * Configure the detailed settings for the **Alert** and select **Next**
        * ![Proof: Alert configuration](/images/1-Worklog/1.1-Week1/Day2/Alert.png)
        * Review the action settings (if any) and select **Next**
        * ![Proof: Review settings](/images/1-Worklog/1.1-Week1/Day2/Check_Alert.png)
        * Review the entire configuration and select **Create budget** to complete
        * ![Proof: Create budget](/images/1-Worklog/1.1-Week1/Day2/Create_budget.png)
        * Confirm that the Budget has been created successfully
        * ![Proof: Budget created successfully](/images/1-Worklog/1.1-Week1/Day2/Budget_tạo_thành_công.png)

    * **Create Usage Budget**
        * Monitor resource usage quotas (such as EC2 running hours, S3 storage) to ensure they do not exceed Free Tier limits
        * Log in to the AWS Management Console and search for "Billing and Cost Management" in the search bar
        * ![Proof: Select AWS Billing and Cost Management service](/images/1-Worklog/1.1-Week1/Day2/AWS_Billing_and_Cost_Management.png)
        * In the management dashboard, select "Budgets" from the left menu. Click "Create budget"
        * ![Proof: Create a budget](/images/1-Worklog/1.1-Week1/Day2/Create_a_budget.png)
        * Select "Customize"
        * Under "Budget types", select "Usage budget"
        * Click "Next"
        * ![Proof: Budget setup](/images/1-Worklog/1.1-Week1/Day2/Budget_setup.png)
        * In the "Set your budget" interface:
            * Under "Budget name", enter a name for your budget
        * In the "Budget against" section:
            * Select "Usage type groups"
            * Select "EC2: ELB - Running Hours" to track EC2 instance hours
        * ![Proof: Budgeting Details](/images/1-Worklog/1.1-Week1/Day2/Details_Budget.png)
        * Period: Choose the budget timeframe (Daily/Monthly/Quarterly/Annually)
        * Budget renewal type: Choose renewal type (Recurring/Expiring)
        * Budgeting method: Choose budgeting method (Fixed/Planned)
        * Enter the maximum usage hours you want to limit
        * ![Proof: Set budget amount](/images/1-Worklog/1.1-Week1/Day2/Set_budget_amount.png)
        * In the "Budget scope" section, keep the default and click "Next"
        * ![Proof: Budget scope](/images/1-Worklog/1.1-Week1/Day2/Budget_scope.png)
        * In the "Configure alerts" section, select "Add an alert threshold"
        * ![Proof: Set up alert threshold](/images/1-Worklog/1.1-Week1/Day2/Add_an_alert_threshold.png)
        * Set the alert threshold (% of budget)
        * Add an email address to receive notifications when the threshold is exceeded
        * ![Proof: Alert configuration](/images/1-Worklog/1.1-Week1/Day2/Alert.png)
        * Click "Next" to continue
        * ![Proof: Review settings](/images/1-Worklog/1.1-Week1/Day2/Check_Alert.png)
        * Review settings and click "Create budget" to finish
        * ![Proof: Create budget](/images/1-Worklog/1.1-Week1/Day2/Create_budget.png)
        * Once successfully created, you will see the new budget in the list
        * ![Proof: Usage budget successfully created](/images/1-Worklog/1.1-Week1/Day2/Tạo_Usage_budget_thành_công.png)
        * Check "Budget health" to monitor current usage against the established budget
        * ![Proof: Budget health](/images/1-Worklog/1.1-Week1/Day2/Budget_health.png)
        * View "Budget history" to track usage trends over time
        * ![Proof: Budget history](/images/1-Worklog/1.1-Week1/Day2/Budget_history.png)

    * **Create RI & Savings Plans Budget**
        * Set up monitoring for reserved entities and savings plans to optimize costs for long-term projects
        * Log in to the AWS Management Console and select "Billing and Cost Management"
        * ![Proof: Select AWS Billing and Cost Management service](/images/1-Worklog/1.1-Week1/Day2/AWS_Billing_and_Cost_Management.png)
        * In the management dashboard, select "Budgets" from the left menu. Click "Create budget"
        * ![Proof: Create a budget](/images/1-Worklog/1.1-Week1/Day2/Create_a_budget.png)
        * Select "Customize"
        * Select "Reservation budget"
        * Click "Next"
        * ![Proof: Budget setup](/images/1-Worklog/1.1-Week1/Day2/Budget_setup_3.png)
        * Enter the budget name
        * ![Proof: Budget name](/images/1-Worklog/1.1-Week1/Day2/Budget_name.png)
        * Configure the "Coverage threshold"
        * ![Proof: Coverage threshold](/images/1-Worklog/1.1-Week1/Day2/Coverage_threshold.png)
        * Configure the "Budget scope"
        * ![Proof: Budget scope](/images/1-Worklog/1.1-Week1/Day2/Budget_scope.png)
        * In the "Alert setting" section, enter the email address. Click "Next"
        * ![Proof: Alert setting](/images/1-Worklog/1.1-Week1/Day2/Alert_setting.png)
        * Click "Create budget"
        * ![Proof: Create RI budget](/images/1-Worklog/1.1-Week1/Day2/Create_RI_budget.png)
        * Budget creation complete
        * ![Proof: RI budget successfully created](/images/1-Worklog/1.1-Week1/Day2/Tạo_RI_Budget_thành_công.png)
        * Verify the created budget
        * ![Proof: Check RI budget](/images/1-Worklog/1.1-Week1/Day2/Check_RI_budget.png)

    * **Configure Alerts & Email Notifications**
        * Set up automatic email notifications to personal accounts when actual or forecasted costs hit established thresholds
        * Log in to the AWS Management Console and search for "Billing and Cost Management"
        * ![Proof: Select AWS Billing and Cost Management service](/images/1-Worklog/1.1-Week1/Day2/AWS_Billing_and_Cost_Management.png)
        * In the management dashboard, select "Budgets" then "Create budget"
        * ![Proof: Create a budget](/images/1-Worklog/1.1-Week1/Day2/Create_a_budget.png)
        * Select "Customize"
        * Under "Budget types", select "Savings Plans budget"
        * Click "Next"
        * ![Proof: Budget setup](/images/1-Worklog/1.1-Week1/Day2/Budget_setup_3.png)
        * In the "Details" section, enter your budget name
        * Configure the "Utilization threshold" for Savings Plans
        * ![Proof: Budgeting Details](/images/1-Worklog/1.1-Week1/Day2/Details_saving_plan_budget.png)
        * In "Budget scope", keep the default options. Click "Next"
        * ![Proof: Budget scope](/images/1-Worklog/1.1-Week1/Day2/Budget_scope.png)
        * In the "Alert setting" section, enter the email address. Click "Next"
        * ![Proof: Alert setting](/images/1-Worklog/1.1-Week1/Day2/Alert_setting.png)
        * Review the settings and click "Create budget" to finish
        * ![Proof: Create Savings Plan budget](/images/1-Worklog/1.1-Week1/Day2/Create_saving_plan_budget.png)
        * Upon successful creation, a confirmation message will appear
        * Check the details of the created budget in the budget list
        * ![Proof: Savings Plan budget successfully created](/images/1-Worklog/1.1-Week1/Day2/Tạo_saving_plan_Budget_thành_công.png)

    * **Resource Cleanup**
        * Performed inspections and deleted unnecessary experimental resources to maintain a clean account state and avoid hidden maintenance fees
        * Log in to the AWS Management Console and search for "Billing and Cost Management"
        * ![Proof: Select AWS Billing and Cost Management service](/images/1-Worklog/1.1-Week1/Day2/AWS_Billing_and_Cost_Management.png)
        * In the management dashboard, select "Budgets" from the left menu
        * Perform budget deletion:
            * Select the Budget to be deleted
            * Select "Action"
            * Click the "Delete" button
        * ![Proof: Delete budget](/images/1-Worklog/1.1-Week1/Day2/Delete_budget.png)
        * In the confirmation dialog, click "Delete" to finalize the budget removal
        * Repeat the above steps for all remaining Budgets created during the practice session

## Tuesday: Identity and Access Management (AWS IAM)

* **Overview of Core Service Groups (Global Infrastructure & Core Services):**
    * **Compute (The "Brain"):**
        * This is where commands are processed and applications are run
        * **Amazon EC2 (Elastic Compute Cloud):** Provides virtualized servers. You have full control over the operating system
        * **AWS Lambda (Serverless):** Runs code based on events without managing servers. You only pay for the time the code is actually running
    * **Storage (The "Warehouse"):**
        * **Amazon S3 (Simple Storage Service):** Object storage (images, videos, backup files). It has data durability of up to 99.999999999% (11 nines)
        * **Amazon EBS (Elastic Block Store):** Acts like an external SSD/HDD drive to be attached to EC2 instances
    * **Networking (The "Pathways"):**
        * **Amazon VPC (Virtual Private Cloud):** Creates an isolated network partition for your resources
        * **Amazon Route 53:** A Domain Name System (DNS) that helps route users to your applications
    * **Database (The "Memory"):**
        * **Amazon RDS (Relational Database Service):** For structured data (MySQL, PostgreSQL, SQL Server)
        * **Amazon DynamoDB:** For unstructured data, requiring ultra-fast speed and massive scale

* **AWS IAM (Identity and Access Management)**
    * **Core Concepts (The Big Four):**
        * **IAM Users:** Represents a person or an application. Each User has its own set of credentials (Password or Access Key)
        * **IAM Groups:** A collection of Users. Instead of granting permissions to 10 engineers individually, you create a "Developers" group and assign permissions to that group
        * **IAM Policies:** A JSON file that defines permissions
            * **Managed Policies:** Pre-created by AWS (e.g., AdministratorAccess)
            * **Customer Managed Policies:** Written by you to customize permissions
        * **IAM Roles:** Like a "hat" of authority. A service (such as EC2) can "wear" this hat to gain access to S3 without needing to store passwords inside the server
    * **"Classic" Security Principles:**
        * **Principle of Least Privilege:** Always start by allowing nothing (Deny all), then grant only the specific permissions necessary to complete the task
        * **Shared Responsibility Model:**
            * **AWS is responsible for:** Security "Of" the Cloud (Physical infrastructure, data centers)
            * **The Customer is responsible for:** Security "In" the Cloud (Data, IAM configurations, EC2 Operating Systems)

* **Secure Workflow (Best Practices):**
    * Based on theory, the standard process when working with AWS is:
        * Lock away the Root account (only use it when absolutely necessary)
        * Create an IAM User for yourself and assign it to an Admin group
        * Enable MFA for all accounts
        * Use Roles instead of Access Keys whenever possible to avoid credential exposure

* **Create Admin Group:**
    * Create a new user, set a custom password
    * Add the user to the `admin` group to inherit permissions
    * Access AWS Management Console at AWS Web Service page
    * Click on your AWS account name in the top right corner and select Security Credentials
    * ![Proof: AWS Management Console](/images/1-Worklog/1.1-Week1/Day3/AWS_Management_Console.png)
    * Use the Search bar on AWS Management Console
    * Enter “IAM”
    * Select IAM service from the search results
    * ![Proof: Search IAM](/images/1-Worklog/1.1-Week1/Day3/Search_bar.png)
    * In the left navigation pane, select User Groups and click Create Group
    * ![Proof: Create Group](/images/1-Worklog/1.1-Week1/Day3/Create_Group.png)
    * In the Name the group section, enter the group name (e.g., AdminGroup)
    * ![Proof: Name the group](/images/1-Worklog/1.1-Week1/Day3/Name_the_group.png)
    * Search for AdministratorAccess
    * Select policy AdministratorAccess from the list
    * Click Create Group
    * ![Proof: Attach permissions policies](/images/1-Worklog/1.1-Week1/Day3/Attach_permissions_policies.png)
    * Confirm the Admin Group creation has been completed successfully
    * ![Proof: Admin Group created successfully](/images/1-Worklog/1.1-Week1/Day3/Admin_group_created.png)

* **Create Admin User:**
    * Create a new user, set a custom password
    * Add the user to the `admin` group to inherit permissions
    * ![Proof: Create Admin User](/images/1-Worklog/1.1-Week1/Day3/Create_Admin_User.png)
    * ![Proof: User details](/images/1-Worklog/1.1-Week1/Day3/Specify_user_details_1.png)
    * ![Proof: User details](/images/1-Worklog/1.1-Week1/Day3/Specify_user_details_2.png)
    * ![Proof: Permissions Options](/images/1-Worklog/1.1-Week1/Day3/Set_permissions.png)
    * ![Proof: Review and create](/images/1-Worklog/1.1-Week1/Day3/Review_and_create.png)
    * ![Proof: Retrieve password](/images/1-Worklog/1.1-Week1/Day3/Retrieve_pasword.png)
    * ![Proof: Download .csv file](/images/1-Worklog/1.1-Week1/Day3/Dowload_csv_file.png)
    * ![Proof: Admin User created successfully](/images/1-Worklog/1.1-Week1/Day3/Create_adminuser_success.png)

* **Login and Check:**
    * Use the specific login path for IAM User to check actual permissions
    * Open the login URL saved from the user creation step
    * Or access IAM Dashboard to get the login URL
    * ![Proof: Access URL](/images/1-Worklog/1.1-Week1/Day3/Truy_cập_URL.png)
    * Open an Incognito/Private browser window
    * ![Proof: Incognito/Private](/images/1-Worklog/1.1-Week1/Day3/Đăng_nhập_ẩn_danh.png)
    * Enter Account ID or alias (if any)
    * Enter IAM Username
    * Enter temporary password from the .csv file
    * Follow instructions to change password
    * ![Proof: Change password](/images/1-Worklog/1.1-Week1/Day3/Thay_đổi_mật_khẩu.png)
    * Confirm successful login
    * ![Proof: Admin User logged in successfully](/images/1-Worklog/1.1-Week1/Day3/Đăng_nhập_thành_công.png)
    * Check Administrator permissions
    * ![Proof: Check Admin permissions](/images/1-Worklog/1.1-Week1/Day3/Kiểm_tra_quyền.png)

* **Create Admin Role:**
    * Set up Role with Trusted Entity being the current AWS account itself
    * Assign `AdministratorAccess` permission to this Role
    * Access AWS Management Console and open IAM service
    * In the left navigation pane, select Roles and click Create role
    * ![Proof: Initialize Role](/images/1-Worklog/1.1-Week1/Day3/Create_role.png)
    * Select AWS account
    * This option allows the role to be used within the current AWS account or another account
    * ![Proof: Select trusted entity](/images/1-Worklog/1.1-Week1/Day3/Select_trusted_entity.png)
    * Select Another AWS account
    * Enter Account ID of the current AWS account
    * To view Account ID, click on the account name in the top right corner
    * Click Next
    * Search for and select policy AdministratorAccess
    * This policy grants full administrative permissions for the AWS account
    * Click Next
    * ![Proof: Add permissions](/images/1-Worklog/1.1-Week1/Day3/Add_permissions.png)
    * Enter role name (e.g., AdminRole)
    * Add a detailed description of the role's purpose
    * ![Proof: Role name](/images/1-Worklog/1.1-Week1/Day3/Role_name.png)
    * Review configuration and click Create role
    * ![Proof: Add tag](/images/1-Worklog/1.1-Week1/Day3/Add_tag.png)
    * Confirm role creation was successful
    * ![Proof: Role created successfully](/images/1-Worklog/1.1-Week1/Day3/Tạo_role_thành_công.png)
    * Check detailed information of the newly created role
    * ![Proof: View Role information](/images/1-Worklog/1.1-Week1/Day3/Kiểm_tra_role.png)

* **Create Operator User:**
    * Create a new user (e.g., `OperatorUser`) but **do not** assign any direct permissions
    * Access IAM service via the search bar
    * Enter “IAM” and select the service from results
    * ![Proof: Search IAM](/images/1-Worklog/1.1-Week1/Day3/Search_bar.png)
    * Select Users from the left menu
    * Click Add Users
    * ![Proof: Create Operator User](/images/1-Worklog/1.1-Week1/Day3/Create_Admin_User.png)
    * Enter user name: OperatorUser
    * Select Provide user access to the AWS Management Console
    * Select I want to create an IAM user
    * Set up password:
        * Select Autogenerated password or
        * Select Custom password to set manually
    * Uncheck Users must create a new password at next sign-in
    * ![Proof: User information](/images/1-Worklog/1.1-Week1/Day3/thông_tin_User.png)
    * Click Next to continue
    * ![Proof: Skip permissions](/images/1-Worklog/1.1-Week1/Day3/Pass_permission.png)
    * Add tags to classify and manage user
    * Example: Department = Operations, Environment = Production
    * Review configuration and click Create user
    * ![Proof: Skip tag](/images/1-Worklog/1.1-Week1/Day3/Pass_add_tag.png)
    * Store login information securely
    * Prepare for assume role configuration
    * ![Proof: OperatorUser created successfully](/images/1-Worklog/1.1-Week1/Day3/Tạo_OperatorUser_thành_công.png)
    * Set up MFA immediately after creating the user
    * Save console login URL to bookmarks
    * Prepare assume role instructions for the user

* **Allow OperatorUser to switch role**
    * **Initialize Admin Role:** Create an IAM Role with `AdministratorAccess` policy, set the Trust Entity as the current AWS account
    * **Create OperatorUser:** Initialize the operational user initially without permissions. Then, attach an **Inline Policy** allowing the `sts:AssumeRole` action pointing to the ARN of the created Admin Role
    * Click Users
    * Click OperatorUser
    * ![Proof: Select Role](/images/1-Worklog/1.1-Week1/Day3/Chọn_role.png)
    * Click Add inline policy
    * ![Proof: Create inline policy](/images/1-Worklog/1.1-Week1/Day3/Add_inline_policy.png)
    * Fill in the policy content below, remember to replace with the account ID you are using and the AdminRole you created earlier
    * This policy allows the IAM User to assume the AdminRole located in the specified account ID
    * Click Review Policy
    * ![Proof: Policy editor](/images/1-Worklog/1.1-Week1/Day3/Policy_editor.png)
    * Name the inline policy AllowSwitchAdminPolicy
    * Click Create Policy
    * ![Proof: Create Policy](/images/1-Worklog/1.1-Week1/Day3/Create_Policy.png)

* **Login OperatorUser**
    * Log into the Console with the `OperatorUser` account. At this point, the User does not have access to services like S3 or Billing
    * In the Security credentials tab of OperatorUser
    * Copy the specific console login link for your AWS account
    * ![Proof: Enter OperatorUser](/images/1-Worklog/1.1-Week1/Day3/Vào_operatoruser.png)
    * Open a new browser window
    * Paste the login URL into the address bar
    * Enter login information:
        * IAM user name: OperatorUser
        * Provided password
    * Click Sign in
    * ![Proof: Login OperatorUser](/images/1-Worklog/1.1-Week1/Day3/Đn_role_operator.png)
    * Try accessing the IAM service
    * You will see a notification of no access permissions
    * This confirms OperatorUser has no direct permissions for AWS services
    * ![Proof: Check status](/images/1-Worklog/1.1-Week1/Day3/Xác_nhận_trạng_thái.png)

* **Switch Role**
    * Use the **Switch Role** feature on the user menu bar, enter Account ID and Role Name (`AdminRole`)
    * After switching successfully, the user identity changes and the account has full administrative rights to operate
    * Click on the OperatorUser name in the top right corner
    * Select Switch Roles
    * ![Proof: Switch Role operation](/images/1-Worklog/1.1-Week1/Day3/Switch_role.png)
    * Account: Enter your AWS Account ID
    * Role: Enter the AdminRole created earlier
    * Color: Select a color to distinguish roles (optional)
    * Click Switch Role to confirm
    * ![Proof: Switch role information](/images/1-Worklog/1.1-Week1/Day3/Thông_tin_chuyển_role.png)
    * The displayed role name will change to AdminRole
    * You can return to OperatorUser by clicking Switch back
    * You now have full AdministratorAccess permissions
    * ![Proof: Switch role successful](/images/1-Worklog/1.1-Week1/Day3/Chuyển_role_thành_công.png)

* **Cleanup**
    * After completing the lab, I proceeded to delete the IAM Users, Groups, and Roles to ensure security and maintain a clean account
    * Access AWS Management Console
    * Navigate to IAM service
    * Select Users
    * Select user related to the lab
    * Click Delete
    * ![Proof: Delete IAM User](/images/1-Worklog/1.1-Week1/Day3/Xóa_IAM_User.png)
    * Carefully check the user information to be deleted
    * Enter user name to confirm
    * Click Delete to complete
    * ![Proof: Confirm delete IAM User](/images/1-Worklog/1.1-Week1/Day3/Xác_nhận_xóa_IAM_User.png)
    * Return to IAM service
    * Select User groups
    * Select group related to the lab
    * Click Delete
    * ![Proof: Delete IAM User Group](/images/1-Worklog/1.1-Week1/Day3/Xóa_IAM_User_Group.png)
    * Carefully check the group information to be deleted
    * Click Delete to complete
    * ![Proof: Confirm delete IAM User Group](/images/1-Worklog/1.1-Week1/Day3/Xác_nhận_xóa_IAM_User_Group.png)

## Wednesday: Advanced Network Infrastructure - AMAZON VPC

### Amazon VPC Overview
**Amazon Virtual Private Cloud (VPC)** is a private virtual network dedicated to your AWS account. It allows you to launch AWS resources in a logically isolated virtual network, providing complete control over your networking environment

* **Core Characteristics:**
    * **Isolation:** Completely separate from other virtual networks on the AWS infrastructure
    * **Scope:** A VPC spans an entire **Region** but is divided into **Availability Zones (AZs)** through Subnets
    * **Control:** Define your own IP ranges, Route Tables, and configure security layers (Security Groups/NACLs)

### Key Components
* **CIDR Block & IP Addressing**
    * VPC uses the **CIDR** methodology to define IP address ranges.
    * **VPC CIDR:** Typically uses a `/16` range (65,536 IPs) to optimize scalability
    * **Subnet CIDR:** Subdivided from the VPC CIDR (commonly using `/24` - 256 IPs)
    * **5 AWS Reserved IPs:**
        * `.0`: Network address
        * `.1`: VPC Router (Default gateway)
        * `.2`: Amazon Provided DNS
        * `.3`: Reserved for future use
        * `.255`: Network broadcast address (though VPC does not support broadcast)

* **Subnets (Network Partitions)**
    * **Public Subnet:** Has a Route pointing to an **Internet Gateway (IGW)**. Contains resources that need to communicate directly with the Internet (Web Servers, NAT Gateways)
    * **Private Subnet:** No Route to the IGW. Contains resources requiring high security (Databases, Backend Apps)

* **Traffic Coordination (Routing)**
    * **Internet Gateway (IGW):** The gateway connecting the VPC to the Internet. It is essential for Public Subnets to access the outside world
    * **Route Table:** Contains a set of routing rules
        * *Local Route:* Allows resources within the same VPC to communicate with each other
        * *Public Route:* `0.0.0.0/0 -> IGW`
    * **NAT Gateway:** A service residing in a Public Subnet that enables resources in a Private Subnet to access the Internet (for patches or library downloads) while preventing the Internet from initiating a connection back to them

### Multi-layered Security
* **The VPC security system operates based on two main firewall layers:**
    * **Security Groups (Instance Level)**
        * Acts as a firewall for servers (EC2)
        * **Stateful:** If you allow inbound traffic, the return outbound traffic is automatically allowed
        * Only supports **Allow** rules

    * **Network ACLs (Subnet Level)**
        * Acts as a firewall for the entire partition (Subnet)
        * **Stateless:** You must explicitly configure both Inbound and Outbound rules
        * Supports both **Allow** and **Deny** rules

### High Availability (HA) Design Thinking
* **To ensure the system remains uninterrupted when a data center encounters an issue:**
    * Deploy resources across at least **2 Availability Zones**
    * In each AZ, set up corresponding pairs of Public/Private Subnets
    * Utilize high-availability AWS services like **ELB (Elastic Load Balancing)** to distribute traffic

## Thursday: Overview of Cloud Computing and AWS Infrastructure

* **Introduction to AWS**
    * **The New Era of Services:** Introduction to emerging services and the rise of **AI Agents** in learning and professional environments.

    * **Cloud Computing:**
        * Definition: Providing IT services over the internet using a **"Pay-as-you-go"** pricing model.

        * **Traditional (On-premises) vs. Modern (Cloud) Models:**
            * **Traditional (On-premises):** * To build systems or products for a large user base, businesses must build their own infrastructure (data centers/in-house).
                * Requires massive upfront investment in hardware and facilities.
                * High cost of failure: If the project or service is unsuccessful, the wasted capital investment is significant

            * **Modern (Cloud):** * Cloud computing is essentially "renting" resources. Instead of buying a whole house, you can rent hotel rooms
                * Operates on a "Pay-as-you-go" model (paying only for what you use)

        * **Key Benefits:**
            * **Cost Optimization:** Eliminates unnecessary hardware maintenance and ownership costs
            * **Speed & Agility:** Deploy resources globally in just a few minutes
            * **Security & AI:** Leverage built-in security tools and advanced Artificial Intelligence from the provider
            * **Global Scale:** Easily scale applications to serve customers anywhere in the world
    
    * **AWS Global Infrastructure**
        * **AWS Data Center**
            * Centralizes all AWS hardware and equipment on a massive scale, housing tens of thousands of servers
            * All equipment within an AWS data center is **custom-designed** based on AWS operational standards
            * AWS designs its own motherboards, servers, networking systems, security systems, and even specialized **GPU lines**

        * **Availability Zone (AZ)**
            * Each AZ consists of one or more discrete data centers
            * **Fault Isolation:** Designed so that if an incident occurs, it will not affect two AZs simultaneously
            * **Incident Prevention:** Mitigates risks from power outages and natural disasters
            * The distance between AZs is large enough to prevent simultaneous impact but close enough for low-latency connectivity
            * Power and networking systems are designed to be highly independent
            * AWS design standards for data centers and AZs are at the highest level, exceeding general industry standards

        * **Region**
            * A Region consists of a minimum of **3 AZs** (some have more)
            * All Regions are interconnected via the **AWS Backbone Network**
            * Data and services are generally independent between Regions
            * **Global Scale Services:** Some services, such as DNS, are designed at a global scale and operate outside of a specific Region

        * **Edge Locations (Points of Presence - POP)**
            * These are network data centers located at the "edge" of the network
            * A network of data centers used to provide low-latency edge services

        * **Popular Edge Services:**
            * **CloudFront (CDN):** Acts as a Content Delivery Network, caching data that users frequently access to reduce latency
            * **Web Application Firewall (WAF):** Provides firewall protection for web applications
            * **Route 53 (DNS Service):** Domain hosting and resolution for both public and private environments

        * **Local Zone**
            * Functionally similar to a "miniature version" of an Availability Zone, placed closer to specific geographic areas to support ultra-low latency requirements

* **Management Console:**
    * **Root Login**
        * We can log in with the root user or with the IAM User (a sub user that helps manage AWS resource export)

    * **IAM User Login**
        * When logging in with an IAM User, we need to provide additional Account ID information (12-digit string) to identify the AWS Account

    * **Service Search**
        * After logging in to the AWS Management Console interface, we can search for AWS services
        * Each service will have its site management that allows us to the features of that service
    
    * **Support Center**
        * On the left, there is the Support menu, they can go to the Support Center to create support cases to request support from the AWS team

    * **AWS Command Line Interface (CLI)**
        * AWS command line interface (AWS CLI) is an open-source coding tool that allows you to interact with AWS services using commands
        * The AWS CLI allows you to run command development function that are compatible with those provided by the browser-based AWS Management Console
    
    * **AWS SDK**
        * AWS SDK simplifiles the use of AWS services for applications by providing a best-in-class library that is familiar to application development teams
        * The AWS SDK provides support for API lifecycle management tasks to AWS services such as credential management, retrying, data wrangling, serialization and deserialization