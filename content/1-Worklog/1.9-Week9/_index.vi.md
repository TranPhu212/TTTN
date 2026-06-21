---
title: "Worklog Tuần 9"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.9. </b> "
---

### Mục tiêu tuần 9:

* 

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
|  6  | - Thực hành Trực quan hóa Dữ liệu bằng Amazon QuickSight | 12/06/2026 | 12/06/2026 | <https://000073.awsstudygroup.com/> |
|  2  | - Amazon DynamoDB: Thiết kế NoSQL, Mẫu Kiến trúc Nâng cao và Giải pháp Serverless | 15/06/2026 | 15/06/2026 | <https://000039.awsstudygroup.com/> |
|  3  | - Xây dựng Data Lake Serverless trên AWS | 16/06/2026 | 16/06/2026 | <https://000070.awsstudygroup.com/> |
|  4  | - Từ Data Lake đến Dashboard với AWS Glue, Athena và QuickSight | 17/06/2026 | 17/06/2026 | <https://000035.awsstudygroup.com/> |
|  5  | - nội dung thay thế | 18/06/2026 | 18/06/2026 | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 9:

## Thứ 6: Thực hành Phân tích Dữ liệu và Dashboard trên AWS QuickSight
* Giới thiệu workshop "Getting Started with QuickSight". Nội dung chính là hướng dẫn xây dựng dashboard để trực quan hóa dữ liệu bán hàng (sales.csv) bằng Amazon QuickSight. Workshop sử dụng region Singapore (ap-southeast-1), tập trung vào phân tích dữ liệu và biểu diễn qua các visual

* **Các khái niệm cơ bản:**
  * Data source: Nguồn dữ liệu bên ngoài (S3, Athena, Salesforce...)
  * Dataset: Dữ liệu cụ thể từ data source, lưu trữ cả các chuẩn bị dữ liệu (rename field, thay đổi kiểu dữ liệu...)
  * Analysis: Không gian chứa các visual và story liên quan đến một mục tiêu kinh doanh
  * Visual: Biểu đồ trực quan hóa dữ liệu (mỗi visual dùng một dataset)
  * Dashboard: Bản publish chỉ xem (view-only) từ analysis, giữ cấu hình filter, parameter... và cập nhật dữ liệu mới nhất

* **Chuẩn bị**
  * Hướng dẫn tạo tài khoản QuickSight Enterprise (có thể hủy sau lab), upload file sales.csv (khoảng 1.5MB), và thiết lập ban đầu

  * **Các bước chi tiết bao gồm:**
    * Đăng ký qua AWS Console
    * Chọn Enterprise edition
    * Cấu hình IAM federated identities, region Singapore, account name, email
    * Đóng welcome screen sau khi vào QuickSight

* **Xây dựng Dashboard đầu tiên**
  * **Tạo dataset và các visual cơ bản:**
    * Tạo Dataset: Upload file sales.csv từ máy local, sau đó Visualize để vào analysis
    * Line Chart: Tạo biểu đồ đường doanh thu theo tháng (Sales + Order Date). Sử dụng tính năng Forecast (dự báo) của QuickSight ML để dự đoán tương lai, so sánh với dữ liệu thực tế (Periods backward = 6)
    * KPI và Insights: Tạo KPI so sánh doanh thu theo năm (Year over Year). Sử dụng Insights tự động từ ML để sinh ra các phân tích như Month over Month, Forecast. Điều chỉnh format số và resize visual
    * Donut/Pie Chart: Tạo donut chart theo ngành (Industry), thêm drill-down layer xuống Customer. Hiển thị data labels, áp dụng filter tương tác trên toàn dashboard khi click ngành
    * Pivot Table: Tạo bảng xoay theo Region, Subregion, Order Date (theo năm), thêm subtotal. Ẩn một số label không cần thiết
    * Hoàn thiện Dashboard: Thêm filter control (Segment), title dashboard và title từng chart. Publish dashboard ban đầu

* **Tạo Interactive Dashboard**
  * **Nâng cao về tính tương tác:**
    * Tạo bản backup dashboard (Save as)
    * Filter Settings: Thiết lập cascading filter (Region → Subregion), kiểu dropdown, "Show relevant visuals only"
    * Filter Actions: Áp dụng filter action từ chart (ví dụ line chart) sang các visual khác, loại trừ một số chart cụ thể (như Forecast)
    * Navigation Actions: Tạo parameter (Industry), custom action để click pie chart chuyển sang sheet chi tiết (Details) và tự động filter theo ngành đã chọn
    * Publish dashboard tương tác

* **Clean up**
  * Hướng dẫn xóa tài khoản QuickSight (chuyển region về N. Virginia, Manage QuickSight → Delete Account) và dọn IAM roles liên quan để tránh chi phí

## Thứ 2: Thực hành và Thiết kế Dữ liệu với Amazon DynamoDB
* **Mô tả tổng quát**
  * DynamoDB là một cơ sở dữ liệu key-value và document cung cấp hiệu suất mili-giây đơn chữ số ở bất kỳ quy mô nào. Trang tập hợp nhiều workshop và lab thực hành nhằm giúp người dùng hiểu rõ các tính năng của DynamoDB cũng như best practices về mô hình hóa dữ liệu NoSQL

* **Cấu trúc nội dung chính**
  * **LHOL: Hands-on Labs for Amazon DynamoDB (Labs cơ bản mức 200)**
    * Getting Started
    * Explore DynamoDB with the CLI (đọc dữ liệu mẫu, Query, Scan, Insert/Update, Delete, Transactions, Global Secondary Indexes)
    * Explore the DynamoDB Console (xem dữ liệu, Query, Scan, chỉnh sửa dữ liệu, GSI)
    * Backups (AWS Backup, Point-In-Time Recovery, On-Demand, Scheduled, xóa backup, cleanup)
    * Relational Modeling & Migration (sử dụng MySQL → DMS → DynamoDB)

  * **LBED: Generative AI with DynamoDB zero-ETL to OpenSearch + Amazon Bedrock**
    * Cấu hình dịch vụ (quyền OpenSearch, enable Bedrock models, load dữ liệu)
    * Query và kết luận

  * **LADV: Advanced Design Patterns for Amazon DynamoDB**
    * Getting Started (kiểm tra môi trường, Python, AWS CLI, boto3…)
    * Exercise 1: Capacity Units & Partitioning
    * Exercise 2: Sequential & Parallel Table Scans
    * Exercise 3: GSI Write Sharding
    * Exercise 4: GSI Key Overloading
    * Exercise 5: Sparse Global Secondary Indexes
    * Exercise 6: Composite Keys
    * Exercise 7: Adjacency Lists
    * Exercise 8: DynamoDB Streams + AWS Lambda

  * **LCDC: Change Data Capture for Amazon DynamoDB**
    * CDC bằng DynamoDB Streams (enable stream, Dead Letter Queue, Lambda, IAM, simulate updates)
    * CDC bằng Kinesis Data Streams
    * Summary & Clean Up

  * **LMR: Build and Deploy a Global Serverless Application with Amazon DynamoDB (Global Tables)**
    * Deploy backend, explore Global Tables, giao diện Globalflix, discussion topics, cleanup

  * **LEDA: Build a Serverless Event Driven Architecture with DynamoDB**
    * Lab 1: Connect pipeline (StateLambda, MapLambda, ReduceLambda)
    * Lab 2: Fault tolerance & exactly-once processing

  * **LGME: Modeling Game Player Data with Amazon DynamoDB**
    * Plan data model, user profiles & games, sparse GSI để tìm open games, summary & cleanup

  * **LDC: Design Challenges**
    * Liên kết tài liệu tham khảo NoSQL Design

## Thứ 3: Xây dựng Data Lake Serverless trên AWS từ Thu thập Dữ liệu đến Trực quan hóa
* **Mô tả tổng quát**
  * Đây là hướng dẫn xây dựng Data Lake serverless trên AWS sử dụng dữ liệu của chính bạn. Workshop tập trung vào việc xây dựng một pipeline dữ liệu hoàn chỉnh: từ chuẩn bị dữ liệu thô → làm sạch → ingestion → query → visualization, mà không cần quản lý server

* **Mục tiêu sau khi hoàn thành:**
  * Hiểu cách xây dựng Data Lake trên Amazon S3
  * Sử dụng các dịch vụ AWS: Glue DataBrew, AWS Glue, Amazon Athena, Amazon QuickSight
  * Biết các best practices về bảo mật S3

* **Region khuyến nghị:** Singapore (ap-southeast-1), nhưng có thể dùng region khác

* **Cấu trúc chi tiết workshop**
  * **Chuẩn bị**
    * Tạo môi trường để tải dữ liệu mẫu về, kiểm tra encoding, và chuẩn bị upload lên S3

  * **Chuẩn bị dữ liệu**
    * Sử dụng AWS Glue DataBrew:
      * Setting up DataBrew
      * Phân tích profile dữ liệu
      * Làm sạch và biến đổi dữ liệu
      * Preparing the Next Table
      * Upload cleaned dataset lên S3

  * **Data Ingestion with AWS Glue**
    * Configuring IAM roles cho Glue
    * Tạo Data Catalog bằng Glue Crawler
    * Transform dữ liệu từ CSV sang định dạng Parquet
    * Tạo Data Catalog mới cho dữ liệu đã curated
    * Kiểm tra schema thông tin

  * **Query dữ liệu**
    * Cài đặt và thiết lập Athena
    * Basic query
    * Join 2 tables
    * Create Table As Select (CTAS)
    * Tạo View
    * Data Partitioning
    * So sánh Columnar (Parquet) vs Row-based format

  * **Visualization with QuickSight**
    * Đăng ký QuickSight
    * Thiết lập quyền
    * Kết nối Dataset
    * Chỉnh sửa Dataset
    * Xây dựng Dashboard

  * **Resource Cleanup**
    * Hướng dẫn dọn dẹp tài nguyên để tránh phát sinh chi phí

## Thứ 4: Triển khai Hệ thống Data Lake trên AWS với Glue, Athena và QuickSight
* **Tổng quan**
  * Data Lake được định nghĩa là kho lưu trữ dữ liệu thô (raw data) chưa qua xử lý, dùng để phân tích và rút ra insights sau này
  
  * Đặc điểm chính của Data Lake:
    * Thu thập mọi loại dữ liệu (raw hoặc processed) trong thời gian dài
    * Hỗ trợ đa người dùng (multi-user) để tinh chỉnh, khám phá và làm giàu dữ liệu
    * Linh hoạt trong truy cập: batch, interactive, real-time, search, in-memory...

  * Vai trò người thực hành: Thành viên đội ngũ Data Analysis của một công ty startup về âm nhạc (music startup), sẽ khám phá, phân tích và thống kê dữ liệu

  * Công cụ sử dụng:
    * AWS Glue: ETL service, Data Catalog (crawler), Glue Jobs
    * Amazon Athena: Query dữ liệu trực tiếp trên S3 bằng SQL (serverless)
    * Amazon QuickSight: Tạo dashboard, visualization

* **Cấu trúc nội dung**
  * **Introduction**
    * Giải thích khái niệm Data Lake
    * Giới thiệu chi tiết các dịch vụ:
      * AWS Glue (ETL, Crawler, Data Catalog, Spark jobs)
      * Amazon Athena (query SQL trên S3, hỗ trợ nhiều format: CSV, JSON, Parquet...)
      * Amazon QuickSight (các khái niệm: Data Source, Dataset, Analysis, Visual, Dashboard)

  * **Preparation Steps**
    * Chuẩn bị IAM Role cho AWS Glue

  * **Data Collection and Storage**
    * Tạo S3 bucket để lưu dữ liệu
    * Thiết lập Delivery Stream (có lẽ là Kinesis Firehose) để thu thập dữ liệu
    * Tạo sample data để test

  * **Creating a Data Catalog**
    * Sử dụng AWS Glue Crawler để quét dữ liệu trên S3 và tạo metadata (bảng, schema) trong Glue Data Catalog

  * **Data Transformation**
    * Tạo SageMaker Notebook hoặc AWS Glue Notebook
    * Tải notebook mẫu từ GitHub (AWS-First-Cloud-Journey)
    * Chạy code để thực hiện ETL (transform dữ liệu) bằng Interactive Session hoặc Glue Job

  * **Data Analysis & Visualization**
    * **Analyzedatawithathena:** Sử dụng Athena để query và phân tích dữ liệu
    * **Visualizewithquicksight:** Tạo dataset từ Athena, xây dựng analysis, visuals và publish dashboard trên QuickSight

* **Resource Cleanup**
  * Hướng dẫn xóa sạch tài nguyên để tránh phát sinh chi phí:
    * Xóa QuickSight visuals, analyses, dashboards
    * Xóa tables và databases trong AWS Glue
    * Xóa Notebook và Development Endpoints
    * Empty & Delete S3 bucket
    * Xóa CloudFormation stack (nếu có)

## Thứ 5: Triển khai Authentication (Đăng nhập/Đăng ký) cho Frontend
* **Mô tả tổng quát**
  * Cập nhật này thêm hoàn chỉnh hệ thống Authentication (Đăng nhập / Đăng ký) cho frontend React + Vite. Đây là bước quan trọng để bảo vệ dashboard SOC, hỗ trợ quản lý phiên đăng nhập, redirect tự động và cải thiện UX auth

* **Các file được thêm / thay đổi chính**
  * Thư mục frontend/src/pages/
    * LoginPage.tsx — Trang đăng nhập đầy đủ
    * RegisterPage.tsx — Trang đăng ký đầy đủ

  * Thư mục frontend/src/components/auth/
    * AuthLayout.tsx — Layout chung cho các trang auth (background, container, animation)
    * LoginForm.tsx — Form đăng nhập (email/password, validation, submit)
    * RegisterForm.tsx — Form đăng ký (full name, email, password, confirm password)
    * PasswordStrength.tsx — Component hiển thị độ mạnh mật khẩu (real-time)
    * SecurityNotice.tsx — Thông báo bảo mật (2FA gợi ý, chính sách mật khẩu)
    * LanguageSwitcher.tsx — Chuyển đổi ngôn ngữ
    * ThemeSwitcher.tsx — Chuyển đổi Light/Dark mode

  * Thư mục frontend/src/context/
    * AuthContext.tsx — Context quản lý trạng thái authentication toàn app
    * ThemeContext.tsx — Context theme (đã được tinh chỉnh)

  * Thư mục frontend/src/hooks/
    * useAuth.ts — Custom hook xử lý logic auth (login, register, logout, check session)

  * Thư mục frontend/src/types/
    * auth.ts — TypeScript interfaces (User, LoginCredentials, RegisterData, AuthResponse...)

  * File chính
    * frontend/src/App.tsx — Tích hợp sâu logic auth
    * frontend/src/main.tsx — Cập nhật render root
    * frontend/src/components/auth/authService.ts — Service gọi API auth (login, register)

* **Các thay đổi nổi bật trong App.tsx**
  * Thêm useAuth() để kiểm tra isAuthenticated và loading
  * Protected Route: Nếu chưa đăng nhập → tự động redirect về /login hoặc /register
  * Hỗ trợ deep linking: Giữ trạng thái trang auth khi refresh (dùng history.pushState)
  * Chuyển đổi mượt mà giữa Login ↔ Register
  * Sau khi login/register thành công → redirect vào Dashboard chính (/)
  * Tích hợp ThemeContext và loading spinner chuyên nghiệp
  * Quản lý state authScreen ("login" | "register")

* **Tính năng Auth đã triển khai**
  * Form validation (email format, password match, required fields)
  * Hiển thị độ mạnh mật khẩu realtime
  * Security notice & best practices
  * Theme switcher (Light/Dark) đồng bộ
  * Language switcher (cơ bản)
  * Loading state, error handling
  * Mock auth (có thể chuyển sang API thật sau)

* **Tác động đến toàn dự án**
  * Frontend giờ đã có Auth flow hoàn chỉnh, sẵn sàng tích hợp backend user management
  * Cải thiện bảo mật và tính chuyên nghiệp của SOC Dashboard
  * Các trang khác (Dashboard, Alerts, Network, Cloud...) chỉ hiển thị khi đã đăng nhập
  * Cấu trúc code auth rõ ràng, dễ mở rộng (Context + Hook + Service)