---
title: "Week 4 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
---

### Week 4 Objectives:

* Mastering AWS storage services (Amazon S3 and advanced features, Storage Gateway, Snow Family, AWS Backup) and Disaster Recovery strategies
* Proficient in designing and deploying Amazon VPC according to best practices (Multi-AZ, network security, NAT Gateway, VPC Flow Logs, Session Manager
* Establishing secure Hybrid Cloud connectivity via Site-to-Site VPN
* Configuring bi-directional Hybrid DNS between AWS and On-premise environments using Route 53 Resolver (Inbound/Outbound Endpoints + Resolver Rules)

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
|  2  | - Amazon S3 Core Features, Storage Classes, Glacier, Snow Family, Storage Gateway, DR Strategies (RTO/RPO) and AWS Backup | 11/05/2026 | 11/05/2026 | <https://youtu.be/_yunukwcAwc/> <br> <https://youtu.be/mPBjB6Ltl_Q> <br> <https://youtu.be/YXn8Q_Hpsu4> |
|  3  | - Build Multi-AZ VPC, network security (SG + NACLs), NAT Gateway, Flow Logs, Session Manager and configure AWS Site-to-Site VPN for Hybrid Cloud | 12/05/2026 | 12/05/2026 | <https://000003.awsstudygroup.com/> |
|  4  | - Configure bidirectional Hybrid DNS between AWS and On-premise using Route 53 Resolver | 13/05/2026 | 13/08/2026 | <https://000010.awsstudygroup.com/> |

### Week 4 Achievements:

## Friday: Storage Services on AWS
  * Amazon Simple Storage Service – S3
  * Amazon Storage Gateway
  * Snow Family
  * Disaster Recovery on AWS
  * AWS Backup

  * **Amazon Simple Storage Service (S3)**
    * Amazon S3 is object-level storage, meaning if you want to change a part of a file, you must modify it and then re-upload the entire modified file
    * S3 is suitable for write-once, read-many (WORM) data types
    * The smallest storage unit in the system is 1 object
    * When storing data this way, to change the content inside an object, you must replace the entire object by overwriting it with a new object
    * Different from block storage but commonly used
    * (WORM – Write Once Read Many)
    * Amazon S3 has no limit on total data storage volume
    * Each object cannot be larger than 5 TB
    * * In the case of Elastic Block Store, 3 replicas are only within 1 Availability Zone
    * By default, data in Amazon S3 is replicated across 3 AZs in 1 Region
    * Amazon S3 has the ability to trigger events, allowing you to automatically trigger actions when certain events occur, such as uploading or deleting an object from a specific storage area
    * These events can trigger serverless functions
    * When uploading data to S3, S3 itself has many background mechanisms to ensure data integrity and uniqueness
    * Amazon S3 is designed to achieve 99.999999999% durability and 99.99% availability
    * Amazon S3 supports multipart upload for uploading large objects to a bucket
    * We need to create S3 buckets to be able to store objects in Amazon S3
      * https://[bucket-name].s3.amazonaws.com
      * https://[bucket-name].s3.amazonaws.com/capture.mp4
    * Working with S3 via REST API (HTTP)

  * **Amazon Simple Storage Service (S3) – Access Point**
    * Amazon S3 Access Point is a feature that allows you to create unique connection points (unique hostnames) for applications, individual users, or groups
    * We can configure different permissions for each Access Point created
    * When multiple applications need to store data inside S3, we had to create separate S3 buckets for each application, making management and access policy management complex and difficult
    * Assigning access rights to each individual bucket leads to risks, operational errors such as missing or excessive permissions, and it is also difficult to track and maintain those policies
    * Now there is a new feature called Access Point, which allows creating multiple connection points with different hostnames for applications
    * However, all these connection points connect to a single bucket
    * Assigning access rights to each application or user becomes much easier than creating multiple S3 buckets
    * Create S3 Access Points for applications with different access permissions

  * **Amazon Simple Storage Service (S3) – Storage Class**
    * Amazon S3 divides storage into multiple storage classes to help us optimize costs
    * S3 Storage Classes:
      * S3 Standard: Frequently accessed data
      * S3 Standard IA: Infrequently accessed data
      * S3 Intelligent Tiering: Automatically moves objects between tiers based on the number of days the object has not been accessed
      * S3 One Zone IA: Data that can be recreated, long-term storage, infrequently accessed but requires fast access
      * Amazon Glacier / Deep Archive: Long-term archival with very infrequent access
    * We can set up automatic data lifecycle management (Object Lifecycle Management) stored in Amazon S3. By using lifecycle policies, we can transition data within an S3 bucket between storage classes according to customized time (days)
    * Having multiple tiers is to optimize costs
    * S3 has 2 main costs: total storage volume of objects uploaded to S3
    * The second is the number of requests to the S3 service, each upload or download (GET request) is also counted, and these two have different pricing
    * For Standard, the storage price is higher but the request price is lower, so frequently accessed data should be stored here
    * For Standard Infrequent Access, data that is not accessed frequently has a slightly lower storage price but higher request price
    * If you put frequently accessed data into Standard Infrequent Access, you will actually pay a higher fee than S3 Standard
    * Object Lifecycle Management will move the object after the number of days we specify, calculated from the day the object was created

  * **Amazon Simple Storage Service (S3) – Static Website & CORS**
    * Amazon S3 has the capability to host static websites (HTML, media, etc.), making it suitable for Single Page Applications (web applications or websites that interact with users by dynamically rewriting the current page with new data from the web server using JavaScript and its frameworks such as AngularJS, ReactJS, instead of the browser’s default method of loading an entirely new page).
    * Amazon S3 supports CORS. CORS is a mechanism that allows various resources (fonts, JavaScript, etc.) of a website to be requested from a domain different from the website’s own domain. CORS stands for **Cross-Origin Resource Sharing**.
    * https://docs.aws.amazon.com/AmazonS3/latest/userguide/cors.html
    * Amazon S3 supports hosting static websites (HTML, media, etc.), which is suitable for Single Page Applications.
    * Amazon S3 allows configuration of CORS (Cross-Origin Resource Sharing) policies, enabling client web applications to interact with resources located on different domains.

  * **Amazon Simple Storage Service (S3) – Access Control**
      * Amazon S3 provides 2 mechanisms for controlling access to buckets
      * **S3 Access Control List (ACL)** is an access control mechanism that existed before IAM. However, if you are already using S3 ACLs and find them sufficient, there is no need to change. S3 ACLs are attached to both buckets and objects. They define which AWS accounts or groups are granted access and the type of access permitted
      * **S3 Bucket Policies** and **IAM Policies** define permissions by specifying the objects in the `Resource` section of the policy. The statement applies to those objects within the bucket. Consolidating object-specific permissions into a single policy (as opposed to multiple S3 ACLs) makes it easier to determine access rights
      * Every object in S3 is at the same level (no hierarchy) and is identified by an **object key**. Example: `/image/sample.jpg`, `sample.jpg`

  * **Amazon Simple Storage Service (S3) – Endpoint & Versioning**
      * **Amazon S3 Endpoints** allow access to S3 buckets through AWS’s private network. By default, access to S3 goes over the public internet
      * You can enable **Versioning**, which allows you to recover objects after accidental deletion or overwriting. It also helps protect against ransomware/encryption attacks
          * When you delete an object, Amazon S3 does not remove it permanently but instead adds a delete marker
          * When you overwrite an object, a new version of the object is created in the bucket
      * => In both cases, you can restore a previous version
      * Versioning allows you to recover objects after accidental deletion or overwriting and provides protection against ransomware/encryption attacks

  * **Amazon Simple Storage Service (S3) – Object Key & Performance**
      * Every object in S3 is at the same level (no hierarchy) and is identified by an **object key**. Example: `/image/sample.jpg`, `sample.jpg`
      * Internally, S3 divides data into **Partitions**. Partitions are automatically split when the number of requests increases or when there are too many object keys in one partition (which slows down object lookup)
      * S3 stores a **key map** (the key map is also divided into multiple partitions and hashed by the prefix of the object key)
      * To optimize S3 performance, you can use **random prefixes** (e.g., `/fscd/img/sample.jpg` instead of `/img/sample.jpg`). The goal is to distribute objects across as many partitions as possible, since S3 performance scales with the number of partitions

  * **Amazon Simple Storage Service (S3) – Glacier**
      * **Amazon S3 Glacier** is a low-cost storage option suitable for data that does not require immediate or frequent access — ideal for long-term archival
      * When data is stored in Amazon S3 Glacier, you cannot access it directly. You must initiate a **retrieve** request to bring the data back to an S3 bucket
      * There are three retrieval options with different access times and costs:
          * **Expedited** – typically completes in 1–5 minutes
          * **Standard** – typically completes in 3–5 hours
          * **Bulk** – typically completes in 5–12 hours
      * Amazon S3 Glacier is a low-cost storage class for long-term data that does not require direct or frequent retrieval.

  * **Snow Family - Storage Gateway - Backup**
      * **Snow Family – Snowball**
          * A service that helps migrate data from on-premise environments to AWS at petabyte (PB) scale. Each Snowball device can hold up to 80 Terabytes (TB)
          * The Snowball device is shipped back to the chosen AWS Region, where the data is loaded into your selected service (S3 or Glacier)
          * You need to install the Snowball Client on your local machine to perform verification, compression, encryption, and data transfer

      * **Snow Family – Snowball Edge**
          * A service that helps migrate data from on-premise environments to AWS at petabyte (PB) scale. Each Snowball Edge device can hold up to 100 Terabytes (TB)
          * The Snowball Edge device is shipped back to the chosen AWS Region
          * It includes built-in compute resources for processing data locally before importing into the device

      * **Snow Family – Snowmobile**
          * A service for migrating data from on-premise to AWS at exabyte scale. Each Snowmobile can hold up to 100 PB.
          * The Snowmobile is shipped back to the chosen AWS Region

      * **AWS Storage Gateway**
          * AWS Storage Gateway is a **hybrid storage** solution that combines AWS cloud storage with on-premise storage capacity.
          * It allows you to leverage the scale and cost-effectiveness of cloud storage for large volumes of data that require long-term retention
          * AWS Storage Gateway supports three main storage interfaces:
              * **File Gateway**: Allows you to store and retrieve objects in Amazon S3 using standard file protocols (NFS and SMB). Objects written through File Gateway can be accessed directly in S3
              * **Volume Gateway**: Provides block storage for your applications using the iSCSI protocol. Data is stored in Amazon S3. You can create EBS snapshots (automatically via AWS Backup) to restore as EBS volumes
              * **Tape Gateway**: Provides a virtual tape library (VTL) interface via iSCSI, including virtual tape drives and virtual tapes. Virtual tape data is stored in Amazon S3 or can be archived to Amazon Glacier
          * AWS Storage Gateway is a hybrid storage solution combining on-premise and cloud storage

  * **Disaster Recovery on AWS**
      * **RTO / RPO**
          * **Recovery Time Objective (RTO)**: The maximum acceptable time to restore a service to normal operation after a disaster
              * Example: If a disaster occurs at 2:00 PM and the RTO is 4 hours, the service must be restored by 6:00 PM at the latest
          * **Recovery Point Objective (RPO)**: The maximum acceptable amount of data loss (measured in time)
              * Example: If backups are performed once per day, in the worst case you could lose 24 hours of data → RPO = 24 hours

      * **Disaster Recovery Strategies on AWS**
          * Different applications have varying complexity and Service Level Agreements (SLAs) with different RTO/RPO requirements. You should choose the appropriate DR strategy accordingly
          * There are **4 main disaster recovery strategies** on AWS:
              * Backup and Restore
              * Pilot Light (Active–Standby)
              * Warm Standby (Low Capacity Active–Active)
              * Multi-Site Active–Active (Full Capacity)

      * **AWS Backup**
          * AWS Backup is a centralized service to manage backup tasks. You can configure backup schedules, retention policies, and monitor backup activities for various AWS resources, including:
              * Amazon EBS
              * Amazon EC2
              * Amazon RDS databases
              * DynamoDB
              * Amazon EFS
              * AWS Storage Gateway volumes

## Thứ 2: Bắt đầu với Amazon Virtual Private Cloud (VPC) và AWS Site-to-Site VPN
  * **Mô tả:** Workshop hướng dẫn xây dựng và quản lý Amazon VPC kết hợp AWS Site-to-Site VPN. Bạn sẽ thực hành thiết kế mạng ảo, triển khai EC2, cấu hình bảo mật và thiết lập kết nối VPN an toàn giữa on-premise và AWS Cloud.

  * **Mục tiêu chính:**
      * Thiết kế và triển khai VPC theo AWS Well-Architected Framework
      * Cấu hình các thành phần bảo mật mạng (Security Groups, NACLs)
      * Thiết lập kết nối an toàn giữa môi trường on-premise và AWS qua Site-to-Site VPN

  * **Kiến thức thu được:**
      * Thiết kế và triển khai VPC theo best practices
      * Cấu hình bảo mật mạng đa tầng
      * Thiết lập VPN kết nối Hybrid Cloud

  * **Tính năng Production-Ready:**
      * Multi-AZ NAT Gateways
      * VPC Flow Logs
      * CloudWatch monitoring & alerting
      * Systems Manager Session Manager
      * Infrastructure as Code (IaC) templates

  * **Giới thiệu Amazon VPC**
    * **Mô tả:** Amazon Virtual Private Cloud (Amazon VPC) là dịch vụ mạng ảo tùy chỉnh nằm trong AWS Cloud, cho phép tạo môi trường mạng riêng biệt hoàn toàn tách biệt với thế giới bên ngoài.

    * **Tính năng chính:**
        * Kiểm soát hoàn toàn môi trường mạng ảo
        * Tùy chỉnh phạm vi địa chỉ IP (CIDR block)
        * Cấu hình định tuyến và kết nối mạng linh hoạt
        * Hỗ trợ đầy đủ IPv4 và IPv6

    * **Kiến trúc:**
        * Mỗi VPC thuộc một Region và chứa nhiều Availability Zones (AZ)
        * CIDR block từ /16 đến /28
        * CIDR block không thể thay đổi sau khi tạo
        * Mỗi Region có VPC mặc định (172.31.0.0/16)

  * **Tường lửa trong VPC (Network Security)**
    * **Hai lớp bảo mật chính:**
        * Security Groups (cấp Instance - Stateful)
        * Network ACLs (cấp Subnet - Stateless)

    * **Security Groups:**
        * Tường lửa ảo cho từng EC2 instance
        * Mỗi instance có thể gán tối đa 5 Security Groups
        * Kiểm soát chi tiết inbound và outbound traffic

    * **Mô hình bảo mật:**
        * Kết hợp Security Groups + Network ACLs để tạo lớp bảo mật đa tầng

  * **Chuẩn bị Môi trường (Prerequisite)**
    * Xây dựng môi trường VPC hoàn chỉnh từ đầu
    * Triển khai các thành phần mạng cơ bản của AWS
    * Thiết lập cấu trúc mạng an toàn và có khả năng mở rộng

  * **Các Thành phần Chính:**
    * VPC - Môi trường mạng ảo riêng biệt
    * Subnet - Phân đoạn mạng cho các tài nguyên
    * Internet Gateway - Cổng kết nối internet
    * Route Table - Bảng định tuyến lưu lượng mạng
    * Security Group - Tường lửa cấp instance
  
  * **Tạo VPC**
    * **Mục tiêu:**
      * Tạo môi trường mạng ảo riêng biệt trong AWS
      * Thiết lập không gian địa chỉ IP cho VPC
      * Cấu hình các tính năng DNS cơ bản

    * **Các bước thực hiện:**
      * Truy cập **AWS Management Console** → Tìm kiếm và chọn **VPC**
      * Trong **VPC Dashboard** → Chọn **Your VPCs** → Click **Create VPC**
      * **Resources**: Chọn **VPC only**
      * **Name tag**: `ASG`
      * **IPv4 CIDR**: `10.10.0.0/16`
      * Giữ **Tenancy** ở chế độ mặc định (Default)
      * Click **Create VPC**

    * **Cấu hình DNS (Quan trọng):**
      * Chọn VPC vừa tạo → **Actions** → **Edit VPC settings**
      * Bật **DNS hostnames** và **DNS resolution**
      * Lưu thay đổi

  * **Tạo Subnet**
    * **Tổng quan:** Subnet là phân đoạn mạng con trong VPC, cho phép phân phối tài nguyên theo Availability Zone (AZ) và phân loại Public/Private

    * **Các bước tạo Subnet:**
      * **Public Subnet 1**
        * Name: `Public Subnet 1`
        * AZ: `ap-southeast-1a`
        * CIDR: `10.10.1.0/24`

      * **Public Subnet 2**
        * Name: `Public Subnet 2`
        * AZ: `ap-southeast-1b`
        * CIDR: `10.10.2.0/24`

      * **Private Subnet 1**
        * Name: `Private Subnet 1`
        * AZ: `ap-southeast-1a`
        * CIDR: `10.10.3.0/24`

      * **Private Subnet 2**
        * Name: `Private Subnet 2`
        * AZ: `ap-southeast-1b`
        * CIDR: `10.10.4.0/24`

    * **Cấu hình Auto-assign Public IP:**
      * Bật tính năng này cho cả 2 Public Subnet (cho phép EC2 tự động nhận Public IP)

  * **Tạo Internet Gateway**
    * **Tổng quan:** Internet Gateway (IGW) cho phép tài nguyên trong VPC kết nối với internet hai chiều

    * **Các bước thực hiện:**
      * Vào **Internet Gateways** → **Create internet gateway**
      * Name: `Internet Gateway`
      * Click **Create**
      * **Actions** → **Attach to VPC** → Chọn VPC `ASG`
      * Xác nhận trạng thái **Attached**

  * **Tạo Route Table**
    * **Tổng quan:** Route Table định tuyến lưu lượng mạng trong VPC

    * **Các bước thực hiện:**
      * Vào **Route Tables** → **Create route table**
      * Name: `Route table-Public`
      * Chọn VPC `ASG`
      * Tạo xong → **Edit routes** → Thêm route:
        * Destination: `0.0.0.0/0`
        * Target: Internet Gateway (IGW đã tạo)
      * **Subnet associations** → Gắn 2 Public Subnet vào Route Table này

  * **Tạo Security Group**
    * **Public Subnet - SG**
      * Name: `Public subnet - SG`
      * Description: `Allow SSH and Ping for servers in public subnet`
      * Inbound:
        * SSH (port 22) → Source: My IP
        * All ICMP - IPv4 → Anywhere (cho phép ping)

    * **Private Subnet - SG**
      * Name: `Private subnet - SG`
      * Inbound:
          * SSH → Source: Security Group của Public Subnet
          * All ICMP - IPv4 → Anywhere

    * **VPC-Endpoints-SG** (bổ sung)
      * Name: `VPC-Endpoints-SG`
      * Inbound: HTTPS từ CIDR VPC (`10.10.0.0/16`)

  * **Kích hoạt VPC Flow Logs**
    * **Mục đích:** Ghi lại lưu lượng IP để giám sát bảo mật, khắc phục sự cố và kiểm toán

    * **Các bước thực hiện:**
      * Chọn VPC `ASG` → Tab **Flow logs** → **Create flow log**
      * Filter: **All**
      * Maximum aggregation interval: **1 minute**
      * Destination: **CloudWatch Logs**
      * Log group: `/aws/vpc/flowlogs`
      * IAM Role: Tạo mới
      * Tạo Flow Log

    * **Thông tin quan trọng:**
      * Flow Logs ghi srcaddr, dstaddr, ports, protocol, action (ACCEPT/REJECT), bytes, packets...
      * Có độ trễ vài phút
      * Hữu ích cho production monitoring và security analysis

  * **Triển khai Amazon EC2 Instances**
    * **Tính năng Production-Ready:**
      * Kiến trúc Multi-AZ
      * NAT Gateways High-Availability
      * Phương thức truy cập an toàn (SSH và Session Manager)
      * Giám sát CloudWatch metrics và alerting
      * VPC Reachability Analyzer

    * **Tạo máy chủ EC2**
      * **Tổng quan:** Tạo hai EC2 instances: một trong Public Subnet (có Public IP) và một trong Private Subnet (chỉ Private IP)

      * **Tạo EC2 Public Instance:**
        * Name: EC2 Public
        * AMI: Amazon Linux 2
        * Subnet: Public Subnet 1
        * Auto-assign Public IP: Enable
        * Security Group: Public subnet - SG
        * Key Pair: aws-keypair (RSA .pem)

      * **Tạo EC2 Private Instance:**
        * Name: EC2 Private
        * AMI: Amazon Linux 2
        * Subnet: Private Subnet 2
        * Auto-assign Public IP: Disable
        * Security Group: Private subnet - SG
        * Key Pair: aws-keypair

    * **Kiểm tra kết nối**

      * **Mô tả:** Kiểm tra khả năng kết nối đến các EC2 instances (SSH vào Public instance và ping giữa các instance)

    * **Tạo NAT Gateway**
      * **Tổng quan:** NAT Gateway cho phép instances trong Private Subnet kết nối ra internet một cách an toàn (outbound only)

      * **Các bước tạo Elastic IP:**
        * Vào EC2 Dashboard → Elastic IPs
        * Allocate Elastic IP address (Amazon’s pool)

      * **Tạo NAT Gateway:**
        * Name: NAT gateway
        * Subnet: Public Subnet 2
        * Connectivity type: Public
        * Gắn Elastic IP vừa tạo

      * **Cấu hình Route Table Private:**
        * Tạo Route Table mới: Route table - Private
        * Gắn hai Private Subnets vào Route Table
        * Thêm route: Destination 0.0.0.0/0 → Target: NAT Gateway

      * **Kiểm tra:** Thực hiện ping test từ EC2 Private Instance ra internet

    * **Sử dụng Reachability Analyzer**
      * **Mô tả:** Công cụ phân tích khả năng kết nối mạng giữa các tài nguyên trong VPC (kiểm tra reachability giữa Public và Private instances)

    * **Tạo EC2 Instance Connect Endpoint (Optional)**
      * **Mô tả:** Cấu hình endpoint để kết nối EC2 mà không cần Public IP hoặc bastion host

    * **AWS Systems Manager Session Manager**
      * **Tổng quan:** Truy cập shell an toàn qua console mà không cần SSH key, không mở port inbound, và có khả năng audit đầy đủ

      * **Lợi ích chính:**
        * Không cần quản lý SSH keys
        * Không cần mở port 22
        * Tất cả session được ghi log và kiểm toán
        * Kiểm soát truy cập qua IAM
        * Giảm chi phí (không cần bastion host)

      * **Điều kiện tiên quyết:**
        * Tạo IAM Role EC2-SessionManager-Role với policy AmazonSSMManagedInstanceCore
        * Gắn role này vào cả hai EC2 instances (Public và Private)

      * **Tạo VPC Endpoints (cho Private Subnet):**
        * SSM Endpoint
        * SSM Messages Endpoint
        * EC2 Messages Endpoint
        * Sử dụng Security Group VPC-Endpoints-SG

      * **Sử dụng Session Manager:**
        * Vào Systems Manager → Session Manager → Start session
        * Chọn instance và bắt đầu session shell trực tiếp trên browser

    * **CloudWatch Monitoring & Alerting**
      * **Mô tả:** Cấu hình giám sát metrics cho EC2 instances và thiết lập alarm khi có sự cố

  * **Thiết lập AWS Site-to-Site VPN**
    * Tạo kết nối bảo mật IPSec giữa data center on-premise và Amazon VPC
    * Hỗ trợ cả thiết bị VPN phần cứng và phần mềm
    * Mỗi kết nối bao gồm 2 IPSec tunnels để đảm bảo high availability

    * **Thành phần chính**
      * Virtual Private Gateway (VPG): Điểm cuối VPN phía AWS
      * Customer Gateway (CGW): Đại diện cho thiết bị VPN phía khách hàng
      * VPN Connection: Kết nối IPSec giữa VPG và CGW

    * **Đặc điểm quan trọng**
      * Mỗi kết nối có 2 tunnels cho tính sẵn sàng cao
      * Hỗ trợ static routing và dynamic routing (BGP)
      * Một VPG có thể kết nối với nhiều CGW
      * AWS cung cấp file cấu hình chi tiết cho nhiều loại thiết bị

    * **Tạo môi trường VPN (Tạo VPC mô phỏng Branch Office)**
      * Tạo VPC mới tên ASG VPN
      * Tạo các Subnet (Public/Private)
      * Tạo Internet Gateway, Route Table
      * Triển khai EC2 instance trong VPC mới
      * Cấu hình Security Group và kiểm tra kết nối cơ bản

    * **Cấu hình kết nối VPN (Phần chính)**
      * **Tạo Virtual Private Gateway**
        * Tạo VPG và attach vào VPC chính (ASG)

      * **Tạo Customer Gateway**
        * Tạo CGW với Public IP của thiết bị VPN phía khách hàng (hoặc VPC thứ hai)

      * **Tạo kết nối VPN**
        * Tạo VPN Connection giữa VPG và CGW
        * Chọn static hoặc dynamic routing

      * **Cấu hình Customer Gateway**
        * Tải file cấu hình VPN từ AWS
        * Áp dụng cấu hình cho thiết bị hoặc phần mềm VPN (strongSwan, Libreswan...)

      * **Tùy chỉnh AWS VPN Tunnel**
        * Chỉnh sửa tunnel options (IKE, IPsec parameters)
        * Cấu hình Dead Peer Detection (DPD)
        * Tối ưu hóa hiệu suất tunnel

      * **Cấu hình VPN Nâng cao**
        * Sử dụng strongSwan thay thế
        * BGP dynamic routing cho automatic failover
        * Cấu hình IKEv2 và bảo mật nâng cao

      * **Hướng dẫn Troubleshooting VPN**
        * Xử lý vấn đề trên Amazon Linux 2023
        * Migration từ OpenSwan sang Libreswan
        * Cập nhật service management

      * **Hướng dẫn Troubleshooting Chính thức từ AWS**
        * Framework theo thứ tự: IKE → IPsec → Tunnel → Routing
        * Tích hợp CloudWatch monitoring
        * Hướng dẫn cho các thiết bị Cisco, Juniper...

    * **Cấu hình VPN bằng strongSwan với Transit Gateway (Tùy chọn)**
      * Tạo Transit Gateway
      * Tạo VPN Connection với Transit Gateway
      * Cấu hình route propagation
      * Sử dụng strongSwan trên EC2 làm Customer Gateway

  * **Dọn dẹp Tài nguyên**
    * **Thông tin quan trọng**
      * Phải xóa tài nguyên theo thứ tự đúng để tránh lỗi phụ thuộc
      * Một số tài nguyên như Elastic IP và NAT Gateway vẫn tính phí nếu không xóa

    * **Terminate các EC2 Instance**
      * **Các bước thực hiện**
        * Truy cập EC2 Console
        * Chọn tất cả Instances liên quan đến lab
        * Chọn Instance state → Terminate instance
        * Xác nhận terminate

    * **Xóa NAT Gateway và Elastic IP Address**
      * **Xóa NAT Gateway**
        * Vào VPC Console → NAT Gateways
        * Chọn NAT Gateway → Actions → Delete NAT Gateway
        * Nhập “delete” để xác nhận

      * **Xóa Elastic IP**
        * Vào VPC Console → Elastic IPs
        * Chọn EIP → Actions → Release Elastic IP address
        * Xác nhận Release

    * **Xóa VPC Endpoints**
      * **Các bước**
        * Vào VPC Console → Endpoints
        * Chọn các Endpoints liên quan
        * Chọn Action → Delete VPC endpoints
        * Nhập “delete” để xác nhận

    * **Xóa các tài nguyên VPN**
      * **Thứ tự xóa khuyến nghị**
        * Xóa VPN Site-to-Site Connection trước
        * Xóa Virtual Private Gateway (detach khỏi VPC trước nếu cần)
        * Xóa Customer Gateway

      * **Xóa VPC**
        * **Các bước**
          * Xóa VPC ASG VPN (VPC mô phỏng branch office)
          * Xóa VPC ASG (VPC chính)

        * **Security Note**
          * Xóa đúng thứ tự giúp tránh lỗi và đảm bảo dọn dẹp sạch sẽ

  * **Infrastructure as Code Templates**
    * **Infrastructure as Code (IaC) là gì?**
      * Quản lý và cung cấp hạ tầng qua file code thay vì cấu hình thủ công

    * **Lợi ích của IaC**
      * Khả năng lặp lại (Repeatability)
      * Kiểm soát phiên bản (Version Control)
      * Tự động hóa, giảm lỗi con người
      * Tài liệu sống (Living Documentation)
      * Dễ dàng quản lý chi phí và môi trường
      * Tăng cường bảo mật và tuân thủ

    * **CloudFormation Template**
      * **Template VPC Stack Hoàn chỉnh**
        * Bao gồm VPC, Multi-AZ Subnets, Internet Gateway
        * NAT Gateways High Availability
        * Route Tables cho Public/Private
        * Security Groups
        * VPC Flow Logs

      * **Các thành phần chính trong template**
        * VPC với DNS hỗ trợ
        * Public Subnets (Auto-assign Public IP)
        * Private Subnets
        * NAT Gateways + Elastic IPs
        * Route Tables và Associations
        * Security Groups (Public & Private)
        * IAM Role cho VPC Flow Logs

    * **Hướng dẫn Triển khai**
      * **Triển khai CloudFormation**
        * Sử dụng lệnh AWS CLI để create-stack
        * Giám sát trạng thái stack

      * **Các công cụ IaC khác**
        * AWS CDK
        * Terraform

      * **Best Practices cho IaC**
        * Sử dụng Parameter để tùy chỉnh môi trường
        * Tagging nhất quán
        * Lưu giá trị nhạy cảm trong Secrets Manager
        * Áp dụng least privilege cho IAM
        * Tách biệt môi trường (dev/staging/prod)
        * Kiểm tra và validate template trước khi deploy

## Wednesday: Setting up Hybrid DNS with Route 53 Resolver
  * **Introduction**
    * **Overview**
      * Most enterprises have their own on-premise DNS system
      * When migrating to AWS, bidirectional DNS integration between on-premise and AWS is required
      * This workshop uses AWS Managed Microsoft AD to simulate on-premise DNS

    * **Amazon Route 53 Capabilities**
      * Public domain registration
      * Create Private Hosted Zones
      * Hybrid DNS Resolution
      * Recursive DNS Resolver

    * **Three Main Tools of Route 53 Resolver**
      * **Outbound Endpoints**: Send DNS queries from AWS to on-premise
      * **Inbound Endpoints**: Receive DNS queries from on-premise into AWS
      * **Resolver Rules**: Forward DNS rules for specific domain names

  * **Connect to RDGW (Remote Desktop Gateway)**
    * **Description**
      * Connect via RDP to the Remote Desktop Gateway server for administration

    * **Detailed Steps**
      * Access EC2 Console → Select RDGW instance
      * Choose Connect → RDP Client
      * Download Remote Desktop file
      * Choose Get Password → Upload key pair to decrypt password
      * Open the RDP file and log in with the retrieved password
      * Confirm successful connection

  * **Deploy Microsoft AD**
    * **Objective**
      * Deploy AWS Managed Microsoft Active Directory to simulate on-premise DNS

    * **Steps**
      * Access Directory Service Console
      * Select AWS Managed Microsoft AD → Create directory

      * **Directory Information**
          * Edition: Standard Edition
          * Directory DNS name: onprem.example.com
          * Directory NetBIOS name: onprem
          * Description: This is to simulate the on-prem AD
          * Admin Password: Enter a strong password

      * **VPC and subnets**
          * Select VPC: Hybrid-DNS-VPCStack
          * Select two Private Subnets

      * Create Directory (takes approximately 20-40 minutes)
      * Record the two DNS IPs of the Domain Controllers

  * **DNS Configuration**
    * **Overview**
      * Use the three Route 53 Resolver tools to establish bidirectional hybrid DNS

    * **Overall Architecture**
      * Red arrow: Outbound Endpoint + Resolver Rule (AWS → On-prem)
      * Blue arrow: Inbound Endpoint (On-prem → AWS)
      * Green arrow: EC2 uses VPC DNS Resolver (VPC CIDR + 2)

    * **Create Route 53 Outbound Endpoint**
      * **Description**
        * Create an endpoint for Route 53 Resolver to forward queries to on-premise

    * **Create Route 53 Resolver Rules**
      * **Description**
        * Create a forwarding rule for the domain onprem.example.com to the Microsoft AD DNS IPs

    * **Create Route 53 Inbound Endpoints**
      * **Description**
        * Create an endpoint for on-premise to forward queries into AWS

    * **Testing the Results**
      * **Description**
        * Test bidirectional domain name resolution
        * Perform ping and DNS queries between AWS and the simulated on-premise environment

  * **Resource Cleanup**
    * **Important Deletion Order (must follow exactly)**

      * **Delete Inbound Endpoint**
        * Route 53 Console → Inbound endpoints → Delete

      * **Delete Resolver Rule**
        * Disassociate VPC first
        * Then delete the rule

      * **Delete Outbound Endpoint**
        * Route 53 Console → Outbound Endpoints → Delete

      * **Delete AWS Managed Microsoft AD**
        * Directory Service → Delete directory

      * **Delete CloudFormation Stack**
        * CloudFormation Console → Select HybridDNS stack → Delete
        * The stack will delete the entire network infrastructure (VPC, Subnets, RDGW...)