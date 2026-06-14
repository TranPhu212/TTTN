---
title: "Worklog Tuần 8"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.8. </b> "
---

### Mục tiêu tuần 8:

* 

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
|  6  | - Amazon DynamoDB - Quản lý và truy vấn cơ sở dữ liệu NoSQL | 05/06/2026 | 05/06/2026 | <https://000060.awsstudygroup.com/> |
|  2  | - Triển khai Amazon FSx for Windows File Server | 08/06/2026 | 08/06/2026 | <https://000025.awsstudygroup.com/> |
|  3  | - Sử dụng AWS Glue và Amazon Athena để phân tích chi phí và mức độ sử dụng tài nguyên | 09/06/2026 | 09/06/2026 | <https://000040.awsstudygroup.com/> |
|  4  | - Thực hành AWS Analytics: Data Lake, ETL và Phân tích Dữ liệu | 10/06/2026 | 10/06/2026 | <https://000072.awsstudygroup.com/> |
|  5  | - Refactor & Hoàn Thiện Giao Diện SOC Dashboard | 11/06/2026 | 11/06/2026 |


### Kết quả đạt được tuần 8:

## Thứ 6: Amazon DynamoDB – Quản lý và truy vấn cơ sở dữ liệu NoSQL trên AWS
* **Làm việc với Amazon DynamoDB**
  * **Giới thiệu**
    * Amazon DynamoDB là một dịch vụ cơ sở dữ liệu NoSQL được quản lý hoàn toàn, cung cấp hiệu suất nhanh và có thể dự đoán được với khả năng mở rộng liền mạch. DynamoDB cho phép giảm bớt gánh nặng quản trị của việc vận hành và mở rộng cơ sở dữ liệu phân tán, cung cấp phần cứng, thiết lập và cấu hình, sao chép, vá lỗi phần mềm hoặc mở rộng cụm. DynamoDB cũng cung cấp mã hóa ở trạng thái nghỉ
    * DynamoDB tạo các table cơ sở dữ liệu có thể lưu trữ và truy xuất bất kỳ lượng dữ liệu nào và phục vụ bất kỳ mức lưu lượng yêu cầu nào. Có thể tăng hoặc giảm quy mô công suất thông qua table của mình mà không có thời gian chết hoặc giảm hiệu suất
    * DynamoDB cung cấp khả năng sao lưu theo yêu cầu. Nó cho phép bạn tạo bản sao lưu đầy đủ các table để lưu giữ và lưu trữ lâu dài cho các nhu cầu tuân thủ quy định
    * Có thể tạo bản sao lưu theo yêu cầu và bật khôi phục tại thời điểm cho các table Amazon DynamoDB. Khôi phục theo thời gian giúp bảo vệ table khỏi các thao tác ghi hoặc xóa ngẫu nhiên. Với khôi phục theo thời gian, có thể khôi phục table về bất kỳ thời điểm nào trong 35 ngày qua
    * DynamoDB cho phép tự động xóa các item đã hết hạn khỏi table giúp giảm mức sử dụng bộ nhớ và chi phí lưu trữ dữ liệu không còn phù hợp
    
    * **Các thành phần cốt lõi của Amazon DynamoDB**
      * Table: Tương tự như các hệ thống cơ sở dữ liệu khác, DynamoDB lưu trữ dữ liệu trong table. Table là một tập hợp dữ liệu
      * Item: Mỗi table chứa không hoặc nhiều item. Các item trong DynamoDB khá tương đồng với khái niệm hàng trong cơ sở dữ liệu quan hệ, bản ghi hoặc bộ dữ liệu trong các hệ thống cơ sở dữ liệu khác. Trong DynamoDB, không có giới hạn về số lượng item bạn có thể lưu trữ trong một table
      * Attribute: Mỗi item bao gồm một hoặc nhiều attribute. Attribute là một phần tử dữ liệu cơ bản, không cần phải chia nhỏ thêm nữa. Các attribute trong DynamoDB theo nhiều cách tương tự với các cột trong các hệ thống cơ sở dữ liệu khác

      * **Primary Key**
        * Khi bạn tạo một table, ngoài tên table, bạn phải chỉ định primary key của table
        * Primary key xác định duy nhất từng item trong table, do đó không có hai item nào có thể có cùng một key
        * DynamoDB hỗ trợ hai loại primary key khác nhau:
          * Partition key
          * Composite primary key

      * **Partition key**
        * Một primary key đơn giản, bao gồm một attribute được gọi là Partition key
        * DynamoDB sử dụng giá trị của partition key làm đầu vào cho hàm băm bên trong. Đầu ra từ hàm băm xác định phân vùng (bộ nhớ vật lý bên trong DynamoDB) mà item sẽ được lưu trữ
        * Trong table chỉ có partition key, không có hai item nào có thể có cùng giá trị Partition key.

      * **Composite primary key**
        * Attribute đầu tiên là partition key và attribute thứ hai là sort key
        * DynamoDB sử dụng giá trị partition key làm đầu vào cho hàm băm bên trong. Đầu ra từ hàm băm xác định phân vùng (bộ nhớ vật lý bên trong DynamoDB) mà item sẽ được lưu trữ
        * Tất cả các item có cùng giá trị partition key được lưu trữ cùng nhau, theo thứ tự được sắp xếp theo giá trị sort key
        * Trong table có partition key và sort key, nhiều item có thể có cùng giá trị partition key. Tuy nhiên, các item đó phải có các giá trị sort key khác nhau
        * Composite primary key giúp bạn linh hoạt hơn khi truy vấn dữ liệu

    * **Secondary Index**
      * Bạn có thể tạo một hoặc nhiều Secondary Index trên một table
      * Secondary Index cho phép truy vấn dữ liệu trong table bằng các key khác với partition key và sort ban đầu của table. Với DynamoDB thao tác query dữ liệu có tốc độ nhanh và tiết kiệm chi phí hơn rất nhiều so với thao tác scan

      * **DynamoDB hỗ trợ hai loại index:**
        * Global secondary index: index có partition key và sort key có thể khác với các index trên table
        * 
        * Local secondary index: index có cùng partition key với table nhưng có sort key khác

      * Mỗi table trong DynamoDB có tối đa 20 Global secondary index (giới hạn mặc định) và 5 Local secondary index

    * **Quy tắc đặt tên và kiểu dữ liệu**
      * **Quy tắc đặt tên**
        * Các table, attribute và các đối tượng khác trong DynamoDB phải có tên
        * Tất cả các tên phải được mã hóa bằng UTF-8 và có phân biệt chữ hoa chữ thường
        * Tên table và tên index phải dài từ 3 đến 255 ký tự và chỉ được chứa các ký tự sau: a-z, A-Z, 0-9, _, -, 
        * Tên attribute phải dài ít nhất một ký tự, nhưng không dài hơn 64 KB
        * Một số ngoại lệ cho tên attribute không vượt quá 255 ký tự

      * **Kiểu dữ liệu**
        * DynamoDB hỗ trợ nhiều kiểu dữ liệu:
          * Các kiểu vô hướng: số, chuỗi, nhị phân, Boolean và null
          * Loại tài liệu: list và map
          * Loại tập hợp: tập hợp chuỗi, tập hợp số và tập hợp nhị phân

    * **Read Consistency**
      * **Eventually Consistent Reads**
        * Khi bạn đọc dữ liệu từ table DynamoDB, phản hồi có thể không phản ánh kết quả của một thao tác ghi đã hoàn thành gần đây
        * Phản hồi có thể bao gồm một số dữ liệu cũ
        * Nếu bạn lặp lại yêu cầu đọc của mình sau một thời gian ngắn, phản hồi sẽ trả về dữ liệu mới nhất

      * **Strongly Consistent Reads**
        * Khi bạn yêu cầu Strongly Consistent Reads, DynamoDB trả về phản hồi với dữ liệu cập nhật nhất. Tuy nhiên:
          * Có thể không khả dụng nếu có sự cố mạng
          * Có độ trễ cao hơn
          * Không hỗ trợ cho Global secondary indexes
          * Sử dụng gấp đôi dung lượng thông lượng

    * **Read/Write Capacity Mode**
      * **On-Demand Mode**
        * Thanh toán linh hoạt, trả theo sử dụng
        * Phù hợp cho khối lượng công việc không xác định hoặc không thể đoán trước

      * **Provisioned Mode**
        * Chỉ định số lần đọc/ghi mỗi giây
        * Có thể dùng auto scaling
        * Phù hợp cho lưu lượng dự đoán được

  * **Các bước chuẩn bị**
    * Cần tạo sẵn 1 Access key để tiến hành cấu hình AWS CLI
    * Có thể truy cập AWS DynamoDB bằng AWS Management Console hoặc AWS CLI / CloudShell

    * **Sử dụng AWS Management Console**
      * Bạn có thể truy cập tại https://console.aws.amazon.com/dynamodb/home
      * Các chức năng chính: tạo table, quản lý item, query/scan, index, monitoring, backup, v.v

    * **Tạo khóa truy cập**
      * Tạo IAM Access Key qua console IAM

    * **Tạo table**
      * Tạo table Music với Partition key: Artist, Sort key: SongTitle

    * **Ghi dữ liệu**
      * Thêm các item mẫu vào table Music (ví dụ Artist: No One You Know, Acme Band...)

    * **Đọc dữ liệu**
      * Sử dụng Query hoặc Explore items để đọc dữ liệu

    * **Truy vấn dữ liệu**
      * Thực hiện Query theo Partition key và Sort key

    * **Tạo Global secondary index**
      * Tạo GSI trên AlbumTitle

    * **Truy vấn Global secondary index**
      * Query theo index mới tạo

    * **Sử dụng AWS CloudShell**
      * AWS CloudShell là trình dòng lệnh dựa trên trình duyệt, đã cài sẵn AWS CLI

    * **Tạo table**
      * Khởi động AWS CloudShell tại: https://console.aws.amazon.com/cloudshell/home
      * Cấu hình AWS CLI:Bash aws configure
      * Nhập thông tin Access Key, Secret Key, region (ví dụ: us-east-1), output format (json)
      * Tạo table Music:Bash aws dynamodb create-table \
                                --table-name Music \
                                --attribute-definitions \
                                    AttributeName=Artist,AttributeType=S \
                                    AttributeName=SongTitle,AttributeType=S \
                                --key-schema \
                                    AttributeName=Artist,KeyType=HASH \
                                    AttributeName=SongTitle,KeyType=RANGE \
                                --provisioned-throughput \
                                    ReadCapacityUnits=10,WriteCapacityUnits=5 \
                                --table-class STANDARD
      * Kiểm tra trạng thái table:Bash aws dynamodb describe-table --table-name Music | grep TableStatus
      * Chờ đến khi TableStatus là ACTIVE

    * **Ghi dữ liệu**
      * Sử dụng lệnh put-item để thêm dữ liệu mẫu:
        Bash aws dynamodb put-item \
            --table-name Music \
            --item \
                '{"Artist": {"S": "No One You Know"}, "SongTitle": {"S": "Call Me Today"}, "AlbumTitle": {"S": "Somewhat Famous"}, "Awards": {"N": "1"}}'

        aws dynamodb put-item \
            --table-name Music \
            --item \
                '{"Artist": {"S": "No One You Know"}, "SongTitle": {"S": "Howdy"}, "AlbumTitle": {"S": "Somewhat Famous"}, "Awards": {"N": "2"}}'

        aws dynamodb put-item \
            --table-name Music \
            --item \
                '{"Artist": {"S": "Acme Band"}, "SongTitle": {"S": "Happy Day"}, "AlbumTitle": {"S": "Songs About Life"}, "Awards": {"N": "10"} }'

        aws dynamodb put-item \
            --table-name Music \
            --item \
                '{"Artist": {"S": "Acme Band"}, "SongTitle": {"S": "PartiQL Rocks"}, "AlbumTitle": {"S": "Another Album Title"}, "Awards": {"N": "8"} }'

    * **Đọc dữ liệu**
      * Sử dụng lệnh get-item (có thể dùng --consistent-read để strongly consistent):
        Bash aws dynamodb get-item --consistent-read \
            --table-name Music \
            --key '{ "Artist": {"S": "Acme Band"}, "SongTitle": {"S": "Happy Day"}}'

    * **Cập nhật dữ liệu**
      * Sử dụng lệnh update-item:
        Bash aws dynamodb update-item \
            --table-name Music \
            --key '{ "Artist": {"S": "Acme Band"}, "SongTitle": {"S": "Happy Day"}}' \
            --update-expression "SET AlbumTitle = :newval" \
            --expression-attribute-values '{":newval":{"S":"Updated Album Title"}}' \
            --return-values ALL_NEW

    * **Truy vấn dữ liệu**
      * Sử dụng lệnh query theo Partition Key:
        Bash aws dynamodb query \
            --table-name Music \
            --key-condition-expression "Artist = :name" \
            --expression-attribute-values  '{":name":{"S":"Acme Band"}}'

    * **Tạo Global Secondary Index**
        Bash aws dynamodb update-table \
            --table-name Music \
            --attribute-definitions AttributeName=AlbumTitle,AttributeType=S \
            --global-secondary-index-updates \
                "[{\"Create\":{\"IndexName\": \"AlbumTitle-index\",\"KeySchema\":[{\"AttributeName\":\"AlbumTitle\",\"KeyType\":\"HASH\"}], \
                \"ProvisionedThroughput\": {\"ReadCapacityUnits\": 10, \"WriteCapacityUnits\": 5      },\"Projection\":{\"ProjectionType\":\"ALL\"}}}]"
        * Chờ index chuyển sang trạng thái ACTIVE (kiểm tra bằng describe-table)

    * **Truy vấn Global Secondary Index**
        Bash aws dynamodb query \
            --table-name Music \
            --index-name AlbumTitle-index \
            --key-condition-expression "AlbumTitle = :name" \
            --expression-attribute-values  '{":name":{"S":"Somewhat Famous"}}'

  * **Bắt đầu với AWS SDK**
    * **Cấu hình AWS CLI**
      * Sử dụng aws configure với Access Key

    * **Bắt đầu phát triển với Python và DynamoDB (Boto3)**
      * Sử dụng Boto3 Client hoặc Resource
      * Các thao tác:
        * Tạo table
        * Ghi dữ liệu (put_item)
        * Đọc dữ liệu (get_item)
        * Cập nhật dữ liệu
        * Xóa dữ liệu
        * Tải dữ liệu mẫu
        * Truy vấn dữ liệu (query)
        * Quét dữ liệu (scan)
        * Xóa table

  * **Dọn dẹp tài nguyên**
    * Xóa table và các tài nguyên liên quan để tránh phát sinh chi phí

## Thứ 2: Xây dựng hệ thống lưu trữ tệp dùng chung với Amazon FSx
* **Triển khai FSx trên Windows**
  * **Giới thiệu tổng quát**
    * Amazon FSx for Windows File Server cung cấp bộ lưu trữ file dùng chung được quản lý hoàn toàn, tích hợp đầy đủ với Windows Server và hỗ trợ nhiều tính năng quản trị, quản lý dữ liệu
    * Kiến trúc chính:
      * File servers: Các instance EC2 chạy Windows File Server, truy cập qua giao thức SMB
      * Storage: Dữ liệu được lưu trên Amazon S3 (object storage)
      * VPC: Triển khai trong VPC để bảo mật
      * Networking: Sử dụng ENI và VPC
      * Data replication: Tự động sao chép đa AZ
      * Management: AWS quản lý hoàn toàn (backup, patching, monitoring)

  * **Giới thiệu**
    * Amazon FSx for Windows File Server cung cấp bộ lưu trữ dùng chung được quản lý toàn phần, được tích hợp trên Windows Server và cung cấp vô số tính năng quản trị, quản lý dữ liệu và truy cập vào dữ liệu
    * Trong bài thực hành này, chúng ta sẽ thiết lập hệ thống lưu trữ dữ liệu chung cho hạ tầng Windows

  * **Các bước chuẩn bị**
    * Để chuẩn bị cho Amazon FSx for Windows File Server, bạn nên xem xét các bước sau:
      * Xác định yêu cầu lưu trữ: Chọn dung lượng và hiệu suất phù hợp
      * Tạo VPC và cấu hình mạng (subnets, security groups)
      * Thiết lập Windows Active Directory (nếu cần tích hợp)
      * Cấu hình Security Group cho FSx
      * Lập kế hoạch truyền dữ liệu (nếu có)
      * Tạo Amazon FSx file system qua Console, CLI hoặc SDK
      * Kiểm tra kết nối và truy cập

  * **Tạo file share**
    * **Kết nối với EC2 Windows Instance 0**
      * Mở Amazon EC2 Console
      * Chọn instance Windows Instance 0 đang Running
      * Sao chép Public DNS (IPv4)
      * Sử dụng Remote Desktop (RDP) kết nối đến instance
      * Lấy username/password từ AWS Secrets Manager (Secret name chứa "Mật khẩu-<GUID>")

    * **Ánh xạ file share mặc định**
      * Trong File Explorer trên Windows Instance:
        * Right-click This PC → Map network drive
        * Drive: Z:
        * Folder: UNC path của file share mặc định (ví dụ: \\fs-0123456789abcdef.example.com\share)
          * Sao chép DNS Name từ tab Network & security của FSx file system
          * Check Reconnect at sign-in

      * Tạo một số file test trên ổ Z:

      * Tải dữ liệu mẫu từ NASA NEX (sử dụng PowerShell):PowerShell Read-S3Object -BucketName nasanex -KeyPrefix /AVHRR -Folder Z:/nasanex/AVHRR(Quá trình tải mất ~20 phút).

    * **Tạo file share mới**
      * Mở Amazon FSx Console → Chọn file system → Tab Network & security → Sao chép DNS Name.
      * Trên Windows Instance: Start → gõ fsmgmt.msc.
      * Action → Connect to another computer → Dán DNS Name.
      * Trong Shares → Action → New Share….
      * Tạo các share sau (trên ổ D:):
      Folder path      Share name   Create new path Shared folder permissions
      D:\application   application  Yes             Everyone - Full Control
      D:\data           data        Yes             Everyone - Full Control
      * Thử nghiệm tạo thêm các share khác trên ổ D:

    * **Quản lý file shares qua PowerShell Remote**
      * Lấy Windows Remote PowerShell Endpoint từ tab Network & security của FSx.
      * Chạy script để remote:
      PowerShell    $WindowsRemotePowerShellEndpoint = "fs-0123456789abcdef.example.com"
                    Enter-PSSession -ComputerName ${WindowsRemotePowerShellEndpoint} -ConfigurationName FsxRemoteAdmin
      * Kiểm tra các lệnh:
        Get-Command
        Get-FSxSmbShare
        Get-FSxSmbSession
        Get-FSxSmbServerConfiguration
        Get-FSxSmbShareAccess

  * **Kiểm tra hiệu năng**
    * **Kiểm tra hiệu năng**
      * Phần này sẽ kiểm tra hiệu năng của STG326 - SAZ
      * Có rất nhiều công cụ kiểm tra hiệu suất đĩa. Lab đã cài sẵn DiskSpd và fio trên Windows Instance 0.
    
    * **DiskSpd Read tests**
      * RDP vào Windows Instance 0
      * Mở Windows PowerShell
      * Tạo file test 100GB:
        PowerShell  $random = $(Get-Random)
                    fsutil file createnew Z:\${env:computername}-$random.dat 100000000000
      * Chạy test đọc:
            PowerShell C:\Tools\DiskSpd-2.0.21a\amd64\DiskSpd.exe -d120 -w0 -r -t1 -o32 -b64K -Su -L Z:\${env:computername}-$random.dat
        * Trong lúc chạy, mở Task Manager → Performance → Ethernet để theo dõi

    * **Câu hỏi:**
      * Thông lượng đọc cao nhất đạt được?
      * P99 latency?
      * Tổng IO MiB/s?
      * IOPS?
      * AvgLat?
      * Tại sao thông lượng thực tế cao hơn baseline?
      * Thử nghiệm với các tham số khác nhau (-b, -o, -t, -Su, v.v.)

    * **DiskSpd Write tests**
      * Chạy test ghi:
        PowerShell  $random = $(Get-Random)
                    C:\Tools\DiskSpd-2.0.21a\AMD64\DiskSpd.exe -d120 -c2G -s64K -w100 -t1 -o32 -b64K -Sh -L Z:\${env:computername}-$random.dat
      * Theo dõi tương tự và trả lời các câu hỏi về write performance.

    * **fio read / write tests**
      * Sử dụng fio để test:
        PowerShell # Read test
        $random = $(Get-Random)
        C:\Tools\fio-3.16-x64\fio --randrepeat=1 --direct=1 --name="Z:\${env:computername}-$random.dat" --numjobs=1 --bs=64K --iodepth=32 --size=1024M --readwrite=read --rwmixread=100 --thread --time_based --runtime=120

  * **Giám sát hiệu năng**
    * Phần này sẽ theo dõi hiệu suất của STG326 - SAZ

    * **Bảng điều khiển CloudWatch**
      * Mở CloudWatch Console
      * Chọn Dashboards từ menu bên trái
      * Chọn dashboard đã được tạo sẵn (tên thường là region-fs-id, ví dụ: us-east-2-fs-0123456789abcdef)
      * Khám phá các widget, zoom in/out, và quan sát sự đồng bộ thời gian giữa các metric

    * **CloudWatch Alarm**
      * Sao chép FSx File System ID từ dashboard
      * Maximize widget Throughput (Bytes per second) → View in metrics
      * Tìm metric Total Data Throughput (B/s) → Create alarm
      * Đặt threshold > 200000000 (200 MB/s)
      * Tạo SNS topic mới và subscribe email của bạn
      * Đặt tên alarm và tạo
      * Xác nhận subscription qua email
      * Chạy lại các test performance (đọc/ghi) ít nhất 2 phút để kích hoạt alarm
      * Kiểm tra email nhận thông báo

  * **Kích hoạt chống dữ liệu trùng lặp**
    * Sử dụng Windows Remote PowerShell Endpoint từ tab Network & security của FSx
    * Kết nối Remote PowerShell:
      PowerShell  $WindowsRemotePowerShellEndpoint = "fs-..."
                  Enter-PSSession -ComputerName $WindowsRemotePowerShellEndpoint -ConfigurationName FsxRemoteAdmin
    * Xem lệnh:PowerShell Get-Command *-FSxDedup*
    * Kích hoạt:PowerShell Enable-FSxDedup
    * Kiểm tra trạng thái:
      PowerShell  Get-FSxDedupConfiguration
                  Get-FSxDedupStatus
                  Get-FSxDedupJob

    * **Tạo lịch trình tối ưu hóa**
      * Tạo schedule DailyOptimization
      * Cập nhật MinimumFileAgeDays = 0
      * Chạy job và theo dõi Get-FSxDedupStatus để xem dung lượng được tiết kiệm

  * **Kích hoạt Shadow Copies**
    * Kết nối Remote PowerShell tương tự
    * Xem lệnh:PowerShell Get-Command *-FSxShadow*
    * Thiết lập mặc định:
      PowerShell  Set-FsxShadowStorage -Default
                  Set-FsxShadowCopySchedule -Default
    * Kiểm tra:
      PowerShell  Get-FSxShadowCopies
                  Get-FSxShadowCopySchedule
                  Get-FSxShadowStorage

    * **Sửa đổi và tạo Shadow Copy**
      * Đặt max size 20%: Set-FSxShadowStorage -maxsize "20%"
      * Tạo Shadow Copy mới: New-FSxShadowCopy
      * Thử nghiệm restore previous versions qua File Explorer

  * **Quản lý Session người dùng và mở tệp**
    * **Qua giao diện (fsmgmt.msc)**
      * Kết nối đến DNS Name của FSx
      * Xem Sessions và Open Files
      * Chạy DiskSpd test và quan sát file đang mở → Close Open File

    * **Qua PowerShell Remote**
      * Kết nối Remote PowerShell.
      * Xem lệnh: Get-Command *SmbSession*, Get-Command *Open*
      * Chạy test và dùng:
        PowerShell  Get-FSxSmbOpenFile
                    Close-FSxSmbOpenFile

  * **Kích hoạt hạn ngạch bộ nhớ của người dùng (User Quotas)**
    * Kết nối Remote PowerShell.
    * Xem lệnh: Get-Command *-FSxUserQuota*
    * Bật quota:PowerShell Enable-FSxUserQuotas -Track -DefaultLimit 200000000000 -DefaultWarningLimit 100000000000
    * Tạo file lớn vượt limit → Kiểm tra Get-FSxUserQuotaEntries
    * Chuyển sang Enforce mode và thử nghiệm.
    * Vô hiệu hóa: Disable-FSxUserQuotas

  * **Kích hoạt chia sẻ Truy cập liên tục (Continuously Available Share)**
    * Sử dụng file system MAZ.
    * Tạo thư mục D:\sql
    * Tạo CA Share:PowerShellNew-FSxSmbShare -Name "SQL CA Share" -Path "D:\sql" -Description "SQL CA share" -ContinuouslyAvailable $True -FolderEnumerationMode AccessBased -EncryptData $true

  * **Mở rộng khả năng thông lượng (Scale Throughput Capacity)**
    * Vào FSx Console → Chọn file system MAZ → Update Throughput capacity lên 64 MB/s
    * Theo dõi tab Updates
    * Quá trình sẽ thực hiện failover (Multi-AZ) hoặc downtime ngắn (Single-AZ)

  * **Mở rộng dung lượng lưu trữ (Scale Storage Capacity)**
    * Vào FSx Console → Chọn file system → Update Storage capacity tăng 10%
    * Theo dõi tab Updates và widget Free storage capacity
    * Quá trình tối ưu hóa chạy nền (có thể mất vài giờ/ngày)

  * **Dọn dẹp tài nguyên**
    * Xóa các backup thủ công (nếu có)
    * Xóa file system Multi-AZ
    * Xóa CloudFormation stack để dọn dẹp toàn bộ môi trường

## Thứ 3: Phân tích Chi phí và Hiệu năng AWS với Glue và Athena
* **Giới thiệu**
  * Phần này cung cấp kiến thức nền tảng về hai dịch vụ cốt lõi sẽ sử dụng trong bài thực hành:
    * AWS Glue: Là dịch vụ chuẩn bị dữ liệu hỗ trợ quá trình ETL (Extract - Transform - Load). Tài liệu giải thích cách thức hoạt động cơ bản của Glue từ việc trích xuất dữ liệu thô từ các nguồn như Amazon S3, chuyển đổi định dạng (ví dụ: sang tối ưu như Parquet), rồi đẩy vào kho dữ liệu
    * Amazon Athena: Dịch vụ truy vấn tương tác cho phép phân tích dữ liệu trực tiếp trong Amazon S3 bằng ngôn ngữ SQL tiêu chuẩn
    * Mô hình hoạt động: Tài liệu phác thảo quy trình chuẩn gồm 7 bước từ lúc đẩy dữ liệu vào S3, dùng Glue Crawler quét dữ liệu, biến đổi qua ETL, lưu lại định dạng Parquet cho đến khi dùng Athena để truy vấn. Tuy nhiên, để tối giản, bài Lab này sẽ bỏ qua bước biến đổi ban đầu và làm việc trực tiếp với các tệp Parquet có sẵn

* **Các bước chuẩn bị**
  * Phần này hướng dẫn người học chuẩn bị cơ sở dữ liệu để phục vụ cho việc phân tích, chia làm 3 bước nhỏ:
  * **Chuẩn bị cơ sở dữ liệu:** Các thiết lập ban đầu về quyền truy cập (IAM), cấu hình phân quyền dịch vụ và chuẩn bị xô lưu trữ (S3 bucket) chứa dữ liệu đầu vào
  * **Xây dựng cơ sở dữ liệu:** Tạo cấu trúc dữ liệu, cấu hình AWS Glue Crawler để quét các tệp Parquet mẫu có sẵn và tự động tạo ra các bảng (tables) trong Glue Data Catalog
  * **Kiểm tra cơ sở dữ liệu:** Xác thực xem dữ liệu đã được nạp đúng cấu trúc chưa trước khi tiến hành phân tích

* **Phân tích hiệu năng sử dụng và chi phí**
  * Đây là nội dung thực hành cốt lõi, nơi người học viết các câu lệnh truy vấn SQL trên Amazon Athena để bóc tách dữ liệu báo cáo:
  * **Dữ liệu trong bảng:** Khám phá cấu trúc tổng quan của bảng dữ liệu sau khi crawl, hiểu ý nghĩa các trường dữ liệu liên quan đến chi phí và tài nguyên
  * **Chi phí:** Thực hiện các câu lệnh truy vấn để thống kê chi phí, tìm ra dịch vụ nào đang tiêu tốn nhiều tiền nhất, xu hướng tăng trưởng chi phí theo thời gian
  * **Gắn thẻ và Phân bổ chi phí:** Hướng dẫn cách phân tích chi phí dựa trên các thẻ (Tags) được gắn cho tài nguyên (ví dụ: theo môi trường Dev/Prod, theo phòng ban, theo dự án)
  * Mức độ sử dụng:** Đối chiếu chi phí với hiệu suất sử dụng thực tế của tài nguyên (CPU, dung lượng lưu trữ, số lượng request...) nhằm tìm ra các tài nguyên đang bị lãng phí (Idle hoặc Underutilized)

* **Dọn dẹp tài nguyên**
  * Phần cuối cùng hướng dẫn người học cách xóa bỏ các tài nguyên AWS đã tạo ra trong suốt quá trình làm Lab (như xóa S3 bucket kết quả, xóa Glue database/crawler, xóa lịch sử truy vấn Athena). Bước này vô cùng quan trọng nhằm giúp tài khoản AWS của người học không phát sinh chi phí ngoài ý muốn sau khi hoàn thành bài học

## Thứ 4: Xây dựng Data Lake và Quy trình Phân tích Dữ liệu End-to-End trên AWS
* **Giới thiệu & Chuẩn bị**
  * Giới thiệu: Tổng quan về các dịch vụ phân tích trong danh mục AWS Analytics. Các mục tiêu học tập cốt lõi bao gồm xây dựng Data Lake với S3, xử lý dữ liệu thời gian thực, quản lý siêu dữ liệu (metadata) và tối ưu hóa truy vấn
  * Các bước chuẩn bị: Hướng dẫn thiết lập môi trường lab, khởi tạo cơ sở dữ liệu ban đầu (Amazon RDS) để làm nguồn dữ liệu mẫu

* **Thu thập và Lưu trữ dữ liệu**
  * Creating Kinesis Firehose: Hướng dẫn cấu hình Amazon Kinesis Data Firehose để thu thập và truyền tải dữ liệu streaming một cách liên tục vào hồ dữ liệu lưu trữ trên Amazon S3
  * Generate Dummy Data: Cung cấp phương thức hoặc kịch bản tạo dữ liệu giả lập (phát sinh liên tục) để kiểm thử luồng ingest của hệ thống

* **Định danh và Lập mục lục dữ liệu**
  * Create IAM Role: Cấu hình phân quyền AWS IAM để cấp phép cho các dịch vụ bảo mật truy cập lẫn nhau
  * Creating AWS Glue Crawlers: Thiết lập các trình quét tự động (Crawlers) của AWS Glue để quét qua dữ liệu thô trong S3, tự động khám phá cấu trúc dữ liệu (schema) và ghi lại vào AWS Glue Data Catalog
  * Verify tables: Kiểm tra và xác thực các bảng dữ liệu vừa được tự động tạo ra trong danh mục lưu trữ

* **Biến đổi dữ liệu**
  * Nội dung này hướng dẫn người dùng thực hiện ETL (Extract, Transform, Load) bằng nhiều công cụ và phương pháp khác nhau trên AWS:
  * AWS Glue Interactive Sessions: Chạy và thử nghiệm trực tiếp các đoạn mã ETL Spark thông qua môi trường sổ ghi chép Jupyter Notebook giao diện tương tác
  * AWS Glue Studio: Sử dụng giao diện đồ họa (Kéo - Thả) để thiết kế, vận hành và giám sát các luồng công việc (ETL jobs) mà không cần viết nhiều mã nguồn
  * AWS Glue DataBrew: Sử dụng công cụ trực quan hóa chuyên biệt để chuẩn bị, làm sạch, và chuẩn hóa dữ liệu một cách nhanh chóng
  * Amazon EMR (Elastic MapReduce): Thực hiện các tác vụ chuyển đổi dữ liệu quy mô lớn bằng cách chạy các job Spark trên cụm máy chủ Amazon EMR

* **Phân tích và Khai thác dữ liệu**
  * Analysis with Athena: Sử dụng Amazon Athena để truy vấn phân tích dữ liệu trực tiếp trên S3 bằng ngôn ngữ SQL tiêu chuẩn mà không cần quản lý máy chủ
  * Analysis with Kinesis Data Analytics: Thực hiện phân tích, tính toán các chỉ số trên luồng dữ liệu truyền tải theo thời gian thực (Real-time analytics)
  * Serve with Lambda: Sử dụng hàm AWS Lambda để xử lý và cung cấp dữ liệu cho các ứng dụng hoặc dịch vụ khác
  * Warehouse on Redshift: Tải dữ liệu đã qua xử lý từ AWS Glue/S3 vào kho dữ liệu Amazon Redshift, đồng thời tìm hiểu các kiến trúc và thực hành tốt nhất (best practices) để tối ưu hóa hiệu năng kho dữ liệu này

* **Trực quan hóa & Dọn dẹp**
  * Visualize in QuickSight: Kết nối công cụ Amazon QuickSight vào nguồn dữ liệu (Athena/Redshift) để xây dựng các biểu đồ, bảng điều khiển (Dashboard) trực quan hóa dữ liệu phục vụ báo cáo doanh nghiệp
  * Clean up: Hướng dẫn chi tiết cách xóa bỏ toàn bộ tài nguyên (S3, Redshift, EMR, Glue, RDS...)

## Thứ 5: Refactor Toàn Diện và Chuẩn Bị Tích Hợp Realtime
* **Tóm tắt tiến độ tuần này**
  * Tuần này tập trung mạnh vào **refactor & hoàn thiện giao diện các trang chính** của SOC Dashboard. 
    - Hoàn tất refactor nhiều module quan trọng: Settings, Reports, Dashboard, Cloud, Threat Intel, Attack Surface...
    - Xử lý merge conflict và đồng bộ routing, sidebar.
    - Cải thiện consistency UI/UX, đặc biệt là **Light/Dark mode**.
    - Branch `devphu` hiện **16 commits ahead** so với `main`.
  * **Mục tiêu tuần**: Xây dựng nền tảng frontend vững chắc, sẵn sàng kết nối realtime với backend Track A.

* **Các Commit**
  - **fix conflic** (`556d881c7e07e03edc64e9f6d9d72782fb894b93`)  
    Sửa xung đột merge sau khi tích hợp các branch khác.  
    **Thay đổi chính**: Cập nhật routing trong `App.tsx`, import các page mới (CloudPage, ThreatIntelPage...), điều chỉnh logic Sidebar và type `AppView`.
  - **refactor settings** (`660438543037e5d5ad1d9951e1bdf2273e3b8334`)  
    Refactor toàn bộ trang **Settings**.  
    **Nổi bật**:
    - Thêm thư viện `zod` cho validation form.
    - Tạo mới/tối ưu nhiều tab: General, Appearance, AWS, AccessControl, UserManagement, AiEngineSettingsTab, Integrations, Monitoring, Backup, Dataset, Reporting, Fusion...
    - Cải thiện UI permission grid, toast notification, dark/light mode.
  - **refactor reports** (`1d95e6e6f193645d032472422a0cde8ff7d55754`)  
    Refactor trang Reports.
  - **refactor dashboard** (`5a0ee2d71cd33cde4818639b4348884384ca48ff`)
  - **refactor cloud** (`62d0307ffd30131ad117538dc462c9d8014b5631`)
  - **refactor threat intel** (`85d2434f3ad2626c5514e955787c9e28d0f277ea`)
  - **refactor attack surface, integrations, mitre att&ck, playbooks** (`e731649666c89b2789be1a858fab5a3c05518993`)
  - Refactor AI Threat Detection, Alerts, Case Management, Endpoint, Network.
  - Thêm trang Cloud và Threat Intel.
  - Update Attack Surface, Playbooks, Geomap.
  - Fix Light/Dark mode trên nhiều trang (Dashboard, Network, Alerts, Integrations...).
  - Merge pull request từ các feature branch.

* **Chi Tiết Công Việc Đã Hoàn Thành**
  * Frontend Improvements
  - **Routing & Navigation**: Đồng bộ React Router, Sidebar, AppView types.
  - **Settings Module**: Hoàn thiện hệ thống cấu hình chi tiết với validation mạnh mẽ.
  - **Reports**: Cải tiến giao diện báo cáo.
  - **Core Pages**: Dashboard, Cloud Security, Threat Intelligence, Attack Surface, MITRE ATT&CK, Playbooks, AI Threat Detection, Alerts, Network, Endpoint.
  - **UI/UX Consistency**: 
    - Light/Dark mode ổn định trên toàn bộ ứng dụng.
    - KPI cards, MITRE matrix, alert feed, event detail modal.
    - Toast notification, permission management, responsive design.
  * Công nghệ & Dependencies
    - Thêm `zod` cho schema validation.
    - Tiếp tục sử dụng React + Vite + Tailwind CSS.
    - Mock data & chuẩn bị WebSocket integration.

* **Khó khăn & Giải pháp**
  - **Xung đột merge**: Đã giải quyết triệt để bằng commit `fix conflic`.
  - **Tính nhất quán UI**: Đã fix Light/Dark mode trên nhiều trang.
  - **Phức tạp của Settings**: Đã tách thành nhiều component riêng biệt + validation.o-end giao diện SOC Dashboard.

* **Trạng Thái Tổng Thể Project**
  - **Frontend (Track B)**: Đang rất tốt, giao diện SOC Dashboard đã khá hoàn chỉnh và chuyên nghiệp.
  - **Tích hợp**: Sẵn sàng kết nối với Track A (API + WebSocket).
  - **Demo**: Có thể chạy `pnpm dev` trong thư mục `frontend` để demo ngay.