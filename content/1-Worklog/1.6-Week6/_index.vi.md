---
title: "Worklog Tuần 6"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.6. </b> "
---

### Mục tiêu tuần 6:

* Hoàn thiện và nâng cấp Frontend Dashboard, bổ sung các tính năng và trang chức năng mới
* Thực hành triển khai AWS Storage Gateway và File Shares
* Tìm hiểu quy trình di chuyển máy ảo với AWS VM Import/Export
* Thực hành quản lý tài nguyên bằng AWS Tags và Resource Groups
* Triển khai và đánh giá bảo mật với AWS Security Hub

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
|  6  | - Frontend Dashboard | 22/05/2026 | 22/05/2026 |
|  2  | - Thực hành triển khai AWS Storage Gateway và File Shares | 24/05/2026 | 24/05/2026 | <https://000024.awsstudygroup.com/> |
|  3  | - Virtual Machine Migration Guide | 26/05/2026 | 26/05/2026 | <https://000014.awsstudygroup.com/> |
|  4  | - AWS Tags và Resource Group | 27/05/2026 | 27/05/2026 | <https://cloudjourney.awsstudygroup.com/> |
|  5  | - Hands-on AWS Security Hub: Enable, Evaluate Security Standards, and Resource Cleanup | 28/05/2025 | 28/05/2025 | <https://cloudjourney.awsstudygroup.com/> |

### Kết quả đạt được tuần 6:

## Thứ 6: Frontend Dashboard (Track B)
  * **Tổng quan về branch devphu**
    * Branch devphu là nhánh phát triển chính cho Track B (Real-time & UX Dashboard). Tuần này tập trung mạnh vào polish UI/UX, mở rộng tính năng, cải thiện trải nghiệm người dùng và bổ sung các trang mới
    * Frontend đã chuyển sang giai đoạn triển khai nâng cao + tinh chỉnh chi tiết, vẫn dùng mock data chất lượng cao nhưng đã chuẩn bị rất tốt cho việc tích hợp backend sau này

  * **Những thay đổi & Tính năng MỚI được thêm**
    * Các thay đổi quan trọng:
      * Fix hoàn toàn Light/Dark Mode: Sửa bug toggle theme, cải thiện animation chuyển mode mượt mà hơn, đồng bộ màu sắc nhất quán trên toàn bộ ứng dụng
      * Cải thiện Animation & List: Tối ưu animation khi alert mới xuất hiện, sort/filter mượt mà, loading states và transition đẹp hơn
      * Refactor cấu trúc component: Tổ chức lại rõ ràng hơn theo từng module (dashboard, network, reports, playbooks, integrations...)

    * Tính năng được thêm mới:
      * Trang Network Monitoring Page:
        * NetworkChart.tsx (line chart realtime)
        * NetworkStreamTable.tsx
        * NetworkStats.tsx
        * useNetworkStream hook
        * NetworkGenerator & NetworkConfig (mock data)
      * Playbooks Page: PlaybookList, PlaybookCard, PlaybookModal, PlaybookFilters
      * Reports Page: ExecutiveSummaryTab, ThreatIntelTab, AIPerformanceTab, InfrastructureTab, ReportFilters
      * Integrations Page: IntegrationGrid, IntegrationCard, IntegrationFormModal, IntegrationTabs
      * Settings Page
      * Các component chung mới: FloatingPanel, BottomWidgets, SecondaryWidgets, AnalyticsZone
      * Hooks mới:
        * useRealtimeBuffer.ts
        * useThreatAnalytics.ts
        * useNetworkStream.ts
      * Tối ưu mock data: Cập nhật securityData.ts và các generator (networkGenerator, syslogGenerator)

  * **Cấu trúc Frontend - Cập nhật mới nhất**
Bash
frontend/src/
├── components/
│   ├── common/              # EventModal, FloatingPanel...
│   ├── dashboard/           # KPIOverview, AnalyticsZone, BottomWidgets...
│   ├── network/             # NetworkChart, NetworkStreamTable... (MỚI)
│   ├── playbooks/           # PlaybookList, PlaybookModal... (MỚI)
│   ├── reports/             # Report tabs (MỚI)
│   ├── integrations/        # Integration components (MỚI)
│   └── layout/              # Sidebar, Header...
├── pages/
│   ├── Dashboard.tsx
│   ├── NetworkMonitoringPage.tsx   (MỚI)
│   ├── PlaybooksPage.tsx           (MỚI)
│   ├── ReportsPage.tsx             (MỚI)
│   ├── IntegrationsPage.tsx        (MỚI)
│   └── SettingsPage.tsx            (MỚI)
├── hooks/                   # useSocket, useRealtimeBuffer, useNetworkStream...
├── mocks/
├── utils/
├── types/
└── App.tsx

  * **Tính năng cốt lõi - Tiến độ hiện tại**
    * Hoàn thành tốt:
      * Dark/Light mode + Animation mượt
      * KPI Overview
      * Realtime Alert Feed (cải thiện list & animation)
      * Event Detail Modal (chi tiết, MITRE, Evidence, AI Analysis)
      * Header (WebSocket status, AI Engine, User)
      * Network Activity Page (mới)
      * Playbooks & Reports sections
    * Sẵn sàng tích hợp:
      * WebSocket client (useSocket.ts)
      * Contract data (snake_case ↔ camelCase)
      * Action buttons (Block IP, Export, Create Ticket)

  * **Hướng dẫn chạy local**
Bash
cd frontend
pnpm install
cp .env.example .env
pnpm dev

## Thứ 2: Thực hành triển khai AWS Storage Gateway và File Shares
* **Tổng quan**
  * Workshop giúp người đọc tìm hiểu và thực hành:
    * Cách khởi tạo Storage Gateway
    * Cách tạo các File Share
    * Cách kết nối/gắn ổ đĩa File Sharing đó lên máy chủ On-premise

* **Bố cục các bước thực hiện chi tiết**
  * **Chuẩn bị**
    * Khởi tạo S3 Bucket: Tạo bộ lưu trữ Amazon S3 trên đám mây, nơi dữ liệu thực tế sẽ được đồng bộ và lưu trữ
    * Khởi tạo EC2 làm Storage Gateway (Create EC2 for Storage Gateway): Cấu hình một máy ảo Amazon EC2 đóng vai trò giả lập hoặc làm cổng kết nối Storage Gateway trong môi trường lab

  * **Sử dụng AWS Storage Gateway**
    * Khởi tạo Storage Gateway: Thiết lập cấu hình và kích hoạt cổng lưu trữ Storage Gateway để kết nối giữa local và cloud
    * Tạo các File Share (Create File Shares): Cấu hình các mục chia sẻ tệp tin dựa trên nền tảng S3 đã tạo trước đó
    * Gắn File Shares lên máy On-premises (Mount File shares on On-premises machine): Hướng dẫn các lệnh hoặc thao tác để máy chủ local nhận diện và sử dụng ổ đĩa mạng này như một ổ đĩa thông thường.

  * **Dọn dẹp tài nguyên**
    * Hướng dẫn xóa các tài nguyên đã tạo (S3 Bucket, EC2, Storage Gateway...) sau khi hoàn thành bài thực hành để tránh phát sinh chi phí ngoài ý muốn trên tài khoản AWS

* **Tạo S3 Bucket**
  * Truy cập vào giao diện quản trị dịch vụ S3
    * Click Create bucket
  * Đặt tên s3 bucket của chúng ta là s3-instancestoragegw-2023
  * Kéo màn hình xuống dưới, sau đó click Create bucket
  * Đảm bảo bucket được tạo thành công như hình dưới, trước khi qua các bước tiếp theo

* **Tạo EC2 cho Storage Gateway**
  * Truy cập vào giao diện quản trị dịch vụ Storage Gateway
    * Chúng ta sẽ sử dụng Region Singapore (ap-southeast-1) nếu bị đổi region
    * Click Create gateway

  * Kéo màn hình xuống phần Platform options, Chọn Amazon EC2
    * Click Customize your settings
    * Chọn Launch instance

  * AWS sẽ tự động lựa chọn AMI cho việc khởi tạo

  * Kéo màn hình xuống phần Instance type, Chọn m4.large

  * Kéo màn hình xuống phần Key pair, Chọn Create new key pair
    * Đặt tên Key pair name là storagegw-key
    * Click RSA ở mục Key pair type
    * Click .pem ở mục Key pair file format
    * Chọn Create key pair
    * Sau đó chọn storagegw-key ở mục Key pair name -required

  * Kéo màn hình xuống phần Network settings, Chọn Edit

  * Kéo màn hình xuống phần Firewall (security groups)
    * Tại mục Security group name điền storagegw-instance-sg
    * Tại mục Description điền storagegw-instance-sg

  * Kéo màn hình xuống phần Inbound security groups rules
    * Click Add security group rule để thêm một rule
    * Tại mục Type Chọn Custom TCP
    * Tại mục Port range điền 111
    * Tại mục Source type Chọn Custom
    * Tại mục Source type Chọn 0.0.0.0/0
    * Tương tự với các rule khác
    * Rule 3, 4
    * Rule 5, 6
    * Rule 7, 8
    * Rule 9, 10
    * Rule 11, 12
    * Rule 13, 14
  
  * Kéo màn hình xuống phần Configure storage
    * Click Add new volume
    * Tại mục dung lượng điền 150

  * Click Launch instance

  * Click View all instances chọn Public IP của Instance và lưu lại để sử dụng ở bước sau

* **Tạo Storage Gateway**
  * **Tạo Storage Gateway**
    * Truy cập vào giao diện quản trị dịch vụ Storage Gateway
      * Chúng ta sẽ sử dụng Region Singapore (ap-southeast-1) nếu bị đổi region
      * Click Create gateway

    * Trong phần Gateway settings
      * Tại mục Gateway name điền filesgw

    * Kéo màn hình xuống phần Platform options, Chọn Amazon EC2
      * Click Customize your settings

    * Kéo màn hình xuống dưới, Chọn I completed all the steps above and launched the EC2 instance
      * Click Next

    * Trong phần Gateway settings
      * Tại mục Gateway name điền 54.179.17.167 (Public IP của Instance chúng ta đã tạo ở cuối mục 1.2)
      * Click Next

    * Tại trang Review and activate, Click Next

    * Trong phần Configure cache storage, mục Allocated to Chọn Cache
      * Trong phần CloudWatch log group, Chọn Deactivate logging

    * Trong phần CloudWatch alarms
      * Click No alarm
      * Sau đó chọn Configure
      * Hoàn tất xong việc tạo Gateway

  * **Thiết lập cấu hình SMB**
    * Khi bạn sử dụng SMB File share cho các máy Windows, bạn sẽ cần cấu hình chứng thực cho SMB:
      * Truy cập vào giao diện quản trị dịch vụ Storage Gateway
        * Click Gateways
        * Chọn vào Gateway mà chúng ta đã tạo trước đó
        * Click Actions
        * Click Edit SMB settings
        * Click Guest access settings

      * Tại mục Guest password điền mật khẩu bạn muốn và phải ghi nhớ để sử dụng
        * Click Save changes

* **Tạo File Shares**
  * Truy cập vào giao diện quản trị dịch vụ Storage Gateway
    * Click File Shares
    * Click Create file share

  * Tại mục Gateway Chọn filesgw.
    * Tại mục File share type Chọn SMB
    * Tại mục Amazon S3 bucket name chọn s3-instancestoragegw-2023 (tên S3 bucket chúng ta đã tạo)
    * Tại mục User Authentication Chọn Guest access
    * Sau đó chọn Configure
    * Nhập mật khẩu ta đã tạo trước đó và sau đó click Save

  * Kéo màn hình xuống dưới và Click Create file share
    * Hoàn tất tạo File shares

* **Kết nối File shares ở máy On-premise**
  * Truy cập vào giao diện quản trị dịch vụ Storage Gateway
    * Click File Shares
    * Click tên File Shares chúng ta đã tạo
  
  * Ở mục thông tin của File share mà bạn đã tạo sẽ hiển thị câu lệnh mà bạn có thể tham khảo để sử dụng cho việc mount file share
  * Ở máy Windows của bạn phía On-premise, sử dụng Command Prompt để chạy lệnh
  * Nhập Guest password mà bạn đã thiết lập ở mục Guest access ở phần trước, Nhấn Enter
  * Bạn hãy kiểm tra trong File Explorer của Windows sẽ thấy một ổ đĩa Z mới xuất hiện
  * Tạo một tập tin vào ổ đĩa này và kiểm tra lại trên S3 bucket, bạn sẽ thấy tập tin sẽ được đồng bộ với S3 bucket
    * Truy cập vào S3 đã tạo trước đó, tập tin được đồng bộ

* **Dọn dẹp tài nguyên**
  * **Xoá Storage Gateway**
    * Truy cập vào giao diện quản trị dịch vụ Storage Gateway
      * Chọn Region Singapore
      * Click Gateways
      * Chọn vào Gateway mà chúng ta đã tạo trước đó
      * Click Actions
      * Click Delete gateway
      * Delete Storage Gateway
      * Gõ delete
      * Click Delete để xác nhận xóa

  * **Xoá EC2 Instance**
    * Truy cập Amazon EC2 console
      * Trên thanh điều hướng bên trái, chọn Instances
      * Chọn EC2 Instance chúng ta tạo cho bài lab
      * Click Instance state
      * Click Terminate instance
      * Click Terminate

  * **Xoá S3 bucket**
    * Truy cập vào giao diện quản trị dịch vụ S3
      * Click chọn S3 bucket s3-instancestoragegw-2023
      * Click Empty

    * Điền permanently delete để xác nhận, sau đó click Empty để xóa toàn bộ dữ liệu trong S3 bucket
      * Click Exit để trở lại giao diện S3

    * Click chọn S3 bucket s3-instancestoragegw-2023, sau đó click Delete

    * Điền tên bucket sau đó click Delete bucket để xóa S3 bucket

## Thứ 3: Virtual Machine Migration Guide (AWS VM Import/Export)
* **Tổng quan**
  * **Khái niệm cốt lõi:**
    * **VM Import/Export:** Là tính năng cho phép di chuyển các hình ảnh máy ảo từ môi trường on-premises lên Amazon EC2 và ngược lại, xuất từ EC2 về lại on-premises. Tính năng này giúp:
      * Dịch chuyển các ứng dụng và khối lượng công việc hiện có lên Amazon EC2
      * Tạo bản sao lưu cho các máy ảo on-premises trên Amazon EC2
      * Hỗ trợ cho các kịch bản khắc phục sự cố sau thảm họa
      * Chi phí: Tính năng này không tốn thêm phí dịch vụ (người dùng chỉ trả tiền cho các tài nguyên EC2 và bộ lưu trữ Amazon S3 thực tế sử dụng)

    * **Amazon S3:** Là dịch vụ lưu trữ đối tượng được sử dụng trong bài lab này để chứa các file máy ảo trước khi import hoặc sau khi export. Mỗi bucket có thể chứa các đối tượng có dung lượng lên tới 5 TB và không giới hạn số lượng file

* **Cấu trúc các bước thực hiện chi tiết trong Bài Lab**
  * Menu điều hướng của trang web chia lộ trình thực hành thành các chương cụ thể sau:
    * **VMWare Workstation**
      * Hướng dẫn chuẩn bị và cấu hình môi trường máy ảo trên phần mềm VMware Workstation tại máy cá nhân/on-premises để làm tài nguyên mẫu đem đi thực hành

    * **Import virtual machine to AWS**
      * Quá trình này được chia nhỏ thành 4 bước:
        * Export Virtual Machine from On-premises: Xuất file máy ảo từ môi trường ảo hóa nội bộ (VMware) thành các định dạng được AWS hỗ trợ (như OVA, VMDK, VHD,...)
        * Upload virtual machine to AWS: Sử dụng AWS CLI hoặc Console để tải (upload) file máy ảo đã xuất lên một Amazon S3 bucket
        * Import virtual machine to AWS: Thực hiện lệnh/cấu hình dịch vụ VM Import để chuyển đổi file máy ảo đang lưu ở S3 thành một Amazon Machine Image (AMI) hoặc Snapshot
        * Deploy Instance from AMI: Tiến hành khởi tạo (deploy) một máy ảo EC2 Instance mới từ file AMI vừa được import thành công để kiểm tra hoạt động

    * **Export instance from AWS**
      * Quá trình đưa một máy ảo từ đám mây ngược về máy cá nhân bao gồm:
        * Setting up S3 bucket ACL: Cấu hình quyền truy cập (Access Control List - ACL) cho S3 bucket nhằm cho phép dịch vụ VM Export có quyền ghi file cấu hình máy ảo vào đó
        * Export virtual machine from Instance: Hướng dẫn cách xuất trực tiếp một EC2 Instance đang chạy thành file máy ảo tải về
        * Export virtual machine from AMI: Hướng dẫn cách xuất một bản sao lưu AMI thành file máy ảo

    * **Các nội dung bổ sung**
      * **Reference video:** Cung cấp video hướng dẫn trực quan để người học dễ dàng làm theo từng bước thao tác thực tế
      * **Resource Cleanup on AWS Cloud:** Hướng dẫn dọn dẹp các tài nguyên sau khi làm xong bài lab (Xóa EC2 instance, xóa AMI, xóa S3 bucket) nhằm tránh phát sinh chi phí ngoài ý muốn trên tài khoản AWS Cloud

* **Chuẩn bị máy ảo**
  * Bắt đầu bằng việc cài đặt VMware Workstation Pro từ đây
  * Tiếp theo, tải hệ điều hành Ubuntu
  * Mở VMware Workstation và chọn Create a New Virtual Machine
  * Ở màn hình Welcome to the New Virtual Machine Wizard, chọn Typical (recommended)
  * Tại màn hình Guest Operating System Installation, chọn Image file (.iso) của phiên bản mới nhất của Ubuntu dành cho Desktop. Bạn có thể tải tệp này từ Ubuntu Releases
  * Tại màn hình Easy Install Information, nhập Username là awsstudent và đặt password tương ứng
  * Đặt tên cho instance tại màn hình Name the Virtual Machine, ví dụ: Ubuntu
  * Thiết lập dung lượng storage tại màn hình Specify Disk Capacity, nhập giá trị 20GB
  * Xem lại các thông số và chọn Finish để bắt đầu quá trình cài đặt
  * Hoàn tất quá trình cài đặt hệ điều hành Ubuntu trên VMware
  * Thực hiện cấu hình cho user
  * Khi quá trình cài đặt và cấu hình hoàn tất, bạn cần cài đặt OpenSSH Server để có thể kết nối SSH tới instance qua các lệnh sau:
    ```bash
    sudo apt install openssh-server
    sudo systemctl start ssh
    sudo systemctl enable ssh
    ```

* **Export máy ảo từ On-premise**
  * Bước này sẽ hướng dẫn cách xuất máy ảo từ VMWare Workstation để chuẩn bị cho việc chuyển đổi lên nền tảng AWS
    * Mở ứng dụng VMWare Workstation, chọn máy ảo bạn muốn xuất, sau đó nhấn vào File và chọn Export to OVF…
    * Chọn vị trí để lưu tệp xuất máy ảo
    * Đợi khoảng 5 phút cho quá trình xuất máy ảo hoàn tất
    * Truy cập vào vị trí bạn đã chọn để lưu tệp máy ảo sau khi xuất. Tập tin quan trọng mà chúng ta sẽ sử dụng là tệp .vmdk

* **Tải máy ảo lên AWS**
  * **Tạo S3 bucket để lưu trữ máy ảo**
    * Để tạo S3 bucket, thực hiện các bước sau:
      * Truy cập vào Amazon S3 console
        * Trong thanh điều hướng, chọn Buckets
        * Chọn Create bucket để tạo một S3 bucket mới

      * Trong trang Create bucket, cấu hình các thông số cho S3 bucket:
        * Bucket name: Nhập tên cho bucket. Tên này phải là duy nhất trên toàn cầu. (Ví dụ: import-bucket-2023)
        * AWS Region: Chọn Region cho bucket

      * Bỏ chọn tùy chọn Block all public access để cho phép truy cập công khai. AWS sẽ hiển thị cảnh báo, chọn I acknowledge that the current settings might result in this bucket and the objects within becoming public

      * Chọn Create bucket

      * Bucket được tạo thành công.

  * **Tải máy ảo lên S3 bucket**
    * Sau khi tạo bucket, tiếp theo chúng ta sẽ tải lên các tập tin máy ảo đã được xuất từ môi trường ảo hóa on-premises
      * Truy cập vào S3 bucket vừa tạo. (Ví dụ: import-bucket-2023)
      * Tại phần Objects, chọn Upload.

    * Kéo và thả các tập tin máy ảo vào cửa sổ này hoặc chọn Add files để chọn các tập tin máy ảo. Sau đó, nhấn Upload. Trong ví dụ này, chúng ta đã tạo máy ảo bằng VMware Workstation, tập tin máy ảo là Ubuntu-disk1.vmdk

    * Quá trình tải lên tập tin vào S3 bucket sẽ mất một khoảng thời gian nhất định

* **Import máy ảo vào AWS**
  * Trước khi thực hiện việc import máy ảo vào AWS, bạn cần tạo IAM role cần thiết
    * Truy cập vào AWS IAM console
    * Trong thanh điều hướng, chọn Roles
    * Nếu chưa có role vmimport, tiến hành tạo role này
    * Tạo một file có tên trust-policy.json để cho phép dịch vụ VM Import/Export assume role vmimport:
    * Sử dụng AWS CLI command create-role để tạo IAM role vmimport và gán trust policy:
    * Kiểm tra role đã tạo trong IAM console
    * Xem Trust relationships của role
    * Tạo file role-policy.json chứa các IAM policy cần thiết:
    * Gán policy vào role vmimport sử dụng AWS CLI command put-role-policy:
    * Kiểm tra permissions của role trong IAM console

  * **Import máy ảo thành AMI**
    * Sử dụng AWS CLI để import máy ảo thành AMI:
      * Chạy AWS CLI command ec2 import-image:
      * Quá trình import có thể mất 5-10 phút tùy kích thước máy ảo
      * Sau khi hoàn thành, AMI mới sẽ xuất hiện trong danh sách AMIs với AMI name là task ID
      * Kiểm tra để đảm bảo Amazon EBS volume không bị encrypted

* **Triển khai EC2 Instance từ AMI**
  * Dưới đây là hướng dẫn chi tiết để triển khai EC2 instance từ AMI vừa được import:
    * Truy cập vào Amazon EC2 console
    * Trong navigation pane, chọn mục AMIs
    * Tìm và chọn AMI bạn vừa import (ví dụ: import-ami-08a9efac866dfcb04) và click nút Launch instance from AMI
    * Name: Nhập tên cho EC2 instance, ví dụ: Import-Server
    * AMI: Giữ nguyên AMI mặc định đã chọn
    * Instance type: Giữ nguyên instance type đã chọn và click Create new key pair
    * Key pair name: Nhập tên cho key pair và click Create key pair
    * Network settings: Giữ nguyên cấu hình mạng mặc định
    * Click View all instances
    * Xác nhận thông tin instance vừa tạo
    * Thực hiện SSH connection tới instance
    * Chọn SSH client để lấy thông tin kết nối
    * Hoàn tất nhập thông tin SSH connection
    * Nhập password để hoàn tất SSH authentication
    * Sau khi SSH connection thành công, bạn đã triển khai xong EC2 instance từ AMI và có thể kiểm tra connectivity bằng lệnh ping

* **Thiết lập ACL cho S3 Bucket**
  * **Hướng dẫn lưu trữ bản Export trên Amazon S3 Bucket**
    * Khi thực hiện export instance từ môi trường AWS sang các môi trường ảo hóa khác, việc lưu trữ chúng trên S3 bucket là rất quan trọng

  * **Tạo S3 Bucket để lưu trữ bản Export**
    * Truy cập Amazon S3 Management Console
    * Trong navigation pane, chọn Buckets
    * Click Create bucket để tạo một S3 bucket mới
    * Tại trang Create bucket, nhập các thông tin cần thiết:
      * Bucket name: Nhập tên cho bucket. Tên phải là globally unique. Ví dụ: export-bucket-2023
      * AWS Region: Chọn region cho bucket

  * **Cấu hình Block Public Access và Permissions**
    * Bỏ chọn Block all public access để cho phép public access. AWS sẽ hiển thị warning, bạn cần chọn I acknowledge that the current settings might result in this bucket and the objects within becoming public
    * Click Create bucket

  * **Cấu hình Access Control List (ACL)**
    * Chọn Bucket owner enforced trong phần Object Ownership
    * Enable ACLs, sau đó click Save changes
    * Click Add grantee
    * Nhập Canonical ID và chọn Write Objects và Read bucket ACL permissions, sau đó click Save changes

  * Lưu ý: Canonical ID sẽ khác nhau tùy theo AWS Region. Dưới đây là danh sách Canonical ID cho user vm-import-export@amazon.com theo từng region.

  * **Danh sách Canonical ID của user vm-import-export@amazon.com theo từng AWS Region:**
    * Africa (Cape Town)
    * f7744aeebaf91dd60ab135eb1cf908700c8d2bc9133e61261e6c582be6e33ee
    * Asia Pacific (Hong Kong)
    * 97ee7ab57cc9b5034f31e107741a968e595c0d7a19ec23330eae8d045a46edfb
    * Europe (Milan)
    * 04636d9a349e458b0c1cbf1421858b9788b4ec28b066148d4907bb15c52b5b9c
    * Middle East (Bahrain)
    * aa763f2cf70006650562c62a09433f04353db3cba6ba6aeb3550fdc8065d3d9f
    * China (Beijing)
    * 834bafd86b15b6ca71074df0fd1f93d234b9d5e848a2cb31f880c149003ce36f
    * AWS GovCloud (US)
    * af913ca13efe7a94b88392711f6cfc8aa07c9d1454d4f190a624b126733a5602
    * Other Regions
    * c4d8eabf8db69dbe46bfe0e517100c554f01200b104d59cd408e777ba442a322

* **Export máy ảo từ EC2 Instance**
  * **Export máy ảo từ EC2 Instance**
    * Truy cập vào Amazon EC2 console để lấy thông tin Instance ID cần export

    * Chạy lệnh aws ec2 create-instance-export-task để khởi tạo task export EC2 Instance ra định dạng phù hợp với môi trường ảo hóa đích. Cần nhập các tham số sau:
      * --instance-id: Instance ID đã lấy từ danh sách EC2 instances
      * --target-environment: Môi trường ảo hóa đích (VD: vmware)
      * --export-to-s3-task: Xác định các thông số của máy ảo được export:
        * Định dạng (vmdk)
        * S3 bucket lưu trữ (export-bucket-2021)
        * Prefix trong bucket (vms/)
      * Để tránh lỗi nhập liệu, tạo file JSON export-task.json chứa các thông số cho --export-to-s3-task:

    * Quá trình export có thể mất một khoảng thời gian. Sử dụng lệnh sau để kiểm tra tiến độ:

    * Sau khi hoàn thành, file máy ảo sẽ được lưu trong S3 bucket đã chỉ định

  * **Thử nghiệm triển khai máy ảo đã export**
    * Sau khi download file disk image (VMDK hoặc VHD) về hệ thống on-premises, bạn có thể triển khai máy ảo sử dụng file này trên nền tảng ảo hóa tương ứng (VMware hoặc Hyper-V)

* **Export máy ảo từ AMI**
  * **Export máy ảo từ Amazon EC2 AMI**
    * Để export máy ảo nhằm triển khai lên môi trường ảo hóa on-premises, AWS hỗ trợ việc export từ AMI thông qua việc sử dụng AWS CLI
    * Truy cập vào EC2 Management Console để lấy thông tin AMI ID cần export

    * Chạy lệnh aws ec2 export-image để khởi chạy tiến trình export AMI ra định dạng mong muốn cho môi trường ảo hóa của bạn
      * --image-id: AMI ID đã lấy từ danh sách EC2 instance
      * --disk-image-format: Định dạng tập tin máy ảo/đĩa ảo (ví dụ: vmdk hoặc vhdx)
      * --s3-export-location: Xác định vị trí tập tin được export ra:
        * S3 bucket lưu trữ (ví dụ: import-bucket-2021)
        * Đường dẫn lưu trữ trong bucket (ví dụ: export/)

    * Quá trình export AMI ra tập tin VHD (để triển khai trên Hyper-V) hoặc VMDK (cho VMware) sẽ mất một khoảng thời gian. Bạn có thể sử dụng lệnh aws ec2 describe-export-image-tasks để kiểm tra tiến độ export:

    * Sau khi hoàn thành, bạn sẽ có tập tin đĩa ảo của máy ảo được lưu trữ trong S3 bucket.

  * **Thử nghiệm triển khai máy ảo đã export**
    * Sau khi tải tập tin đĩa ảo VHD về hệ thống on-premises, bạn có thể thử triển khai máy ảo sử dụng tập tin VHD này trên nền tảng ảo hóa tương ứng

## Thứ 4: Thực hành Gắn Thẻ (Tags) và Nhóm Tài Nguyên (Resource Groups) trên AWS
* **Tổng quan & Khái niệm**
  * **Tag (Thẻ):** Là các nhãn (nhập dưới dạng cặp Key - Khóa và Value - Giá trị) được gán vào tài nguyên AWS nhằm phân loại chúng theo mục đích, chủ sở hữu hoặc môi trường, giúp người dùng dễ dàng tìm kiếm và quản lý khi số lượng tài nguyên lớn
  * **AWS Resource Groups:** Là tính năng giúp quản lý và tự động hóa các thao tác trên nhiều tài nguyên cùng một lúc thông qua việc gom nhóm dựa trên Tag (Tag-based) hoặc theo CloudFormation stack

* **Chi tiết các bước thực hành trong Workshop**
  * Nội dung bài học được chia thành các chương mục rõ ràng để người học làm theo:
    * **Giới thiệu:** Tổng quan về lý do và lợi ích của việc gắn tag cũng như tạo nhóm tài nguyên
    * **Sử dụng Tag:**
      * Sử dụng tag trên giao diện Console:
        * Tạo EC2 Instance có tag: Hướng dẫn từng bước khởi tạo một máy ảo và đính kèm các thẻ định danh ngay từ đầu
        * Thêm hoặc xóa tag: Cách chỉnh sửa, bổ sung hoặc loại bỏ các thẻ của tài nguyên đang hoạt động
        * Lọc tài nguyên theo tag: Cách tìm kiếm nhanh các tài nguyên dựa trên các bộ lọc thẻ đã tạo
      * Sử dụng tag bằng CLI: Hướng dẫn quản lý, gán và lọc thẻ thông qua giao diện dòng lệnh (AWS Command Line Interface)
    * Tạo một Resource Group: Hướng dẫn cách tạo một nhóm tài nguyên (Resource Group) dựa trên các điều kiện thẻ (Tag-based) để quản lý tập trung
    * Dọn dẹp tài nguyên: Hướng dẫn xóa bỏ các tài nguyên đã tạo trong bài lab để tránh phát sinh chi phí không mong muốn trên tài khoản AWS

* **Tạo EC2 Instance có tag**
  * Truy cập EC2 Management Console
    * Nhấp vào Launch Instances
  * Nhấp vào Select để chọn AMI
  * Tại trang Choose an Instance Type
    * Nhấp vào Review and Launch
  * Tại trang Review Instance Launch
    * Kéo màn hình xuống dưới cùng
    * Nhấp vào Edit Tags để thực hiện chỉnh sửa tag cho EC2 instance
  * Nhấp vào Add Tag để tiến hành thêm tag
  * Điền các giá trị Tag như hình dưới và nhấp vào Review and Launch
  * Nhấp vào Launch để tiến hành tạo EC2 instance
  * Chọn Create a new key pair
    * Chọn Key pair type là RSA
    * Đặt tên Key pair name là TestTagging
    * Nhấp vào Download Key Pair
    * Nhấp vào Launch Instances
  * Nhấp vào View Instances để xem EC2 instance chúng ta vừa tạo
  * Nhấp chọn EC2 Instance chúng ta vừa tạo
    * Nhấp vào tab Tags để kiểm tra các tag đã tạo
  * Lặp lại các bước từ 1 - 10 để tạo thêm EC2 Instance có Tag như sau:
    | Key         | Value       |
    | ----------- | ----------- |
    | Owner       | Yourname    |
    | Service     | Yourservice |
    | Environment | UAT         |
  * Bước tiếp theo chúng ta sẽ thực hiện thêm các Tag mới cho EC2 instance của chúng ta

* **Thêm hoặc xóa tag**
  * **Thêm hoặc xóa tag trên các tài nguyên đơn lẻ**
    * Truy cập Amazon EC2 Console
    * Tại thanh điều hướng phía trên, chọn Region cần thao tác ( Hiện tại chúng ta đang dùng Region Singapore )
    * Tại thanh bên trái, chọn loại tài nguyên muốn gắn tag (ví dụ: Instances)
    * Click chọn tài nguyên cần gắn tag từ danh sách các tài nguyên, chọn vào tab Tags, và chọn Manage tags
    * Chọn tiếp Add tag. Nhập thông tin Key và Value cho tag như hình dưới và nhấn Save
      * Chúng ta đã thêm tag giúp xác định hệ điều hành cho EC2 Instance

  * **Thêm hoặc xóa tag trên các nhóm các tài nguyên**
    * Truy cập Amazon EC2 Console
    * Tại thanh bên trái, chọn Tags
    * Chọn Manage Tags
    * Tại trang Manage Tags, chọn loại tài nguyên cần lọc tại Filter (ví dụ: Instances)
    * Để thêm tag trên nhóm các tài nguyên:
      * Chọn các tài nguyên muốn gắn tag
      * Tại Add Tag, điền thông tin Key và Value của tag và chọn Add Tag
    * Để xóa tag trên nhóm các tài nguyên:
      * Chọn các tài nguyên muốn xóa tag
      * Tại Remove Tag, điền thông tin Key và chọn Remove Tag

* **Lọc tài nguyên theo tag**
  * Nhấn vào Instance để trở về danh sách EC2 Instance
  * Nhấn vào ô Lọc Instances
    * Chọn tag Owner từ danh sách
  * Chọn Owner: Tên của bạn
  * Kết quả sẽ hiển thị thông tin tài nguyên đã được gắn tag và có giá trị tương ứng với lựa chọn của bạn
  * Sau khi hoàn tất, chọn Xóa bộ lọc để loại bỏ các bộ lọc

* **Sử dụng tag bằng CLI**
  * **Thêm tag cho tài nguyên hiện có**
    * Sử dụng CLI create-tags với tham số --resources và --tags
      * aws ec2 create-tags --resources <ResourceID> --tags Key=<Key>,Value=<Value>
    * Ví dụ: bạn muốn tạo tag là “Key=Environment,Value=Test” cho tài nguyên là một EC2 instance. Vậy, tham số của bạn sẽ là:
      * aws ec2 create-tags --resources i-01234example56789 --tags Key=Environment,Value=Test

  * **Thêm tag cho tài nguyên mới**
    * **Thêm tag cho máy ảo mới**
      * Sử dụng CLI run-instances để tạo máy ảo mới và dùng tham số --tag-spectifications để khai báo thông tin tag như sau:
        ```bash
        aws ec2 run-instances\
        --image-id <image-id> \
        --count 1 \
        --instance-type t2.micro \
        --key-name <YourKeyPair> \
        --subnet-id <YouSubnetID> \
        --tag-specifications ResourceType=instance,Tags=[{Key=Environment,Value=Test}] ResourceType=volume,Tags=[{Key=Environment,Value=Test}] 
        #Volume được tạo cùng instace cũng sẽ có tag "Key=Environment,Value=Test"
        ```
      * Lưu ý: Bạn sẽ phải thay thế những tham số phù hợp với tài khoản của bạn

    * **Thêm tag cho ổ đĩa mới**
      * Sử dụng CLI create-volume để tạo volume mới và dùng tham số --tag-specifications để khai báo thông tin tag như sau:
        ``` bash
        aws ec2 create-volume \
        --availability-zone ap-southeast-1a \
        --volume-type gp2 \
        --size 80 \
        --tag-specifications ResourceType=volume,Tags=[{Key=Environment,Value=Test},{Key=cost-center,Value=cc123}]
        #Volume được tạo sẽ được gán 2 tag là "Key=Environment,Value=Test" và "Key=cost-center,Value=cc123"
        ```
      * Lưu ý: Bạn sẽ phải thay thế những tham số phù hợp với tài khoản của bạn

  * **Mô tả các tài nguyên được gắn tag**
    * Sử dụng CLI derscibe-instances với tham số --filters:
      * aws ec2 describe-instances --filters Name=tag-key,Values=<SampleTagKey>

* **Tạo một Resource Group**
  * Ở bước này, bạn sẽ tạo một Resource Group được phân loại theo thẻ. Phần Tag trong bài lab này ví dụ, bạn có thể thêm tùy chọn theo Tag đã tạo
    * Truy cập vào AWS Resource Group Console
    * Ở thanh bên trái, click chọn Create Resource Group
    * Ở trang Create query-based group, dưới mục Group type, chọn Tag-based để tạo một Resource Group được phân loại theo thẻ
    * Ở mục Grouping criteria, làm theo hướng dẫn sau:
      * Chọn Resource types (loại tài nguyên) là AWS::EC2::Instance. Bạn có thể chọn tối đa 20 loại tài nguyên
    * Dưới Tags, nhập thẻ “Key=BusinessUnit,Value=Marketing” và sau đó nhấn Add để thêm thẻ. Bạn có thể thêm Tag đã tạo ở bước trước
    * Click Preview group resources để thể hiện ở mục Group Resources các tài nguyên có loại tài nguyên và thẻ đã nêu ở trên
    * Ở mục Group details, nhập các thông số sau:
      * Group name: MarketingBU
      * Group description - optional: nhập mô tả cho Resource Group (ví du: Servers of Marketing BU)
      * Kiểm tra và click Create group
    * Sau khi Resource Group đã tạo thành công
      * Click Saved Resource Group để xem các Resource Group chúng ta đã tạo
    * Click vào Resource Group MarketingBU
    * Kéo xuống mục Group resources, bạn sẽ thấy tất cả các tài nguyên thuộc Resource Group này

* **Dọn dẹp tài nguyên**
  * **Xóa EC2 Instance**
    * Truy cập EC2 Management Console
    * Trên thanh điều hướng bên trái, chọn Intances
    * Chọn tất cả EC2 Instance liên quan tới bài lab (bạn có thể sử dụng thẻ để lọc các instance cần xóa hoặc tham khảo Resource Group được tạo)
    * Click Actions
    * Click Manage Instance State
    * Click chọn Terminate
    * Click Change State , sau đó click Terminate

  * **Xóa Resource Group**
    * Truy cập vào AWS Resource Group Console
    * Click Saved Resource Group ở thanh bên trái
    * Click vào tên Resource Group liên quan tới bài lab ( MarketingBU )
    * Click Delete, sau đó click Delete một lần nữa để xác nhận xóa Resource Group

## Thứ 5: Thực hành AWS Security Hub
* **Tổng quan về AWS Security Hub**
  * AWS Security Hub là dịch vụ cung cấp cho bạn một cái nhìn toàn diện về các cảnh báo bảo mật có mức độ ưu tiên cao và trạng thái tuân thủ (compliance status) trên toàn bộ các tài khoản AWS của bạn
  * Vấn đề giải quyết: Thông thường, các doanh nghiệp sử dụng rất nhiều công cụ bảo mật khác nhau (từ tường lửa, ứng dụng bảo vệ điểm cuối đến quét lỗ hổng bảo mật). Việc này khiến đội ngũ quản trị phải liên tục chuyển đổi qua lại giữa các công cụ để xử lý hàng trăm, hàng ngàn cảnh báo mỗi ngày
  * Giải pháp từ Security Hub: Dịch vụ này đóng vai trò như một nơi tập trung duy nhất để sắp xếp và ưu tiên các cảnh báo bảo mật hoặc các phát hiện (findings) từ nhiều dịch vụ AWS khác nhau (như Amazon GuardDuty, Amazon Inspector, Amazon Macie) hoặc từ các giải pháp của các đối tác AWS
  * Tính năng hiển thị: Các rủi ro tìm thấy được tóm tắt trực quan trên một bảng điều khiển (dashboard) tích hợp với các biểu đồ và bảng số liệu có khả năng tương tác
  * Giám sát liên tục: Bạn có thể liên tục theo dõi hệ thống của mình bằng cách sử dụng các tính năng kiểm tra tuân thủ tự động dựa trên các tiêu chuẩn thực hành tốt nhất của AWS (AWS best practices) và các tiêu chuẩn công nghiệp mà tổ chức của bạn áp dụng

* **Chi phí ước tính**
  * Mức phí thông thường: Đối với tài khoản chỉ dùng để thử nghiệm, thực hành và không thực hiện các cuộc tấn công mô phỏng, chi phí thường sẽ thấp hơn $1 mỗi tháng
  * Chi tiết bảng giá AWS Security Hub:
    * Kiểm tra bảo mật (Security checks):
      * 100.000 lượt kiểm tra đầu tiên: 0.0010 USD / lượt kiểm tra
      * 100.001 – 500.000 lượt kiểm tra: 0.0008 USD / lượt kiểm tra
      * Trên 500.001 lượt kiểm tra: 0.0005 USD / lượt kiểm tra
    * Sự kiện thu thập phát hiện (Finding ingestion events):
      * 10.000 sự kiện đầu tiên: Miễn phí
      * Từ sự kiện thứ 10.001 trở đi: 0.00003 USD / sự kiện

* **Cấu trúc các bước thực hành trong Workshop**
  * Workshop được chia thành các phần nội dung chính để người học thực hành theo từng bước:
    * Tổng quan - nội dung chi tiết như trên
    * Các tiêu chuẩn bảo mật
    * Hướng dẫn các bước kích hoạt dịch vụ AWS Security Hub
    * Xem và đánh giá điểm số bảo mật theo các tiêu chuẩn
    * Hướng dẫn dọn dẹp các tài nguyên sau khi thực hành xong để tránh phát sinh chi phí ngoài ý muốn

* **Kích hoạt Security Hub**
  * **Tổng quan**
    * Để kích hoạt Security Hub, AWS có cung cấp cho người dùng một giao diện hình ảnh để tương tác với dịch vụ này. Ở bước này, chúng ta sẽ kích hoạt Security Hub thông qua giao diện console này

  * **Kích hoạt Security Hub thông qua console**
    * Để kích hoạt Security Hub trên một Region, bạn hãy làm theo các bước sau đây:
      * Đăng nhập vào Amazon Management Console. Trên thanh tìm kiếm, nhập và tìm kiếm dịch vụ Security Hub CSPM
      * Ở trang AWS Security Hub CSPM, chọn Go to Security Hub CSPM
      * Trên trang Welcome to AWS Security Hub, chọn các tiêu chuẩn về bảo mật (Security standards) như là AWS Foundational Security Best Practices, CIS AWS Foundations Benchmark, và PCI DSS
      * Chọn Enable Security Hub CSPM
      * Sau khi kích hoạt, bạn sẽ cần chờ một khoản thời gian để Security Hub đánh giá Security Score của tài khoản hiện tại của bạn so với từng bộ tiêu chuẩn bảo mật mà bạn thiết lập
      * Chọn vào mục Control để xem Security Score

  * **Cấu hình AWS Config**
    * Ở trang console, tìm kiếm và chọn dịch vụ AWS Config
    * Chọn Get started
    * Ở phần Override settings, chọn All globally recorded IAM resource type và Exclude from recording
    * Ở phần Data governance, chọn Create AWS Config service-linked role
    * Ở phần Delivery channel, chọn Create a bucket, giữ nguyên bucket name, chọn Next
    * Tiếp tục chọn Next
    * Chọn Confirm
    * Hoàn tất thiết lập AWS Config

* **Điểm từng bộ tiêu chuẩn**
  * Sau một khoản thời gian, Security Hub sẽ đưa ra các đánh giá dựa trên số điểm cũng như chỉ ra các rủi ro về bảo mật đang tồn tại trên tài khoản của bạn. Để liệt kê các rủi ro được tìm thấy, các bạn có thể truy cập vào từng bộ tiêu chuẩn để xem các điểm đánh giá:
    * Đăng nhập vào Amazon Management Console. Trên thanh tìm kiếm, nhập và tìm kiếm dịch vụ Security Hub CSPM
    * Ở thanh điều hướng bên trái, chọn Security standards để xem thông tin tổng quan về điểm đánh giá theo từng bộ tiêu chuẩn đánh giá bảo mật
    * Để xem chi tiết các tiêu chí đánh giá của từng bộ tiêu chuẩn, chọn View results (theo từng bộ tiêu chuẩn)
      * VD: Bộ tiêu chuẩn Foundational Security Best Practices v1.0.0
    * Với trường hợp bạn có một số tiêu chí không muốn áp dụng, để loại bỏ khỏi đánh giá, bạn có thể chọn vào tiêu chí đó trong danh sách của bộ tiêu chuẩn
      * Ví dụ: Bạn muốn loại bỏ EC2 instances managed by Systems Manager should have an association compliance status of COMPLIANT ở bộ tiêu chuẩn PCI DSS v3.2.1. Chọn View results
    * Sau đó chọn EC2 instances managed by Systems Manager should have an association compliance status of COMPLIANT
      * Ở trang thông tin chi tiết về tiêu chí, chọn Disable control
      * Nhập lý do loại bỏ Not aligned to risk threshold, chọn Disable

* **Dọn dẹp tài nguyên**
  * Ở phần này, bạn sẽ tắt AWS Security Hub để không phát sinh chi phí cho tài khoản AWS của bạn ( Phần lớn chi phí của việc bật Security Hub đến từ AWS Config ). Tuy nhiên, nếu bạn đang triển khai trên môi trường production, bạn nên để AWS Security Hub hoạt động để giúp bạn quản lý an ninh tài khoản tốt hơn

  * **Bỏ kích hoạt AWS Security Hub**
    * Truy cập vào Security Hub CSPM
      * Chọn Settings > General ở thanh bên trái
    * Trong trang Settings ở bên phải, chọn tab General
      * Cuộn xuống dưới cùng và chọn Disable AWS Security Hub
      * Trong prompt, chọn Disable AWS Security Hub
    * Sau đó chọn Disable AWS Security Hub CSPM

  * **Bỏ kích hoạt AWS Config**
    * Truy cập AWS Config, ở bên phải chọn Settings, chọn Stop recording
    * Chọn Confirm để xác nhận

  * **Xóa S3 Bucket**
    * Truy cập AWS S3 Bucket
    * Chọn bucket vừa tạo, chọn Empty
    * Nhập parmanently delete, chọn Empty
    * Sau khi xóa xong, chọn Exit
    * Chọn bucket vừa tạo, chọn Delete
    * Nhập tên bucket, chọn Delete bucket