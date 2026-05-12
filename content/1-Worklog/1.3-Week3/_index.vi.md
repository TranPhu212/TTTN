---
title: "Worklog Tuần 3"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.3. </b> "
---

### Mục tiêu tuần 3:
* Làm quen và thực hành sử dụng AWS Backup để xây dựng kế hoạch sao lưu và khôi phục dữ liệu tự động cho các dịch vụ AWS (EBS, RDS, DynamoDB, EFS)
* Cài đặt, cấu hình AWS CLI v2 và thực hành quản lý các dịch vụ cốt lõi qua dòng lệnh (S3, SNS, IAM, VPC, EC2)
* Triển khai và sử dụng Amazon CloudWatch để giám sát, thu thập metrics, logs, tạo alarm và dashboard

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
|  2  | - * **Thực hành** <br>&emsp; + Implemented AWS Backup system with CloudFormation deployment <br>&emsp; + Backup plan configuration <br>&emsp; + SNS notifications <br>&emsp; + Backup/restore testing | 04/05/2026 | 04/05/2026 | <https://000013.awsstudygroup.com/> |
|  3  | - Cài đặt AWS CLI v2, cấu hình Profile, thực hành quản lý Amazon S3, SNS, IAM, VPC, Internet Gateway và tạo EC2 qua dòng lệnh <br> - Dọn dẹp tài nguyên và xử lý lỗi cơ bản | 05/05/2026 | 05/05/2026 | <https://000011.awsstudygroup.com/> |
|  4  | - Triển khai Stack, Metrics, Logs Insights, Metric Filter, Alarm và Dashboard | 06/05/2026 | 06/05/2026 | <https://000008.awsstudygroup.com/> |

### Kết quả đạt được tuần 3:

## Thứ 2: Implementing AWS Backup for Systems
* **Triển khai AWS Backup cho hệ thống**
  * **Tổng quan bài thực hành**
    * Bài thực hành này hướng dẫn người dùng làm quen với dịch vụ AWS Backup để:
      * Tạo kế hoạch sao lưu (Backup plan) cho các tài nguyên phổ biến trên AWS như: EBS Volumes, RDS Databases, DynamoDB Tables, và EFS File Systems
      * Học cách khôi phục dữ liệu từ các bản sao lưu
      * Tự động hóa toàn bộ quá trình sao lưu và phục hồi

  * **Tầm quan trọng của việc sao lưu**
    * Nhấn mạnh dữ liệu là tài sản quý giá nhất của tổ chức
    * Việc sao lưu thường xuyên là yếu tố sống còn cho sự thành công lâu dài
    * Trong môi trường đám mây (Cloud), việc sao lưu và kiểm tra khôi phục trở nên dễ dàng và linh hoạt hơn so với trung tâm dữ liệu truyền thống (On-premises)

  * **Mục tiêu cụ thể**
    * Xây dựng kế hoạch sao lưu tự động
    * Thực hiện kiểm thử (Testing) quy trình sao lưu và phục hồi dữ liệu
    * Thiết lập hệ thống thông báo để đảm bảo các bên liên quan nhận được thông tin khi quy trình hoàn tất hoặc có lỗi xảy ra

  * **Các dịch vụ AWS được sử dụng trong bài**
    * AWS Backup: Dịch vụ quản lý tập trung và tự động hóa việc bảo vệ dữ liệu trên các dịch vụ AWS và môi trường on-premises. Nó cho phép thiết lập các chính sách bảo trì dữ liệu từ một nơi duy nhất
    * AWS Simple Notification Service (SNS): Dịch vụ thông báo được sử dụng để gửi tin nhắn từ bên phát (Publisher) tới bên nhận (Subscriber) thông qua các Topic. Trong bài này, SNS dùng để thông báo trạng thái của các tác vụ backup

  * **Cấu trúc các bước tiếp theo**
    * Trang giới thiệu cũng liệt kê lộ trình thực hiện bao gồm:
      * Giới thiệu (Trang hiện tại)
      * Các bước chuẩn bị (Tạo S3 Bucket, Triển khai hạ tầng)
      * Tạo Backup plan
      * Thiết lập thông báo
      * Kiểm tra hoạt động
      * Dọn dẹp tài nguyên

  * **Tạo S3 Bucket**
    * Tải template CloudFormation và Lambda Function
      * Sau khi tải template CloudFormation và Lambda Function từ link trên:
        * Chúng ta sẽ tạo một S3 bucket để lưu trữ source
        * Truy cập vào AWS Management Console, tìm và chọn S3
      * ![Tìm kiếm S3](/images/1-Worklog/1.3-Week3/Day2/SearchS3.png)
      * Trong giao diện S3, chọn Create bucket
      * ![Tạo bucket](/images/1-Worklog/1.3-Week3/Day2/Createbucket.png)
      * Trong giao diện Create bucket:
        * Nhập Bucket name, phải nhập tên duy nhất, bạn có thể chọn tùy ý (Nếu trùng sẽ dẫn đến lỗi và không khởi tạo bucket được)
      * ![Bucket Name](/images/1-Worklog/1.3-Week3/Day2/Bucket%20name.png)
      * Giữ nguyên cấu hình
      * ![Default Setting](/images/1-Worklog/1.3-Week3/Day2/DefaultSetting.png)
      * Tại mục Default encryption, chọn Disable, sau đó chọn Create bucket
      * ![Default encryption](/images/1-Worklog/1.3-Week3/Day2/Default%20encryption.png)
      * Hoàn thành tạo S3 bucket
      * ![Tạo S3 bucket thành công](/images/1-Worklog/1.3-Week3/Day2/CreateBucketSuccess.png)
      * Thực hiện tạo một folder lưu trữ
      * Trong giao diện tạo một folder:
        * Nhập tên Folder name
        * Chọn Create folder
      * ![Folder name](/images/1-Worklog/1.3-Week3/Day2/FolderName.png)
      * Hoàn thành tạo một folder
      * ![Tạo Folder thành công](/images/1-Worklog/1.3-Week3/Day2/CreateFolderSuccess.png)
      * Trong folder vừa tạo, thực hiện Upload các file đã tải về và đã giải nén
      * ![Upload các file](/images/1-Worklog/1.3-Week3/Day2/UploadFile.png)
      * Trong phần Upload:
        * Chọn Add files
        * Chọn các file muốn tải lên
        * Chọn Upload
      * ![Add files](/images/1-Worklog/1.3-Week3/Day2/AddFiles.png)
      * Hoàn thành tải các file
      * ![Tải các file thành công](/images/1-Worklog/1.3-Week3/Day2/UploadSuccess.png)
      * Thực hiện cấu hình Permissions cho S3 bucket:
        * Đối với Block public access (bucket settings)
      * ![Tải các file thành công](/images/1-Worklog/1.3-Week3/Day2/UploadSuccess.png)
      * Bỏ chọn Block all public access:
        * Sau đó, chọn Save changes
      * ![Save changes](/images/1-Worklog/1.3-Week3/Day2/Blockallpublicaccess.png)
      * Xác nhận bằng cách chọn confirm và sau đó chọn Confirm
      * ![Confirm](/images/1-Worklog/1.3-Week3/Day2/ConfirmEditBucket.png)
      * Sau đó sẽ thực hiện cấu hình Bucket policy:
        * Chọn Edit
      * ![Bucket policy](/images/1-Worklog/1.3-Week3/Day2/BucketPolicy.png)
      * Trong giao diện Edit bucket policy:
        * Nhập đoạn code sau và thay bằng Bucket ARN của bạn
      * ![Edit bucket policy](/images/1-Worklog/1.3-Week3/Day2/Editbucketpolicy.png)
      * Chọn Save changes
      * ![Save changes](/images/1-Worklog/1.3-Week3/Day2/Blockallpublicaccess.png)
      * Kiểm tra Permissions đã Public
      * ![Kiểm tra Permissions](/images/1-Worklog/1.3-Week3/Day2/PermissionsCheck.png)
      * Sao chép thông tin đường dẫn của lambda_function.zip
      * ![Sao chép thông tin đường dẫn](/images/1-Worklog/1.3-Week3/Day2/CopyURL.png)
      * Sao chép thông tin Object URL của file backup-lab.yaml 

  * **Triển khai hạ tầng**
    * Hướng dẫn cách sử dụng AWS CloudFormation để tự động hóa việc khởi tạo và triển khai các tài nguyên hạ tầng cần thiết cho các bài lab thực hành
    * Thay vì tạo thủ công từng dịch vụ, bạn sẽ dùng một mẫu (template) có sẵn để thiết lập mọi thứ nhanh chóng
    * Truy cập giao diện AWS Management Console
      * Tìm và chọn CloudFormation
    * ![Tìm CloudFormation](/images/1-Worklog/1.3-Week3/Day2/SearchCloudFormation.png)
    * Chọn Create stack
    * ![Create stack](/images/1-Worklog/1.3-Week3/Day2/CreateStack.png)
    * Trong giao diện Create stack
      * Đối với PREREQUISITE - PREPARE TEMPLATE, Chọn Template is ready
      * Đối với SPECIFY TEMPLATE, Chọn Amazon S3 URL
      * Đối với Amazon S3 URL, nhập URL bạn đã tạo
      * Chọn Next
    * ![Giao diện Create stack](/images/1-Worklog/1.3-Week3/Day2/PerformanceCreate%20stack.png)
    * Trong phần STACK NAME, nhập Buckup-plan (nhập tùy ý bạn)
      * Chọn AvailabilityZone
      * Đối với LatestAmiId, chọn giá trị mặc định
      * Đối với NotificationEmail, nhập email của bạn để nhận thông báo
      * Đối với S3BucketName, nhập tên S3 bucket bạn đã tạo
      * Đối với S3KeyLambdaZip, nhập đường dẫn của lambda_function.zip
    * ![Sao chép thông tin đường dẫn](/images/1-Worklog/1.3-Week3/Day2/STACKNAME.png)
    * Trong phần CONFIGURE STACK OPTIONS, Chọn I acknowledge that AWS CloudFormation might create IAM resources, Chọn Next
    * ![Configure stack options](/images/1-Worklog/1.3-Week3/Day2/CONFIGURESTACK.png)
    * Đối với CAPABILITIES
      * Chọn Submit
    * ![Capabilities](/images/1-Worklog/1.3-Week3/Day2/CAPABILITIES.png)
    * Hoàn thành tạo stack Cloudformation
    * ![Tạo Stack thành công](/images/1-Worklog/1.3-Week3/Day2/CopyURL.png)
    * Kiểm tra lại Output của stack CloudFormation
    * ![Kiểm tra Output](/images/1-Worklog/1.3-Week3/Day2/CheckOutput.png)
    * Chọn vào Value của ApplicationURL
    * ![ApplicationURL](/images/1-Worklog/1.3-Week3/Day2/ApplicationURL.png)
    * Kiểm tra mail sẽ nhận được mail thông báo
    * ![Kiểm tra mail](/images/1-Worklog/1.3-Week3/Day2/CheckMail.png)
    * Thực hiện xác nhận mail
    * ![Xác nhận mail](/images/1-Worklog/1.3-Week3/Day2/confirm.png)

  * **Tạo Backup plan**
    * Trước khi bắt đầu, trang web nhấn mạnh việc xác định chiến lược sao lưu dựa trên hai chỉ số quan trọng:
      * RTO (Recovery Time Objective): Mục tiêu thời gian khôi phục
      * RPO (Recovery Point Objective): Mục tiêu điểm khôi phục
      * Các chỉ số này cần được xác định cụ thể cho từng khối lượng công việc (workload) thay vì áp dụng chung cho toàn bộ hạ tầng
    * Truy cập vào AWS Management Console
      * Mở AWS Management Console
      * Tìm và chọn AWS Backup
    * ![Tìm AWS Backup](/static/images/1-Worklog/1.3-Week3/Day2/SearchAWSBackup.png)
    * Chọn AWS Backup Plan
    * ![Tạo Backup Plan](/static/images/1-Worklog/1.3-Week3/Day2/CreateBackupPlan.png)
    * Tạo kế hoạch sao lưu
      * Trong giao diện Create backup plan, chọn Build a new plan
      * Đối với trường Backup plan name, nhập BACKUP-LAB
    * ![Giao diện backup plan](/static/images/1-Worklog/1.3-Week3/Day2/BackupPlanPerfomance.png)
    * Cấu hình quy tắc sao lưu
      * Điền RULE NAME là BACKUP-LAB-RULE
      * Về phần SCHEDULE, mục FREQUENCY, chọn Daily
      * Chọn Use backup window defaults - recommended để sử dụng cài đặt mặc định cho cửa sổ sao lưu
      * Đối với BACKUP VAULT, chọn CREATE NEW BACKUP VAULT
    * ![Backup Rule](/static/images/1-Worklog/1.3-Week3/Day2/BackupRule.png)
    * Đặt tên cho Backup Vault
      * Điền tên BACKUP VAULT NAME là BACKUP-LAB-VAULT
      * Chọn (default) aws/backup
      * Chọn CREATE BACKUP VAULT
    * ![Backup Vault](/static/images/1-Worklog/1.3-Week3/Day2/BackupVaultName.png)
    * Thêm các cặp Key và Value cho tag
      * Chọn Create plan
    * ![Tạo Plan](/static/images/1-Worklog/1.3-Week3/Day2/CreateBackup.png)
    * Hoàn tất việc tạo Backup Plan
      * Trong phần RESOURCE ASSIGNMENTS, chọn ASSIGN RESOURCES
    * ![Tạo Backup Plan thành công](/static/images/1-Worklog/1.3-Week3/Day2/ASSIGNRESOURCES.png)
    * Gán tài nguyên cho Backup Plan
      * Điền RESOURCE ASSIGNMENT NAME là BACKUP-RESOURCES
      * Chọn DEFAULT ROLE cho IAM ROLE. Nếu role không tồn tại, AWS Backup sẽ tự động tạo một role mới với các quyền cần thiết
      * Thêm Tag Key và Tag Value
      * Chọn ASSIGN RESOURCES
      * ![Gán tài nguyên](/static/images/1-Worklog/1.3-Week3/Day2/ASSIGNRESOURCESname.png)
    * Xác nhận và tiếp tục
      * Xác nhận bằng cách chọn Continue
    * ![Xác nhận gán](/static/images/1-Worklog/1.3-Week3/Day2/ConfirmPlan.png)
    * Hoàn tất việc gán tài nguyên
    * ![Hoàn tất gán](/static/images/1-Worklog/1.3-Week3/Day2/CompletePlan.png)

  * **Thiết lập thông báo**
    * Việc thiết lập thông báo giúp nhóm vận hành nắm bắt kịp thời trạng thái của các tác vụ sao lưu (backup) và khôi phục (restore), từ đó có phản ứng nhanh chóng nếu có lỗi xảy ra
    * Cấu hình AWS CLI
      * Mở Terminal và đảm bảo bạn có quyền truy cập vào AWS CLI. Hãy chắc chắn rằng phiên bản CLI đã được cập nhật và bạn có Quyền của quản trị viên AWS để thực thi các lệnh AWS CLI
      * Chỉnh sửa lệnh AWS CLI sau và thay thế bằng ARN của SNS TOPIC bạn đã tạo. ARN này có thể tìm thấy trong phần đầu ra của CloudFormation Stack
      * Sau khi đã chỉnh sửa, thực thi lệnh trên. Điều này sẽ kích hoạt thông báo thông qua SNS TOPIC mỗi khi một công việc sao lưu hoặc khôi phục hoàn thành. Thông tin này giúp nhóm Vận hành nắm bắt được các lỗi có thể xảy ra trong quá trình sao lưu hoặc khôi phục dữ liệu
      * ![Lệnh AWS CLI](/static/images/1-Worklog/1.3-Week3/Day2/CommandAWSCLI.png)
    * Kiểm tra giao diện SNS
    * ![Kiểm tra SNS](/static/images/1-Worklog/1.3-Week3/Day2/CheckSNS.png)
    * Xác minh thông báo
      * Để xác minh rằng thông báo đã được kích hoạt thành công, bạn có thể sử dụng lệnh sau. Kết quả đầu ra sẽ bao gồm một phần được gọi là SNSTopicArn, theo sau là ARN của SNS Topic đã được tạo
      * ![Lệnh SNSTopicArn](/static/images/1-Worklog/1.3-Week3/Day2/CommandSNSTopicArn.png)
      * Bây giờ, bạn đã kích hoạt thành công thông báo cho BACKUP-LAB-VAULT, đảm bảo rằng nhóm Vận hành biết về việc hoàn thành các hoạt động sao lưu và khôi phục liên quan đến vault này cũng như bất kỳ lỗi nào liên quan đến các hoạt động đó

  * **Kiểm tra hoạt động**
    * Xác minh các điểm khôi phục (Recovery Points) đã được tạo thành công trong Backup Vault
    * Thực hiện quy trình khôi phục một tài nguyên từ bản sao lưu để kiểm tra tính sẵn sàng
    * Hiểu cách theo dõi trạng thái của các tác vụ khôi phục (Restore Jobs)
    * Truy cập vào AWS Management Console:
      * Mở giao diện AWS Backup
      * Chọn CREATE AN ON-DEMAND BACKUP
    * ![Giao diện AWS Backup](/static/images/1-Worklog/1.3-Week3/Day2/AWSBackupDashboard.png)
    * Trong phần RESOURCE TYPE, chọn EC2, sau đó dán Instance ID từ phần Output của CloudFormation Stack
      * Trong BACKUP WINDOW, chọn CREATE BACKUP NOW
      * Đối với Backup Vault, chọn BACKUP-LAB-VAULT
      * Sử dụng vai trò IAM mặc định
      * Chọn CREATE ON-DEMAND BACKUP
    * ![Tạo on-demand backup](/static/images/1-Worklog/1.3-Week3/Day2/On-demandbackup.png)
    * Trong Jobs, chọn Backup jobs, và chờ cho đến khi trạng thái chuyển sang Completed
    * ![Backup jobs](/static/images/1-Worklog/1.3-Week3/Day2/WaitBackupJobs.png)
    * Nhấp vào Backup jobs ID để xem chi tiết
    * ![Backup jobs ID](/static/images/1-Worklog/1.3-Week3/Day2/BackupJobsID.png)
    * Kiểm tra email để xác nhận thông báo
    * Kiểm tra email liên quan đến Restore Test Status
    * Xem thông tin Restore jobs, chọn Restore jobs ID
    * Xem chi tiết Restore jobs
    * Quay lại giao diện AWS Management Console:
      * Tìm và chọn CloudWatch
    * ![Giao diện CloudWatch](/static/images/1-Worklog/1.3-Week3/Day2/SearchCloudWatch.png)
    * Trong giao diện CloudWatch:
      * Chọn Logs
      * Chọn Log group của bài lab. (/aws/lambda/RestoreTestFunction-<YOUR CLOUDFORMATION STACK NAME>)
    * ![Logs](/static/images/1-Worklog/1.3-Week3/Day2/Logs.png)
    * Trong giao diện Logs:
      * Chọn Log streams
      * Chọn Log stream của bài lab
    * ![Log stream](/static/images/1-Worklog/1.3-Week3/Day2/LogStreams.png)
    * Xem chi tiết Log Events
    * ![Chi tiết Log Events](/static/images/1-Worklog/1.3-Week3/Day2/LogEvents.png)
  
  * **Dọn dẹp tài nguyên**
    * **Xóa SNS Subscriber**
      * Truy cập vào AWS SNS Console
      * Chọn Subscription ở thanh bên trái
      * Chọn và xóa các Subscriber liên quan
    * ![SNS Subscriber](/static/images/1-Worklog/1.3-Week3/Day2/SNSSubscriber.png)

    * **Xóa SNS Topic**
      * Truy cập vào AWS SNS Console
      * Chọn Topics ở thanh bên trái
      * Chọn và xóa Topic liên quan
    * ![SNS Topic](/static/images/1-Worklog/1.3-Week3/Day2/SNSTopic.png)

    * **Xóa Backup Vaults**
      * Truy cập vào AWS Backup Console
      * Chọn Backup Vaults ở thanh bên trái
      * Chọn Backup Vault được tạo trong bài này
      * ![Backup Vaults](/static/images/1-Worklog/1.3-Week3/Day2/BackupVaults.png)
      * Ở trang thông tin Backup Vault
      * Ở mục Recovery points, tick vào Recovery points, chọn Actions, và chọn Delete
      * ![Recovery points](/static/images/1-Worklog/1.3-Week3/Day2/RecoveryPoints.png)
      * Tiếp theo ở mục Backups khi đã xóa Recovery points ta chọn Delete vault
      * ![Delete vault](/static/images/1-Worklog/1.3-Week3/Day2/Deletevault.png)

    * **Xóa Backup Plans**
      * Truy cập vào AWS Backup Console
      * Chọn Backup plans ở thanh bên trái
      * Chọn Backup plan được tạo trong bài này
      * ![Backup Plans](/static/images/1-Worklog/1.3-Week3/Day2/BackupPlans.png)
      * Ở mục Resource assignments, chọn resource đã tạo và chọn Delete
      * ![Backup Resource](/static/images/1-Worklog/1.3-Week3/Day2/BackupResource.png)
      * Ở trang thông tin Backup plan, chọn Delete
      * ![Backup Lab](/static/images/1-Worklog/1.3-Week3/Day2/BackupLab.png)

    * **Xóa CloudFormation Stack**
      * Truy nhập vào AWS CloudFormation
      * Chọn Stack của bài lab
      * Chọn Delete
    * ![Backup Stack](/static/images/1-Worklog/1.3-Week3/Day2/BackupStack.png)

    * **Xóa CloudWatch Logs**
      * Truy nhập vào AWS CloudWatch
      * Chọn Logs
      * Chọn /aws/lambda/RestoreTestFunction
      * Chọn Actions, chọn Delete Log Group
      * Chọn Yes, Delete
    * ![CloudWatch Logs](/static/images/1-Worklog/1.3-Week3/Day2/CloudWatchLogs.png)

## Thứ 3: Giới thiệu và Thực hành AWS CLI
* **Giới thiệu về AWS CLI**
  * **Định nghĩa:** AWS Command Line Interface (AWS CLI) là một công cụ mã nguồn mở cho phép bạn tương tác với các dịch vụ AWS bằng cách sử dụng các lệnh trong cửa sổ lệnh (command-line shell)
  * **Lợi ích:** * Cung cấp các chức năng tương đương với AWS Management Console.
    * Cho phép tự động hóa các tác vụ thông qua shell script
    * Truy cập trực tiếp vào các API công khai của dịch vụ AWS
  * **Môi trường hỗ trợ:** * **Linux/macOS:** bash, zsh, tcsh
    * **Windows:** Command Prompt, PowerShell
    * **Remote:** Thông qua SSH/PuTTY kết nối với máy ảo Amazon EC2 hoặc AWS Systems Manager

* **Cấu hình và Quản lý**
  * Profile trong AWS CLI
  * **Profile:** Là tập hợp các thiết lập và định danh. Mặc định AWS CLI sử dụng `default profile`
  * **Profile riêng:** Sử dụng tham số `--profile` để chỉ định các tài khoản hoặc thiết lập khác nhau
  * **Lưu trữ:** Thông tin được lưu cục bộ trong các tệp `config` và `credentials`
  * **Lệnh cấu hình cơ bản**
    * Sử dụng lệnh `aws configure` để thiết lập 4 thông tin quan trọng:
    * **Access Key ID:** Định danh truy cập
    * **Secret Access Key:** Khóa bảo mật (cần được giữ kín)
    * **AWS Region:** Vùng mặc định để gửi yêu cầu (ví dụ: `us-west-2`, `ap-southeast-1`).
    * **Default Output Format:** Định dạng dữ liệu trả về (`json`, `yaml`, `text`, hoặc `table`

* **Các nội dung thực hành chi tiết**
  * Workshop cung cấp hướng dẫn tương tác với các dịch vụ cốt lõi:
  * **Amazon S3:** Các lệnh tạo bucket, tải lên/tải xuống và quản lý đối tượng
  * **Amazon SNS (Simple Notification Service):** Cấu hình chủ đề (topic) và gửi thông báo
  * **IAM (Identity and Access Management):** Quản lý người dùng, nhóm và phân quyền qua CLI
  * **VPC (Virtual Private Cloud):** Thiết lập hạ tầng mạng ảo bao gồm Subnet, Internet Gateway và bảng định tuyến
  * **Amazon EC2:** Khởi tạo, quản lý trạng thái (start/stop/terminate) và cấu hình các máy chủ ảo

* **Các bước cuối cùng**
  * **Khắc phục lỗi:** Hướng dẫn cách đọc log và xử lý các lỗi thường gặp về quyền truy cập hoặc sai cú pháp lệnh
  * **Dọn dẹp tài nguyên:** Hướng dẫn xóa các tài nguyên đã tạo (EC2, S3, VPC...) để tránh phát sinh chi phí ngoài ý muốn sau khi học xong

* **Cài đặt AWS CLI**
  * AWS Command Line Interface (AWS CLI) có hai phiên bản. Trong bài hướng dẫn này, chúng ta sẽ cài đặt AWS CLI v2 trên cả Windows và Ubuntu, vì phiên bản này đơn giản và hỗ trợ đầy đủ hơn so với AWS CLI v1
    * AWS CLI phiên bản 1 (v1): Phiên bản ban đầu của AWS CLI, vẫn được hỗ trợ bởi AWS
    * AWS CLI phiên bản 2 (v2): Phiên bản mới nhất, hỗ trợ tất cả các tính năng mới của AWS. Một số tính năng chỉ có trên v2 và không có trên v1
    * ![Tạo Key pair](/images/1-Worklog/1.3-Week3/Day3/create-key-pair.png)

  * **Cài đặt AWS CLI**
    * Đối với Windows: msiexec.exe /i https://awscli.amazonaws.com/AWSCLIV2.msi
    * ![Cài AWS](/images/1-Worklog/1.3-Week3/Day3/AWSWindows.png)

  * **Kiểm tra cài đặt AWS CLI:**
    * ![Kiểm tra version](/images/1-Worklog/1.3-Week3/Day3/AWSversion.png)

  * **Tạo Default Profile**
    * Sử dụng lệnh aws configure để thiết lập AWS CLI. Lệnh này sẽ yêu cầu nhập các thông tin quan trọng:
      * Access Key ID
      * Secret Access Key
      * Vùng AWS (Region)
      * Định dạng xuất (Output format)
    * ![Tạo Default Profile](/images/1-Worklog/1.3-Week3/Day3/AWSconfigure.png)
    * Cấu hình này được lưu trong file credentials dưới profile default. Profile default sẽ được AWS CLI sử dụng nếu không chỉ định profile khác

  * **Cấu hình nhiều profile**
    * Để tạo profile khác, ví dụ devops, sử dụng lệnh sau:
    * ![Tạo Another Profile](/images/1-Worklog/1.3-Week3/Day3/ProfileDevop.png)
    * Profile chứa Access Key ID và Secret Access Key để ký các yêu cầu gửi tới AWS
  
  * **Kiểm tra vùng (region) của profile**
    * ![Kiểm tra region](/images/1-Worklog/1.3-Week3/Day3/RegionProfile.png)

  * **Liệt kê danh sách cấu hình**
    * ![Liệt kê danh sách](/images/1-Worklog/1.3-Week3/Day3/AWSlist.png)

  * **Liệt kê các profile**
    * ![Liệt kê profile](/images/1-Worklog/1.3-Week3/Day3/ListProfiles.png)

* **Kiểm tra tài nguyên qua CLI**
  * **Kiểm tra số lượng S3 bucket của profile**
    * Để liệt kê các bucket S3 của profile, sử dụng lệnh:
    * ![liệt kê bucket S3](/images/1-Worklog/1.3-Week3/Day3/S3bucket.png)
  
  * **Sử dụng CLI Auto Prompt**
    * Auto Prompt của AWS CLI giúp gợi ý các tham số và lệnh, rất tiện dụng khi không nhớ chính xác cú pháp:
    * ![Command Prompt](/images/1-Worklog/1.3-Week3/Day3/CLIAutoPrompt.png)

* **AWS CLI với Amazon S3**
  * **Sử dụng AWS CLI để khởi tạo tài nguyên S3**
    * **Liệt kê danh sách các S3 bucket**
      * Để xem danh sách các bucket hiện có trong tài khoản của bạn:
      * ![Danh sách S3 bucket](/images/1-Worklog/1.3-Week3/Day3/S3list.png)
      * Nếu không thấy bucket nào, bạn cần đảm bảo rằng bạn đã có quyền truy cập vào AWS S3
  
    * **Kiểm tra object trong S3 bucket**
      * Để liệt kê các object trong một bucket cụ thể:
      * ![Liệt kê object](/images/1-Worklog/1.3-Week3/Day3/ObjectS3.png)
    
    * **Xóa object trong S3 bucket**
      * Khi cần xóa một object từ bucket:
      * ![Xóa object](/images/1-Worklog/1.3-Week3/Day3/RemoveObject.png)

    * **Xóa S3 bucket**
      * Sau khi đã xóa toàn bộ object trong bucket, bạn có thể xóa bucket bằng lệnh sau:
      * ![Xóa S3](/images/1-Worklog/1.3-Week3/Day3/RemoveS3.png)

* **AWS CLI với Amazon SNS**
  * **Tạo một topic SNS**
    * Để tạo một topic SNS, chúng ta làm như sau:
    * Đây là lệnh để tạo một topic SNS với tên là aws-cli
    * ![Tạo topic SNS](/images/1-Worklog/1.3-Week3/Day3/SNScreate.png)
  
  * **Thực hiện đăng ký subscriber**
    * Sau khi đã tạo thành công topic SNS, ta thực hiện đăng ký subscriber bằng lệnh sau:
    * ![đăng ký subscriber](/images/1-Worklog/1.3-Week3/Day3/SNSsubscribe.png)

  * **Xác nhận đăng ký**
    * Kiểm tra email mà bạn đã sử dụng trong lệnh trước. Sau đó, chọn Confirm subscription trong email để hoàn tất đăng ký
    * ![Kiểm tra email](/images/1-Worklog/1.3-Week3/Day3/ConfirmEmail.png)
  
  * **Hoàn thành đăng ký**
    * Khi bạn đã xác nhận đăng ký, trạng thái subscription sẽ hoàn tất
    * ![Hoàn tất đăng ký](/images/1-Worklog/1.3-Week3/Day3/Completesubscript.png)
  
  * **Push một tin nhắn để kiểm tra**
    * Sau khi đăng ký thành công, chúng ta sẽ thử push một tin nhắn để kiểm tra:
    * Lệnh này gửi một tin nhắn có nội dung "Hello" đến tất cả các subscriber đã đăng ký
    * ![Push tin nhắn](/images/1-Worklog/1.3-Week3/Day3/SNSpublish.png)
  
  * **Nhận tin nhắn qua email**
    * Nếu mọi thứ hoạt động đúng, bạn sẽ nhận được tin nhắn đã gửi qua email
    * ![Nhận tin nhắn email](/images/1-Worklog/1.3-Week3/Day3/AWSmessage.png)

* **AWS CLI với IAM**
  * Chúng ta có thể thực hiện tạo IAM group, IAM user, và policy một cách nhanh chóng bằng CLI. Các bước thực hiện như sau:
  * **Tạo IAM Group**
    * Đầu tiên, chúng ta sẽ thực hiện tạo một IAM group mới với CLI:
    * ![Tạo Group](/images/1-Worklog/1.3-Week3/Day3/IAMcreate.png)

  * **Tạo IAM User**
    * Tiếp theo, chúng ta sẽ tạo một user mới và đặt tên cho user là dev-1:
    * ![Tạo User](/images/1-Worklog/1.3-Week3/Day3/IAMuser.png)

  * **Thêm User vào Group**
    * Bước tiếp theo là thêm user vừa tạo vào group dev:
    * ![Thêm user vào group](/images/1-Worklog/1.3-Week3/Day3/add-user-to-group.png)

  * **Kiểm tra Chi Tiết Group và User**
    * Chúng ta có thể kiểm tra chi tiết của group và user bằng lệnh sau:
    * ![Kiểm tra group](/images/1-Worklog/1.3-Week3/Day3/CheckGroup.png)

  * **Tạo Access Key cho User**
    * Tiếp theo, chúng ta sẽ tạo Access Key cho user dev-1:
    * ![Tạo Access Key](/images/1-Worklog/1.3-Week3/Day3/create-key-pair.png)

  * **Xóa Access Key**
    * Cuối cùng, nếu muốn xóa Access Key đã tạo, chúng ta có thể thực hiện với lệnh sau:
    * ![Xóa Access Key](/images/1-Worklog/1.3-Week3/Day3/delete-access-key.png)

  * **AWS CLI với VPC**
    * **Tạo VPC**
      * Thực hiện tạo VPC bằng AWS CLI:
      * ![Tạo VPC](/images/1-Worklog/1.3-Week3/Day3/create-vpc.png)
    
    * **Tạo Subnet**
      * Tiếp theo, chúng ta sẽ tạo subnet dựa theo VPC ID đã tạo:
      * ![Tạo Subnet](/images/1-Worklog/1.3-Week3/Day3/create-subnet.png)
      * Tạo một subnet thứ hai với CIDR khác:
      * ![Tạo Subnet thứ hai](/images/1-Worklog/1.3-Week3/Day3/SecondSubnet.png)

    * **Kiểm tra và quản lý tài nguyên VPC**
      * Kiểm tra kết quả tạo subnet:
      * ![Kiểm tra subnet](/images/1-Worklog/1.3-Week3/Day3/delete-subnet.png)

  * **AWS CLI với Internet Gateway**
    * **Thực hiện tạo Internet Gateway**
      * ![Tạo Internet Gateway](/images/1-Worklog/1.3-Week3/Day3/CreateInternetGateway.png)
      * Đây là bước khởi tạo Internet Gateway

    * **Xác nhận Internet Gateway**
      * Chúng ta sẽ xác nhận lại đã tạo thành công Internet Gateway và sử dụng Internet Gateway ID để thực hiện các bước tiếp theo
      * ![Xác nhận Internet Gateway](/images/1-Worklog/1.3-Week3/Day3/ConfirmInternetGateway.png)
      * Xác nhận Internet Gateway là bước quan trọng trước khi thực hiện các bước tiếp theo

    * **Kiểm tra VPC**
      * Chúng ta sẽ kiểm tra VPC để sử dụng VPC ID cho bước tiếp theo
      * ![Kiểm tra VPC](/images/1-Worklog/1.3-Week3/Day3/CheckVPC.png)
    
    * **Attach Internet Gateway**
      * Sau khi kiểm tra Internet Gateway và VPC, chúng ta thực hiện attach internet gateway bằng cách:
      * ![Attach Internet Gateway](/images/1-Worklog/1.3-Week3/Day3/attach-internet-gateway.png)
      * Chúng ta cần sử dụng đúng VPC ID và Internet Gateway ID để attach thành công

    * **Tạo Route Table**
      * Tương tự, chúng ta tạo Route Table cho VPC của mình
      * ![Tạo Route Table](/images/1-Worklog/1.3-Week3/Day3/create-route-table.png)

    * **Định tuyến Route Table**
      * Sau đó, chúng ta định tuyến cho Route Table để kết nối ra Internet:
      * ![Định tuyến Route Table](/images/1-Worklog/1.3-Week3/Day3/dinh-tuyen-%20Route-Table.png)
    
    * **Kiểm tra Route Table**
      * Sau khi tạo route, chúng ta kiểm tra lại cấu hình của Route Table:
      * ![Kiểm tra Route Table](/images/1-Worklog/1.3-Week3/Day3/describe-route-tables.png)

* **Tạo EC2 sử dụng AWS CLI**
  * **Tạo EC2 sử dụng AWS CLI**
    * Từ hạ tầng mạng đã tạo bằng CLI, chúng ta sẽ tạo EC2. Trước hết, tạo AWS Key pair:
    * ![Tạo Key pair](/images/1-Worklog/1.3-Week3/Day3/create-key-pair.png)
    * Kiểm tra trên giao diện, xác nhận đã tạo thành công Key pair
    * ![Kiểm tra Key pair](/images/1-Worklog/1.3-Week3/Day3/ConfirmCreateKeyPair.png)
    * Tạo Security group cho EC2:
    * ![Tạo Security Group](/images/1-Worklog/1.3-Week3/Day3/create-security-group.png)
    * Kiểm tra Security group vừa tạo.
    * ![Kiểm tra Security Group](/images/1-Worklog/1.3-Week3/Day3/CheckSecuritygroup.png)
    * Cấp quyền để SSH:
    * ![Cấp quyền SSH](/images/1-Worklog/1.3-Week3/Day3/authorize-security-group-ingress.png)

* **Dọn dẹp tài nguyên**
  * **Xóa Security Group**
    * Đảm bảo bạn đã xác nhận xóa mọi kết nối liên quan đến Security Group trước khi thực hiện lệnh xóa
    * ![Xóa Security Group](/images/1-Worklog/1.3-Week3/Day3/delete-security-group.png)
  
  * **Xóa Subnet**
    * ![Xóa Subnet](/images/1-Worklog/1.3-Week3/Day3/delete-subnet.png)

  * **Xóa Route Table**
    * ![Xóa Route Table](/images/1-Worklog/1.3-Week3/Day3/delete-route-table.png)

  * **Detach Internet Gateway**
    * ![Detach Internet Gateway](/images/1-Worklog/1.3-Week3/Day3/detach-internet-gateway.png)

  * **Xóa Internet Gateway**
    * ![Xóa Internet Gateway](/images/1-Worklog/1.3-Week3/Day3/delete-internet-gateway.png)

  * **Xóa VPC**
    * ![Xóa VPC](/images/1-Worklog/1.3-Week3/Day3/delete-vpc.png)

## Thứ 4: Amazon CloudWatch - Giám sát và Quản lý Tài nguyên AWS
* **Giới thiệu về Amazon CloudWatch**
  * CloudWatch là dịch vụ theo dõi và quản lý cung cấp dữ liệu cho tài nguyên AWS, các ứng dụng hybrid và on-premises. Các tính năng chính bao gồm:
    * Thu thập dữ liệu: Tập hợp logs (nhật ký) và metrics (chỉ số) trên cùng một nền tảng
    * Giám sát End-to-End: Theo dõi toàn bộ ứng dụng, hạ tầng và dịch vụ
    * Tự động hóa: Sử dụng cảnh báo và dữ liệu sự kiện để giảm thời gian giải quyết sự cố (MTTR)
    * Lưu trữ: Lưu trữ chỉ số metrics lên đến 15 tháng

* **Triển khai CloudFormation Stack**
  * Truy cập vào AWS Management Console
    * Tìm kiếm dịch vụ CloudFormation trong thanh tìm kiếm
    * Chọn CloudFormation từ kết quả tìm kiếm
  * ![Seach CloudFormation](/images/1-Worklog/1.3-Week3/Day4/SeachCloudFormation.png)
  * Trong giao diện CloudFormation
    * Chọn Create stack
    * Chọn With new resources (standard)
  * ![Create stack](/images/1-Worklog/1.3-Week3/Day4/Createstack.png)
  * Trong giao diện Create stack
    * Tải file cấu hình template về máy
    * Trong phần Prerequisite - Prepare template, chọn Choose an existing template
    * Tiếp theo chọn Upload a template file
    * Ấn Choose file để tải lên file template đã tải về
    * Ấn Next
  * ![Info stack](/images/1-Worklog/1.3-Week3/Day4/Infostack.png)
  * Cấu hình thông tin Stack
    * Stack name: Nhập FCJ-CloudWatch-Workshop (hoặc một tên dễ nhớ khác)
    * RegionId: Chọn đúng Region ID nơi bạn đang thực hiện workshop (ví dụ: us-east-1 cho N. Virginia)
    * Giữ nguyên các tham số còn lại với giá trị mặc định
    * Ấn Next
  * ![Stack detail](/images/1-Worklog/1.3-Week3/Day4/Stackdetail.png)
  * Cấu hình tùy chọn Stack
    * Không cần thay đổi cấu hình mặc định trên trang này
    * Cuộn xuống dưới cùng
    * Tích chọn I acknowledge that AWS CloudFormation might create IAM resources with custom names
    * Ấn Next
  * ![Stack setting](/images/1-Worklog/1.3-Week3/Day4/Stacksetting.png)
  * Xem lại và tạo Stack
    * Kiểm tra lại tất cả thông tin cấu hình
    * Cuộn xuống dưới cùng và ấn Submit để bắt đầu tạo Stack
  * ![Submit stack](/images/1-Worklog/1.3-Week3/Day4/Submitstack.png)
  * Theo dõi quá trình triển khai
  * ![Watch create](/images/1-Worklog/1.3-Week3/Day4/Watchcreate.png)

* **Xem các Metrics**
  * **Xem các Metrics**
    * Truy cập AWS Management Console
      * Tìm kiếm dịch vụ CloudWatch trong thanh tìm kiếm
      * Chọn CloudWatch từ kết quả tìm kiếm
      * ![Search CloudWatch](/images/1-Worklog/1.3-Week3/Day4/SearchCloudWatch.png)
    * Trong giao diện CloudWatch
      * Mở rộng phần Metrics ở menu bên trái
      * Chọn All metrics
      * ![All metrics](/images/1-Worklog/1.3-Week3/Day4/Metrics.png)
    * Trong giao diện biểu đồ metrics, nhập EC2 vào ô tìm kiếm
    * ![Nhập EC2](/images/1-Worklog/1.3-Week3/Day4/TypeEC2.png)
    * Từ kết quả tìm kiếm, chọn EC2 > Per-Instance Metrics
    * ![Per-Instance Metrics](/images/1-Worklog/1.3-Week3/Day4/Per-InstanceMetrics.png)
    * ![Per-Instance List](/images/1-Worklog/1.3-Week3/Day4/Per-InstanceList.png)
    * Trên thanh tìm kiếm, nhập CPUUtilization và tìm kiếm
    * ![Nhập CPUUtilization](/images/1-Worklog/1.3-Week3/Day4/TypeCPUUtilization.png)
    * ![CPUUtilization List](/images/1-Worklog/1.3-Week3/Day4/CPUUtilizationList.png)
    * Chọn 2 trong số 5 instances được tạo ra từ CloudFormation stack để so sánh thông số CPUUtilization
    * ![Chọn instances](/images/1-Worklog/1.3-Week3/Day4/Choseinstances.png)
    * Tiếp theo, chúng ta sẽ xem các metrics khác của cùng một Instance
      * Bỏ chọn dòng của Instance B
      * Xóa tag tìm kiếm CPUUtilization
      * Nhập EBSWriteBytes vào thanh tìm kiếm
    * ![Nhập EBSWriteBytes](/images/1-Worklog/1.3-Week3/Day4/TypeEBSWriteBytes.png)
    * ![EBSWriteBytes List](/images/1-Worklog/1.3-Week3/Day4/EBSWriteBytesList.png)
    * Kéo xuống và chọn Instance A
    * ![Chọn Instance A](/images/1-Worklog/1.3-Week3/Day4/ChoseInstanceA.png)
    * Bạn có thể ẩn một trong hai metrics để xem chi tiết hơn
    * ![Hide metrics](/images/1-Worklog/1.3-Week3/Day4/Hidemetrics.png)
  * **Thao tác với biểu đồ**
    * Trong tab Graphed metrics, tại dòng EBSWriteBytes, cột Y axis, chọn > để chuyển metric này sang trục Y thứ hai
    * ![Graphed metrics](/images/1-Worklog/1.3-Week3/Day4/Graphedmetrics.png)
    * Thêm đánh dấu ngang (horizontal annotation) cho biểu đồ
      * Chuyển sang tab Options
      * Chọn Add horizontal annotation
    * ![Options Graphed metrics](/images/1-Worklog/1.3-Week3/Day4/OptionsGraphedmetrics.png)
    * Cấu hình horizontal annotation với các thông tin sau:
      * Label: 5% Mark
      * Value: 5
    * ![Horizontal Annotation](/images/1-Worklog/1.3-Week3/Day4/HorizontalAnnotation.png)
    * Tạo thêm Vertical annotation với label là Job start
    * ![Vertical annotation](/images/1-Worklog/1.3-Week3/Day4/Verticalannotation.png)
    * Điều chỉnh thời gian cho vertical annotation
      * Di chuột vào phần đầu của đường chỉ trên biểu đồ
      * Quan sát thấy công việc bắt đầu vào khoảng 03:00
    * ![Điều chỉnh thời gian](/images/1-Worklog/1.3-Week3/Day4/Changetime.png)
    * Sửa thông tin giờ của Date của Job start thành 02:40
    * Chọn Apply để áp dụng thay đổi
    * ![Date của Job](/images/1-Worklog/1.3-Week3/Day4/DateOfJob.png)
    * Đường Job start đã được di chuyển đến vị trí chính xác
    * ![Job start](/images/1-Worklog/1.3-Week3/Day4/Jobstart.png)

* **Thực hiện các phép tìm kiếm**
  * Ở phần trước thì chúng ta thực hiện xem metric theo cách thủ công, tuy nhiên nó vẫn còn nhiều hạn chế cũng như là phải thao tác nhiều lần với nhiều metrics khác nhau. Trong phần này chúng ta có thể thực hiện việc này nhanh hơn với Search Expression
    * Xoá hết các thông tin trong biểu đồ cũ đi, ấn X hoặc ấn Clear graph
    * ![Clear graph](/images/1-Worklog/1.3-Week3/Day4/Cleargraph.png)
    * Trở lại tab Browse
      * Xoá bộ lọc EBSWriteBytes đi
      * Ấn Graph search
    * ![Xoá EBSWriteBytes](/images/1-Worklog/1.3-Week3/Day4/DeleteEBSWriteBytes.png)
    * ![Press Graph search](/images/1-Worklog/1.3-Week3/Day4/PressGraphsearch.png)
    * Quay trở lại tab Graphed metrics, chúng ta có thể thấy cột Details có một biểu thức tìm kiếm vừa mới hiện lên ở đây
    * ![Quay trở lại Graphed metrics](/images/1-Worklog/1.3-Week3/Day4/BackGraphedmetrics.png)
    * Ở góc bên trên bên phải cùng
      * Xổ ô Line
      * Chọn Stacked area
    * ![Stacked area](/images/1-Worklog/1.3-Week3/Day4/Stackedarea.png)
    * Và biểu đồ của chúng ta đã dễ nhìn hơn
    * ![Easy look](/images/1-Worklog/1.3-Week3/Day4/Outlook.png)
    * Tìm lượng bộ nhớ trung bình sử dụng theo phần trăm (Disk Used Percent)
    * ![Disk Used Percent](/images/1-Worklog/1.3-Week3/Day4/DiskUsedPercent.png)
    * ![Disk Used Percent Look](/images/1-Worklog/1.3-Week3/Day4/DiskUsedPercentLook.png)
    * Tìm theo từ khoá “used”
    * ![Search used](/images/1-Worklog/1.3-Week3/Day4/Searchused.png)
    * Có thể thấy là kết quả ít nhiều đã khác đi
    * ![Search used look](/images/1-Worklog/1.3-Week3/Day4/Searchusedlook.png)

* **Thực hiện các phép toán học**
  * Đầu tiên là dọn dẹp biểu thức tìm kiếm trước đó
  * ![Dọn dẹp biểu thức](/images/1-Worklog/1.3-Week3/Day4/CleanSearch.png)
  * Về lại tab Browse
    * Ấn Graph search để lấy lại biểu đồ như ban đầu ở bước trước
  * ![Back Browse](/images/1-Worklog/1.3-Week3/Day4/BackBrowse.png)
  * Sau đó xổ phần Add math ở bên góc trên bên phải, dưới biểu đồ
    * Xổ tiếp Filter
    * Chọn Top 10 by sum
  * ![Add math](/images/1-Worklog/1.3-Week3/Day4/Addmath.png)
  * Giờ thì chúng ta sẽ tiến hành sắp xếp lại biểu đồ dựa trên biểu thức tìm kiếm đầu tiên, với biểu thức như bên dưới
  * ![Biểu thức tìm kiếm đầu tiên](/images/1-Worklog/1.3-Week3/Day4/FirstSearch.png)

* **Tạo dynamic labels**
  * Xoá các biểu thức cũ trong phần trước
  * Xoá hết các Filers và ấn vào All để trở phần phần namespaces
  * ![Xoá Filers](/images/1-Worklog/1.3-Week3/Day4/CleanFilers.png)
  * Sau đó là vào trong namespace CWAgent
  * ![CWAgent](/images/1-Worklog/1.3-Week3/Day4/CWAgent.png)
  * Chọn tiếp Dimension là ImageId, InstanceId, InstanceType, exe, process_name
  * ![Dimension](/images/1-Worklog/1.3-Week3/Day4/Dimension.png)
  * ![Dimension Look](/images/1-Worklog/1.3-Week3/Day4/DimensionLook.png)
  * Trên thanh tìm kiếm, chúng ta nhập 2 thông tin sau
    * exe=cloudwatch
    * MetricName=procstat_memory_rss (trong phần này thì chúng ta chỉ rõ là cần Metric name)
  * ![Search](/images/1-Worklog/1.3-Week3/Day4/Search.png)
  * Tiếp tục ấn vào Graph search để hiển thị biểu đồ
  * ![Graph search](/images/1-Worklog/1.3-Week3/Day4/Graphsearch.png)
  * Sang tab Graphed metrics
    * Xổ Add dynamic label
    * Xổ All labels
    * Chọn PROP(‘Dim.DimName’)
  * ![All labels](/images/1-Worklog/1.3-Week3/Day4/Alllabels.png)
  * Chúng ta có thể thấy là Label trên biểu đồ đã thay đổi
  * ![Label Change](/images/1-Worklog/1.3-Week3/Day4/LabelChange.png)
  * Sửa lại biểu thức của label theo dạng
  * ![Sửa label](/images/1-Worklog/1.3-Week3/Day4/FixLabel.png)
  * Label đã chuyển về thành các phần như sau
  * ![Label](/images/1-Worklog/1.3-Week3/Day4/Label.png)

* **CloudWatch Logs**
  * **CloudWatch Logs**
    * Trong trang chính của CloudWatch
      * Phần menu bên trái, mở rộng mục Logs
    * ![Logs](/images/1-Worklog/1.3-Week3/Day4/Logs.png)
    * Trên thanh tìm kiếm, nhập /ec2 và chọn /ec2/linux/var/log/messages
    * ![Nhập EC2](/images/1-Worklog/1.3-Week3/Day4/SearchEC2.png)
    * ![EC2 Info](/images/1-Worklog/1.3-Week3/Day4/EC2Info.png)
    * Chọn một instance bất kỳ để xem chi tiết logs
    * Trong giao diện logs, bạn có thể thấy các bản ghi từ instance này được tạo ra từ nhiều nguồn khác nhau như: dhclient, NET, ec2net, systemd…
    * ![Logs Event](/images/1-Worklog/1.3-Week3/Day4/LogsEvent.png)
    * Trở lại thông tin của log group /ec2/linux/var/log/messages. Bây giờ chúng ta sẽ cấu hình thời gian lưu trữ (retention) cho các log events
      * Mở rộng menu Actions
      * Chọn Edit retention setting
    * ![Edit retention setting](/images/1-Worklog/1.3-Week3/Day4/Editretentionsetting.png)
    * Trong phần Retention setting, chọn 1 week (7 days) cho Expire events after
    * ![Retention setting](/images/1-Worklog/1.3-Week3/Day4/Retentionsetting.png)
    * ![Success Setting.](/images/1-Worklog/1.3-Week3/Day4/SuccessSetting..png)

  * **CloudWatch Logs Insights**
    * Trong phần này thì chúng ta sẽ thực hiện tạo logs từ một ứng dụng, sau đó là sẽ query những logs này ở trong CloudWatch Logs Insights. Mình sẽ chọn một instance nào đó để làm mẫu
    * Trên thanh tìm kiếm dịch vụ
      * Nhập EC2
      * Chọn EC2
    * ![Find EC2](/images/1-Worklog/1.3-Week3/Day4/FindEC2.png)
    * Vào trong trang Instances của EC2 Console
      * Chọn một Instance bất kì, ở đây mình chọn Instance-A
      * Ấn chọn Connect
    * ![Connect](/images/1-Worklog/1.3-Week3/Day4/Connect.png)
    * Trong trang Connect to instance
      * Chọn tab Session Manager
      * Ấn Connect
    * ![Session Manager](/images/1-Worklog/1.3-Week3/Day4/SessionManager.png)
    * Chờ một ít phút thì một Terminal hiện lên
      * Đầu tiên là vào trong tmp
      * Sau đó là tải file py script về
    * ![tmp](/images/1-Worklog/1.3-Week3/Day4/tmp.png)
    * Cấp quyền thực thi và thực thi file script này
    * Kiểm tra các logger đang chạy dưới dạng process
    * Có thể thấy thì hiện tại có 2 processes đang chạy, nó sẽ chạy cho tới cuối bài
    * Dùng lệnh để in ra các dòng log từ file /var/log/messages, nó sẽ in cho tới khi nào mình huỷ
    * Trở lại CloudWatch Console, vào trong Logs Insights ở thanh menu bên trái. Chúng ta sẽ thực hiện query logs ở trong này
    * Trong Selection criteria, tìm /ec2 và chọn /ec2/linux/var/log/messages
    * Nhập vào dòng query như bên dưới và ấn Run query
    * Và được kết quả
    * Đây chính là log mà chúng ta mới tạo ra ở bước trên
    * Giờ thì thử query là các ERROR Logs
    * Cũng là những log lỗi mà hồi nãy chúng ta đã tạo ra
    * Tiếp theo là các WARN Logs
    * Đây là các logs mới được tạo ra
    * Giờ thử query lại log, lỗi, chúng ta cũng sẽ thấy được các log mới được tạo ra
    * Ngoài ra thì chúng ta còn có thể thực hiện được việc query theo từ khoá khác. Như câu query ở bên dưới

  * **Trực quan hoá query log**
    * Ngoài ra thì chúng ta còn có thể xem được biểu đồ của các query này nữa. Chuyển sang tab Visualization
  
  * **Lưu lệnh truy vấn**
    * Về sau thì có thể chúng ta sẽ có nhiều câu truy vấn cần sử dụng lại hoặc là có những câu truy vấn phức tạp hơn mà chúng ta cần phải lưu lại. Thì Logs Insights có hỗ trợ cho chúng ta lưu lại các câu truy vấn này
    * Ví dụ mình sẽ lưu lại câu truy vấn lỗi
      * Trở lại màn hình chính của Logs Insights
      * Dán lại lệnh query tìm Error logs
      * Ấn chọn Save
    * Trong trang Save a new query, điền các thông tin như
      * Query name: Erors
      * Folder: cloudwatch-workshop, và tích chọn Create new
      * Kiểm tra lại thông tin trong phần Query definition details
      * Ấn Save
  
  * **Lịch sử truy vấn**
    * Logs Insights còn cho phép chúng ta có thể xem lại được lịch sử đã truy vấn. Trên giao diện, ấn chọn History (dưới Query editor)

  * **CloudWatch Metric Filter**
    * Quay lại màn hình chính của CloudWatch
      * Chọn Log groups từ menu bên trái
      * Tìm kiếm /ec2 trong thanh tìm kiếm
      * Chọn /ec2/linux/var/log/messages
    * Trong giao diện của /ec2/linux/var/log/messages
      * Mở rộng menu Actions
      * Chọn Create metric filter
    * ![Create metric filter](/images/1-Worklog/1.3-Week3/Day4/Createmetricfilter.png)
    * Trong phần Define Pattern, cấu hình các thông tin sau:
      * Filter pattern: mở rộng dropdown và chọn ERROR
      * Test pattern: mở rộng và chọn một instance (nên chọn instance mà chúng ta đã tạo processes ở các bước trước)
    * ![Define Pattern](/images/1-Worklog/1.3-Week3/Day4/DefinePattern.png)
    * Nhấn Test pattern để kiểm tra xem filter hoạt động chính xác không
    * ![Test pattern](/images/1-Worklog/1.3-Week3/Day4/Testpattern.png)
    * Trong phần Create filter name của Assign metric, nhập PythonAppErrors
    * ![Create filter name](/images/1-Worklog/1.3-Week3/Day4/Createfiltername.png)
    * Trong phần Metric details, cấu hình các thông tin sau:
      * Metric namespace: ec2-logs
      * Metric name: /var/log/messages - ERROR
      * Metric value: 1
      * Default value: 0
      * Unit: mở rộng dropdown và chọn Count
      * Nhấn Next
    * ![Metric details](/images/1-Worklog/1.3-Week3/Day4/Metricdetails.png)
    * Xem lại cấu hình và nhấn Create metric filter
    * ![Create metric](/images/1-Worklog/1.3-Week3/Day4/Createmetric.png)
    * ![Create Success](/images/1-Worklog/1.3-Week3/Day4/CreateSuccess.png)
    * Trở lại Metrics > All metrics
      * Tìm kiếm với từ khóa /var/log/messages và ERROR
      * Chọn ec2-logs > Metrics with no dimensions
    * ![Metrics with no dimensions](/images/1-Worklog/1.3-Week3/Day4/Metricswithnodimensions.png)
    * ![Metric name](/images/1-Worklog/1.3-Week3/Day4/Metricname.png)

* **CloudWatch Alarms**
  * Trở lại màn hình chính của CloudWatch
    * Chọn Alarms ở menu bên trái
    * Chọn All alarms
    * Ấn chọn Create alarm
  * ![Create alarm](/images/1-Worklog/1.3-Week3/Day4/Createalarm.png)
  * Chọn Select metric
  * ![Select metric](/images/1-Worklog/1.3-Week3/Day4/Selectmetric.png)
  * Cửa sổ metrics hiện lên, trong Custom namespaces, chọn ec2-logs
  * ![Custom namespaces](/images/1-Worklog/1.3-Week3/Day4/Customnamespaces.png)
  * Chọn tiếp Metrics with no dimensions, chọn /var/log/messages và ấn chọn Select metric
  * ![Metrics with no dimensions](/images/1-Worklog/1.3-Week3/Day4/Metricsnodimensions.png)
  * Trong phần Specify metric and conditions, chọn Period là 1 minutes
  * ![Period](/images/1-Worklog/1.3-Week3/Day4/Period.png)
  * Trong phần Conditions
    * Threshold type: Static
    * Điều kiện: Greater than 10
  * ![Conditions](/images/1-Worklog/1.3-Week3/Day4/Conditions.png)
  * ![Conditions Look](/images/1-Worklog/1.3-Week3/Day4/ConditionsLook.png)
  * Sau đó ấn Next để tiếp tục
  * Giờ thì chúng ta cấu hình thông báo như sau
    * Alarm state trigger: In alarm
    * Chọn Create new topic
    * Tên topic là: Error_logs_reach_10
    * Email thông báo tới: bạn sẽ nhập email của bạn vào, ở đây mình sẽ nhập của mình
    * Ấn Create topic
  * ![Create topic](/images/1-Worklog/1.3-Week3/Day4/Createtopic.png)
  * ![Topic Info](/images/1-Worklog/1.3-Week3/Day4/TopicInfo.png)
  * Ấn chọn Next
  * ![Next](/images/1-Worklog/1.3-Week3/Day4/Next.png)
  * Ở bước cuối, nhập tên alarm là PythonApplicationErrorAlarm và ấn chọn Next
  * ![PythonApplicationErrorAlarm ](/images/1-Worklog/1.3-Week3/Day4/PythonApplicationErrorAlarm .png)
  * Xem lại kết quả và ấn chọn Create alarm
  * ![Info Alarm.](/images/1-Worklog/1.3-Week3/Day4/InfoAlarm..png)
  * ![Create Alarm](/images/1-Worklog/1.3-Week3/Day4/CreateAlarm.png)
  * Kết quả
  * ![Final.](/images/1-Worklog/1.3-Week3/Day4/Final.png)
  * Đăng nhập vào Gmail hoặc bất kì trang email nào mà bạn dùng. Bạn sẽ thấy một email được gửi tới từ AWS Notification
  * Ấn chọn Confirm subscription
  * ![Confirm subscription](/images/1-Worklog/1.3-Week3/Day4/Confirmsubscription.png)
  * ![Success Subscription](/images/1-Worklog/1.3-Week3/Day4/SuccessSubscription.png)

* **CloudWatch Dashboards**
  * Trong phần cuối của workshop này, chúng ta sẽ tạo một Dashboard đơn giản để tập trung quản lý các Metrics và Alarms đã thiết lập trước đó, đặc biệt là Error Logs đã cấu hình trong phần trước
  * Thêm alarm đã tạo vào Dashboard:
    * Chọn PythonApplicationErrorAlarm
    * Mở rộng menu Actions
    * Chọn Add to dashboard
  * ![Add to dashboard](/images/1-Worklog/1.3-Week3/Day4/Addtodashboard.png)
  * Trong hộp thoại Add to dashboard, chọn Create new
  * ![Create new](/images/1-Worklog/1.3-Week3/Day4/Createnew.png)
  * Cấu hình Dashboard mới:
    * Nhập tên dashboard: CloudWatch-Workshop
    * Nhấn Create
    * Nhấn Add to dashboard
  * ![CloudWatch-Workshop](/images/1-Worklog/1.3-Week3/Day4/CloudWatch-Workshop.png)
  * ![Success Create Alarm](/images/1-Worklog/1.3-Week3/Day4/SuccessCreateAlarm.png)
  * Dưới đây là dashboard vừa được tạo:
  * ![Dashboard](/images/1-Worklog/1.3-Week3/Day4/dashboard.png)
  * Bạn có thể thực hiện nhiều thao tác tùy chỉnh trên widget này:
  * ![widget](/images/1-Worklog/1.3-Week3/Day4/widget.png)
  * ![widget look](/images/1-Worklog/1.3-Week3/Day4/widgetlook.png)

* **Dọn dẹp tài nguyên**
  * Trên thanh tìm kiếm dịch vụ AWS:
    * Nhập CloudFormation
    * Chọn CloudFormation
  * ![Seach CloudFormation](/images/1-Worklog/1.3-Week3/Day4/SeachCloudFormation.png)
  * Trong CloudFormation Console:
    * Chọn stack đã tạo trong workshop này
    * Ấn chọn Delete
  * ![Delete](/images/1-Worklog/1.3-Week3/Day4/Delete.png)
  * Trong hộp thoại xác nhận:
    * Ấn chọn Delete để xác nhận việc xóa stack
  * ![Delete stack](/images/1-Worklog/1.3-Week3/Day4/Deletestack.png)
  * Chờ đợi quá trình xóa hoàn tất:
    * Stack sẽ hiển thị trạng thái “DELETE_IN_PROGRESS” trong quá trình xóa
    * Sau khi hoàn tất, stack sẽ biến mất khỏi danh sách
  * ![Delete complete](/images/1-Worklog/1.3-Week3/Day4/Deletecomplete.png)