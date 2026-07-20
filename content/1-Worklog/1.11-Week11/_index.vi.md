---
title: "Worklog Tuần 11"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 1.11. </b> "
---

### Mục tiêu tuần 11:

* Nghiên cứu và triển khai mô hình Static Website Hosting trên AWS bằng Amazon S3 kết hợp CloudFront, tập trung vào tối ưu hiệu năng phân phối nội dung và áp dụng các cơ chế bảo mật như Origin Access Control (OAC), HTTPS và hạn chế truy cập trực tiếp vào bucket
* Tìm hiểu và thực hành quản lý thông tin xác thực cơ sở dữ liệu bằng AWS Secrets Manager, triển khai cơ chế Secret Rotation tự động và kiểm chứng khả năng truy cập Amazon RDS từ môi trường container AWS Fargate theo hướng bảo mật và tự động hóa
*  Xây dựng và kiểm thử quy trình xử lý đơn hàng theo kiến trúc Serverless sử dụng Amazon SQS, SNS và DynamoDB, đảm bảo luồng dữ liệu từ đặt hàng, thông báo, xử lý đến lưu trữ được vận hành ổn định và có khả năng mở rộng
*  Chuẩn hóa kiến trúc dữ liệu cho SOC Console bằng cách tách biệt ba chế độ Demo, Replay và Live, đồng thời cải thiện hệ thống realtime, quản lý trạng thái kết nối và khả năng tích hợp dữ liệu từ nhiều nguồn phục vụ quá trình phát triển và trình diễn hệ thống

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
|  2  | - Triển khai website tĩnh bảo mật với Amazon S3 và CloudFront | 29/06/2026 | 29/06/2026 | <https://000094.awsstudygroup.com/> |
|  3  | - Quản lý thông tin xác thực RDS bằng AWS Secrets Manager, Secret Rotation và truy cập RDS từ AWS Fargate | 30/06/2026 | 30/06/2026 | <https://000096.awsstudygroup.com/> |
|  4  | - Xử lý đơn hàng Serverless với SQS, SNS và DynamoDB | 01/07/2026 | 01/07/2026 | <https://000083.awsstudygroup.com/> |
|  5  | - Triển khai kiến trúc dữ liệu đa chế độ Demo / Replay / Live cho SOC Console | 02/07/2026 | 02/07/2026 |


### Kết quả đạt được tuần 11:

### Công việc đã thực hiện trong dự án FCAJ Hybrid SOC/AWS

* Cập nhật frontend **SOC Console** để dữ liệu không còn phụ thuộc vào một luồng cố định, mà có thể chọn rõ ba chế độ `demo`, `replay` và `live` thông qua biến cấu hình `VITE_DATA_MODE`.
* Chỉnh sửa `App.tsx`, `useSocket.ts` và `RealtimeIncidentStream.tsx` để đồng bộ trạng thái kết nối, hạn chế tạo WebSocket trùng lặp và ưu tiên hiển thị cảnh báo mới nhất.
* Điều chỉnh các trang Network Monitoring, AI Threat Detection và Threat Hunting để nhận đúng dữ liệu từ Zeek, Suricata và các mô hình AI theo từng chế độ vận hành.
* Bổ sung các API hỗ trợ ở backend FastAPI (`/api/status`, `/api/events`, `/api/replay/demo`, `/ws/alerts`) và dữ liệu người dùng demo để kiểm thử luồng đăng nhập, replay và realtime.
* Kiểm tra luồng frontend–backend và chuẩn bị nền tảng để SOC Console có thể trình diễn bằng dữ liệu mẫu, phát lại dữ liệu lịch sử hoặc kết nối với Local Security Lab.

Ba ngày đầu tuần là các bài thực hành AWS bổ trợ cho kiến thức bảo mật, serverless và data pipeline; công việc đóng góp trực tiếp vào project được thực hiện vào thứ 5 với SOC Console như mô tả trên.

## Thứ 2: CLOUDFRONT WITH S3 BUCKET ORIGIN
* **Giới thiệu**
  * Hướng dẫn cách **host nội dung web tĩnh** trên **Amazon S3 bucket**, sau đó sử dụng **Amazon CloudFront** để bảo vệ và tăng tốc độ phân phối nội dung

* **Mục tiêu**:
  * Học cách kết hợp S3 + CloudFront
  * Áp dụng best practices bảo mật theo AWS Well-Architected Framework
  * Xây dựng kiến trúc static website production-ready

* **Điều kiện tiên quyết**
  * Tài khoản AWS (AWS Free Tier hoặc account test)
  * Quyền IAM đầy đủ cho Amazon S3 và Amazon CloudFront
  * Kiến thức cơ bản về AWS Console

* **Chi phí**
  * Thường **dưới 1 USD/tháng** nếu chỉ dùng để học và dọn dẹp (teardown) sau khi xong

* **Các bước thực hiện**

* **Tạo S3 Bucket và Upload nội dung**
  * **Vào **S3 Console** → **Create bucket****
    * Đặt tên bucket (ví dụ: `my-static-site-000094` – phải unique toàn cầu)
    * Chọn Region phù hợp
    * **Block all public access** = OFF (hoặc cấu hình sau)

  * **Upload files:**
    * Tạo file `index.html` đơn giản:
     ```html
     <!DOCTYPE html>
     <html>
     <head><title>My Static Site</title></head>
     <body><h1>Hello from S3 + CloudFront!</h1></body>
     </html>
     ```
    * Upload index.html và các file khác (CSS, JS, images)

  * **Enable Static Website Hosting:**
    * Properties → Static website hosting → Enable
    * Index document: index.html
    * Lưu lại Endpoint

* **Tạo CloudFront Distribution**
  * Vào CloudFront Console → Create distribution
  * Origin settings:
    * Origin domain: Chọn S3 bucket (hoặc nhập manual)
    * Origin access: Chọn Origin access control (OAC) (khuyến nghị)

  * Tạo OAC mới nếu chưa có:
    * Signing behavior: Sign requests
    * Update S3 bucket policy tự động hoặc manual

  * Behavior settings:
    * Viewer protocol policy: Redirect HTTP to HTTPS
    * Cache policy: CachingOptimized
    * Compress objects: Yes

  * Settings:
    * Alternate domain names (nếu có custom domain)
    * Custom SSL certificate (ACM)

  * Create distribution (chờ ~5-10 phút để deploy)

* **Cấu hình Security (Bucket Policy + OAC)**
  * Cập nhật S3 Bucket Policy để chỉ cho phép CloudFront truy cập:
  JSON{
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
  * (Thay bằng ARN của OAC)

* **Kiểm tra**
  * Truy cập URL CloudFront (ví dụ: https://dxxxxxx.cloudfront.net)
  * Kiểm tra tốc độ, HTTPS, và xác nhận không truy cập trực tiếp S3 được

* **Dọn dẹp**
  * Xóa CloudFront Distribution
  * Xóa S3 Bucket và objects

## Thứ 3: Thực hành AWS Secrets Manager, Secret Rotation và Truy cập RDS từ Fargate
* **Mục tiêu**
  * Truy cập RDS Database qua Secrets Manager
  * Thực hiện **Secret Rotation** (thay đổi password định kỳ)
  * Truy cập RDS từ ứng dụng chạy trên **AWS Fargate**

* **Dịch vụ AWS sử dụng**
  * Amazon RDS (MySQL)
  * AWS Secrets Manager
  * AWS Fargate + ECS + ECR
  * Amazon EC2 (Bastion Host)
  * Amazon VPC
  * AWS CloudFormation
  * AWS Systems Manager Session Manager

* **Kiến trúc**
  * VPC với 2 Subnets
  * **Bastion Host** (EC2 Amazon Linux 2) để chạy scripts
  * **Private RDS Instance**
  * **Fargate Tasks** để test kết nối từ container

* **Các Phần Thực Hành**
  * **Chuẩn bị hạ tầng**
    * Sử dụng **AWS CloudFormation** tạo stack tên `smdemo` tại region **us-east-1**
    * Template URL: `https://s3.amazonaws.com/sa-security-specialist-workshops-us-east-1/secrets-manager-workshop/RDSFargate.yml`
    * Ghi chú **Stack Outputs**:
      * `BastionIP`
      * `DBInstance`, `DBUser`, `DBPassword`
      * `EC2UserPassword`
      * `ECRRepository`, `ECSCluster`

  * **Using on RDS**
    * Secure RDS Credential
    * Tạo Secret trong Secrets Manager, chọn kiểu RDS database
    * Liên kết với RDS Instance

  * **Truy cập RDS từ Bastion**
    * Kết nối qua **Session Manager**
    * Chạy script:
      * `mysql.oldway.sh` (hard-coded password)
      * `mysql.newway.sh` (lấy secret động qua AWS CLI + jq)

  * **Secret Rotation**
    * Bật automatic rotation (ví dụ 30 ngày)
    * Secrets Manager dùng Lambda để rotate password và cập nhật RDS

  * **Kiểm tra sau Rotation**
    * Script cũ sẽ lỗi
    * Script mới vẫn truy cập được

  * **Using on Fargate**
    * Build & Push Docker Image
    * Từ Bastion: chạy `dockerbuild.sh` → `dockertagandpush.sh`

  * **Configure Fargate**
    * Chỉnh sửa Task Definition, thêm secret ARN vào Environment Variables
    * Chạy Task trên Fargate

  * **Truy cập & Test**
    * SSH vào Fargate container
    * Chạy script mới để kết nối RDS

* **Clean Up**
  * Chạy `./cleanup.sh` từ Bastion
  * Xóa Secret trong Secrets Manager
  * Xóa CloudFormation stacks

## Thứ 4: Xử lý và Quản lý Đơn hàng với SQS, SNS và DynamoDB
* **Tổng quan**
  * Khi người dùng đặt hàng (Checkout), hệ thống gửi thông tin đơn hàng vào SQS queue, đồng thời publish thông báo qua SNS topic để thông báo cho admin
  * Admin có thể xem danh sách đơn hàng, Handle (xử lý) đơn hàng (lưu vào DynamoDB và xóa khỏi queue), hoặc Delete đơn hàng

* **Kiến trúc chính:**
  * POST /books/order: Đặt hàng → gửi vào SQS queue + publish SNS
  * GET /books/order: Admin lấy danh sách đơn hàng từ DynamoDB
  * POST /books/order/handle: Xử lý đơn hàng → lưu DynamoDB + xóa khỏi queue
  * DELETE /books/order: Xóa đơn hàng khỏi queue

* **Nội dung các phần chính**
  * **Chuẩn bị:**
    * Tải source code fcj-book-store-sam-ws6.zip
    * Chỉnh sửa template.yaml (thay domain, uncomment phần CloudFront + Certificate nếu cần)
    * Deploy SAM (sam build, sam deploy --guided)
    * Clone repo frontend FCJ-Serverless-Workshop, chỉnh isAdmin: true, build và upload lên S3
    * Cấu hình DNS Route 53

  * **Tạo API & Lambda:**
    * Tạo bảng OrdersTable DynamoDB (partition key id, sort key book_id)
    * Tạo các Lambda functions:
      * checkout_order
      * order_management
      * handle_order
      * delete_order
    * Tích hợp với API Gateway

  * **Kiểm tra hoạt động:**
    * Lấy Invoke URL từ API Gateway
    * Cập nhật config frontend, rebuild & upload lại S3
    * Thêm sách mẫu, thêm vào giỏ hàng, checkout
    * Kiểm tra message trong SQS queue
    * Nhận email thông báo từ SNS
    * Admin xem Orders, Handle (kiểm tra DynamoDB), và Delete

  * **Dọn dẹp tài nguyên:**
    * Xóa records Route 53
    * Empty S3 buckets
    * Xóa CloudFormation stacks
    * Xóa SQS queue và SNS topic

## Thứ 5: Chuẩn Hóa Luồng Dữ Liệu và Realtime Cho SOC Console
* **Mục tiêu chính:**  
  * Cải tiến kiến trúc frontend SOC console để hỗ trợ tách biệt rõ ràng giữa **demo mode**, **replay mode** và **live mode**, giúp hệ thống linh hoạt hơn khi chạy demo, test với dữ liệu lịch sử hoặc kết nối realtime với backend/local lab

* **Thay Đổi Chính Trong Frontend**
  * **Cấu Hình Môi Trường (`.env.example`)**
    * Thêm comment hướng dẫn chi tiết về `VITE_DATA_MODE`
    * Giá trị hợp lệ: `demo`, `replay`, `live`
    * Production build yêu cầu set giá trị rõ ràng để tránh lỗi runtime

  * **App.tsx (Core Application Logic)**
    * Tích hợp `dataMode` từ `useSocket` hook vào state quản lý
    * Cải thiện logic routing và auth flow khi chuyển đổi giữa các mode
    * Xử lý redirect sau login/register về dashboard phù hợp với mode hiện tại
    * Tối ưu re-render và state synchronization giữa các component con

  * **Socket & Realtime Handling (`useSocket.ts`, `RealtimeIncidentStream.tsx`)**
    * Mở rộng hook `useSocket` hỗ trợ nhiều mode:
      * **Demo mode**: Sử dụng mock WebSocket server (`server.ts`)
      * **Live mode**: Kết nối trực tiếp với FastAPI WebSocket (`/ws/alerts`)
      * **Replay mode**: Hỗ trợ phát lại dữ liệu lịch sử từ backend
    * Thêm trạng thái `socketStatus`, `platformStatus`, `error` để hiển thị rõ ràng
    * Ngăn chặn duplicate socket connection khi chuyển mode

  * **Các Component Dashboard Được Cập Nhật**
    * **NetworkMonitoringPage.tsx**, **AIThreatDetectionPage.tsx**, **ThreatHuntingPanel.tsx**: Hỗ trợ render dữ liệu theo mode
      * **RealtimeIncidentStream.tsx**: Cải tiến stream alert realtime, ưu tiên hiển thị alert mới nhất
      * **DatasetMismatchPanel.tsx**, **SuricataCenter.tsx**, **AttackReplayCampaignPanel.tsx**: Tích hợp logic mode-aware
      * **FlowDetailPanel.tsx**, **ExplainabilityCenter.tsx**: Hiển thị chi tiết event phù hợp với nguồn dữ liệu (Zeek, Suricata, AI models)

  * **Auth & User Management**
    * Cập nhật `authService.ts` và các form (`LoginForm.tsx`)
    * Hỗ trợ demo credentials và register localStorage
    * Thêm endpoint backend mock cho `/api/auth/*`

* **Thay Đổi Trong Backend (Hỗ Trợ Mode)**
  * **main.py**: 
    * Thêm hỗ trợ CORS, auth users demo
    * Cải tiến `/api/status`, `/api/events`, `/api/replay/demo`
    * Thêm hàm `_encode_demo_token` cho JWT-like demo token
  * Hỗ trợ ingest event từ nhiều nguồn (Zeek conn, HTTP logs, Suricata)

* **Cải Tiến Tổng Thể**
  * **Tính Linh Hoạt**: Dễ dàng chuyển đổi giữa mock data (demo nhanh), replay log (test scenario), và live data (production-like)
  * **UX/UI**: 
    * Hiển thị rõ trạng thái kết nối (connected/disconnected)
    * KPI widgets, alert feed, MITRE mapping hoạt động nhất quán qua các mode
  * **Developer Experience**:
    * Hướng dẫn chạy chi tiết trong README frontend
    * Tách biệt mock server (`server.ts`) và production backend
  * **Tích Hợp Multi-Model**: Hỗ trợ hiển thị output từ AI1 (Anomaly), AI2A (Network), AI2B (HTTP Web Attack) và Fusion Layer

* **Lợi Ích Của Thay Đổi Này**
  * Giảm thời gian demo và testing
  * Dễ debug giữa frontend và backend
  * Chuẩn bị cho tích hợp live với Local Lab (pfSense, Zeek, Suricata) và AWS deployment
  * Nền tảng vững chắc cho các tính năng realtime sau này (WebSocket scaling, CloudWatch monitoring)
