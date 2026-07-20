---
title: "Worklog Tuần 12"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 1.12 </b> "
---

### Mục tiêu tuần 12:

* Hoàn thiện báo cáo workshop **FCAJ Hybrid SOC/AWS** dựa trên các nội dung đã tìm hiểu và triển khai trong những tuần trước
* Chuẩn hóa cấu trúc workshop, mô tả rõ kiến trúc hệ thống, các dịch vụ AWS sử dụng và luồng xử lý dữ liệu
* Rà soát lại nội dung, hình ảnh minh họa và evidence để đảm bảo báo cáo không ghi nhận vượt quá phạm vi đã xác minh

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2 | Viết phần tổng quan, phạm vi và sơ đồ kiến trúc Hybrid SOC/AWS | 06/07/2026 | 06/07/2026 | Nội dung project và evidence các tuần trước |
| 3 | Hoàn thiện hướng dẫn Networking, IAM, S3, CloudFront, WAF và Backend EC2 | 07/07/2026 | 07/07/2026 | Cấu hình và ảnh kiểm chứng của project |
| 4 | Viết luồng SQS/DLQ, S3 Data Bucket, RDS, Secrets Manager và Worker Pipeline | 08/07/2026 | 08/07/2026 | Kết quả triển khai data pipeline |
| 5 | Bổ sung phần kiểm chứng Dashboard, AI Fusion, Monitoring, Audit và Notification | 09/07/2026 | 09/07/2026 | Screenshot, log và kết quả test |
| 6 | Rà soát song ngữ, chuẩn hóa hình ảnh/đường dẫn và hoàn thiện Cleanup & Cost Control | 10/07/2026 | 10/07/2026 | Toàn bộ nội dung workshop |


### Kết quả đạt được tuần 12:

## Viết báo cáo workshop FCAJ Hybrid SOC/AWS

* **Mục tiêu công việc**
  * Tổng hợp lại quá trình tìm hiểu và thực hành AWS trong kỳ thực tập thành một workshop có cấu trúc rõ ràng
  * Trình bày kiến trúc tổng quan của hệ thống Hybrid SOC/AWS
  * Mô tả vai trò của các thành phần chính như Local Security Lab, Backend EC2, S3, SQS, RDS, CloudFront, WAF, CloudWatch và Dashboard
  * Chuẩn bị nội dung báo cáo theo hướng có thể dùng để hướng dẫn lại cho người đọc triển khai hoặc hiểu luồng hệ thống

* **Nội dung đã thực hiện**
  * Viết phần tổng quan workshop, mô tả mục tiêu, phạm vi và kiến trúc của project **FCAJ Hybrid SOC/AWS**
  * Tổ chức workshop thành các section chính:
    * Overview and Architecture
    * Prerequisites and Naming
    * Networking, IAM and Security Baseline
    * Frontend S3, CloudFront and WAF
    * Backend EC2 Runtime
    * SQS, DLQ and S3 Data Bucket
    * RDS, Secrets and Worker Pipeline
    * AWS Pipeline Validation and Dashboard Evidence
    * AI Fusion and Dashboard Validation
    * Monitoring, Audit and Notification
    * Cleanup and Cost Control
  * Rà soát lại nội dung từng section để đảm bảo cách viết thống nhất, dễ theo dõi và đúng phạm vi báo cáo
  * Bổ sung mô tả cho các bước triển khai, kiểm tra và xác thực evidence trong workshop
  * Điều chỉnh wording ở những phần chưa có evidence đầy đủ, tránh claim hệ thống đã hoàn thiện production hoặc đã tích hợp đầy đủ khi chưa có ảnh xác minh tương ứng
  * Kiểm tra lại đường dẫn hình ảnh, tiêu đề section và cách trình bày trong báo cáo

* **Kiến thức và kỹ năng rút ra**
  * Hiểu rõ hơn cách trình bày một workshop kỹ thuật theo trình tự: tổng quan kiến trúc, chuẩn bị môi trường, triển khai từng thành phần, kiểm tra kết quả và cleanup
  * Biết cách chuyển nội dung thực hành rời rạc ở nhiều tuần thành một báo cáo có tính hệ thống
  * Rèn luyện kỹ năng viết tài liệu kỹ thuật, đặc biệt là cách mô tả kiến trúc cloud, luồng dữ liệu và evidence
  * Nhận thức rõ hơn tầm quan trọng của việc chỉ ghi nhận những nội dung đã được kiểm chứng bằng screenshot, log hoặc kết quả test

* **Khó khăn gặp phải**
  * Một số phần workshop có nhiều thành phần liên quan với nhau nên cần sắp xếp lại thứ tự để người đọc dễ hiểu luồng hệ thống
  * Cần phân biệt rõ giữa nội dung đã có evidence thật và nội dung chỉ là kế hoạch hoặc phần mở rộng
  * Việc chuẩn hóa cách đặt tên section, hình ảnh và mô tả mất khá nhiều thời gian vì báo cáo có nhiều phần nhỏ

* **Kết quả hoàn thành**
  * Hoàn thiện nội dung chính cho báo cáo workshop **FCAJ Hybrid SOC/AWS**
  * Workshop đã được tổ chức thành 11 section theo đúng luồng triển khai và kiểm chứng hệ thống
  * Nội dung báo cáo đã tập trung vào công việc viết workshop, tổng hợp kiến thức và chuẩn hóa evidence thay vì triển khai thêm chức năng mới
  * Hoàn thành công việc tuần 12 theo kế hoạch từ **06/07/2026** đến **10/07/2026**
