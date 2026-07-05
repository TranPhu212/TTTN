---
title: "Week 5 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.5. </b> "
---

### Week 5 Objectives:

* Develop and complete the Real-time Security Dashboard (Frontend Track B)
* Achieve full proficiency in Amazon EC2 on both Windows Server 2025 and Amazon Linux 2023, including deployment of Node.js applications
* Successfully implement VPC Peering and understand AWS Transit Gateway architecture
* Deepen understanding of AWS Security fundamentals: Shared Responsibility Model, IAM, Cognito, Organizations, Identity Center, and KMS

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
|  2  | - Devphu Frontend Dashboard Progress Update | 18/05/2026 | 18/05/2026 |
|  3  | - Windows Server 2025 & Amazon Linux 2023 (VPC, SG, Launch, Connect, Node.js App, Custom AMI, IAM Policy) | 19/05/2026 | 19/05/2026 | <https://000004.awsstudygroup.com/> |
|  4  | - Configuring VPC Peering & Cross-Peer DNS | 20/05/2026 | 20/05/2026 | <https://000010.awsstudygroup.com/> |
|  5  | - Overview of AWS Transit Gateway | 21/05/2026 | 21/05/2026 | <https://000010.awsstudygroup.com/> |
|  6  | - AWS Security Services - Shared Responsibility Model, IAM, Cognito, Organizations, Identity Center (SSO), KMS | 22/05/2026 | 22/05/2026 | <https://youtu.be/tsobAlSg19g> <br> <https://youtu.be/N_vlJGAqZxo> <br> <https://youtu.be/pZ2fgEFK3Vs> <br> <https://youtu.be/5oQY8Rogz9Y> <br> <https://youtu.be/NW1xrMkNMjU> <br> <https://youtu.be/GMihNQojhZc> <br> <https://youtu.be/clj2E0rNBEs> <br> <https://youtu.be/0SdpD2GPYz4> |


### Week 5 Achievements:

# Friday: Frontend Dashboard

## 1. Overview of branch `devphu`

The **devphu** branch is the main development branch for **Track B (Frontend Dashboard)**. 
It focuses on building a real-time dashboard interface, WebSocket integration, MITRE ATT&CK mapping, Event Detail Modal, UX/UI improvements, and Docker packaging

The branch is currently in the **initial frontend design and implementation phase**, using mock data and prepared for future backend integration

## 2. Current Status

- **Main technologies:** React + Vite + TypeScript + Tailwind CSS  
- **Commits:** Actively in development (focused on project structure setup)

### Main project structure
frontend/
├── src/
│ ├── components/ # Header, KPI widgets, Alert Feed, Charts, Modal...
│ ├── pages/ # Main dashboard page
│ ├── hooks/ # useSocket, useAlerts...
│ ├── store/ # State management
│ ├── utils/ # MITRE mapping, formatters, export helpers
│ ├── types/ # TypeScript interfaces (Alert, KPI, MITRE...)
│ ├── lib/ # Shared utilities
│ ├── assets/
│ └── App.tsx
├── package.json
├── vite.config.ts
├── .env.example
└── README.md

The dashboard currently uses **mock data** based on the expected backend contract and follows a modern **dark-themed UI concept**

## 3. Frontend Architecture (Track B)

### Technology stack

- React 18 + Vite  
- TypeScript  
- Tailwind CSS (Dark mode)  
- WebSocket client  
- Zustand or Context API for state management  
- React Router (if multi-page structure is required)

### Implemented features

- Modern dashboard layout (Sidebar + Header + Main content)
- KPI Widgets:
  - Total Alerts
  - Total Flows
  - Risk Score
  - Top Threat
- Real-time Alert Feed with filtering and sorting
- WebSocket hook (`useSocket.ts`) ready for real-time data streaming
- Event Details Modal concept
- MITRE ATT&CK technique mapping
- Fully responsive dark theme UI

## 4. Core Features

### 1. Header
- System name
- WebSocket status indicator
- AI Engine status
- User information

### 2. KPI Dashboard
- Real-time statistics over the last 24 hours

### 3. Visual Analytics
- Line chart
- Pie/Doughnut chart for attack classification

### 4. Real-time Alert Feed
- Live alert table with severity-based color coding

### 5. Event Detail Modal
- Detailed event information
- MITRE ATT&CK tactics & techniques mapping
- Evidence (Zeek, Suricata logs)
- AI analysis & decision flow
- Action buttons:
  - Block IP
  - Create Ticket
  - Export

## 5. How to run locally

```bash
cd frontend
npm install
cp .env.example .env

# Configure GEMINI_API_KEY if AI features are used
npm run dev
```

## Monday: Introduction to Amazon EC2
* **Introduction to Amazon EC2**
  * **Overview**
    * **Amazon Elastic Compute Cloud (EC2)** is a service that provides resizable virtual servers (virtual servers) in the AWS cloud.

  * **Key Features**
    * Fast instance provisioning
    * Scale resources up/down according to demand
    * Supports multiple operating systems (Linux, Windows, macOS...)
    * Pay-as-you-go billing by the hour/second

  * **Instance Types**
    * Instance Type determines:
      * **CPU**: Intel, AMD, ARM (Graviton), GPU
      * **Memory**: RAM capacity
      * **Network**: Network bandwidth
      * **Storage**: Supports EBS and Instance Store

  * **Important Components**
    * **AMI (Amazon Machine Image)**: Template containing OS + software
    * **Key Pair**: Used to SSH/RDP into the instance
    * **Security Group**: Instance-level firewall
    * **EBS Volume**: Network-attached storage
    * **Snapshot**: Backup copy of an EBS Volume

* **Prerequisites**
  * **Create VPC for Linux Instance**
    * **Create VPC for Linux Instance**
      * Amazon Virtual Private Cloud (VPC) allows you to launch AWS resources in a logically isolated virtual network. In this section, we will create a dedicated VPC for the Linux instance with public subnets for internet access.

    * **Steps**
      * Access the **AWS Management Console** → Search for and select **VPC**
      * Choose **Create VPC** → Select **VPC and more**
      * In **Name tag auto-generation**, enter `Linux`
      * For **VPC endpoints**, select **None** → Click **Create VPC**
      * After successful creation, select **View VPC**
      * Choose **Subnets** from the left menu
      * Select **Public subnet** → **Actions** → **Edit subnet settings**
      * Enable **Enable auto-assign public IPv4 address** → **Save**
      * Repeat the same for the remaining public subnets

  * **Create VPC for Windows Instance**
    * **Create VPC for Windows Instance**
      * Similar to the Linux section, we create a dedicated VPC for the Windows instance.

    * **Steps**
      * Go to **VPC** → **Create VPC** → Select **VPC and more**
      * In **Name tag auto-generation**, enter `Windows`
      * **VPC endpoints** = **None** → **Create VPC**
      * View VPC details
      * Go to **Subnets** → Select public subnet → **Edit subnet settings**
      * Enable **Enable auto-assign public IPv4 address** → **Save**
      * Repeat for the remaining public subnets

  * **Create Security Group for Linux Instance**
    * **Create Security Group for Linux Instance**
      * A Security Group acts as a virtual firewall to control inbound and outbound traffic to the EC2 instance.

    * **Steps**
      * Go to **VPC** → **Security Groups** → **Create security group**.
      * **Name**: `Linux-SG`  
         **Description**: `Security group for Linux instance`  
         **VPC**: Select `Linux-vpc`.
      * Configure **Inbound rules** (add 7 rules):

| Type              | Port     | Description                    |
|-------------------|----------|--------------------------------|
| SSH               | 22       | SSH/PuTTY connection           |
| All ICMP-IPv4     | -        | Ping and error messages        |
| All ICMP-IPv6     | -        | IPv6 Ping                      |
| HTTP              | 80       | Unsecured web                  |
| HTTPS             | 443      | Secured web                    |
| MySQL/Aurora      | 3306     | MySQL Database                 |
| Custom TCP        | 5000     | Node.js application            |

  * **Create Security Group for Windows Instance**
    * **Create Security Group for Windows Instance**
      * Create a dedicated Security Group for the Windows instance.

    * **Steps**
      * **Create security group**:
       * **Name**: `Windows-SG`
       * **Description**: `Security group for Windows instance`
       * **VPC**: Select `Windows-vpc`

      * Configure **Inbound rules** (add 8 rules):

| Type              | Port     | Description                    |
|-------------------|----------|--------------------------------|
| SSH               | 22       | SSH connection                 |
| HTTP              | 80       | Web                            |
| HTTPS             | 443      | Secured web                    |
| RDP               | 3389     | Remote Desktop (Windows)       |
| All ICMP-IPv4     | -        | Ping                           |
| All ICMP-IPv6     | -        | IPv6 Ping                      |
| Custom TCP        | 5000     | Node.js app                    |
| MySQL/Aurora      | 3306     | Database                       |

* **Launch Windows Instance**
  * **Overview**
    * **Launch Microsoft Windows Server 2025 Instance**
      * Amazon EC2 provides Microsoft Windows Server 2025 as an operating system option for enterprise workloads on the AWS Cloud. Windows Server 2025 brings enhanced security features, efficient management capabilities, and optimal performance for your Windows applications.

  * **Create Windows Instance**
    * **Launch Microsoft Windows Server 2025 Instance**
      * In this section, you will learn how to launch a Microsoft Windows Server 2025 instance on Amazon EC2. EC2 currently supports Windows Server 2025 Base AMI with License Included, making it easy to deploy the latest version of Windows Server in the AWS cloud environment.

    * **Steps**
      * Access the **AWS Management Console** → Search for and select **EC2** → Choose **Instances** → Click **Launch instances**
      * **Name**: Enter `Windows-instance`.
      * Select **AMI**:
        * Choose **Quick Start** → **Windows**
        * Select **Microsoft Windows Server 2025 Base**

      * Choose **Instance type** → Click **Create new key pair**

      * In the **Create key pair** interface:
        * **Key pair name**: Enter `kp-windows`
        * **Private key file format**: Select `.pem`
        * Click **Create key pair** (the key pair file will be downloaded to your computer)

      * In the **Network settings** section → Click **Edit**:
        * **VPC**: Select `Windows-vpc`
        * **Subnet**: Select **public subnet**
        * **Auto-assign public IP**: Select **Enable**
        * **Firewall (security groups)**: Select **Select existing security group**
        * **Common security groups**: Select `Windows-SG`

      * Review the information → Click **Launch instance**
      * After launch is successful, select **View all instances** to see details of the newly created instance
      * Wait approximately 5 minutes until **Status check** shows **3/3 checks passed** and the instance state is **Running**

  * **Connect to Windows Instance**
    * **Connect to Microsoft Windows Server 2025 Instance**
      * Connecting to a Windows instance on AWS EC2 is done via Remote Desktop Protocol (RDP) on port 3389. AWS provides a secure mechanism to retrieve the administrator password using the previously created key pair.

    * **Steps**
      * In the **EC2** interface → Select **Instances** → Select the `Windows-instance` → Click **Connect**

      * Choose **RDP Client**:
        * Click **Download remote desktop file**
        * Click **Get password**

      * In the **Get Windows password** interface:
        * Click **Browse** → Select the `kp-windows.pem` file
        * Click **Decrypt password**

      * Copy the decrypted **password**

      * Open the downloaded **Remote Desktop** file:
        * Click **Connect**
        * Enter the copied password → Click **OK**
        * Click **Yes** when prompted about the security certificate

      * Successfully connected to the **Microsoft Windows Server 2025** instance

    * **Prepare Sysprep for Custom AMI**
      * Sysprep (System Preparation) is a Microsoft tool that prepares the Windows system for imaging. When using Sysprep, system-specific information such as the SID is removed, allowing multiple instances to be created from one AMI without conflicts.

    * **Steps**
      * After RDP into the Windows instance, search for and open **EC2LaunchSettings**
      * In **Administrator Password setting**, select **Random**
      * At the bottom of the page, select **Shutdown with Sysprep** → Confirm **Yes**
      * Result: The instance will automatically shut down after running Sysprep. The instance will be in **Stopped** state

* **Launch Linux Instance**
  * **Overview**
    * **Launch Amazon Linux 2023 Instance**
      * Amazon Linux 2023 is a Linux operating system developed by AWS, specifically optimized for cloud computing environments. It delivers high performance, security, and stability for your applications on AWS.

  * **Create Linux Instance**
    * **Create Amazon Linux 2023 Instance**
      * The Amazon Linux 2023 AMI is regularly updated by AWS with security patches and performance improvements.

    * **Steps**
      * Access the **AWS Management Console** → Search for and select **EC2** → Choose **Instances** → Click **Launch instances**

      * **Name**: Enter `Linux-instance`

      * Select **AMI**:
        * Choose **Quick Start** → **Amazon Linux**
        * Select **Amazon Linux 2023 AMI**

      * Choose **Instance type** → Click **Create new key pair**

      * In the **Create key pair** interface:
        * **Key pair name**: Enter `kp-linux`
        * **Key pair type**: Select **RSA**
        * **Private key file format**: Select **.pem**
        * Click **Create key pair** (the file will be automatically downloaded)

      * In the **Network settings** section → Click **Edit**:
        * **VPC**: Select `Linux-vpc`
        * **Subnet**: Select **public subnet**
        * **Auto-assign public IP**: Select **Enable**
        * **Firewall (security groups)**: Select **Select existing security group**
        * **Common security groups**: Select `Linux-SG`

      * Review the information → Click **Launch instance**

      * After launch is successful, select **View all instances** to see the instance details

      * Wait approximately 5 minutes until **Status check** shows **3/3 checks passed** and the instance state is **Running**

  * **Connect to Linux Instance**
    * **Connect to Amazon Linux 2023 Instance**
      * There are multiple ways to connect to an EC2 Linux instance. In this lab, we will learn two popular methods: using **MobaXterm** and **PuTTY**.

    * **Connect using MobaXterm**
      * Download [MobaXterm](https://mobaxterm.mobatek.net/download.html)

      * Open **MobaXterm** → Select **Session**

      * In the **Session settings** interface:
        * Select **SSH**
        * **Remote host**: Enter the **Public IPv4** of the instance
        * **Specify username**: Enter `ec2-user`
        * **Use private key**: Select the `kp-linux.pem` file

      * Click **OK** to connect
        * On first connection, an alert will appear → Click **Accept**
        * Connection successful

    * **Connect using PuTTY**
      * PuTTY does not support `.pem` files directly, so you need to convert it to `.ppk` format.

    * **Steps**
      * Open **PuTTYgen** → Click **Load** → Select the `kp-linux.pem` file

      * After successful import → Click **Save private key** → Name it `kp-linux.ppk`

      * Open **PuTTY**:
         * In the left menu: **Connection** → **SSH** → **Auth** → **Credentials**
         * Click **Browse** → Select the `kp-linux.ppk` file

      * Go back to **Session**:
        * **Host Name**: Paste the **Public IPv4** or `ec2-user@Public_IP`
        * **Saved Sessions**: Enter `Linux-Server` → Click **Save**
        * Click **Open**

      * When the security warning appears → Click **Accept**

      * When prompted for login → Enter username: `ec2-user`

      * Connection successful

    * **Verify Connection**
      * After connecting successfully, run the command:
      ```bash
      ping 8.8.8.8
      ```

* **Basic Amazon EC2 Operations** 
  * **Overview**
    * This hands-on lab provides an overview of working with Amazon EC2 objects and related components. We will focus on basic tasks such as changing configuration, creating snapshots, building custom AMIs, and accessing instances when the key pair is lost.

  * **Modify EC2 Configuration**
    * **Change Instance Type (Resize Instance)**
      * You can change the instance type to better suit your CPU, RAM, network... requirements without creating a new instance.

    * **Steps**
      * Go to **EC2** → Select the instance you want to change
      * Choose **Instance state** → **Stop instance**
      * Wait until the instance status changes to **Stopped**
      * Select **Actions** → **Instance settings** → **Change instance type**
      * Select the new **Instance type** (e.g., from t2.micro to t3.small)
      * Click **Apply**
      * Choose **Instance state** → **Start instance**

  * **Create and Manage EBS Snapshots**
    * **Create EC2 Snapshot**
      * An Amazon EBS Snapshot is a point-in-time copy of your volume data, stored incrementally on Amazon S3.

    * **Steps**
      * Go to **EC2** → Select **Snapshots** → **Create snapshot**
      * **Resource type**: Select **Instance**.
      * Select the instance (`Windows-instance` or `Linux-instance`)
      * **Copy tags from source volume**: Select **Copy tags**
      * Click **Create snapshot**
      * Wait until the Snapshot status changes to **Completed**

  * **Create Custom AMI**
    * **Create Custom AMI from Windows Instance**
      * An Amazon Machine Image (AMI) is a template that contains the operating system, applications, and configurations. Creating a Custom AMI allows you to quickly reuse instance configurations.

    * **Steps**
      * Go to **EC2** → Select `Windows-instance` → **Instance state** → **Stop instance**
      * Wait until the instance is in **Stopped** state
      * Select **Actions** → **Image and templates** → **Create image**
      * **Image name**: `Custom Windows AMI`
      * **Image description**: `Custom Windows AMI`
      * Uncheck **Reboot instance**
      * Click **Create image**
      * Go to **AMIs** to monitor the progress (approximately 5 minutes)

  * **Launch Instance from Custom AMI**
    * **Launch Instance from Custom AMI**
      * Use the created Custom AMI to launch a new instance with all existing configurations.

    * **Steps**
      * Go to **EC2** → **AMIs** → Select `Custom Windows AMI`
      * Choose **Launch instance from AMI**
      * **Name**: `Windows Server AMI`
      * Select **Instance type**
      * Create a **new key pair** (`kp-windows2`)
      * **Network settings**:
        * VPC: `Windows-vpc`
        * Subnet: public subnet
        * Auto-assign public IP: Enable
        * Security Group: `Windows-SG`
      * Click **Launch instance**
      * Wait until Status check reaches **3/3 checks passed**

  * **Access Windows EC2 When Key Pair is Lost using SSM**
    * **Access EC2 Windows Instance When Key Pair is Lost**
      * The Key Pair is used to encrypt and decrypt login credentials to the EC2 virtual server. When the Key Pair is lost, AWS Systems Manager (SSM) provides a secure solution to regain access to the EC2 instance without recreating it.

    * **Prerequisites**
      * The EC2 instance needs internet connectivity (public IP or NAT Gateway) or VPC Endpoint for SSM.
      * SSM Agent must be installed and running on the instance.
      * The EC2 instance must have an IAM role with SSM permissions.

    * **Create and Attach IAM Role for EC2**
      * Go to **IAM** → **Roles** → **Create role**
      * Select **AWS service** → **EC2**
      * Search and attach **AmazonSSMFullAccess** → Next
      * Set **Role name**: `Windows-instance` → **Create role**
      * Go back to **EC2** → Select the `Windows-instance` → **Actions** → **Security** → **Modify IAM role**
      * Select the role `Windows-instance` → **Update IAM role**

    * **Install AWSPowerShell Module (via Session Manager)**
      * Go to **EC2** → Select the instance → **Connect** → Select the **Session Manager** tab → **Connect**.
      * Run the command to install the module:
         ```powershell
         Install-Module -Name AWSPowerShell -Force -AllowClobber -SkipPublisherCheck
          ```
    
    * **Use AWS Systems Manager to Reset Password**
      * Go to Systems Manager → Run Command → Run a command
      * Search for and select **AWSSupport-RunEC2RescueForWindowsTool**
      * Select the `Windows-instance`
      * Uncheck **Enable an S3 bucket** → Click **Run**
      * Wait until the status changes to **Success**

    * **Retrieve New Password from Parameter Store**
      * Go to Systems Manager → Parameter Store
      * Find the parameter with the format `/EC2Rescue/Passwords/[instance-id]`
      * Select **Show decrypted value** to view the new password
      * Copy the password

    * **Connect via RDP**
      * Go to EC2 → Select the instance → Connect → RDP client
      * Download the RDP file → Open the file → Paste the new password → Connect

  * **Access EC2 Linux When Key Pair is Lost using User Data**
    * **Access EC2 Linux Instance When Key Pair is Lost using User Data**
      * When the key pair is lost, we create a new key pair and replace the public key by editing the EC2 User Data.

    * **Steps**
      * Create a new Key Pair:
        * Go to EC2 → Key Pairs → Create key pair
        * Name: `new-key`, Type: RSA, Format: `.pem` → Create
      * Convert to `.ppk` using PuTTYgen:
        * Load the `new-key.pem` file → Copy the entire **Public key** (starts with `ssh-rsa`).
        * Save the private key as `new-key.ppk`.
      * Stop the instance:
        * Select `Linux-instance` → Instance state → Stop instance.
      * Edit User Data:
        * Select **Actions** → **Instance settings** → **Edit user data**.
        * Paste the following content (replace with your public key):

* **Deploy Node.js Application on Amazon Linux**
  * **Overview**
    * In this lab, we will deploy the **AWS User Management** application - a web application built with **Node.js, Express, Express-Handlebars**, and **MySQL**. The application supports CRUD (Create, Read, Update, Delete) functions and user search.

  * **Deployment Architecture**
    * Install **LAMP stack** (Linux + Apache + MariaDB + PHP)
    * Configure **phpMyAdmin** for database management
    * Install **Node.js** Runtime
    * Deploy and run the **AWS User Management** application

  * **Install LAMP Web Server**
    * **Install LAMP Web Server on Amazon Linux 2023**
      * LAMP is a popular stack consisting of **Linux, Apache, MySQL/MariaDB, and PHP**. We will install it on Amazon Linux 2023 to serve as the foundation for the web application.

    * **Main Steps (Summary of sub-sections)**
      * **Prepare LAMP Server**: Update the system and install Apache, MariaDB, and PHP packages
      * **Verify LAMP Server**: Check that Apache and PHP are working via a web browser
      * **Configure Database Server**: Start MariaDB and run `mysql_secure_installation` for security
      * **Install phpMyAdmin**: Install the web-based database management tool

  * **Install Node.js on Linux**
    * **Install Node.js on Amazon Linux 2023**
      * Node.js is a server-side JavaScript runtime environment that allows you to build scalable web applications.

    * **Steps**
      * Install **Node Version Manager (nvm)**:
         ```bash
         curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.0/install.sh | 
         ```
      * Activate nvm: Bash. ~/.nvm/nvm.sh
      * Install Node.js LTS version: Bash nvm install --lts
      * Check the installation:
        Bash node -v
        npm -v
  
  * **Deploying Application on Linux Instance**
    * **Deploying AWS User Management Application** 
      * **Implementation Steps**
        * Install Git:
          ```bash
          sudo dnf install git
          git version ```
        * Clone source code:
          ```bash
          cd ~
          git clone https://github.com/First-Cloud-Journey/000004-EC2.git
          cd 000004-EC2```
        * Initialize project and install dependencies:
          ```bash
          npm init
          npm install express dotenv express-handlebars body-parser mysql```
        * Install Nodemon (dev dependency):
          ```bash
          npm install nodemon@latest --save-dev```
        * Create .env file and configure database:
          ```text
          DB_HOST=localhost
          DB_NAME=awsuser
          DB_USER=root
          DB_PASS=123Admin   # (password set in the MariaDB security section)```
        * Start the application:
          ```bash
          npm start```
        * Access the application:
          * Open browser → Paste the instance's Public IPv4 DNS + :5000
          * Example: http://ec2-xxx-xxx-xxx-xxx.ap-southeast-1.compute.amazonaws.com:5000
        * Add sample data via phpMyAdmin (run SQL INSERT to have demo data).
          * Application Features:
            * View user list
            * Add / Edit / Delete users
            * Search users

  * **Node.js Application on Amazon EC2 Windows**
    * **Overview**
      * In this section, we will deploy the **AWS User Management** application on Amazon EC2 running **Microsoft Windows Server 2025**
      * The application is built using **Node.js, Express, Express-Handlebars, and MySQL**. 

    * **Main Steps**
      * Install **XAMPP** (Apache + MariaDB + PHP) to use MySQL and phpMyAdmin
      * Install **Node.js** and Git
      * Clone source code and deploy the application

  * **Installing XAMPP on Windows Instance**
    * **Installing XAMPP on Microsoft Windows Server 2025**
      * XAMPP is a software package that includes **Apache, MariaDB (MySQL), PHP, and Perl**, making it easy to set up a web development environment on Windows

    * **Implementation Steps**
      * Connect via RDP to the **Windows instance**.
      * Download XAMPP from: [https://www.apachefriends.org/download.html](https://www.apachefriends.org/download.html)
      * Run the installer and follow the instructions (accept default options).
      * After installation, open **XAMPP Control Panel**:
        * Start **Apache** (port 80)
        * Start **MySQL** (port 3306)
      * Access phpMyAdmin: `http://localhost/phpmyadmin`
      * Create database:
        * Select **New** → Set database name: `awsuser` → **Create**
      * Create `user` table using SQL Query:

  * **Installing Node.js on Windows Instance**
    * **Installing Node.js on Microsoft Windows Server 2025**
      * Install Node.js Runtime, Git, and Visual Studio Code for development and running the application

    * **Implementation Steps**
      * Download and install Git from: https://gitforwindows.org/
      * Check Git:
      bash
      git version
      * Download and install Visual Studio Code
      * Download and install Node.js (Windows Installer) from the official website.
      * Check Node.js:
      bash
      node -v
      npm -v
      * Create directory and clone source code:
      bash
      mkdir AWSManagement
      cd AWSManagement
      git init
      git clone https://github.com/First-Cloud-Journey/000004-EC2.git
      cd 000004-EC2

    * **Deploying the Application on Windows Instance**
    * **Deploying AWS User Management Application**
      * Install dependencies, configure database and run the Node.js application

    * **Implementation Steps**
      * Initialize project:
      bash
      npm init
      * Install dependencies:
      bash 
      npm install express dotenv express-handlebars body-parser mysql
      * (Optional) Install Nodemon:
      bash
      npm install nodemon@latest --save-dev
      * Open the folder with Visual Studio Code and create .env file:
      text
      DB_HOST=localhost
      DB_NAME=awsuser
      DB_USER=root
      DB_PASS=
      * Start the application:
      bash
      npm start
      * Access the application:
        * Open browser → `http://localhost:5000` or use the instance's Public IP: `http://<Public-IP>:5000`
      * Add user data via phpMyAdmin or through the application interface.
      * Application Features: CRUD (Create, Read, Update, Delete) and user search

    * **Resource Limitation using IAM :: INTRODUCTION TO AMAZON EC2**
      * **Overview**
        * AWS Identity and Access Management (IAM) allows you to control who can access AWS resources and what actions they can perform. This section focuses on using **IAM Policy** to restrict permissions, helping with **Cost Optimization** and enhancing security according to the **least-privilege permissions** principle.

      * **Objectives**: Use IAM Policy to restrict:
        * Region
        * Instance Family
        * Instance Type
        * Type of EBS Volume
        * Source IP
        * Time of performing actions

      * **Allow Service Usage by Specific Region**
        * **Allow EC2 Usage Only in Singapore Region (ap-southeast-1)**
          * **Implementation Steps**
            * **Create Policy** (JSON):
          * Policy name: RegionRestrict
        * Create Group **CostTest** and attach the **RegionRestrict** policy
        * Create IAM User **TestUser**, add to the **CostTest** group
        * Test:
          * In Singapore Region → Launch EC2 → Success
          * In Tokyo Region → Launch EC2 → Failed
          * Try using S3 in Singapore → Failed (because the policy only allows EC2)

    * **Restrict EC2 Usage by Instance Family**
      * **Restrict Instance Family: T3, T4g, M5**
        * **Implementation Steps**
          * Create Policy (JSON):
          * Policy name: EC2_FamilyRestrict
        * Attach policy to the **CostTest** group
        * Test:
          * Create instance **t4g.micro** → Success
          * Create instance **m6i.large** → Failed

  * **Restrict EC2 Usage by Instance Type**
    * **Restrict Instance Type: t3.small and t3.large**
      * **Implementation Steps**
        * Create Policy (JSON):
        * Policy name: EC2_InstanceTypeRestrict
        * Attach policy to the **CostTest** group (remove the previous policy to comply with least-privilege).
        * Test:
          * Create **t3.small** → Success
          * Create **m5.4xlarge** → Failed

  * **Restrict EBS Volume Storage Type**
    * Objective: Only allow the use of certain EBS Volume types (e.g., gp3, gp2) to control storage costs

  * **Restrict Resource Deletion by Company IP Address**
    * Objective: Only allow resource deletion from the company’s IP (office IP), preventing deletion from outside

  * **Restrict Resource Deletion by Time Window**
    * Objective: Only allow deletion actions during business hours (e.g., 08:00 - 18:00, Monday to Friday)

* **Resource Cleanup**
  * **Important Steps**
    * **Terminate** all EC2 Instances
    * **Deregister** AMIs
    * **Delete** Snapshots
    * **Delete** Security Groups
    * **Delete** Key Pairs
    * **Delete** VPC
    * **Delete** IAM policies, roles, users (if any)

## Tuesday: Setting up VPC Peering
  * **Overview**
    * By default, VPCs inside the AWS Cloud are isolated and cannot communicate directly with each other. In this hands-on lab, you will establish a **VPC Peering** connection between two VPCs so that resources inside these two VPCs can communicate directly with each other. This eliminates the need to route traffic through the public Internet, thereby enhancing the security of the VPCs

  * **Convention:**  
    * **Default VPC = VPC 1 (My VPC)** – CIDR: `172.31.0.0/16`  
    * **HG VPC = VPC 2** – CIDR: `10.10.0.0/16`

  * **Key Concepts**
    * **VPC Peering Connection**
      * A VPC Peering connection is a networking connection between two VPCs that allows you to route traffic between them using private IPv4 or IPv6 addresses. Instances in one VPC can communicate with instances in the other VPC as if they were on the same network

  * **Network Access Control List (Network ACL)**
    * Network ACL is a **stateless firewall** at the subnet level. Unlike Security Groups (stateful, resource-level), Network ACLs can only be associated with subnets

  * **Best practice:** Combine SG + NACL to create defense-in-depth.

  * **Cross-Peering DNS**
    * A feature that allows resources in one VPC to resolve the private DNS of resources in the other VPC through the peering connection

  * **Introduction**
    * **Overview:** By default, VPCs are isolated. This lab sets up VPC Peering to enable private communication

  * **Benefits of VPC Peering:**
    * Direct connection (no need for gateway or VPN)
    * Traffic travels through the AWS backbone (high security, low latency)
    * Supports cross-region and cross-account peering
    * Low cost

  * **Main Features:**
    * Direct connectivity
    * Security (each VPC manages its own SG/NACL)
    * High performance
    * Scalability

  * **Preparation Steps**
    * Use **CloudFormation** to quickly provision the infrastructure.

  * **Launch CloudFormation Template**
    * **Detailed Instructions:**
      * Download the template `VPCTemplate.yaml` from:
        * AWS Documentation or
        * GitHub AWS-First-Cloud-Journey
      * Go to **CloudFormation** → **Create stack**

  * **Stack 1: My-VPC-Stack**
    * Stack name: `My-VPC-Stack`
    * EnvironmentName: `My VPC`
    * VpcCIDR: `172.31.0.0/16`
    * PublicSubnet1CIDR: `172.31.1.0/24`
    * PublicSubnet2CIDR: `172.31.2.0/24`
    * PrivateSubnet1CIDR: `172.31.3.0/24`
    * PrivateSubnet2CIDR: `172.31.4.0/24`

  * **Stack 2: HG-VPC-Stack**
    * Stack name: `HG-VPC-Stack`
    * EnvironmentName: `HG VPC`
    * VpcCIDR: `10.10.0.0/16`
    * PublicSubnet1CIDR: `10.10.1.0/24`
    * PublicSubnet2CIDR: `10.10.2.0/24`
    * PrivateSubnet1CIDR: `10.10.3.0/24`
    * PrivateSubnet2CIDR: `10.10.4.0/24`

  * Wait for the stacks to be created successfully (approximately 5-10 minutes)

  * **Create Security Groups**
    * **My VPC SG (assigned to My VPC):**
      * Name: `My VPC SG`
      * Inbound rules:
        * SSH (port 22) → My IP
        * All ICMP - IPv4 → Anywhere
        * All ICMP - IPv4 → `10.10.0.0/16` (HG VPC)

    * **HG VPC SG (assigned to HG VPC):**
      * Name: `HG VPC SG`
      * Inbound rules:
        * SSH (port 22) → My IP
        * All ICMP - IPv4 → Anywhere
        * All ICMP - IPv4 → `172.31.0.0/16` (My VPC)

  * **Create EC2 Instances**
    * Create 2 instances in **Public Subnets**:
    * **EC2 - My VPC:**
      * Name: `EC2 - My VPC`
      * AMI: Amazon Linux 2
      * Type: t2.micro
      * Key pair: `vpcpeering-key` (create new)
      * Network: My VPC → Public Subnet 2
      * Auto-assign Public IP: Enable
      * Security Group: `My VPC SG`

    * **EC2 - HG VPC:**
      * Name: `EC2 - HG VPC`
      * Similar settings, use key pair `vpcpeering-key`
      * Network: HG VPC → Public Subnet 2
      * Security Group: `HG VPC SG`

    * **Initial Testing:**
      * Ping the Public IP of the other EC2 → Successful (via Internet)
      * Ping the Private IP of the other EC2 → Failed (VPCs not yet connected)

  * **Update Network ACL**
    * Go to **VPC** → **Network ACLs**
    * Select the NACL of **HG VPC**
    * **Inbound Rules** tab → **Edit inbound rules**
    * Rule 100: Change Source from `0.0.0.0/0` → `172.31.0.0/16`
    * Save changes

    * **Result:** Ping from the Internet to HG VPC will fail. Only traffic from My VPC is allowed

  * **Create Peering Connection**
    * Go to **VPC** → **Peering Connections** → **Create Peering Connection**
      * Name: `lab-vpc-peer`
      * VPC (Requester): My VPC
      * Account: My account
      * Region: This region (ap-southeast-1)
      * VPC (Accepter): HG VPC

    * Accept the request from either the requester or accepter side.
    * **At this point, pinging Private IP still fails** (Route Tables not yet configured)

  * **Enable Cross-Peer DNS**
    * Go to **Peering Connections**
    * Select the peering connection → **Actions** → **Edit DNS settings**
    * Check both options:
      * Requester DNS resolution
      * Accepter DNS resolution
    * Save

    * **Result:** From the EC2 in My VPC, pinging the **Public DNS** of the EC2 in HG VPC will resolve to the Private IP and traffic will go through the peering connection (no longer through the Internet)

  * **Resource Cleanup**
    * **Recommended Order:**
      * **Terminate EC2 instances** (EC2 Console)
      * **Delete VPC Peering Connection** (VPC Console)
      * **Delete Security Groups**
      * **Delete CloudFormation Stacks** (My-VPC-Stack and HG-VPC-Stack) – this will automatically delete VPCs, Subnets, IGWs, Route Tables, etc

## Wednesday: Overview of AWS Transit Gateway
* **Introduction**
  * **Overview & Lab Architecture**
    * This lab guides you through deploying an architecture that connects four VPCs using a single AWS Transit Gateway (TGW) acting as a central cloud router.
    * Comparison with VPC Peering: The guide notes that using the traditional VPC Peering method to connect 4 VPCs would require 6 peering connections. As the number of VPCs increases (6, 8, 10 VPCs), the peering model becomes extremely complex and difficult to manage.
    * Benefits of AWS Transit Gateway: Simplifies network architecture by connecting VPCs and on-premises networks through a central hub.
      * Reduces complex routing relationships.
      * Each new connection only needs to be configured once.

  * **Important Concepts Covered**
    * AWS Transit Gateway Attachment: A resource used to attach subnets from a VPC to the Transit Gateway.
      * Operates at the Availability Zone (AZ) level.
      * Once a subnet in an AZ is attached, other subnets in the same AZ can also connect to the TGW, providing flexible connectivity management.

  * **Cost Warning**
    * This lab will incur costs on your AWS account, including:
      * Costs for configured instances (using t3.nano type)
      * Costs directly related to maintaining the Transit Gateway

  * **Create Key Pair**
    * Create a Key Pair
      * Log in to the AWS Management Console
      * Search for EC2
      * Select EC2

    * In the EC2 interface
      * Select Key Pairs
      * Choose Create key pair

    * In the Create key pair interface
      * Name: enter `tgw-key`
      * Key pair type: select RSA
      * Private key file format: select `.pem`
      * Choose Create key pair

    * Key pair created successfully

  * **Launch CloudFormation Template**
    * Access the CloudFormation Management Console by typing CloudFormation in the search bar
    * In the CloudFormation interface
      * Select Create stack
    * Choose Upload a template file, select `tgw-lab.yaml` from the source you downloaded, then select Next
    * On the Specify stack details page, enter a stack name (e.g., Lab20-Stack), select your SSH Key, then choose Next
    * On the Configure stack options page, keep the defaults and select Next
    * On the Review page, check the information and select Submit
    * Stack creation successful
    * View the Output of the created stack
    * Return to the AWS Management Console
       * Search for EC2
       * Select EC2
    * In the EC2 interface
      * Select Instances
      * Select the First EC2 host
    * Go to the folder containing your SSH Key pair and run the following command in the command prompt to copy the Key Pair to the First EC2 Host for the next step
    * Go to the folder containing your SSH Key pair and run the following command to copy the Key Pair to the Third EC2 Host for the next step

  * **Create Transit Gateway**
    * Access the VPC Management Console
      * Open the AWS Management Console
      * Search for and select VPC
    * Create Transit Gateway
      * Select Transit Gateway from the left menu
      * Click Create Transit Gateway
    * Basic Configuration
      * Name tag: `lab20-tgw`
      * Description: Transit Gateway for lab20
    * Advanced Configuration
      * Uncheck Default route table association
      * Uncheck Default route table propagation
    * Review and Create
      * Review the information
      * Click Create Transit Gateway

  * **Create Transit Gateway Attachments**
    * Access the VPC Management Console
      * Open the VPC Management Console
      * Select Transit Gateway Attachments
      * Click Create Transit Gateway Attachment
    * Basic Configuration
      * Transit Gateway ID: Select the ID of the Transit Gateway you created
      * Attachment type: Select VPC
    * Detailed Configuration
      * Attachment name tag: Enter the VPC name (e.g., VPC1)
      * VPC ID: Select the First VPC (VPC1)
      * Subnet ID: Select the subnet in the corresponding AZ
      * Click Create transit gateway attachment
    * Confirm successful creation
      * Wait for the status to change to Available
    * Create Attachment for VPC2
      * Repeat the steps above for VPC2
      * Use an appropriate name (e.g., VPC2)
    * Create Attachment for VPC3
      * Repeat the process for VPC3
      * Use an appropriate name (e.g., VPC3)
    * Create Attachment for VPC4
      * Complete the process for VPC4
      * Use an appropriate name (e.g., VPC4)
    * SSH to EC2 in VPC1
      * Use command: `ping <IPv4 Public of EC2> -c5`
    * Test connectivity between VPCs
      * Try pinging the private IP addresses of other instances
      * Note: Connectivity will fail because routing has not been configured yet

  * **Create Transit Gateway Route Tables**
    * Access the VPC Management Console
      * Open the VPC Management Console
      * Select Transit Gateway Route Tables
      * Click Create Transit Gateway Route Table
    * Configure Route Table
      * Name tag: `lab20-TGW-RT`
      * Select the Transit Gateway you created
      * Click Create Transit Gateway Route Table
    * Confirm successful creation
      * Wait for the Route Table status to change to Available
    * Create Association
      * Select the newly created Route Table
      * Go to the Associations tab
      * Click Create association
    * Add VPCs to Association
      * Add each VPC one by one
      * Ensure all 4 VPCs are added
    * Confirm Association
      * Check the status of the Associations
      * Ensure all are in Associated state
    * Create Propagation
      * Go to the Propagations tab
      * Click Create propagation
    * Add VPCs to Propagation
      * Add each VPC one by one
      * Ensure all 4 VPCs are added
    * Confirm Propagation
      * Check the status of the Propagations
      * Ensure all are in Enabled state

  * **Add Transit Gateway Routes to VPC Route Tables**
    * Select Route Table
      * Open the VPC Management Console
      * Select Route Tables
      * Select the Route Table of VPC1
      * Click Edit routes
    * Add route
      * Destination: `172.16.0.0/16`
      * Target: Select the Transit Gateway you created
    * Confirm route
      * Check that the new route has been added
      * This route allows VPC1 to send traffic to the `172.16.x.x` network via Transit Gateway
    * Add similar route
      * Select the Route Table of VPC3
      * Add a route with Destination `172.16.0.0/16`
      * Target is Transit Gateway
    * Confirm route
      * Check that the new route has been added
      * This route allows VPC3 to send traffic to the `172.16.x.x` network via Transit Gateway
    * Add route for VPC2
      * Select the Route Table of VPC2
      * Add a route with Destination `0.0.0.0/0`
      * Target is Transit Gateway
    * Add route for VPC4
      * Select the Route Table of VPC4
      * Add a route with Destination `0.0.0.0/0`
      * Target is Transit Gateway
    * Test Internet connectivity
      * SSH to EC2 in VPC1
      * Try pinging `amazon.com` to verify internet connectivity
    * Test connectivity between VPCs
      * Ping the IP of EC2 in VPC2
      * SSH between instances
      * Test connectivity to VPC3 and VPC4

  * **Clean up Resources**
    * **Delete Transit Gateway Attachments**
      * Access the VPC Management Console
        * Open the VPC Management Console
        * Select Transit Gateway Attachments
      * Delete Attachments
        * Select all related Attachments
        * Click Actions > Delete
        * Confirm deletion in the prompt
      * Confirm deletion
        * Wait 1-2 minutes for the deletion to complete
        * Check the status of the Attachments

    * **Delete Transit Gateway**
      * Access Transit Gateway
        * Select Transit Gateways from the left menu
        * Select the Transit Gateway to delete
      * Delete Transit Gateway
        * Click Actions > Delete
        * Confirm deletion in the prompt

    * **Delete CloudFormation Stack**
      * Access CloudFormation
        * Open the CloudFormation Management Console
        * Select Stacks
      * Delete Stack
        * Select the stack related to the lab
        * Click Delete
        * Confirm deletion in the prompt

## Thursday: AWS Security Services
  * Shared Responsibility Model
  * AWS Identity and Access Management
  * Amazon Cognito
  * AWS Organizations & AWS Identity Center (SSO)
  * AWS KMS

  * **Shared Responsibility Model**
    * **Shared Responsibility Model:** When using cloud computing services from a provider, the security of the application and services is a shared responsibility between the customer and the cloud service provider.
    * The customer is responsible for configuring and applying services to ensure security from the Hypervisor level up to the data/application level.
    
    * **Security in the cloud:** 
      * Starts from the hypervisor level and the operating system level.
      * Some key considerations include data encryption needs, implementing data encryption, and managing file storage locations within storage services.
      * Network traffic management services such as building firewalls also require configuration at the operating system, network, and firewall levels.
      * Above the operating system level are platforms and applications for access control and identity management.
      * If installing a Windows operating system, managing security inside the OS is the customer's responsibility. The cloud provider cannot see inside; they only provide the underlying infrastructure.
      * If they cannot see inside the operating system, they certainly cannot see inside the applications.
      * Access control and identity management are also the customer's responsibility. We manage the users who log into the operating system, the users who log into the cloud platform, and the data itself. This is the customer's responsibility.
      * This does not mean doing everything from scratch. AWS provides a set of ready-made services to meet the different security needs of various organizations. AWS cannot impose one single security standard on all organizations.
      * AWS builds the platform, services, best practices, and guidelines first, then allows customers to configure them according to their specific needs.
      * Organizations configure security to the level their needs require. AWS provides both the services and the documentation to make this possible.
      * AWS is responsible from the hypervisor downward. This includes the physical global infrastructure, data centers, network layers, Regions, Availability Zones, and Edge Locations.
      * Above that are the foundational infrastructure services such as compute, storage, databases, and networking — these are primarily AWS's security responsibilities.

      * Security responsibilities vary depending on the type of service:
        * Infrastructure-level services
        * Managed services (shared management)
        * Fully managed services by AWS
        
      * However, the Shared Responsibility Model is not fixed. It differs between services.
      * Amazon EC2 (virtual server) is an infrastructure-level service. With infrastructure services, customers have many management responsibilities: data encryption, network traffic control, OS patching, firewall configuration, application installation and management, data management, permissions, etc.
      * Services with shared management: AWS takes on more responsibilities. For example, with managed database services like Amazon RDS (MySQL), AWS manages the database platform. Customers only connect to the database server and use MySQL management tools. Customers do not manage the operating system. AWS handles part of the OS management and part of the database/platform management.
      * The more AWS manages, the less effort the customer needs to spend on infrastructure, allowing them to focus on higher-value tasks such as building optimized applications and designing high-performance queries.
      * Fully managed services: When AWS manages everything, customer responsibility is minimal. For example, with Amazon S3, customers only need to focus on where to store data, cost optimization, whether to enable encryption, versioning, etc.
      * Security on the cloud platform is a shared responsibility between AWS and the customer. Responsibilities differ based on whether the service is infrastructure-level, shared management, or fully managed by AWS. The trend is that customers increasingly prefer fully managed services to reduce infrastructure management effort and focus on application development.

  * **AWS Identity and Access Management**
    * **AWS Identity and Access Management - Root Account**
      * This account has full access to all AWS services and resources and can remove any permission policies attached to resources.
        * Billing information
        * Personal data (when registering the account)
        * No permission restrictions
        
      * Best Practices:
        * Create and use an IAM Administrator User
        * Lock away the root user's credentials (split between two people)
        * Ensure the root user's domain and email are renewed/controlled

      * The root account is the initial account used to register with AWS, including business email, phone number, name, password, etc. It has full access to all AWS services and resources.
      * Root cannot have its permissions restricted because it has the special privilege of being able to remove any permission policies attached to resources.
      * Example: Even if you attach a policy to a server denying root access, the root user can remove that policy. It also has full access to personal registration data and is essentially an unrestricted entity.
      * Best practice: Do not use the root account for daily operations. Instead, create IAM users, assign permissions/policies to create an admin user, and use that admin user.
      * Root user credentials should be secured with MFA (virtual or hardware), split between two high-level people in the organization, or even sealed. Some organizations use hardware security keys for easier splitting.
      * Use a business email for root account registration and ensure the domain is owned by the organization.

      * IAM is a service that allows you to control access to AWS services and resources within your AWS account. IAM enables you to create multiple user accounts (IAM users) with different credentials and permission levels.
      * **IAM Principal** is an entity that can perform actions on specific resources in your AWS account.
        * AWS account and root user
        * IAM users
        * Federated users (using web identity or SAML federation)
        * IAM roles
        * Assumed-role sessions
        * AWS services
        * Anonymous users (not recommended)

      * An IAM User is not a separate AWS account. IAM Users have their own passwords for accessing the Management Console or access key/secret key for programmatic access (AWS CLI and AWS SDK).
        * Newly created IAM Users have no permissions by default.
        * IAM Users are not used to manage access to applications or operating systems.
        * To grant permissions to an IAM User, attach IAM Policies to it.
        * For easier management, you can group multiple IAM Users into an IAM Group.
        * IAM Groups cannot be members of other IAM Groups.

    * **AWS Identity and Access Management - IAM Policy**
      * Written in JSON format.
      * IAM Policies have 2 types:
        * Identity-based Policies — attached to an IAM Principal
        * Resource-based Policies — attached to an AWS Resource

      * IAM permission evaluation always gives **Deny** higher priority than **Allow**. If there is an explicit Deny in any policy, access is denied even if another policy allows it.

      * Example: An IAM Policy that restricts S3 management by:
        * Allowing all S3 actions on a specific bucket
        * Explicitly denying access to all AWS services except Amazon S3

    * **AWS Identity and Access Management - IAM Role**
      * An IAM Role defines a set of permissions for accessing resources (by attaching IAM Policies). IAM Roles do not have credentials for accessing the Management Console or AWS CLI/SDK.
      * When an IAM User wants to use an IAM Role, they must **assume** the role. Once assumed, the user's current permissions are replaced by the permissions of the IAM Role. Temporary security credentials are then issued.
      * The Assume Role operation works with AWS STS (Security Token Service) to generate temporary credentials (similar to access keys).
      * For a user to assume a role, the IAM Role has a trust policy (resource-based policy) that defines who can assume it.
      * IAM Roles are commonly used to follow the principle of least privilege and to grant access to resources across different AWS accounts.
      * IAM Roles are also used to grant permissions to AWS Services themselves.
      * The most common use case is assigning IAM Roles to applications running on compute services (e.g., EC2 instances).

    * **Amazon Cognito**
      * Amazon Cognito is a fully managed AWS service that provides authentication, authorization, and user management for web and mobile applications. Users can sign in directly with username and password or through third parties such as Facebook, Amazon, or Google.
      * Two main components of Amazon Cognito are **User Pools** and **Identity Pools**:
        * **User Pool**: A user directory that provides sign-up and sign-in options for application users.
        * **Identity Pool**: Grants users access to other AWS services.

      * After signing in with a User Pool, application users can access resources permitted by the application.
      * After signing in with a User Pool, application users can call API Endpoints (backend) permitted by the application.
      * User Pools can be combined with Identity Pools to access AWS services directly.

  * **AWS Organizations**
    * AWS Organizations helps centrally manage and govern multiple AWS accounts.
    * You can create new AWS accounts, organize them into Organizational Units (OUs), allocate resources, and simplify billing with consolidated billing.
    * AWS Organizations allows you to apply **Service Control Policies (SCPs)** to OUs or individual accounts. SCPs set the maximum permission boundaries for IAM Users and IAM Roles within the targeted OU or account.
    * SCPs also support deny-based policies.

  * **AWS Identity Center (SSO)**
    * AWS Identity Center (formerly AWS SSO) helps manage access to AWS accounts and external applications.
      * Identity sources can be within AWS Identity Center or linked to Active Directory (AWS Managed Microsoft AD, on-premises Microsoft AD via two-way trust, or AD Connector).

    * **Permission Sets** define the level of access that Users and Groups have to AWS accounts within the AWS Organization. Permission sets are stored in AWS Identity Center and provisioned to AWS accounts as IAM roles. You can assign multiple permission sets to a single user.

  * **Amazon Key Management Service**
    * **AWS KMS**
      * AWS Key Management Service allows you to create and manage encryption keys for encrypting/decrypting data in AWS (**Encryption at rest**).
      * Encryption keys always remain within AWS KMS and comply with FIPS 140-2 standards.
      * **CMK (Customer Managed Key)** is the primary resource in AWS KMS. CMKs can be up to 4KB in size. However, CMKs are typically used to create, encrypt, and decrypt **Data Keys**, which are then used outside KMS to encrypt actual data.

    * **AWS Security Hub**
      * AWS Security Hub is a service that allows you to perform security checks based on standards and best practices.
      * Security Hub runs continuous checks on service configurations across your AWS accounts and evaluates security against AWS best practices and industry standards (e.g., PCI DSS).
      * Security Hub provides findings with security scores and helps identify specific accounts and resources that need attention.