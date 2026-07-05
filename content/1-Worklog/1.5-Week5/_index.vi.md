---
title: "Worklog Tuần 5"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.5. </b> "
---

### Mục tiêu tuần 5:

* Xây dựng và hoàn thiện Frontend Real-time Security Dashboard (Track B)
* Làm chủ Amazon EC2 trên cả Windows Server 2025 và Amazon Linux 2023 (từ tạo instance đến triển khai ứng dụng Node.js)
* Thực hành VPC Peering và AWS Transit Gateway
* Hiểu sâu mô hình Shared Responsibility cùng các dịch vụ bảo mật cốt lõi của AWS (IAM, Cognito, Organizations, SSO, KMS)

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
|  2  | - Devphu Frontend Dashboard Progress Update | 18/05/2026 | 18/05/2026 |
|  3  | - Windows Server 2025 & Amazon Linux 2023 (VPC, SG, Launch, Connect, Node.js App, Custom AMI, IAM Policy) | 19/05/2026 | 19/05/2026 | <https://000004.awsstudygroup.com/> |
|  4  | - Thiết lập và Cấu hình bảo mật mạng VPC Peering | 20/05/2026 | 20/05/2026 | <https://000019.awsstudygroup.com/> |
|  5  | - Tổng quan về AWS Transit Gateway | 21/05/2026 | 21/05/2026 | https://000020.awsstudygroup.com/vi/ |
|  6  | - Dịch vụ bảo mật AWS - Shared Responsibility Model, IAM, Cognito, Organizations, Identity Center (SSO), KMS | 22/05/2026 | 22/05/2026 | <https://youtu.be/tsobAlSg19g> <br> <https://youtu.be/N_vlJGAqZxo> <br> <https://youtu.be/pZ2fgEFK3Vs> <br> <https://youtu.be/5oQY8Rogz9Y> <br> <https://youtu.be/NW1xrMkNMjU> <br> <https://youtu.be/GMihNQojhZc> <br> <https://youtu.be/clj2E0rNBEs> <br> <https://youtu.be/0SdpD2GPYz4> |


### Kết quả đạt được tuần 5:

## Thứ 6: Frontend Dashboard

## 1. Tổng quan về branch `devphu`

Branch **devphu** là nhánh phát triển chính dành cho **Track B (Frontend Dashboard)**. 
Nội dung tập trung vào việc xây dựng giao diện Real*time Dashboard, WebSocket integration, MITRE ATT&CK mapping, Event Detail Modal, UX/UI và Docker packaging

Hiện tại branch đang ở giai đoạn **thiết kế + triển khai ban đầu frontend**, sử dụng mock data và sẵn sàng tích hợp với backend sau này

## 2. Trạng thái hiện tại

* **Công nghệ chính:** React + Vite + TypeScript + Tailwind CSS  
* **Số commits:** Đang phát triển (commits tập trung vào cấu trúc dự án)  

### Thư mục chính
frontend/
├── src/
│ ├── components/ # Header, KPI widgets, Alert Feed, Charts, Modal...
│ ├── pages/ # Dashboard main page
│ ├── hooks/ # useSocket, useAlerts...
│ ├── store/ # State management
│ ├── utils/ # MITRE mapping, formatters, export helpers
│ ├── types/ # TypeScript interfaces (Alert, KPI, MITRE...)
│ ├── lib/ # Utilities chung
│ ├── assets/
│ └── App.tsx
├── package.json
├── vite.config.ts
├── .env.example
└── README.md

Dashboard hiện sử dụng **mock data** theo contract backend dự kiến và concept UI hiện đại (dark theme)

## 3. Cấu trúc Frontend (Track B)

### Công nghệ stack

* React 18 + Vite  
* TypeScript  
* Tailwind CSS (Dark mode)  
* WebSocket Client  
* Zustand hoặc Context API cho state management  
* React Router (nếu có multi*page)

### Tính năng đã triển khai

* Layout dashboard hiện đại (Sidebar + Header + Main content)
* KPI Widgets:
  * Total Alerts
  * Total Flows
  * Risk Score
  * Top Threat
* Realtime Alert Feed với filter và sort
* WebSocket hook (`useSocket.ts`) sẵn sàng nhận dữ liệu realtime
* Event Details Modal concept
* MITRE ATT&CK technique mapping
* Responsive + Dark theme

## 4. Tính năng cốt lõi

### 1. Header
* Tên hệ thống
* WebSocket status
* AI Engine status
* User info

### 2. KPI Dashboard
* Thống kê 24h realtime

### 3. Visual Analytics
* Line chart
* Pie/Doughnut chart theo loại tấn công

### 4. Realtime Alert Feed
* Bảng cảnh báo live với severity color

### 5. Event Detail Modal
* Thông tin chi tiết sự kiện
* MITRE ATT&CK tactics & techniques
* Evidence (Zeek, Suricata logs)
* AI Analysis & Decision flow
* Action buttons:
  * Block IP
  * Create Ticket
  * Export

## 5. Hướng dẫn chạy local

```bash
cd frontend
npm install
cp .env.example .env
# Cấu hình GEMINI_API_KEY (nếu dùng AI features)
npm run dev
```

## Thứ 2: Giới thiệu về Amazon EC2
* **Giới thiệu về Amazon EC2**
  * **Tổng quan**
    * **Amazon Elastic Compute Cloud (EC2)** là dịch vụ cung cấp máy chủ ảo (virtual servers) có khả năng thay đổi kích thước linh hoạt trên đám mây AWS

  * **Đặc điểm chính**
    * Khởi tạo nhanh chóng
    * Co giãn tài nguyên (scale up/down) theo nhu cầu
    * Hỗ trợ nhiều hệ điều hành (Linux, Windows, macOS...)
    * Thanh toán theo giờ/giây sử dụng

  * **Instance Types**
    * Instance Type quyết định:
      * **CPU**: Intel, AMD, ARM (Graviton), GPU
      * **Memory**: Dung lượng RAM
      * **Network**: Băng thông mạng
      * **Storage**: Hỗ trợ EBS và Instance Store

  * **Các thành phần quan trọng**
    * **AMI (Amazon Machine Image)**: Template chứa OS + phần mềm
    * **Key Pair**: Dùng để SSH/RDP vào instance
    * **Security Group**: Firewall ở mức instance
    * **EBS Volume**: Ổ cứng mạng
    * **Snapshot**: Bản sao lưu của EBS Volume

* **Các bước chuẩn bị (Prerequisite)**
  * **Tạo VPC cho Linux Instance**
    * **Tạo VPC cho Linux Instance**
      * Amazon Virtual Private Cloud (VPC) cho phép bạn khởi chạy tài nguyên AWS trong một mạng ảo được định nghĩa. Trong phần này, chúng ta sẽ tạo một VPC riêng biệt cho Linux instance với các subnet công khai để có thể truy cập từ internet

    * **Các bước thực hiện**
      * Truy cập **AWS Management Console** → Tìm và chọn **VPC**
      * Chọn **Create VPC** → Chọn **VPC and more**
      * Tại **Name tag auto*generation**, nhập `Linux`
      * Tại **VPC endpoints**, chọn **None** → Chọn **Create VPC**
      * Sau khi tạo thành công, chọn **View VPC**
      * Chọn **Subnets** từ menu bên trái
      * Chọn **Public subnet** → **Actions** → **Edit subnet settings**
      * Bật **Enable auto*assign public IPv4 address** → **Save**
      * Thực hiện tương tự cho các public subnet còn lại

  * **Tạo VPC cho Windows Instance**
    * **Tạo VPC cho Windows Instance**
      * Tương tự phần Linux, chúng ta tạo VPC riêng cho Windows instance

    * **Các bước thực hiện**
      * Vào **VPC** → **Create VPC** → Chọn **VPC and more**
      * Tại **Name tag auto*generation**, nhập `Windows`
      * **VPC endpoints** = **None** → **Create VPC**
      * Xem chi tiết VPC
      * Vào **Subnets** → Chọn public subnet → **Edit subnet settings**
      * Bật **Enable auto*assign public IPv4 address** → **Save**
      * Lặp lại cho các public subnet còn lại

  * **Tạo Security Group cho Linux Instance**
    * **Tạo Security Group cho Linux Instance**
      * Security Group hoạt động như tường lửa ảo để kiểm soát lưu lượng vào/ra EC2 instance

    * **Các bước thực hiện**
      * Vào **VPC** → **Security Groups** → **Create security group**.
      * **Name**: `Linux*SG`  
         **Description**: `Security group for Linux instance`  
         **VPC**: Chọn `Linux*vpc`.
      * Cấu hình **Inbound rules** (thêm 7 rules):

| Loại              | Cổng     | Mô tả                          |
|*******************|**********|********************************|
| SSH               | 22       | Kết nối SSH/PuTTY              |
| All ICMP*IPv4     | *        | Ping và thông báo lỗi          |
| All ICMP*IPv6     | *        | Ping IPv6                      |
| HTTP              | 80       | Web không bảo mật              |
| HTTPS             | 443      | Web bảo mật                    |
| MySQL/Aurora      | 3306     | Database MySQL                 |
| Custom TCP        | 5000     | Ứng dụng Node.js               |

  * **Tạo Security Group cho Windows Instance**
    * **Tạo Security Group cho Windows Instance**
      * Tạo Security Group dành riêng cho Windows instance

    * **Các bước thực hiện**
      * **Create security group**:
       * **Name**: `Windows*SG`
       * **Description**: `Security group for Windows instance`
       * **VPC**: Chọn `Windows*vpc`

      * Cấu hình **Inbound rules** (thêm 8 rules):

| Loại              | Cổng     | Mô tả                          |
|*******************|**********|********************************|
| SSH               | 22       | Kết nối SSH                    |
| HTTP              | 80       | Web                            |
| HTTPS             | 443      | Web bảo mật                    |
| RDP               | 3389     | Remote Desktop (Windows)       |
| All ICMP*IPv4     | *        | Ping                           |
| All ICMP*IPv6     | *        | Ping IPv6                      |
| Custom TCP        | 5000     | Node.js app                    |
| MySQL/Aurora      | 3306     | Database                       |

* **Khởi tạo Windows instance**
  * **Tổng quan**
    * **Khởi tạo Microsoft Windows Server 2025 instance**
      * Amazon EC2 cung cấp Microsoft Windows Server 2025 như một tùy chọn hệ điều hành cho các workload doanh nghiệp trên AWS Cloud. Windows Server 2025 mang đến các tính năng bảo mật nâng cao, khả năng quản lý hiệu quả và hiệu suất tối ưu cho ứng dụng Windows của bạn

  * **Tạo Windows Instance**
    * **Khởi tạo Microsoft Windows Server 2025 instance**
      * Trong phần này, bạn sẽ tìm hiểu cách khởi tạo một phiên bản Microsoft Windows Server 2025 trên Amazon EC2. Hiện tại EC2 đã hỗ trợ AMI Windows Server 2025 kèm giấy phép (License Included), giúp bạn dễ dàng triển khai phiên bản Windows Server mới nhất trên môi trường đám mây AWS

    * **Các bước thực hiện**
      * Truy cập **AWS Management Console** → Tìm và chọn **EC2** → Chọn **Instances** → Chọn **Launch instances**
      * **Name**: Nhập `Windows*instance`.
      * Chọn **AMI**:
        * Chọn **Quick Start** → **Windows**
        * Chọn **Microsoft Windows Server 2025 Base**

      * Chọn **Instance type** → Chọn **Create new key pair**

      * Trong giao diện **Create key pair**:
        * **Key pair name**: Nhập `kp*windows`
        * **Private key file format**: Chọn `.pem`
        * Chọn **Create key pair** (file key pair sẽ được tải về máy tính)

      * Trong phần **Network settings** → Chọn **Edit**:
        * **VPC**: Chọn `Windows*vpc`
        * **Subnet**: Chọn **public subnet**
        * **Auto*assign public IP**: Chọn **Enable**
        * **Firewall (security groups)**: Chọn **Select existing security group**
        * **Common security groups**: Chọn `Windows*SG`

      * Kiểm tra lại thông tin → Chọn **Launch instance**
      * Sau khi launch thành công, chọn **View all instances** để xem chi tiết instance vừa tạo
      * Đợi khoảng 5 phút cho đến khi **Status check** hiển thị **3/3 checks passed** và trạng thái instance là **Running**

  * **Kết nối Windows Instance**
    * **Kết nối từ máy tính đến Microsoft Windows Server 2025 instance**
      * Kết nối đến Windows instance trên AWS EC2 được thực hiện thông qua Remote Desktop Protocol (RDP) qua cổng 3389. AWS cung cấp cơ chế bảo mật để lấy mật khẩu quản trị viên bằng cách sử dụng key pair đã tạo trước đó

    * **Các bước thực hiện**
      * Trong giao diện **EC2** → Chọn **Instances** → Chọn instance `Windows*instance` → Chọn **Connect**

      * Chọn **RDP Client**:
        * Chọn **Download remote desktop file**
        * Chọn **Get password**

      * Trong giao diện **Get Windows password**:
        * Chọn **Browse** → Chọn file `kp*windows.pem
        * Chọn **Decrypt password**.

      * Sao chép **password** đã giải mã

      * Mở file **Remote Desktop** vừa tải về:
        * Chọn **Connect**
        * Nhập password đã sao chép → Chọn **OK**
        * Chọn **Yes** khi được hỏi về chứng chỉ bảo mật

      * Hoàn thành kết nối với **Microsoft Windows Server 2025** instance

    * **Chuẩn bị Sysprep cho custom AMI**
      * Sysprep (System Preparation) là công cụ của Microsoft giúp chuẩn bị hệ thống Windows để tạo image. Khi sử dụng Sysprep, các thông tin đặc thù của hệ thống như SID sẽ được xóa, cho phép tạo nhiều instance từ một AMI mà không gặp xung đột

    * **Các bước thực hiện**
      * Sau khi RDP vào Windows instance, tìm và mở **EC2LaunchSettings**
      * Tại **Administrator Password setting**, chọn **Random**
      * Cuối trang, chọn **Shutdown with Sysprep** → Xác nhận **Yes**
      * Kết quả: Instance sẽ tự động shutdown sau khi chạy Sysprep. Instance sẽ ở trạng thái **Stopped**

* **Khởi tạo Linux instance**
  * **Tổng quan**
    * **Khởi tạo Amazon Linux 2023 instance**
      * Amazon Linux 2023 là hệ điều hành Linux do AWS phát triển, được tối ưu hóa đặc biệt cho môi trường điện toán đám mây và cung cấp hiệu suất, bảo mật và tính ổn định cao cho các ứng dụng của bạn trên AWS.

  * **Tạo Linux Instance**
    * **Tạo Amazon Linux 2023 instance**
      * Amazon Linux 2023 AMI được AWS cập nhật thường xuyên với các bản vá bảo mật và cải tiến hiệu suất.

    * **Các bước thực hiện**
      * Truy cập **AWS Management Console** → Tìm và chọn **EC2** → Chọn **Instances** → Chọn **Launch instances**

      * **Name**: Nhập `Linux*instance`

      * Chọn **AMI**:
        * Chọn **Quick Start** → **Amazon Linux**
        * Chọn **Amazon Linux 2023 AMI**

      * Chọn **Instance type** → Chọn **Create new key pair**

      * Trong giao diện **Create key pair**:
        * **Key pair name**: Nhập `kp*linux`
        * **Key pair type**: Chọn **RSA**
        * **Private key file format**: Chọn **.pem**
        * Chọn **Create key pair** (file sẽ tự động tải về)

      * Trong phần **Network settings** → Chọn **Edit**:
        * **VPC**: Chọn `Linux*vpc`
        * **Subnet**: Chọn **public subnet**
        * **Auto*assign public IP**: Chọn **Enable**
        * **Firewall (security groups)**: Chọn **Select existing security group**
        * **Common security groups**: Chọn `Linux*SG`

      * Kiểm tra lại thông tin → Chọn **Launch instance**

      * Sau khi launch thành công, chọn **View all instances** để xem chi tiết instance

      * Đợi khoảng 5 phút cho đến khi **Status check** hiển thị **3/3 checks passed** và trạng thái instance là **Running**

  * **Kết nối Linux Instance**
    * **Kết nối đến Amazon Linux 2023 instance**
      * Có nhiều phương thức để kết nối đến EC2 Linux instance. Trong bài lab này, chúng ta sẽ tìm hiểu hai phương pháp phổ biến: sử dụng **MobaXterm** và **PuTTY**

    * **Kết nối bằng MobaXterm
      * Tải xuống [MobaXterm](https://mobaxterm.mobatek.net/download.html)

      * Mở **MobaXterm** → Chọn **Session**

      * Trong giao diện **Session settings**:
        * Chọn **SSH**
        * **Remote host**: Nhập **Public IPv4** của instance
        * **Specify username**: Nhập `ec2*user`
        * **Use private key**: Chọn file `kp*linux.pem`

      * Nhấn **OK** để kết nối
        * Lần đầu kết nối sẽ hiện thông báo → Chọn **Accept**
        * Kết nối thành công

    * **Kết nối bằng PuTTY**
      * PuTTY không hỗ trợ trực tiếp file `.pem`, cần chuyển đổi sang định dạng `.ppk`

    * **Các bước thực hiện**
      * Mở **PuTTYgen** → Chọn **Load** → Chọn file `kp*linux.pem`

      * Sau khi import thành công → Chọn **Save private key** → Đặt tên `kp*linux.ppk`

      * Mở **PuTTY**:
         * Trong menu bên trái: **Connection** → **SSH** → **Auth** → **Credentials**
         * Chọn **Browse** → Chọn file `kp*linux.ppk`

      * Quay lại **Session**:
        * **Host Name**: Dán **Public IPv4** hoặc `ec2*user@Public_IP`
        * **Saved Sessions**: Nhập `Linux*Server` → **Save**
        * Chọn **Open**

      * Khi hiện cảnh báo bảo mật → Chọn **Accept**

      * Khi yêu cầu đăng nhập → Nhập username: `ec2*user`

      * Kết nối thành công

    * **Kiểm tra kết nối
      * Sau khi kết nối thành công, chạy lệnh:
      ```bash
      ping 8.8.8.8
      ```

* **Amazon EC2 cơ bản** 
  * **Tổng quan**
    * Bài thực hành này cung cấp cái nhìn tổng quan khi làm việc với các đối tượng Amazon EC2 và các thành phần liên quan. Chúng ta sẽ tập trung vào những tác vụ cơ bản như thay đổi cấu hình, tạo snapshot, xây dựng AMI tùy chỉnh, và truy cập instance khi mất key pair

  * **Thay đổi cấu hình EC2**
    * **Thay đổi loại instance (Resize Instance)**
      * Bạn có thể thay đổi loại instance (instance type) để phù hợp với nhu cầu về CPU, RAM, network... mà không cần tạo instance mới

    * **Các bước thực hiện**
      * Vào **EC2** → Chọn instance cần thay đổi
      * Chọn **Instance state** → **Stop instance**
      * Đợi instance chuyển sang trạng thái **Stopped**
      * Chọn **Actions** → **Instance settings** → **Change instance type**
      * Chọn **Instance type** mới (ví dụ: từ t2.micro sang t3.small)
      * Chọn **Apply**
      * Chọn **Instance state** → **Start instance**

  * **Tạo và quản lý EBS Snapshots**
    * **Tạo EC2 Snapshot**
      * Amazon EBS Snapshot là bản sao dữ liệu tại một thời điểm cụ thể của volume, được lưu trữ theo cơ chế incremental trên Amazon S3

    * **Các bước thực hiện**
      * Vào **EC2** → Chọn **Snapshots** → **Create snapshot*
      * **Resource type**: Chọn **Instance**.
      * Chọn instance (`Windows*instance` hoặc `Linux*instance`)
      * **Copy tags from source volume**: Chọn **Copy tags**
      * Chọn **Create snapshot**
      * Đợi Snapshot status chuyển sang **Completed**

  * **Tạo Custom AMI**
    * **Tạo Custom AMI từ Windows Instance**
      * Amazon Machine Image (AMI) là template chứa hệ điều hành, ứng dụng và cấu hình. Tạo Custom AMI giúp tái sử dụng instance nhanh chóng

    * **Các bước thực hiện**
      * Vào **EC2** → Chọn `Windows*instance` → **Instance state** → **Stop instance**
      * Đợi instance ở trạng thái **Stopped**
      * Chọn **Actions** → **Image and templates** → **Create image**
      * **Image name**: `Custom Windows AMI`
      * **Image description**: `Custom Windows AMI`
      * Bỏ chọn **Reboot instance**
      * Chọn **Create image**
      * Vào **AMIs** để theo dõi tiến trình (khoảng 5 phút)

  * **Tạo instance từ Custom AMI**
    * **Khởi tạo instance từ Custom AMI**
      * Sử dụng Custom AMI đã tạo để khởi chạy instance mới với toàn bộ cấu hình sẵn có

    * **Các bước thực hiện**
      * Vào **EC2** → **AMIs** → Chọn `Custom Windows AMI`
      * Chọn **Launch instance from AMI**
      * **Name**: `Windows Server AMI`
      * Chọn **Instance type**
      * Tạo **new key pair** (`kp*windows2`)
      * **Network settings**:
        * VPC: `Windows*vpc`
        * Subnet: public subnet
        * Auto*assign public IP: Enable
        * Security Group: `Windows*SG`
      * Chọn **Launch instance**
      * Đợi Status check đạt **3/3 checks passed**

  * **Truy cập khi mất Key Pair EC2*Windows bằng SSM**
    * **Truy cập EC2 Windows khi mất Key Pair**
      * Key Pair được dùng để mã hóa và giải mã thông tin đăng nhập vào máy chủ ảo EC2. Khi bị mất Key Pair, AWS Systems Manager (SSM) cung cấp giải pháp an toàn để khôi phục quyền truy cập vào EC2 instance mà không cần tạo lại instance

    * **Điều kiện tiên quyết**
      * EC2 cần có kết nối Internet (public IP hoặc NAT Gateway) hoặc VPC Endpoint cho SSM.
      * SSM Agent phải được cài đặt và đang chạy trên instance.
      * EC2 instance phải có IAM role với quyền SSM.

    * **Tạo và gán IAM Role cho EC2**
      * Vào **IAM** → **Roles** → **Create role**
      * Chọn **AWS service** → **EC2**
      * Tìm và tích **AmazonSSMFullAccess** → Next
      * Đặt **Role name**: `Windows*instance` → **Create role**
      * Quay lại **EC2** → Chọn instance `Windows*instance` → **Actions** → **Security** → **Modify IAM role**
      * Chọn role `Windows*instance` → **Update IAM role**

    * **Cài đặt module AWSPowerShell (qua Session Manager)**
      * Vào **EC2** → Chọn instance → **Connect** → Chọn tab **Session Manager** → **Connect**.
      * Chạy lệnh cài module:
         ```powershell
         Install-Module -Name AWSPowerShell -Force -AllowClobber -SkipPublisherCheck
          ```
      * Kiểm tra:PowerShellGet-Module -ListAvailable AWSPowerShell

    * **Sử dụng AWS Systems Manager để reset password**
      * Vào Systems Manager → Run Command → Run a command
      * Tìm và chọn AWSSupport*RunEC2RescueForWindowsTool
      * Chọn instance Windows*instance
      * Bỏ chọn Enable an S3 bucket → Run
      * Đợi status chuyển sang Success

    * **Lấy mật khẩu mới từ Parameter Store**
      * Vào Systems Manager → Parameter Store
      * Tìm parameter có dạng /EC2Rescue/Passwords/[instance*id]
      * Chọn Show decrypted value để xem mật khẩu mới
      * Sao chép mật khẩu

    * **Kết nối RDP**
      * Vào EC2 → Chọn instance → Connect → RDP client
      * Tải file RDP → Mở file → Dán mật khẩu mới → Connect

  * **Truy cập khi mất Key Pair EC2-Linux bằng User Data**
    * **Truy cập khi mất Key Pair EC2*Linux bằng User Data**
      * Khi mất key pair, chúng ta tạo key pair mới và thay thế public key bằng cách chỉnh sửa EC2 User Data

    * **Các bước thực hiện**
      * Tạo Key Pair mới:
        * Vào EC2 → Key Pairs → Create key pair
        * Name: new*key, Type: RSA, Format: .pem → Create
      * Chuyển đổi sang .ppk bằng PuTTYgen:
        * Load file new*key.pem → Copy toàn bộ Public key (bắt đầu bằng ssh*rsa).
        * Save private key thành new*key.ppk.
      * Stop instance:
        * Chọn Linux*instance → Instance state → Stop instance.
      * Chỉnh sửa User Data:
        * Chọn Actions → Instance settings → Edit user data.
        * Dán nội dung sau (thay public key của bạn):
      * Save → Sau đó Start instance
      * Đợi Status check đạt 3/3 checks passed
      * Kết nối bằng PuTTY sử dụng file new-key.ppk

* **Triển khai ứng dụng Node.js trên Amazon Linu**
  * **Tổng quan**
    * Trong bài lab này, chúng ta sẽ triển khai ứng dụng **AWS User Management** - một ứng dụng web được xây dựng bằng **Node.js, Express, Express-Handlebars** và **MySQL**. Ứng dụng hỗ trợ các chức năng CRUD (Create, Read, Update, Delete) và tìm kiếm người dùng

  * **Kiến trúc triển khai**
    * Cài đặt **LAMP stack** (Linux + Apache + MariaDB + PHP)
    * Cấu hình **phpMyAdmin** để quản lý database
    * Cài đặt **Node.js** Runtime
    * Triển khai và chạy ứng dụng **AWS User Management**

  * **Cài đặt LAMP web server**
    * **Cài đặt LAMP web server trên Amazon Linux 2023**
      * LAMP là stack phổ biến gồm **Linux, Apache, MySQL/MariaDB, PHP**. Chúng ta sẽ cài đặt trên Amazon Linux 2023 để làm nền tảng cho ứng dụng web

    * **Các bước chính (tóm tắt các sub-section)**
      * **Chuẩn bị LAMP Server**: Cập nhật hệ thống và cài đặt các gói Apache, MariaDB, PHP
      * **Kiểm tra LAMP server**: Kiểm tra Apache và PHP hoạt động qua trình duyệt
      * **Cấu hình database server**: Khởi động MariaDB, chạy `mysql_secure_installation` để bảo mật
      * **Cài đặt phpMyAdmin**: Cài đặt công cụ quản lý database qua giao diện web

  * **Cài đặt Node.js trên Linux**
    * **Cài đặt Node.js trên Amazon Linux 2023**
      * Node.js là môi trường runtime JavaScript phía server, cho phép xây dựng ứng dụng web scalable

    * **Các bước thực hiện**
      * Cài đặt **Node Version Manager (nvm)**:
         ```bash
         curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.0/install.sh |
        ```
      * Kích hoạt nvm:Bash. ~/.nvm/nvm.sh
      * Cài đặt Node.js phiên bản LTS:Bashnvm install --lts
      * Kiểm tra cài đặt:
        Bashnode -v
        npm -v

  * **Triển khai ứng dụng trên Linux Instance**
    * **Triển khai ứng dụng AWS User Management** 
      * **Các bước thực hiện**
        * Cài đặt Git:
          ```bash
          sudo dnf install git
          git version ```
        * Clone source code:
          ```bash
          cd ~
          git clone https://github.com/First-Cloud-Journey/000004-EC2.git
          cd 000004-EC2```
        * Khởi tạo project và cài dependencies:
          ```bash
          npm init
          npm install express dotenv express-handlebars body-parser mysql```
        * Cài Nodemon (dev dependency):
          ```bash
          npm install nodemon@latest --save-dev```
        * Tạo file .env và cấu hình database:
          ```text
          DB_HOST=localhost
          DB_NAME=awsuser
          DB_USER=root
          DB_PASS=123Admin   # (password đã set ở phần bảo mật MariaDB)```
        * Khởi chạy ứng dụng:
          ```bash
          npm start```
        * Truy cập ứng dụng:
          * Mở trình duyệt → Dán Public IPv4 DNS của instance + :5000
          * Ví dụ: http://ec2-xxx-xxx-xxx-xxx.ap-southeast-1.compute.amazonaws.com:5000
        * Thêm dữ liệu mẫu qua phpMyAdmin (chạy SQL INSERT để có dữ liệu demo).
          * Chức năng ứng dụng:
            * Xem danh sách user
            * Thêm / Sửa / Xóa user
            * Tìm kiếm user

  * **Ứng dụng Node.js trên Amazon EC2 Windows**
    * **Tổng quan**
      * Trong phần này, chúng ta sẽ triển khai ứng dụng **AWS User Management** trên Amazon EC2 chạy **Microsoft Windows Server 2025**
      * Ứng dụng được xây dựng bằng **Node.js, Express, Express-Handlebars và MySQL**. 

    * **Các bước chính**
      * Cài đặt **XAMPP** (Apache + MariaDB + PHP) để sử dụng MySQL và phpMyAdmin
      * Cài đặt **Node.js** và Git
      * Clone source code và triển khai ứng dụng

  * **Cài đặt XAMPP trên Windows instance**
    * **Cài đặt XAMPP trên Microsoft Windows Server 2025**
      * XAMPP là gói phần mềm bao gồm **Apache, MariaDB (MySQL), PHP và Perl**, giúp dễ dàng thiết lập môi trường web development trên Windows

    * **Các bước thực hiện**
      * Kết nối RDP vào **Windows-instance**.
      * Tải XAMPP tại: [https://www.apachefriends.org/download.html](https://www.apachefriends.org/download.html)
      * Chạy file cài đặt và làm theo hướng dẫn (chấp nhận tùy chọn mặc định).
      * Sau khi cài xong, mở **XAMPP Control Panel**:
        * Start **Apache** (cổng 80)
        * Start **MySQL** (cổng 3306)
      * Truy cập phpMyAdmin: `http://localhost/phpmyadmin`
      * Tạo database:
        * Chọn **New** → Đặt tên database: `awsuser` → **Create**
      * Tạo bảng `user` bằng SQL Query:

  * **Cài đặt Node.js trên Windows instance**
    * **Cài đặt Node.js trên Microsoft Windows Server 2025**
      * Cài đặt Node.js Runtime, Git và Visual Studio Code để phát triển và chạy ứng dụng

    * **Các bước thực hiện**
      * Tải và cài đặt Git tại: https://gitforwindows.org/
      * Kiểm tra Git:
        bash git version
      * Tải và cài đặt Visual Studio Code
      * Tải và cài đặt Node.js (Windows Installer) từ trang chính thức.
      * Kiểm tra Node.js:
        bash
        node -v
        npm -v
      * Tạo thư mục và clone source code:
        bash
        mkdir AWSManagement
        cd AWSManagement
        git init
        git clone https://github.com/First-Cloud-Journey/000004-EC2.git
        cd 000004-EC2

  * **Triển khai ứng dụng trên Windows instance**
    * **Triển khai ứng dụng AWS User Management**
      * Cài dependencies, cấu hình database và chạy ứng dụng Node.js

    * **Các bước thực hiện**
      * Khởi tạo project:Bashnpm init
      * Cài đặt dependencies:Bashnpm install express dotenv express-handlebars body-parser mysql
      * (Tùy chọn) Cài Nodemon:Bashnpm install nodemon@latest --save-dev
      * Mở thư mục bằng Visual Studio Code và tạo file .env:
        text
        DB_HOST=localhost
        DB_NAME=awsuser
        DB_USER=root
        DB_PASS=
      * Khởi chạy ứng dụng:Bashnpm start
      * Truy cập ứng dụng:
        * Mở trình duyệt → http://localhost:5000 hoặc dùng Public IP của instance: http://<Public-IP>:5000
      * Thêm dữ liệu user qua phpMyAdmin hoặc giao diện ứng dụng.

      * Chức năng ứng dụng: CRUD (Create, Read, Update, Delete) và tìm kiếm người dùng

* **Giới hạn sử dụng tài nguyên bằng IAM :: GIỚI THIỆU VỀ AMAZON EC2**
  * **Tổng quan**
    * AWS Identity and Access Management (IAM) cho phép kiểm soát ai được truy cập vào tài nguyên AWS và thực hiện những hành động nào. Phần này tập trung vào việc sử dụng **IAM Policy** để giới hạn quyền, giúp **Cost Optimization** và tăng cường bảo mật theo nguyên tắc **least-privilege permissions**

  * **Mục tiêu**: Sử dụng IAM Policy để giới hạn:
    * Region
    * Instance Family
    * Instance Type
    * Loại EBS Volume
    * IP nguồn
    * Thời gian thực hiện hành động

  * **Cho phép sử dụng dịch vụ theo Region cụ thể**
    * **Cho phép sử dụng EC2 chỉ trên Region Singapore (ap-southeast-1)**
      * **Các bước thực hiện**
        * **Tạo Policy** (JSON):
        * Policy name: RegionRestrict
        * Tạo Group CostTest và attach policy RegionRestrict
        * Tạo IAM User TestUser, thêm vào group CostTest
        * Kiểm tra:
          * Tại Region Singapore → Launch EC2 → Thành công
          * Tại Region Tokyo → Launch EC2 → Thất bại
          * Thử sử dụng S3 tại Singapore → Thất bại (vì policy chỉ cho EC2)

  * **Giới hạn sử dụng EC2 theo Instance Family**
    * **Giới hạn Instance Family: T3, T4g, M5**
      * **Các bước thực hiện**
        * Tạo Policy (JSON):
        * Policy name: EC2_FamilyRestrict
        * Attach policy vào group CostTest
        * Kiểm tra:
          * Tạo instance t4g.micro → Thành công
          * Tạo instance m6i.large → Thất bại

  * **Giới hạn sử dụng EC2 theo Instance Type**
    * **Giới hạn Instance Type: t3.small và t3.large**
      * **Các bước thực hiện**
        * Tạo Policy (JSON):
        * Policy name: EC2_InstanceTypeRestrict
        * Attach policy vào group CostTest (gỡ policy cũ hơn để tuân thủ least-privilege).
        * Kiểm tra:
          * Tạo t3.small → Thành công.
          * Tạo m5.4xlarge → Thất bại.

  * **Giới hạn sử dụng EBS Volume Storage Type**
    * Mục tiêu: Chỉ cho phép sử dụng một số loại EBS Volume (ví dụ: gp3, gp2) để kiểm soát chi phí lưu trữ

  * **Giới hạn quyền xóa tài nguyên theo địa chỉ IP của Doanh nghiệp**
    * Mục tiêu: Chỉ cho phép xóa tài nguyên từ IP công ty (office IP), ngăn chặn xóa từ bên ngoài

  * **Giới hạn quyền xóa tài nguyên theo khoảng thời gian**
    * Mục tiêu: Chỉ cho phép thực hiện hành động xóa trong khung giờ làm việc (ví dụ: 8h00 - 18h00, thứ 2 đến thứ 6)

* **Dọn dẹp tài nguyên (Cleanup)**
  * **Các bước quan trọng**
    * **Terminate** tất cả EC2 Instances
    * **Deregister** AMI
    * **Xóa Snapshots**
    * **Xóa Security Groups**
    * **Xóa Key Pairs**
    * **Xóa VPC**
    * **Xóa IAM** policies, roles, users (nếu có)

## Thứ 3: Thiết lập VPC Peering
  * **Tổng quan**
    * Theo mặc định, các VPC bên trong AWS Cloud là tách biệt và không thể giao tiếp trực tiếp với nhau. Ở bài thực hành này, bạn sẽ tiến hành thiết lập kết nối **VPC Peering** giữa hai VPC để các tài nguyên bên trong hai VPC đó có thể liên lạc trực tiếp với nhau. Nhờ vậy, các giao tiếp giữa hai VPC không cần phải thông qua Internet công cộng nữa, góp phần gia tăng tính bảo mật cho VPC

  * **Quy ước:**  
    * **VPC default = VPC 1 (My VPC)** – CIDR: `172.31.0.0/16`  
    * **HG VPC = VPC 2** – CIDR: `10.10.0.0/16`

  * **Các khái niệm chính**
    * **VPC Peering Connection**
      * Kết nối VPC Peering là một kết nối mạng giữa 2 VPC cho phép bạn định tuyến traffic giữa chúng sử dụng địa chỉ private IPv4 hoặc IPv6. Những instance ở trong 1 trong 2 VPC có thể giao tiếp với nhau như chúng đang nằm cùng 1 mạng

  * **Network Access Control List (Network ACL)**
    * Network ACL là một dạng **stateless firewall** ở quy mô subnet. Khác với Security Group (stateful, resource-level), Network ACL chỉ gán được vào subnet

  * **Best practice:** Kết hợp SG + NACL để tạo defense-in-depth

  * **Cross-Peering DNS**
    * Tính năng cho phép các tài nguyên trong một VPC phân giải DNS private của tài nguyên trong VPC kia qua peering connection

  * **Giới thiệu**
    * **Tổng quan:** Theo mặc định, các VPC là tách biệt. Lab này thiết lập VPC Peering để giao tiếp private

  * **Lợi ích của VPC Peering:**
    * Kết nối trực tiếp (không cần gateway, VPN)
    * Traffic đi qua backbone AWS (bảo mật cao, độ trễ thấp)
    * Hỗ trợ cross-region, cross-account
    * Chi phí thấp

  * **Tính năng chính:**
    * Kết nối trực tiếp
    * Bảo mật (mỗi VPC quản lý SG/NACL riêng)
    * Hiệu suất cao
    * Khả năng mở rộng

  * **Các bước chuẩn bị**
    * Sử dụng **CloudFormation** để tạo hạ tầng nhanh chóng

  * **Khởi tạo CloudFormation Template**
    * **Hướng dẫn chi tiết:**
      * Tải template `VPCTemplate.yaml` từ:
        * AWS Documentation hoặc
        * GitHub AWS-First-Cloud-Journey
      * Vào **CloudFormation** → **Create stack**

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

  * Chờ stack tạo thành công (khoảng 5-10 phút)

  * **Tạo Security Group**
    * **My VPC SG (gán cho My VPC):**
      * Name: `My VPC SG`
      * Inbound rules:
        * SSH (port 22) → My IP
        * All ICMP - IPv4 → Anywhere
        * All ICMP - IPv4 → `10.10.0.0/16` (HG VPC)

    * **HG VPC SG (gán cho HG VPC):**
      * Name: `HG VPC SG`
      * Inbound rules:
        * SSH (port 22) → My IP
        * All ICMP - IPv4 → Anywhere
        * All ICMP - IPv4 → `172.31.0.0/16` (My VPC)

  * **Tạo EC2 instance**
    * Tạo 2 instance trên **Public Subnet**:
    * **EC2 - My VPC:**
      * Name: `EC2 - My VPC`
      * AMI: Amazon Linux 2
      * Type: t2.micro
      * Key pair: `vpcpeering-key` (tạo mới)
      * Network: My VPC → Public Subnet 2
      * Auto-assign Public IP: Enable
      * Security Group: `My VPC SG`

    * **EC2 - HG VPC:**
      * Name: `EC2 - HG VPC`
      * Tương tự, dùng key pair `vpcpeering-key`
      * Network: HG VPC → Public Subnet 2
      * Security Group: `HG VPC SG`

    * **Kiểm tra ban đầu:**
      * Ping Public IP của EC2 kia → Thành công (qua Internet)
      * Ping Private IP của EC2 kia → Thất bại (VPC chưa kết nối)

  * **Cập nhật Network ACL**
    * Vào **VPC** → **Network ACLs**
    * Chọn NACL của **HG VPC**
    * Tab **Inbound Rules** → **Edit inbound rules**
    * Rule 100: Đổi Source từ `0.0.0.0/0` → `172.31.0.0/16`
    * Save changes

    * **Kết quả:** Ping từ Internet đến HG VPC sẽ thất bại. Chỉ cho phép traffic từ My VPC

  * **Tạo kết nối Peering**
    * Vào **VPC** → **Peering Connections** → **Create Peering Connection**
      * Name: `lab-vpc-peer`
      * VPC (Requester): My VPC
      * Account: My account
      * Region: This region (ap-southeast-1)
      * VPC (Accepter): HG VPC

    * Accept request từ requester hoặc accepter
    * **Lúc này ping Private IP vẫn thất bại** (chưa config Route Table)

  * **Kích hoạt Cross-Peer DNS**
    * Vào **Peering Connections**
    * Chọn peering connection → **Actions** → **Edit DNS settings**
    * Tick cả hai:
      * Requester DNS resolution
      * Accepter DNS resolution
    * Save

    * **Kết quả:** Từ EC2 My VPC ping **Public DNS** của EC2 HG VPC sẽ resolve ra Private IP và traffic đi qua peering (không qua Internet)

  * **Dọn dẹp tài nguyên**
    * **Thứ tự khuyến nghị:**
      * **Terminate EC2 instances** (EC2 Console)
      * **Delete VPC Peering Connection** (VPC Console)
      * **Delete Security Groups**
      * **Delete CloudFormation Stacks** (My-VPC-Stack và HG-VPC-Stack) – sẽ tự động xóa VPC, Subnet, IGW, Route Table...

## Thứ 4: Tổng quan về AWS Transit Gateway
* **Giới thiệu**
  * **Tổng quan & Kiến trúc bài Lab**
    * Bài lab hướng dẫn cách triển khai kiến trúc kết nối bốn VPC thông qua một AWS Transit Gateway (TGW) đóng vai trò là một bộ định tuyến trung tâm (cloud router)
    * So sánh với VPC Peering: Trang web chỉ ra rằng nếu sử dụng phương pháp cũ (VPC Peering) để kết nối 4 VPC với nhau, bạn sẽ cần tới 6 kết nối Peering. Khi số lượng VPC tăng lên (6, 8, 10 VPC), mô hình Peering sẽ cực kỳ phức tạp và khó quản lý
    * Lợi ích của AWS Transit Gateway: Đơn giản hóa kiến trúc mạng bằng cách kết nối các VPC và mạng on-premises thông qua một hub trung tâm
      * Giảm thiểu các mối quan hệ định tuyến phức tạp
      * Mỗi kết nối mới chỉ cần thực hiện một lần.

  * **Các khái niệm quan trọng được đề cập**
    * AWS Transit Gateway Attachment: Là công cụ dùng để gán các subnet từ VPC vào Transit Gateway
      * Hoạt động ở cấp độ Availability Zone (AZ - Vùng khả dụng)
      * Khi một subnet trong một AZ được gán, các subnet khác trong cùng AZ đó cũng có thể kết nối với TGW, giúp quản lý kết nối linh hoạt

  * **Cảnh báo chi phí (Warning)**
    * Bài lab này có phát sinh chi phí trên tài khoản AWS của bạn, bao gồm:
      * Chi phí cho các instance cấu hình (sử dụng loại t3.nano)
      * Chi phí liên quan trực tiếp đến việc duy trì Transit Gateway

  * **Tạo Key Pair**
    * Thực hiện tạo Key Pair
      * Đăng nhập vào AWS Management Console
      * Tìm EC2
      * Chọn EC2

    * Trong giao diện EC2
      * Chọn Key Pairs
      * Chọn Create key pair

    * Trong giao diện Create key pair
      * Name, nhập tgw-key
      * Key pair type, chọn RSA
      * Private key file format, chọn .pem
      * Chọn Create key pair

    * Tạo key pair thành công

  * **Khởi tạo CloudFormation Template**
    * Truy cập đến CloudFormation Management Conole bằng cách gõ CloudFormation vào thanh tìm kiếm
    * Trong giao diện CloudFormation
      * Chọn Create stack
    * Chọn Upload a template file, chọn tgw-lab.yaml từ source mà chúng ta down về ở trên, và chọn Next
    * Trong trang Specify stack details, nhập tên cho stack (VD: Lab20-Stack), chọn SSH Key của bạn, và sau đó chọn Next
    *  Trong trang Configure stack options, giữ nguyên mặc định và chọn Next
    *  Trong trang Review, kiểm tra thông tin và chọn Submit
    *  Tạo Stack thành công
    *  Xem Output của stack vừa tạo
    *  Quay lại giao diện AWS Management Console
       *  Tìm EC2
       *  Chọn EC2
    * Trong giao diện EC2
      * Chọn Instances
      * Chọn First EC2 host
    * Đi đến folder bạn chứa SSH Key pair và sau đó chạy command prompt sau để sao chép Key Pair đến First EC2 Host cho bước tiếp theo
    * Đi đến folder bạn chứa SSH Key pair và sau đó chạy command sau để sao chép Key Pair đến Third EC2 Host cho bước tiếp theo

  * **Tạo Transit Gateway**
    * Truy cập VPC Management Console
      * Mở AWS Management Console
      * Tìm và chọn VPC
    * Khởi tạo Transit Gateway
      * Chọn Transit Gateway từ menu bên trái
      * Nhấn Create Transit Gateway
    * Cấu hình cơ bản
      * Name tag: lab20-tgw
      * Description: Transit Gateway for lab20
    * Cấu hình nâng cao
      * Bỏ chọn Default route table association
      * Bỏ chọn Default route table propagation
    * Xác nhận và tạo
      * Kiểm tra lại thông tin
      * Nhấn Create Transit Gateway

  * **Tạo Transit Gateway Attachments**
    * Truy cập VPC Management Console
      * Mở VPC Management Console
      * Chọn Transit Gateway Attachments
      * Nhấn Create Transit Gateway Attachment
    * Cấu hình cơ bản
      * Transit Gateway ID: Chọn ID của Transit Gateway đã tạo
      * Attachment type: Chọn VPC
    * Cấu hình chi tiết
      * Attachment name tag: Nhập tên VPC (VD: VPC1)
      * VPC ID: Chọn First VPC (VPC1)
      * Subnet ID: Chọn subnet trong AZ tương ứng
      * Nhấn Create transit gateway attachment
    * Xác nhận tạo thành công
      * Đợi trạng thái chuyển sang Available
    * Tạo Attachment cho VPC2
      * Lặp lại các bước trên cho VPC2
      * Đặt tên phù hợp (VD: VPC2)
    * Tạo Attachment cho VPC3
      * Lặp lại quy trình cho VPC3
      * Đặt tên phù hợp (VD: VPC3)
    * Tạo Attachment cho VPC4
      * Hoàn tất quy trình cho VPC4
      * Đặt tên phù hợp (VD: VPC4)
    * Kết nối SSH đến EC2 trong VPC1
      * Sử dụng lệnh: ping <IPv4 Public của EC2> -c5
    * Kiểm tra kết nối giữa các VPC
      * Thử ping các địa chỉ IP private của các instance khác
      * Lưu ý: Kết nối sẽ thất bại do chưa cấu hình routing

  * **Tạo Transit Gateway Route Tables**
    * Truy cập VPC Management Console
      * Mở VPC Management Console
      * Chọn Transit Gateway Route Tables
      * Nhấn Create Transit Gateway Route Table
    * Cấu hình Route Table
      * Name tag: lab20-TGW-RT
      * Chọn Transit Gateway đã tạo
      * Nhấn Create Transit Gateway Route Table
    * Xác nhận tạo thành công
      * Đợi Route Table chuyển sang trạng thái Available
    * Tạo Association
      * Chọn Route Table vừa tạo
      * Chuyển đến tab Associations
      * Nhấn Create association
    * Thêm VPC vào Association
      * Lần lượt thêm từng VPC
      * Đảm bảo tất cả 4 VPC đều được thêm vào
    * Xác nhận Association
      * Kiểm tra trạng thái của các Association
      * Đảm bảo tất cả đều ở trạng thái Associated
    * Tạo Propagation
      * Chuyển đến tab Propagations
      * Nhấn Create propagation
    * Thêm VPC vào Propagation
      * Lần lượt thêm từng VPC
      * Đảm bảo tất cả 4 VPC đều được thêm vào
    * Xác nhận Propagation
      * Kiểm tra trạng thái của các Propagation
      * Đảm bảo tất cả đều ở trạng thái Enabled

  * **Thêm Transit Gateway Routes vào VPC Route Tables**
    * Chọn Route Table
      * Mở VPC Management Console
      * Chọn Route Tables
      * Chọn Route Table của VPC1
      * Nhấn Edit routes
    * Thêm route
      * Destination: 172.16.0.0/16
      * Target: Chọn Transit Gateway đã tạo
    * Xác nhận route
      * Kiểm tra route mới đã được thêm
      * Route này cho phép VPC1 gửi traffic đến mạng 172.16.x.x qua Transit Gateway
    * Thêm route tương tự
      * Chọn Route Table của VPC3
      * Thêm route với Destination 172.16.0.0/16
      * Target là Transit Gateway
    * Xác nhận route
      * Kiểm tra route mới đã được thêm
      * Route này cho phép VPC3 gửi traffic đến mạng 172.16.x.x qua Transit Gateway
    * Thêm route cho VPC2
      * Chọn Route Table của VPC2
      * Thêm route với Destination 0.0.0.0/0
      * Target là Transit Gatewa
    * Thêm route cho VPC4
      * Chọn Route Table của VPC4
      * Thêm route với Destination 0.0.0.0/0
      * Target là Transit Gateway
    * Kiểm tra kết nối Internet
      * Kết nối SSH đến EC2 trong VPC1
      * Thử ping amazon.com để kiểm tra kết nối Internet
    * Kiểm tra kết nối giữa các VPC
      * Ping đến IP của EC2 trong VPC2
      * Kết nối SSH giữa các instance
      * Kiểm tra kết nối đến VPC3 và VPC4

  * **Dọn dẹp tài nguyên**
    * **Xóa Transit Gateway Attachments**
      * Truy cập VPC Management Console
        * Mở VPC Management Console
        * Chọn Transit Gateway Attachments
      * Xóa Attachments
        * Chọn tất cả Attachments liên quan
        * Nhấn Actions > Delete
        * Xác nhận xóa trong prompt
      * Xác nhận xóa
        * Đợi 1-2 phút để hoàn tất việc xóa
        * Kiểm tra trạng thái của các Attachments

    * **Xóa Transit Gateway**
      * Truy cập Transit Gateway
        * Chọn Transit Gateways từ menu bên trái
        * Chọn Transit Gateway cần xóa
      * Xóa Transit Gateway
        * Nhấn Actions > Delete
        * Xác nhận xóa trong prompt

    * **Xóa CloudFormation Stack**
      * Truy cập CloudFormation
        * Mở CloudFormation Management Console
        * Chọn Stacks
      * Xóa Stack
        * Chọn Stack liên quan đến lab
        * Nhấn Delete
        * Xác nhận xóa trong prompt

## Thứ 5: Dịch vụ bảo mật AWS
  * Shares Responsibility Model
  * AWs Identity and Access Management
  * Amazon Cognito
  * AWS Organization AWS Identity Center (SSO)
  * AWS KMS

  * **Shares Responsibility Model**
    * **Mô hình chia sẻ trách nhiệm:** khi sử dụng dịch vụ của nhà cung cấp dịch vụ điện toán đám mây, việc bảo mật của ứng dụng dịch vụ sẽ là trách nhiệm chia sẻ của cả khách hàng và nhà cung cấp dịch vụ
    * Khách hàng sẽ chịu tránh nhiệm cho việc cấu hình, áp dụng các dịch vụ để đảm bảo việc bảo mật từ mức Hypervisor tới mức dữ liệu/ứng dụng
    
    * **Security in the cloud:** 
      * Bắt đầu từ mức hypervisor, từ mức hệ điều hành 
      * Một số việc cần quan tâm là nhu cầu mã hóa dữ liệu, thực hiện mã hóa dữ liệu, quản lý nơi đặt file trong dịch vụ lưu trữ
      * Nhóm các dịch vụ về quản lý traffic Network như xây dựng tường lửa cũng phải cấu hình về hệ điều hành, network, firewall
      * Bên trên mức hệ điều hành có các platform, ứng dụng quản lý quyền truy cập và định danh
      * Cài hệ điều hành Windows thì quản lý việc bảo mật bên trong hệ điều hành là việc của mình, của khách hàng, còn bản thân nhà cung cấp dịch vụ sẽ không nhìn vào được bên trong của mình, họ chỉ cung cấp hạ tầng ở bên dưới, bên trong không nhìn được
      * Hệ điều hành không nhìn được thì sao nhìn được hệ ứng dụng
      * Quản lý quyền truy cập và định danh cũng vậy, chúng ta có user đăng nhập vào hệ điều hành thì chúng ta cũng là người quản lý, user chúng ta đăng nhập vào nền tảng cloud, chúng ta cũng là người quản lý và trên cũng là phần dữ liệu thì đây là phần trách nhiệm của khách hàng không có nghĩa phải làm mọi thứ từ con số 0 mà AWS cung cấp sẵn một tập các dịch vụ để đáp ứng các như cầu bảo mật khác nhau của các tổ chức khác nhau vì không thể nào áp đặt một tiêu chuẩn bảo mật lên tất cả các tổ chức phải xây dựng nền tảng trước xây dựng dịch vụ trước xây dựng những best practice, những hướng dẫn trước để khách hàng tùy ý cầu hình theo nhu cầu của riêng mình
      * Nhu cầu của tổ chức tới đâu thì họ sẽ cấu hình tới đó và AWS cung cấp cả dịch vụ, cung cấp cả tài liệu để có thể làm được
      * Mức AWS sẽ là từ hypervisor đi xuống, về phần vật lý thì hạ tầng toàn cầu vật lý của AWS, những trung tâm dữ liệu của AWS, lớp mạng bin, region, ag, ex location
      * Bên trên sẽ có những hạ tầng cơ bản như phần tính toán, phần lưu trữ, cơ sở dữ liệu, network, đây sẽ là những trách nhiệm bảo  mật chính của AWS

      * Trách nhiệm bảo mật sẽ thay đổi tùy vào từng loại hình dịch vụ:
        * Các dịch vụ ở mức hạ tầng
        * Các dịch vụ quản lý ở mức kết hợp
        * Các dịch vụ quản lý hoàn toàn bởi AWS
        
      * Tuy nhiên, mô hình chia sẻ trách nhiệm không phải fix hoàn toàn, sẽ khác nhau giữa các dịch vụ khác nhau
      * Dịch vụ máy chủ ảo EC2 là một dịch vụ ở mức hạ tầng, các dịch vụ ở mức hạ tầng thì trách nhiệm quản lý sẽ khá nhiều, từ việc mã hóa dữ liệu, từ việc control network traffic, hệ điều hành cập nhật bản vá, cấu hình tường lửa, cài đặt ứng dụng, quản lý ứng dụng, quản lý dữ liệu, phân quyền, phải làm rất nhiều thứ
      * Dịch vụ được quản lý ở mức kết hợp là AWS sẽ nhận nhiều nhiệm vụ hơn như dịch vụ cở sở dữ liệu mà AWS đứng ra quản lý platform về database cho mình, ví dụ như my sequel, AWS đứng ra quản lý platform đó, chúng ta chỉ dùng, không có truy cập trực tiếp vào hệ điều hành, chỉ kết nối tới bản thân database server đó, sử dụng các công cụ quản lý của MySQL, kết nối vào database server, không quản lý hệ điều hành, trách nhiệm quản lý hệ điều hành sẽ được AWS gắn một phần, trách nhiệm quản lý database, platform AWS cũng gắn một phần, AWS gắn càng nhiều thì công sức bỏ ra để quản lý phần hạ tầng sẽ càng bớt đi, giảm thiểu đi để có thể tập trung vào những thứ mang giá trị cao hơn như xây dựng ứng dụng tối ưu, ứng dụng thiết kế câu truy vẫn đạt hiệu năng tối ưu,..
      * Các dịch vụ được quản lý hoàn toàn bởi AWS thì khi AWS quản lý hoàn toàn, trách nhiệm của chúng ta sẽ càng ít như đưa dữ liệu lên S3 thì chỉ quan tâm tới dữ liệu đặt ở đâu, làm sao để tối ưu chi phí, có mã hóa dữ liệu không, có bật versioning không,..
      * Việc bảo mật trên nền tảng điện toán đám mây là một sự chia sẻ trách nhiệm giữa cả AWS và khách hàng và sẽ khác nhau dựa trên nhóm dịch vụ ở mức hạ tầng, dịch vụ quản lý kết hợp hay dịch vụ được quản lý hoàn toàn bởi AWS và xu hướng của khách hàng thì sẽ càng muốn dùng những dịch vụ được quản lý hoàn toàn bởi AWS để giảm bớt công sức quản lý hạ tầng và tập trung vào phát triển ứng dụng

  * **AWS Identity and Access Management**
    * **AWS Identity and Access Management - Root Account**
      * Tài khoản này có toàn quyền truy cập vào tất cả các dịch vụ và tài nguyên AWS và có thể gỡ bỏ các chính sách quyền đã gán vào tài nguyên
        * Thông tin chi phí
        * Dữ liệu cá nhân (khi đăng ký account)
        * Không bị giới hạn quyền
        
      * Best Practices:
        * Tạo và sử dụng IAM Administrator User
        * Khóa thông tin xác thực của root user (chia hai người giữ)
        * Đảm bảo renew thông tin domain và email của root user

      * Root account là thông tin đăng ký account AWS ban đầu bao gồm thông tin email, thông tin SDT, tên, tuổi, password đăng nhập, có toàn quyền truy cập vào tất cả các dịch vụ và tài nguyên của AWS
      * Và nếu muốn gán quyền để hạn chế thì sẽ không hạn chế được bởi toàn khoản root account có 1 đặc quyền là có thể gỡ được những chính sách quyền đã gán vào tài nguyên
      * Ví dụ chúng ta có máy chủ muốn gán vào máy chủ này không cho phép root user can thiệp vào thì nếu là root user có thể gỡ luôn cái chính sách quyền đó, cũng có toàn quyền xem thông tin dữ liệu cá nhân khi đăng ký và gần như là 1 thực thể không bị giới hạn cho nên best practice phương pháp thực hành tốt nhất là không sử dụng root account đó
      * Bây giờ còn dùng root account thì nên dừng, chúng ta sẽ tạo user con gọi là IAM user và gán quyền, chính sách quyền, policy vào user đó để cho thành một admin user và sử dụng admin user này rồi thông tin root user thì khi đăng nhập sẽ thấy thường sẽ có password và thêm sử dụng mfa cấu hình chứng thực 2 lớp bằng virtual appliance hoặc hardware, chia đổi nó ra để không có ai giữ cả 2 cái đó một phần và thường ở trong doanh nghiệp chia đôi ra 2 người có chức cao nhất, có quyền cao nhất ở trong tổ chức chia ra, thậm chí là niêm phong lại và không sử dụng và một số tổ chức sử dụng cả khóa chứng thực bằng phần cứng để dễ chia
      * Thông tin khi đăng ký root user là sử dụng email doanh nghiệp và đảm bảo domain phải thuộc quyền sở hữu của mình

      * IAM là dịch vụ giúp bạn có thể kiểm soát quyền truy cập vào các dịch vụ và các tài nguyên ở trong AWS account của mình. IAM cho phép bạn tạo nhiều tài khoản người dùng (IAM user) với thông tin xác thực (credentials) và quyền hạn khác nhau
      * IAm Principal (chủ thể IAM) là một thực thể có thể thực hiện các hành động trên tài nguyên nhất định trong AWS account của bạn
        * AWS account and root user
        * IAM users
        * Federated users (sử dụng web identity hoặc SAML federation)
        * IAM roles
        * Assumed-role sessions
        * AWS services
        * Anonymous users (không khuyến nghị)

      * Người dùng IAM (IAM user) không phải là toàn khoản AWS  riêng biệt, IAM Users có mật khẩu riêng để truy cập vào management console hoặc access key/secret key để thực hiện programmatic access (AWS CKI và AWS SDK)
        * IAM User  khi được tại ra mặc định không có bất cứ quyền gì
        * IAM User không được dùng để quản lý truy cập vào ứng dụng hay hệ điều hành
        * Để cấp quyền cho IAM User chúng ta phải gán IAM Policy vào IAM User
        * Để quản lý dễ dàng hơn chúng ta có thể gom nhiều IAM User thành 1 IAM Group
        * IAM Group không thể là thành viên của 1 IAM Group khác

    * **AWS Identity and Access Management - IAM policy**
      * Được viết dưới dạng JSON
      * IAM Polity có 2 loại
        * Identity based Policy gán với một IAM Principal
        * Resource based Policy gán với một AWS Resource

      * Cách thức tính quyền của IAM luôn ưu tiên Deny so với Allow, nếu đã có Deny tường minh (explicit) thì dù cho có allow ở trên một IAM Policy khác thì cũng vẫn luôn là Deny

      * Ví dụ này cho thấy cách bạn có thể IAM Policy giới hạn việc quản lý S3 bằng cách:
        * Cho phép tất cả các hành động của S3 trên bucket cụ thể
        * Deny tường minh (explicit deny) quyền truy cập vào mọi dịch vụ AWS ngoại trừ Amazon S3

    * **AWS Identity and Access Management - IAM Role**
      * IAM Role cho phép xác định một tập hợp quyền truy cập vào các tài nguyên (thông qua việc gàn IAM Policy vào IAM role). IAM Role không có thông tin chứng thực (credentials) để truy cập vào management console hay AWS CLI/SDK
      * Khi một IAM User muốn sử dụng IAM Role, IAM User sẽ cần assume (đảm nhận) 1IAM Role, ngay sau khi assume role, quyền hiện tại của user sẽ được thay bằng quyền đang được cấp cho IAM Role. Ngoài ra, thông tin xác thực bảo mật tạm thời sẽ được cấp cho IAM User hoặc một AWS Service để có thể truy cập tới các dịch vụ của AWS. Việc assume role sẽ làm việc với dịch vụ AWs STS-Security Token Service giúp tạo ra các thông tin chứng thực tạm (tương tự như access key)
      * Để một user có thể sử dụng IAM Role, IAM Role sẽ được gán một resource base IAM policy, hay còn gọi là IAM Role policy, quy định xem ai có thể sử dụng IAM Role
      * IAM Role thường được dùng trong thực tế để đảm bảo nguyên tắc cấp quyền tối thiểu và dùng trong trường hợp cấp quyền cho các AWS account khác truy cập tài nguyên của AWS account hiện tại
      * Ngoài được sử dụng cho IAM User, IAM Role còn được sử dụng để cấp quyền truy cập các resource của AWS cho chính các AWS Service
      * Trường hợp sử dụng thường thấy nhất là dùng IAM Role cấp quyền cho các ứng dụng chạy bên trong dịch vụ tính toán (EC2)
      * Ngoài được sử dụng cho IAM User, IAM Role còn được sử dụng để cấp quyền truy cập các resource của AWS cho chính các AWS Service

    * **Amazon Cognito**
      * Amazon Cognito là dịch vụ được quản lý bởi AWS có chức năng xác thực, cấp phép và quản lý người dùng cho các ứng dụng web và di động. Người dùng có thể đăng nhập trực tiếp bằng tên người dùng và mật khẩu hoặc thông qua một bên thứ ba như Facebook, Amazon hoặc Google
      * Hai thành phần chính của Amazon Cognito là User Pool và Identity Pool
        * User Pool là thư mục người dùng cung cấp các tùy chọn đăng ký và đăng nhập cho người dùng ứng dụng 
        * Identity Pool cấp cho người dùng quyền truy cập vào các dịch vụ AWS khác

      * User Pool: Sau khi đăng nhập với user pool, người dùng ứng dụng có thể truy cập các tài nguyên mà ứng dụng cho phép
      * User Pool: Sau khi đăng nhập với user pool, người dùng ứng dụng có thể gọi đến API Endpoint (Backend) mà ứng dụng cho phép
      * User Pool kết hợp với Identity Pool để truy cập trực tiếp vào các dịch vụ của AWS

  * **AWS Organization**
    * AWS Organizations giúp quản lý và điều hành tập trung môi trường của mình bao gồm nhiều AWS account
    * AWS Organizations có thể tạo các tài khoản AWS mới và phần bổ tài nguyên, sắp xếp các AWS account theo OU (Organizations Unit), đồng thời đơn giản việc thanh toán với thanh toán tập trung (consolidated billing)
    * AWS Organization có thể áp dụng các chính sách kiểm soát dịch vụ (Service Control Policies) lên các OU hoặc các AWS account, SCP chỉ thiết lập giới hạn quyền tối đa cho các IAM User hoặc IAM role trong OU hoặc AWS account đưuọc gán
    * SCP cũng cho phép thiết lập deny-based policy

  * **AWS Identity Center (SSO)**
    * AWS Identity Center giúp quản lý quyền truy cập tới AWS account và cả các ứng dụng bên ngoài
      * Identity source có thể nằm trong AWS Identity Center hoặc được liên kết với Active Directory. (AWS Managed Microsoft AD, On-premises Microsoft AD thông qua TWO way trust hoặc AD Connector)

    * Permission Set xác định khả năng truy cập mà User và Group có đối với các tài khoản AWS trong AWS Organization. Các bộ quyền được lưu trữ trong AWS Identity Center và được cung cấp cho tài khoản AWS dưới dạng IAM roles. Bạn có thể gán nhiều quyền cho một User

  * **Amazon Key Management Service**
    * **AWS KMS**
      * AWS Key Management Service giúp tạo và quản lý các encryption key, phục vụ cho mục đích encrypt/decrypt dữ liệu trên AWS (Encryption at rest)
      * Encryption key Luôn nằm trong AWS KMS, đảm bảo tiêu chuẩn FÍP 140-2
      * CMK (Customer Managed Key) đóng vai trò là tài nguyên chính trong AWS KMS. CMK có thể có kích thước 4KB. Tuy nhiên thông thường, chúng ta chỉ sử dụng CMK cho mục đích tạo, mã hóa và giải mã Data Key - loại được dùng bên ngoài AWS KMS để mã hóa dữ liệu

    * **AWS Security Hub**
      * AWS Security Hub là dịch vụ cho phép chúng ta thực hiện kiểm tra bảo mật dựa trên các tiêu chuẩn và best practices
      * Security Hub chạy liên tục, kiểm tra cấu hình các dịch vụ trong tài khoản AWS và kiểm tra bảo mật dựa trên các best practice của AWS và tiêu chuẩn ngành (VD: PCIDSS)
      * Security Hub cung cấp kết quả kiểm tra dưới dạng điểm số và giúp chúng ta xác định các tài khoản và tài nguyên cụ thể cần được chú ý