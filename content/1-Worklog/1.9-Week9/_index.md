---
title: "Week 9 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.9. </b> "
---

### Week 9 Objectives:

* 

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
|  6  | - Hands-on Data Visualization with Amazon QuickSight | 12/06/2026 | 12/06/2026 | <https://000073.awsstudygroup.com/> |
|  2  | - Amazon DynamoDB: NoSQL Design, Advanced Patterns, and Serverless Solutions | 15/06/2026 | 15/06/2026 | <https://000039.awsstudygroup.com/> |
|  3  | - Building a Serverless Data Lake on AWS | 16/06/2026 | 16/06/2026 | <https://000070.awsstudygroup.com/> |
|  4  | - From Data Lake to Dashboard with AWS Glue, Athena and QuickSight | 17/06/2026 | 17/06/2026 | <https://000035.awsstudygroup.com/> |
|  5  | - nội dung thay thế | 18/06/2026 | 18/06/2026 | <https://cloudjourney.awsstudygroup.com/> |


### Week 9 Achievements:

## Friday: Hands-on Data Analysis and Dashboard Creation with AWS QuickSight
* Introduction to the **"Getting Started with QuickSight"** workshop. The main objective was to build a dashboard for visualizing sales data (sales.csv) using Amazon QuickSight. The workshop used the Singapore region (ap-southeast-1) and focused on data analysis and visualization through various charts and visuals.

* **Basic Concepts:**
  * **Data Source:** An external data source (e.g., S3, Athena, Salesforce).
  * **Dataset:** A specific collection of data from a data source, including all data preparation steps (renaming fields, changing data types, etc.).
  * **Analysis:** A workspace containing visuals and stories related to a specific business objective.
  * **Visual:** A chart or graphical representation of data (each visual uses a single dataset).
  * **Dashboard:** A published, view-only version of an analysis that preserves filters, parameters, and always reflects the latest data.

* **Preparation**
  * Instructions for creating a QuickSight Enterprise account (which can be deleted after the lab), uploading the sales.csv file (~1.5 MB), and completing the initial setup.

  * **Detailed Steps Included:**
    * Register through the AWS Console.
    * Select the Enterprise Edition.
    * Configure IAM federated identities, choose the Singapore region, and provide an account name and email address.
    * Close the welcome screen after accessing QuickSight.

* **Building the First Dashboard**
  * **Creating a Dataset and Basic Visuals:**
    * **Create Dataset:** Upload the sales.csv file from a local machine and select **Visualize** to enter the analysis workspace.
    * **Line Chart:** Create a line chart showing sales revenue by month (Sales + Order Date). Use QuickSight ML Forecasting to predict future trends and compare them with historical data (Periods backward = 6).
    * **KPI and Insights:** Create a KPI visual to compare year-over-year sales performance. Use ML-powered Insights to automatically generate analyses such as Month-over-Month trends and Forecasts. Adjust number formatting and resize visuals as needed.
    * **Donut/Pie Chart:** Create a donut chart by Industry and add a drill-down layer to Customer. Display data labels and enable interactive filtering across the dashboard when an industry is selected.
    * **Pivot Table:** Create a pivot table using Region, Subregion, and Order Date (grouped by year). Add subtotals and hide unnecessary labels.
    * **Finalize the Dashboard:** Add a Segment filter control, assign dashboard and chart titles, and publish the initial dashboard.

* **Creating an Interactive Dashboard**
  * **Advanced Interactivity Features:**
    * Create a backup copy of the dashboard using **Save As**.
    * **Filter Settings:** Configure cascading filters (Region → Subregion), use dropdown controls, and enable **Show relevant visuals only**.
    * **Filter Actions:** Apply filter actions from one visual (e.g., the line chart) to other visuals while excluding specific charts such as the Forecast chart.
    * **Navigation Actions:** Create an Industry parameter and a custom action that allows users to click a pie chart slice to navigate to a detailed sheet automatically filtered by the selected industry.
    * Publish the interactive dashboard.

* **Clean Up**
  * Instructions for deleting the QuickSight account (switch to the N. Virginia region, navigate to **Manage QuickSight → Delete Account**) and removing related IAM roles to avoid unnecessary charges.

## Monday: Hands-on Labs and Data Modeling with Amazon DynamoDB
* **General Overview**
  * Amazon DynamoDB is a key-value and document database that delivers single-digit millisecond performance at any scale. This page consolidates workshops and hands-on labs to help users understand DynamoDB features and NoSQL data modeling best practices.

* **Main Content Structure**
  * LHOL: Hands-on Labs for Amazon DynamoDB (Fundamental Labs – Level 200)
    * Getting Started
    * Explore DynamoDB with the CLI (read sample data, Query, Scan, Insert/Update, Delete, Transactions, Global Secondary Indexes)
    * Explore the DynamoDB Console (view data, Query, Scan, edit data, GSI)
    * Backups (AWS Backup, Point-in-Time Recovery, On-Demand Backups, Scheduled Backups, delete backups, cleanup)
    * Relational Modeling & Migration (using MySQL → AWS DMS → DynamoDB)

  * **LBED: Generative AI with DynamoDB Zero-ETL to OpenSearch + Amazon Bedrock** 
    * Service Configuration (OpenSearch permissions, enable Bedrock models, load data)
    * Query and Conclusions

  * **LADV: Advanced Design Patterns for Amazon DynamoDB**
    * Getting Started (verify environment, Python, AWS CLI, boto3, etc.)
    * Exercise 1: Capacity Units & Partitioning
    * Exercise 2: Sequential & Parallel Table Scans
    * Exercise 3: GSI Write Sharding
    * Exercise 4: GSI Key Overloading
    * Exercise 5: Sparse Global Secondary Indexes
    * Exercise 6: Composite Keys
    * Exercise 7: Adjacency Lists
    * Exercise 8: DynamoDB Streams + AWS Lambda

  * **LCDC: Change Data Capture for Amazon DynamoDB**
    * CDC with DynamoDB Streams (enable streams, Dead Letter Queue, Lambda, IAM, simulate updates)
    * CDC with Kinesis Data Streams
    * Summary & Cleanup

  * **LMR: Build and Deploy a Global Serverless Application with Amazon DynamoDB (Global Tables)**
    * Deploy backend, explore Global Tables, Globalflix interface, discussion topics, cleanup

  * **LEDA: Build a Serverless Event-Driven Architecture with DynamoDB**
    * Lab 1: Connect Pipeline (StateLambda, MapLambda, ReduceLambda)
    * Lab 2: Fault Tolerance & Exactly-Once Processing

  * **LGME: Modeling Game Player Data with Amazon DynamoDB**
    * Plan the data model, user profiles and games, use a sparse GSI to find open games, summary & cleanup
    * LDC: Design Challenges
    * References to NoSQL Design documentation and resources.

## Tuesday: Building a Serverless Data Lake on AWS from Data Preparation to Visualization
* **Overview**
  * This workshop provides a guide to building a serverless Data Lake on AWS using your own data. It focuses on creating a complete data pipeline: from raw data preparation → data cleansing → ingestion → querying → visualization, without the need to manage servers.

* **Learning Objectives**
  * Understand how to build a Data Lake on Amazon S3
  * Use AWS services including AWS Glue DataBrew, AWS Glue, Amazon Athena, and Amazon QuickSight
  * Learn Amazon S3 security best practices

* **Recommended Region:** Singapore (ap-southeast-1), although other AWS regions can also be used.

* **Detailed Workshop Structure**
  * **Preparation**
    * Set up the environment to download sample datasets, verify file encoding, and prepare data for upload to Amazon S3.

  * **Data Preparation**
    * Using AWS Glue DataBrew:
      * Setting Up DataBrew
      * Data Profiling and Analysis
      * Data Cleansing and Transformation
      * Preparing the Next Table
      * Uploading the Cleaned Dataset to Amazon S3

  * **Data Ingestion with AWS Glue**
    * Configuring IAM Roles for AWS Glue
    * Creating a Data Catalog with Glue Crawlers
    * Transforming Data from CSV to Parquet Format
    * Creating a New Data Catalog for Curated Data
    * Validating and Verifying Data Schemas

  * **Data Querying**
    * Setting Up Amazon Athena
    * Basic Queries
    * Joining Two Tables
    * Create Table As Select (CTAS)
    * Creating Views
    * Data Partitioning
    * Comparing Columnar (Parquet) and Row-Based Data Formats

  * **Visualization with Amazon QuickSight**
    * Registering for QuickSight
    * Configuring Permissions
    * Connecting Datasets
    * Editing and Preparing Datasets
    * Building Dashboards

  * **Resource Cleanup**
    * Guidelines for cleaning up AWS resources to avoid unnecessary charges.

## Wednesday: Implementing an AWS Data Lake with Glue, Athena, and QuickSight
* **Overview**
  * A Data Lake is defined as a storage repository for raw, unprocessed data that can be analyzed later to generate insights.
  * Key characteristics of a Data Lake:
    * Stores all types of data (raw or processed) for long-term retention.
    * Supports multiple users (multi-user) to refine, explore, and enrich data.
    * Provides flexible access methods, including batch, interactive, real-time, search, and in-memory processing.

  * Practitioner Role:
    * A member of the Data Analysis team at a music startup company, responsible for exploring, analyzing, and generating statistics from data.

  * Services Used:
    * AWS Glue: ETL service, Data Catalog (Crawler), and Glue Jobs.
    * Amazon Athena: Serverless SQL query service for analyzing data directly on Amazon S3.
    * Amazon QuickSight: Dashboard creation and data visualization service.

* **Content Structure**
  * **Introduction**
    * Explanation of the Data Lake concept.
    * Detailed introduction to the following services:
      * AWS Glue (ETL, Crawler, Data Catalog, Spark Jobs)
      * Amazon Athena (SQL queries on S3, supports multiple formats such as CSV, JSON, Parquet, etc.)
      * Amazon QuickSight (Concepts: Data Source, Dataset, Analysis, Visual, Dashboard)

  * **Preparation Steps**
    * Prepare an IAM Role for AWS Glue.

  * **Data Collection and Storage**
    * Create an S3 bucket for data storage.
    * Configure a Delivery Stream (likely Amazon Kinesis Data Firehose) for data ingestion.
    * Generate sample data for testing purposes.

  * **Creating a Data Catalog**
  * Use an AWS Glue Crawler to scan data stored in S3 and create metadata (tables and schemas) in the AWS Glue Data Catalog.

  * **Data Transformation**
    * Create an Amazon SageMaker Notebook or AWS Glue Notebook.
    * Download the sample notebook from the AWS-First-Cloud-Journey GitHub repository.
    * Execute the notebook code to perform ETL transformations using an Interactive Session or AWS Glue Job.

* **Data Analysis & Visualization**
  * **Analyze Data with Athena**
    * Use Amazon Athena to query and analyze data.

  * **Visualize with QuickSight**
    * Create a dataset from Athena.
    * Build analyses and visualizations.
    * Publish dashboards using Amazon QuickSight.

* **Resource Cleanup**
  * To avoid unnecessary charges, remove all created resources:
    * Delete QuickSight visuals, analyses, and dashboards.
    * Delete tables and databases in AWS Glue.
    * Delete Notebooks and Development Endpoints.
    * Empty and delete the S3 bucket.
    * Delete the CloudFormation stack (if applicable).

## Thursday: Frontend Authentication Implementation (Login/Register)
* **General Description**
  * This update completes the Authentication system (Login / Register) for the React + Vite frontend. It is a key milestone in securing the SOC dashboard, supporting session management, automatic redirection, and improving the overall authentication user experience.

* **Main Files Added / Modified**
  * Folder frontend/src/pages/
    * LoginPage.tsx — Fully implemented login page
    * RegisterPage.tsx — Fully implemented registration page

  * Folder frontend/src/components/auth/
    * AuthLayout.tsx — Shared layout for authentication pages (background, container, animations)
    * LoginForm.tsx — Login form (email/password, validation, submit handling)
    * RegisterForm.tsx — Registration form (full name, email, password, confirm password)
    * PasswordStrength.tsx — Real-time password strength indicator component
    * SecurityNotice.tsx — Security recommendations (2FA suggestions, password policy guidance)
    * LanguageSwitcher.tsx — Language switching component
    * ThemeSwitcher.tsx — Light/Dark mode switching component

  * Folder frontend/src/context/
    * AuthContext.tsx — Context for managing authentication state across the application
    * ThemeContext.tsx — Theme management context (refined and optimized)

  * Folder frontend/src/hooks/
    * useAuth.ts — Custom hook for authentication logic (login, register, logout, session validation)

  * Folder frontend/src/types/
    * auth.ts — TypeScript interfaces (User, LoginCredentials, RegisterData, AuthResponse, etc.)

  * Core Files
    * frontend/src/App.tsx — Deep integration of authentication logic
    * frontend/src/main.tsx — Updated root rendering configuration
    * frontend/src/components/auth/authService.ts — Authentication API service (login, register)

* **Key Changes in App.tsx**
  * Added useAuth() to manage isAuthenticated and loading states
  * Protected Routes: Unauthenticated users are automatically redirected to /login or /register
  * Deep linking support: Authentication page state is preserved on refresh (using history.pushState)
  * Smooth transitions between Login ↔ Register screens
  * Automatic redirection to the main Dashboard (/) after successful login/registration
  * Integrated ThemeContext and a professional loading spinner experience
  * Managed authScreen state ("login" | "register")

* **Authentication Features Implemented**
  * Form validation (email format, password matching, required fields)
  * Real-time password strength feedback
  * Security notices and best-practice recommendations
  * Synchronized Light/Dark theme switching
  * Basic language switching support
  * Loading states and error handling
  * Mock authentication (ready to be replaced with a real API)

* **Project-Wide Impact**
  * The frontend now includes a complete authentication flow, ready for integration with backend user management services
  * Enhances the security and professionalism of the SOC Dashboard
  * Other pages (Dashboard, Alerts, Network, Cloud, etc.) are accessible only after authentication
  * Authentication architecture is well-structured and scalable (Context + Hook + Service pattern)