---
title: "Worklog Tuần 10"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 1.10. </b> "
---

### Mục tiêu tuần 10:

* Tìm hiểu cách triển khai ứng dụng web sử dụng Amazon RDS trên AWS, kết nối cơ sở dữ liệu với EC2 và thực hành sao lưu, khôi phục dữ liệu
* Nắm được quy trình chuyển đổi lược đồ và di chuyển cơ sở dữ liệu bằng AWS Schema Conversion Tool (SCT) và AWS Database Migration Service (DMS), đồng thời thực hành xử lý các sự cố thường gặp
* Thực hành lưu trữ dữ liệu với Amazon S3, triển khai website tĩnh, tìm hiểu các tính năng quản lý dữ liệu như Versioning, Replication và CloudFront
* Triển khai Grafana trên AWS, kết nối với Amazon CloudWatch và xây dựng dashboard để theo dõi, trực quan hóa các chỉ số hệ thống
* Tìm hiểu và triển khai AWS Web Application Firewall (AWS WAF), cấu hình các Managed Rules và Custom Rules nhằm bảo vệ ứng dụng web trước các cuộc tấn công phổ biến

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
|  6  | - Xây dựng Ứng dụng Web với Amazon RDS trên AWS | 19/06/2026 | 19/06/2026 | <https://000005.awsstudygroup.com/> |
|  2  | - Thực hành chuyển đổi lược đồ, di chuyển dữ liệu và xử lý sự cố với AWS Database Migration Service | 22/06/2026 | 22/06/2026 | <https://000043.awsstudygroup.com/> |
|  3  | - Lưu trữ đối tượng và Hosting Website Tĩnh với Amazon S3 | 23/06/2026 | 23/06/2026 | <https://000057.awsstudygroup.com/> |
|  4  | - Triển khai Grafana và Xây dựng Dashboard Giám sát AWS CloudWatch | 24/06/2026 | 24/06/2026 | <https://000029.awsstudygroup.com/> |
|  5  | - Triển khai và cấu hình AWS Web Application Firewall (AWS WAF) | 25/06/2026 | 25/06/2026 | <https://000026.awsstudygroup.com/> |


### Kết quả đạt được tuần 10:

## Thứ 6: Xây dựng Ứng dụng Web với Amazon RDS trên AWS
* **Giới thiệu**
  * Giải thích Amazon RDS là dịch vụ managed cho phép triển khai và quản lý cơ sở dữ liệu quan hệ trên AWS
  * Phù hợp cho OLTP (Online Transaction Processing), dữ liệu có cấu trúc
  * Lợi ích: Backup tự động, vá lỗi, scale dễ dàng, Multi-AZ, Read Replicas
  * Database engines hỗ trợ: Amazon Aurora, MySQL, MariaDB, Oracle, SQL Server, PostgreSQL
  * So sánh với các dịch vụ khác (EC2, DynamoDB, Redshift…)
  * Các khái niệm quan trọng: DB Instance, Endpoint, DB Subnet Group, Encryption, Billing, Scalability, Multi-AZ vs Read Replicas

* **Các bước chuẩn bị**
  * Hướng dẫn tạo VPC, Subnets (multi-AZ), Security Groups cho EC2 và RDS, DB Subnet Group
  * Nhấn mạnh yêu cầu ít nhất 2 Availability Zones để hỗ trợ Multi-AZ

* **Tạo máy ảo EC2**
  * Hướng dẫn chi tiết tạo EC2 Linux (Amazon Linux 2023, t2.micro/t3.micro – free tier)
  * Cấu hình Security Group, Key Pair
  * Kết nối qua MobaXterm (SSH)

* **Tạo RDS Instance**
  * Cài đặt Git, Node.js trên EC2
  * Hướng dẫn tạo RDS Instance qua AWS Console (Standard create):
    * Chọn engine (MySQL/MariaDB/SQL Server…)
    * Cấu hình Storage, Multi-AZ, Security Group, Credentials
  * Xem Logs, Events, Maintenance & Backups

* **Triển khai ứng dụng**
  * Clone repository mẫu từ GitHub: AWS-First-Cloud-Journey/AWS-FCJ-Management
  * Cài đặt Node.js, các package (Express, MySQL…)
  * Script cài MySQL client, tạo Database + Table trên RDS
  * Insert dữ liệu mẫu (bảng user với thông tin các fighter UFC)
  * Chạy ứng dụng (npm start) và truy cập qua browser (port 5000)

* **Sao lưu & Khôi phục**
  * Hướng dẫn xem Backup, tạo Snapshot
  * Restore từ Snapshot thành RDS Instance mới
  * Monitoring và xác nhận sau restore

* **Dọn dẹp tài nguyên**
  * Xóa RDS Instance, Snapshots, DB Subnet Group
  * Xóa Security Groups, NAT Gateway, Elastic IP, VPC
  * Terminate EC2 Instance
  * Lưu ý tránh phát sinh chi phí không mong muốn

## Thứ 2: Chuyển đổi lược đồ và di dời cơ sở dữ liệu với AWS DMS
* **Tổng quan**
  * Trang giới thiệu tổng quan về hai quy trình quan trọng nhất khi chuyển đổi và di chuyển cơ sở dữ liệu không đồng nhất (heterogeneous database migration) lên nền tảng đám mây AWS:
    * Chuyển đổi lược đồ (Schema Conversion): Giới thiệu công cụ AWS Schema Conversion Tool (SCT) và tính năng Chuyển đổi & Di chuyển ngay trên bảng điều khiển AWS (DMS console) được cập nhật tại AWS re:Invent
    * Công cụ này giúp tự động kiểm tra, chuyển đổi các cấu trúc bảng, view, hàm, thủ tục từ CSDL nguồn sang CSDL đích tương thích, và đánh dấu các đoạn mã cần sửa đổi thủ công
    * Di dời CSDL (Database Migration): Giới thiệu về AWS Database Migration Service (AWS DMS) giúp di chuyển dữ liệu một cách an toàn từ CSDL nguồn (on-premises, EC2, hoặc RDS) sang CSDL đích (EC2, RDS, S3, Kafka, Kinesis, DocumentDB, DynamoDB...) với thời gian gián đoạn (downtime) tối thiểu nhờ tính năng đồng bộ hóa liên tụ

* **Nội dung**
  * Menu của Workshop được chia làm 7 phần lớn với các bước thao tác chi tiết:
  * **Bắt đầu**
    * Đăng nhập vào AWS: Hướng dẫn các bước truy cập vào tài khoản AWS để thực hành
    * Tạo cặp khóa (Key Pair): Hướng dẫn tạo cặp khóa bảo mật để lát nữa truy cập từ xa
    * Chuẩn bị môi trường: Thiết lập hạ tầng cơ bản (mạng VPC, quyền IAM...)
    * Kết nối tới máy ảo EC2 và cài đặt Schema Conversion Tool: Hướng dẫn truy cập máy ảo AWS EC2 từ xa để cài đặt ứng dụng SCT

  * **Chọn nguồn dữ liệu cho DMS**
    * Nguồn Oracle:
      * Kết nối tới CSDL nguồn Oracle
      * Cấu hình CSDL nguồn
    * Nguồn SQL Server:
      * Mở SQL Server Management Studio (SSMS)
      * Cấu hình CSDL nguồn - MS SQL Server

  * **Chọn CSDL đích cho DMS**
    * Quá trình chuyển đổi lược đồ:
      * Cấp quyền trong CSDL đích
      * Tạo dự án (Project) trong SCT
      * Chuyển đổi lược đồ

    * **Data Migration:**
      * Configure the Target Database: Cấu hình chi tiết các loại CSDL đích bao gồm: a. RDS Microsoft SQL Server, b. Aurora (MySQL compatible), và c. Aurora (PostgresSQL compatible)
      * Create a replication instance: Tạo một máy chủ trung gian thực hiện nhiệm vụ sao chép dữ liệu của DMS
      * Create DMS Source and Target Endpoints: Tạo các điểm kết nối đầu vào (Nguồn) và đầu ra (Đích) cho DMS
      * Create a DMS Migration Task: Khởi tạo các tác vụ di chuyển dữ liệu cụ thể
      * Inspect the Content of Target Database: Kiểm tra kết quả dữ liệu đã sang CSDL đích chưa, hỗ trợ kiểm tra trên: a. Microsoft SQL Server, b. Aurora MySQL, c. Aurora PostgreSQL, d. Oracle, và e. Amazon S3
      * Replicate Data Changes: Thiết lập cơ chế đồng bộ (CDC - Change Data Capture) để sao chép các thay đổi phát sinh theo thời gian thực

  * **Sao chép dạng không máy chủ**
    * Dịch chuyển dữ liệu sử dụng DMS Serverless:
      * Tạo quá trình dịch chuyển serverless (Hệ thống tự động co giãn tài nguyên thay vì phải quản lý Replication Instance)
      * AWS DMS Serverless - Các giai đoạn sao chép

    * Kiểm thử hoạt động mở rộng quy mô của DMS Serverless:
      * Tạo khối lượng xử lý trên CSDL nguồn (Tạo tải giả lập)
      * Giám sát sự kiện mở rộng quy mô (Scale-up)
      * Giám sát sự kiện thu nhỏ quy mô (Scale-down)

  * **Theo dõi DMS Migrations**
    * Các số liệu trên CloudWatch: Theo dõi biểu đồ tài nguyên (CPU, Memory, Network...)
    * Thông báo sự kiện (Event Notifications): Cấu hình gửi cảnh báo khi tác vụ có thay đổi
    * Table Statistics: Xem thống kê chi tiết số lượng dòng, trạng thái của từng bảng dữ liệu
    * Task Logs: Kiểm tra log hệ thống để giám sát hoạt động chi tiết
    * Các trạng thái của tác vụ: Giải thích ý nghĩa các trạng thái (Running, Stopped, Failed...)
    * RunBook: Cẩm nang hướng dẫn vận hành chuẩn khi chạy di dời dữ liệu

  * **Xử lý sự cố với AWS DMS**
    * Áp lực bộ nhớ lên DMS Instance:
      * Tạo môi trường (Giả lập tình huống lỗi quá tải bộ nhớ RAM)
      * Troubleshooting Steps: Các bước phân tích nguyên nhân
      * Giải pháp: Cách khắc phục (tăng cấu hình instance, tối ưu bộ nhớ đệm)

    * **Lỗi bảng trong tác vụ DMS:**
      * Tạo môi trường (Giả lập lỗi ở một số bảng cụ thể)
      * Các bước tìm lỗi
      * Giải pháp: Cách reload lại bảng bị lỗi hoặc bỏ qua lỗi để chạy tiếp

* **Dọn dẹp môi trường**
  * Hướng dẫn các bước xóa tài nguyên sau khi thực hành xong để tránh phát sinh chi phí ngoài ý muốn:
    * Xóa Serverless Migration Task
    * Xóa Database Migration Task
    * Xóa các DMS Endpoint
    * Delete the DMS Replication Instance
    * Delete the CloudFormation Stack
    * Delete S3 Bucket and IAM Roles

## Thứ 3: Thực hành Amazon S3 và Triển khai Static Website
* **Giới thiệu về Amazon S3**
  * Phần này giải thích chi tiết Amazon S3 là object storage service cung cấp khả năng mở rộng linh hoạt, độ sẵn sàng cao, bảo mật và hiệu suất tốt
  * Nhấn mạnh độ bền 99.999999999% (11 9’s)
  * So sánh rõ ràng Bucket (container globally unique, chứa objects, áp dụng policy chung) và Object (tập tin dữ liệu thực tế bên trong bucket, có key name, metadata, kích thước lên đến 5TB)
  * Trình bày các storage classes (Standard, Intelligent-Tiering, Standard-IA, Glacier...), tính năng bảo mật (encryption, IAM, bucket policy, ACL), quản lý (versioning, lifecycle, replication), performance và các use case thực tế như static website, backup, data lake, media storage

* **Chuẩn bị**
  * Hướng dẫn các bước chuẩn bị ban đầu: tạo S3 bucket và upload toàn bộ dữ liệu website (folder chứa HTML, CSS, JS, images...) để sẵn sàng cho việc host static website

* **Kích hoạt Static Website Hosting**
  * Giải thích static website hosting là gì (phục vụ nội dung tĩnh trực tiếp từ S3 mà không cần server). Lợi ích: chi phí thấp, scalable, reliable
  * Hướng dẫn chi tiết: Vào tab Properties của bucket → Static website hosting → Enable → Chọn “Host a static website” → Đặt Index document là index.html (có thể thêm Error document)
  * Sau khi bật sẽ có website endpoint dạng http://bucket-name.s3-website-region.amazonaws.com

* **Cấu hình Block Public Access**
  * Giải thích lý do cần Block Public Access và cách tắt nó tạm thời cho lab (cảnh báo mạnh về bảo mật)
  * Các bước: Vào bucket → Block public access → Bỏ tick “Block all public access” → Save changes và confirm

* **Cấu hình Public Objects**
  * Chi tiết về mô hình permission của S3 (Bucket policy, ACL, IAM)
  * Hướng dẫn: Enable ACLs bằng cách chỉnh Object Ownership sang “ACLs enabled” và “Bucket owner preferred”
  * Sau đó chọn objects (hoặc folder) → Actions → Make public using ACL. Có ví dụ bucket policy JSON để public read và khuyến nghị dùng CloudFront cho production

* **Kiểm tra Website**
  * Hướng dẫn kiểm tra thực tế: vào Objects → chọn index.html → copy Object URL → mở browser để xem giao diện website đã hoạt động

* **Tăng tốc website bằng CloudFront**
  * Giới thiệu cách kết hợp CloudFront để tăng tốc, thêm HTTPS và bảo vệ bucket (không cần public trực tiếp)
  * Có note kỹ thuật về S3 website endpoint vs OAC (Origin Access Control). Bao gồm chi phí ước tính và các bước thiết lập distribution

* **Bucket Versioning**
  * Giải thích versioning giúp giữ nhiều phiên bản object, bảo vệ khỏi xóa nhầm hoặc ghi đè. Cách hoạt động, các trạng thái (Enabled/Suspended)
  * Thực hành: Bật versioning → chỉnh sửa file index.html locally → upload lại → bật Show versions để xem và khôi phục version cũ. Kết hợp test với CloudFront bằng cách chỉnh TTL

* **Move Objects**
  * Hướng dẫn di chuyển objects giữa các bucket: tạo bucket đích → chọn tất cả objects ở bucket nguồn → Actions → Move → chọn destination
  * Sử dụng checksum để đảm bảo tính toàn vẹn dữ liệu

* **Replication Object đa Region**
  * Giải thích CRR dùng để sao chép tự động objects sang region khác phục vụ disaster recovery, compliance, giảm latency. Yêu cầu bật versioning cả hai bucket
  * Các bước: Tạo bucket đích ở region khác → tạo replication rule → cấu hình IAM role → test bằng cách upload file mới và kiểm tra replication

* **Dọn dẹp tài nguyên**
  * Hướng dẫn xóa sạch tài nguyên sau lab: Empty bucket trước rồi Delete bucket; Disable rồi Delete CloudFront distribution để tránh phát sinh chi phí

## Thứ 4: Triển khai Grafana và Xây dựng Dashboard Giám sát AWS CloudWatch
* **Giới thiệu về Grafana**
  * Grafana là công cụ mã nguồn mở dùng để visualize và phân tích dữ liệu
  * Nó giúp kéo metrics từ nhiều nguồn khác nhau, tạo dashboard tùy chỉnh, query, visualize, đặt alert và khám phá metrics dù dữ liệu lưu trữ ở đâu
  * Grafana biến dữ liệu time-series thành các biểu đồ đẹp mắt
  * Nó hỗ trợ kết nối với Graphite, Prometheus, InfluxDB, Elasticsearch, MySQL, PostgreSQL...
  * Ngoài phiên bản open source còn có Grafana Cloud và Grafana Enterprise cho doanh nghiệp

* **Các tính năng nổi bật**
  * Visualize: Tạo biểu đồ linh hoạt với nhiều lựa chọn
  * Dynamic Dashboards: Dashboard động sử dụng template variables (dropdown)
  * Explore Metrics: Khám phá dữ liệu qua query ad-hoc, so sánh nhiều khoảng thời gian
  * Explore Logs: Chuyển từ metrics sang logs, tìm kiếm live (tốt nhất với Loki)
  * Alerting: Định nghĩa rule alert và gửi thông báo qua Slack, PagerDuty, VictorOps, OpsGenie
  * Mixed Data Sources: Kết hợp nhiều nguồn dữ liệu trong cùng một panel
  * Annotations: Thêm ghi chú sự kiện lên biểu đồ
  * Ad-hoc Filters: Tạo filter động key/value

* **Các bước thực hiện chi tiết**
  * Tạo VPC và Subnet:
    * Tạo VPC tên Grafana-ASG, CIDR 10.0.0.0/16
    * Tạo subnet public, bật auto-assign public IPv4 address

  * Tạo Security Group (SG-PUB-Grafana-ASG):
    * Inbound rules cho phép: SSH, All ICMP-IPv4, All ICMP-IPv6, Custom TCP
    
  * Tạo EC2 Instance (Grafana-Server):
    * AMI: Amazon Linux
    * Instance type: Chọn phù hợp
    * Tạo Key Pair (GrafanaKeyPair - RSA .pem)
    * Networking: Chọn VPC và subnet public vừa tạo, enable Auto-assign public IP
    * Security Group: Sử dụng SG-PUB-Grafana-ASG
    
  * Tạo IAM User (Grafana-user):
    * Cho phép programmatic access (Access Key) và console access
    * Attach policy AdministratorAccess
    * Tải file .csv chứa Access Key ID và Secret Access Key

  * Tạo IAM Role (GrafanaAccessRole):
    * Tạo policy GrafanaAccessPolicy với quyền CloudWatch (DescribeAlarmsForMetric, ListMetrics, GetMetricStatistics, GetMetricData), EC2 (DescribeTags, DescribeInstances, DescribeRegions), và tag:GetResources
    * Role cho EC2 service, attach policy trên

  * Gán IAM Role cho EC2 instance Grafana-Server qua Modify IAM role

  * **Cài đặt Grafana trên EC2**
    * Kết nối instance qua PuTTY (sử dụng Public IP và key pair) hoặc MobaXterm
    * Cập nhật: sudo yum update -y
    * Tạo repo: sudo nano /etc/yum.repos.d/grafana.repo và dán nội dung repo chính thức
    * Cài đặt: sudo yum install grafana
    * Quản lý service:
      * sudo systemctl daemon-reload
      * sudo systemctl start grafana-server
      * sudo systemctl status grafana-server
      * sudo systemctl enable grafana-server.service
  * Truy cập: http://Public_IP:3000, login admin/admin, đổi password lần đầu

  * **Monitoring với Grafana**
    * Thêm Data Source CloudWatch:
      * Name: CloudWatch-Grafana
      * Authentication: Access & Secret Key của IAM User
      * Save & Test

    * Tạo Dashboard mới:
      * Thêm panel → Namespace: AWS/EC2
      * Metric: CPUUtilization, Statistic: Average
      * Dimension: InstanceId của Grafana-Server
      * Apply, refresh, lưu dashboard (Grafana-Monitoring)
    * Share dashboard qua link
    * Sử dụng Explore để query metric tương tự

  * **Dọn dẹp tài nguyên**
    * Terminate instance Grafana-Server trong EC2 console
    * Xóa VPC trong VPC console

## Thứ 5: Bảo vệ ứng dụng web với AWS Web Application Firewall (AWS WAF)
* **Giới thiệu về AWS Web Application Firewall**
  * AWS WAF (AWS Web Application Firewall) là dịch vụ tường lửa ứng dụng web
  * Nó giúp bảo vệ các ứng dụng web hoặc API của bạn khỏi những khai thác web phổ biến có thể ảnh hưởng đến tính sẵn sàng, làm tổn hại đến bảo mật, hoặc tiêu tốn quá nhiều tài nguyên
  * Sử dụng WAF là cách tuyệt vời để tăng cường lớp bảo vệ cho ứng dụng web. WAF giúp giảm thiểu rủi ro từ các lỗ hổng như SQL Injection, Cross Site Scripting (XSS) và các cuộc tấn công phổ biến khác (được liệt kê trong OWASP Top 10)
  * WAF cho phép bạn tạo các quy tắc (rules) tùy chỉnh để quyết định chặn hoặc cho phép các yêu cầu HTTP trước khi chúng đến ứng dụng

* **Sử dụng AWS WAF**
  * Tạo Web ACL từ bảng điều khiển WAF
  * Tạo Rule cho WAF
  * Kiểm tra các Rule mới
  * Ghi log các yêu cầu

  * **Web ACLs với managed rules**
    * Tình huống
      * Bạn là lập trình viên duy nhất cho startup Juice Shop. Website của bạn là một ứng dụng web đơn giản chạy trên cơ sở dữ liệu SQL. Vì một lý do nào đó, một nhóm “Milkshake bandits” đã bắt đầu tấn công trang web của bạn!
      * May mắn thay, bạn vừa tham gia workshop về AWS WAF. Bạn quyết định triển khai WAF để bảo vệ trang web. Hiện tại bạn không có nhiều thời gian, nên bạn chọn triển khai hai nhóm quy tắc Managed Rule của AWS vào Web ACL để bảo vệ website khỏi các cuộc tấn công phổ biến mà bọn Milkshake bandits đang sử dụng

    * Web ACLs với managed rules
      * Web ACL (Web Access Control List) là tài nguyên cốt lõi trong triển khai AWS WAF. Nó chứa các quy tắc được đánh giá cho từng yêu cầu nhận được. Web ACL được liên kết với ứng dụng web qua Amazon CloudFront, AWS API Gateway hoặc AWS Application Load Balancer
      * Managed rule groups là tập hợp các quy tắc được AWS hoặc bên thứ ba trên AWS Marketplace tạo và duy trì. Những quy tắc này cung cấp khả năng bảo vệ chống lại các loại tấn công phổ biến hoặc dành cho các loại ứng dụng cụ thể

    * Các bước thực hiện:
      * Truy cập AWS WAF Console. Workshop này sử dụng phiên bản mới nhất của AWS WAF (không dùng WAF Classic)
      * Nhấn Create web ACL
      
    * Trong phần Web ACL details:
      * Chọn Resource type: CloudFront distributions
      * Name: waf-workshop-juice-shop
      * Description: Web ACL for the aws-waf-workshop

    * Trong phần Associated AWS resources: Nhấn Add AWS resources, chọn CloudFront distribution đã tạo (E24BURECS1O10C - dkievcmqb5kzc.cloudfront.net), sau đó nhấn Add

    * Trong phần Rules:
      * Nhấn Add rules → Add managed rule groups
      * Chọn AWS managed rule groups
      * Chọn Core Rule Set và SQL Database
      * Thêm rules, thiết lập thứ tự ưu tiên, metrics, rồi nhấn Create web ACL

  * Kiểm tra:
    * Chạy lệnh curl mô phỏng tấn công XSS (phải bị chặn):
      ```bash
      curl -X POST <Your Juice Shop URL> \
      -F "user='<script><alert>(Hello)></alert></script>'"
      ```
      
    * Chạy lệnh curl mô phỏng SQL Injection (phải bị chặn):
      * Bash curl -X POST <Your Juice Shop URL> -F "user='AND 1=1;"

* **Custom Rule**
  * Tình huống
    * Khi bạn vừa nghĩ đã giải quyết xong vấn đề Milkshake, lại có thêm nhiều yêu cầu độc hại nhắm vào ứng dụng. Các cuộc tấn công trở nên cụ thể hơn. Bạn nhận ra có thể chặn chúng bằng một custom rule trong Web ACL. Tất cả các cuộc tấn công dường như đều chứa header lạ là X-TomatoAttack. Chặn các request chứa header này sẽ dừng cuộc tấn công

  * Tạo Custom Rule
    * WAF cho phép bạn tạo quy tắc riêng để xử lý request. Điều này rất hữu ích để thêm logic phù hợp với ứng dụng cụ thể. Phần này cũng giới thiệu request sampling và Web ACL Capacity Units (WCU)

  * Các bước:
    * Trong trang chi tiết Web ACL:
      * Nhấn Rules → Add Rules → Add my own rules and rule groups

    * Trong Rule builder:
      * Name: MyCustomRule-X-TomatoAttack.

    * Trong Statement:
      * Inspect: Single header
      * Header field name: X-TomatoAttack
      * Match type: Size greater than or equal to
      * Size in bytes: 0

    * Action: Block → Add rule → Save

    * Kiểm tra:
      * Bash curl -H "X-TomatoAttack: Red" "<Your Juice Shop URL>"
      * curl -H "X-TomatoAttack: Green" "<Your Juice Shop URL>"

    * Kiểm tra phần Sampled requests trong Overview để thấy request bị BLOCK

* **Advanced Custom Rule**
  * Tình huống
    * Bọn Milkshake bandits quay lại tấn công. Chúng đã thay đổi cách tấn công! Bạn cần cập nhật rule để chặn request độc hại nhưng vẫn cho phép khách hàng thật

  * Tạo Advanced Custom Rule
    * Tất cả rule của WAF đều được định nghĩa dưới dạng đối tượng JSON. Với rule phức tạp, làm việc trực tiếp với JSON sẽ hiệu quả hơn

  * Rule ban đầu (JSON):
    * Rule sẽ chặn request chứa header x-milkshake: chocolate hoặc query parameter milkshake=banana

  * Cập nhật Rule (phiên bản nâng cao):
    * Cập nhật JSON để chặn khi thỏa mãn điều kiện AND:
      * Header x-milkshake: chocolate VÀ x-favourite-topping: nuts
      * Hoặc query milkshake=banana VÀ favourite-topping=sauce

  * Kiểm tra:
    * Các lệnh được phép
    * Các lệnh bị chặn (trả về lỗi 403 HTML)

* **Testing New Rules**
  * Trước khi triển khai rule mới, việc kiểm tra là rất quan trọng để tránh chặn nhầm request hợp lệ
  * Sử dụng action Count (chỉ đếm, không chặn thực sự). Web ACL sẽ tiếp tục xử lý các rule còn lại

  * Rule test (JSON):
    * Tạo rule đếm request có query parameter username

  * Chạy lệnh test:
    * Bash curl "<Your Juice Shop URL>?username=admin"
  
  * Kiểm tra metric trong CloudWatch → WAFv2 → Rule, WebACL

* **Log the requests**
  * Tình huống
    * Juice Shop đang phát triển nhanh chóng. Với nhiều rule, khó xác định rule nào chịu trách nhiệm chặn request. Bạn cần ghi log. Ngoài ra, log chứa thông tin nhạy cảm (header Cookie), nên cần cấu hình redaction (ẩn) trường này

  * Các bước thực hiện:
    * Tạo Kinesis Data Firehose (region us-east-1):
      * Source: Direct PUT, Destination: Amazon S3
      * Tên: aws-waf-logs-workshop-26
      * Chọn S3 bucket aws-waf-logs-001

    * Trong Web ACL → tab Logging and metrics → Enable:
      * Chọn Kinesis stream
      * Redacted fields: Single header Cookie

    * Chạy một số lệnh curl test
    * Tải file log từ S3 và kiểm tra (Cookie đã bị ẩn)

  * Kết luận: WAF cho phép ghi log request qua Kinesis Firehose, hỗ trợ redaction thông tin nhạy cảm. Log cung cấp thông tin request, action và rule liên quan – rất hữu ích khi vận hành WAF

* **Dọn dẹp tài nguyên**
  * Dọn dẹp theo thứ tự sau để tránh phát sinh chi phí:
    * Xóa sample web
      * Vào CloudFormation Console → Chọn WAFWorkshopSampleWebApp → Delete

    * Xóa Web ACL
      * Vào WAF Console → Web ACLs → Chọn waf-workshop-juice-shop → Delete

    * Xóa Kinesis
      * Vào Kinesis Console → Delivery streams → Chọn aws-waf-logs-workshop-26 → Delete

    * Xóa S3 bucket
      * Vào S3 Console → Chọn bucket aws-waf-logs-001 → Empty (nhập "permanently delete" để xác nhận) → Delete bucket