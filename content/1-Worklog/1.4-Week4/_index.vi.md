---
title: "Worklog Tuần 4"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
---

### Mục tiêu tuần 4:

* Nắm vững các dịch vụ lưu trữ của AWS (Amazon S3 và các tính năng nâng cao, Storage Gateway, Snow Family, AWS Backup) cùng chiến lược Disaster Recovery
* Thành thạo thiết kế và triển khai Amazon VPC theo best practices (Multi-AZ, bảo mật mạng, NAT Gateway, VPC Flow Logs, Session Manager)
* Thiết lập kết nối Hybrid Cloud an toàn qua Site-to-Site VPN
* Cấu hình Hybrid DNS hai chiều giữa môi trường AWS và On-premise sử dụng Route 53 Resolver (Inbound/Outbound Endpoints + Resolver Rules)

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
|  6  | - Học Amazon S3 (Storage Class, Access Point, Versioning, Static Website, CORS, Glacier), Snow Family, Storage Gateway, Disaster Recovery (RTO/RPO) và AWS Backup | 08/05/2026 | 08/05/2026 | <https://cloudjourney.awsstudygroup.com/> |
|  2  | - Xây dựng VPC Multi-AZ, cấu hình bảo mật mạng (SG, NACLs), NAT Gateway, VPC Flow Logs, Session Manager và thiết lập kết nối Site-to-Site VPN | 11/05/2026 | 11/05/2026 | <https://000003.awsstudygroup.com/> |
|  4  | - Cấu hình Hybrid DNS hai chiều giữa AWS và On-premise dùng Route 53 Resolver, Endpoints & Resolver Rules | 13/05/2026 | 13/08/2026 | <https://000010.awsstudygroup.com/> |


### Kết quả đạt được tuần 4:

## Thứ 6: Dịch Vụ Lưu Trữ Trên AWS
  * Amazon Simple Storage Service – S3
  * Amazon Storage Gateway
  * Snow Family
  * Disaster Recovery on AWS
  * AWS Backup

  * **Amazon Simple Storage Service (S3)**
    * Amazon S3 là kho lưu trữ ở mức đối tượng, có nghĩa là nếu muốn thay đổi một phần của tập tin, bạn phải thực hiện thay đổi rồi tải lại toàn bộ tập tin đã sửa đổi
    * S3 phù hợp với các loại dữ liệu ghi một lần đọc nhiều lần
    * Đơn vị nhỏ nhất lưu trữ xuống hệ thống lưu trữ là 1 đối tượng, 1 object
    * Khi lưu trữ như vậy, muốn thay đổi nội dung trong object thì phải thay đổi hoàn toàn phải bắt buộc ghi đè để tạo 1 object mới, override cái object cũ
    * Khác với kiểu lưu trữ dạng khối nhưng mà hay sử dụng
    * (WORM – Write Once Read Many)
    * Amazon S3 không giới hạn tổng khối lượng dữ liệu lưu trữ
    * Mỗi đối tượng không được lớn hơn 5 TB
    * * Trường hợp elastic block store, 3 nhân bản chỉ nằm trong 1 AG
    * Theo mặc định, dữ liệu trong Amazon S3 được nhân bản trên 3 AZ trong 1 Region
    * Amazon S3 có khả năng kích hoạt sự kiện (trigger event) cho phép bạn kích hoạt tự động các hành động khi một số sự kiện xảy ra, như tải lên hoặc xóa đối tượng khỏi một vùng lưu trữ cụ thể
    * Bắt được những sự kiện đó có thể chạy những serless function
    * Khi upload dữ liệu lên S3 thì bản thân S3 sé có nhiều cơ chế chạy ngầm vào bên trong để đảm bảo dữ liệu được toàn vẹn và được độc nhất
    * Amazon S3 được thiết kế để đạt được độ bền (durability) 99.999999999% và độ sẵn sàng (high availability) 99.99%
    * Amazon S3 hỗ trợ multipart upload để upload các đối tượng lớn lên bucket
    * Chúng ta cần tạo các S3 bucket để có thể lưu trữ các đối tượng trong Amazon S3
      * https://[tên bucket].s3.amazonaws.com
      * https://[tên bucket].s3.amazonaws.com/capture.mp4
    * Làm việc với S3 thông quá REST API.(HTTP)

  * **Amazon Simple Storage Service (S3) – Access Point**
    * Amazon S3 Access Point là tính năng cho phép tạo các điểm kết nối (hostname unique) dành cho ứng dụng, người dùng đơn lẻ hoặc theo nhóm
    * Chúng ta có thể cấu hình phân quyền khác nhau cho mỗi access point được tạo ra
    * Khi có nhiều ứng dụng cần lưu trữ dữ liệu ở bên trong S3 sẽ phải tạo nhiều S3 bucket riêng biệt cho mỗi ứng dụng và gây nên việc quản lý, chính sách truy cập vào cái S3 quản lý các policy trở nền phức tạp, khó khăn
    * Việc gán quyền truy cập cho từng bucket riêng dẫn đến rủi ro, thao tác lỗi có thể thiếu quyền, dư quyền và nó cũng khó khắn trong việc theo dõi và duy trì policy đó
    * Giờ đây có tính năng mới là access point, cho phép tạo được nhiều điển kết nối có những hostname khác nhau dành cho ứng dụng 
    * Tuy nhiên tát cả những điểm kết nối này đều kết nối vào 1 bucket duy nhất
    * Cái việc chia quyền truy cập cho từng ứng dụng cho người dùng sẽ dễ dàng hơn so với việc tạo ra nhiều S3 bucket
    * Tạo S3 access points cho các ứng dụng với quyền truy cập khác nhau

  * **Amazon Simple Storage Service (S3) – Storage Class**
    * Amazon S3 chia vùng lưu trữ ra nhiều lớp lưu trữ (storage class) giúp chúng ta tối ưu hóa chi phí
    * Các cấp lưu trữ (Storage Class của S3):
      * S3 Standard: Dữ liệu được truy cập thường xuyên
      * S3 Standard IA: Dữ liệu không truy cập thường xuyên
      * S3 Intelligent Tiering: Tự động di chuyển các đối tượng giữa các cấp lưu trữ theo số ngày đối tượng không được truy cập
      * S3 One Zone IA: Dữ liệu có thể tái tạo lại, được lưu trữ dài hạn, không truy cập thường xuyên nhưng cần truy cập nhanh
      * Amazon Glacier / Deep Archive: Lưu trữ dữ liệu ít truy cập
      * Chúng ta có thể thiết lập tự động hóa vòng đời của dữ liệu (Object Life Cycle Management) được lưu trữ trong Amazon S3. Bằng cách sử dụng chính sách vòng đời, chúng ta có thể luân chuyển dữ liệu trong 1 S3 bucket giữa các cấp lưu trữ theo thời gian (ngày) tùy chỉnh
    * Việc chi nhiều cấp là để tối ưu chi phí
    * S3 có 2 chi phí chính là về dung lượng tổng, cái dung lượng của các object đưa vào S3
    * Cái thứ 2 là số lượng request tới cái S3 service của mình, mỗi request là lúc upload dữ liệu lên, lúc lấy dữ liệu về một cái get request cũng đếm theo số lượng request nữa và 2 cái đó có mức giá khác nhau
    * Đối với standard, cái mức giá lưu trữ sẽ cao nhưng bù lại mức giá cho request sẽ thấp cho nên dữ liệu truy cập thường xuyên nên để ở đây
    * Đối với standard infrequent access thì những dữ liệu nào không truy cập thường xuyên, cái giá lưu trữ có thể thấp hơn một chút nhưng giá request sẽ cao
    * Nếu đưa cái đối tượng dữ liệu được truy cập thường xuyên vào cái standard infrequent access thì sẽ phải tra một cái mức phí cao hơn cả S3 standard đó chứ không phải là dữ liệu đưa vào đây là sẽ chắc chắn 100% rẻ hơn ở S3 standard
    * Object Life Cycle Management sẽ di chuyển object sau số ngày chúng ta quy định, được tính từ ngày object được tạo

  * **Amazon Simple Storage Service ( S3 ) – Static Website & CORS**
    * Amazon S3 có tính năng cho phép host các static website ( html , media ... ) , phù hợp cho Single Page Application ( ứng dụng web hoặc trang web tương tác với người dùng bằng cách tự động viết lại trang web hiện tại với dữ liệu mới từ máy chủ web sử dụng javascript và các framework của nó như AngularJs, ReactJS, thay vì phương pháp mặc định của trình duyệt web tải toàn bộ trang mới )
    * Amazon S3 hỗ trợ CORS. CORS là một cơ chế cho phép nhiều tài nguyên khác nhau (fonts, Javascript, v.v...) của một trang web có thể được truy vấn từ domain khác với domain của trang đó. CORS là viết tắt của từ Cross-origin resource sharing
    * https://docs.aws.amazon.com/AmazonS3/latest/userguide/cors.html
    * Amazon S3 có tính năng cho phép host các static website ( html , media ... ) , phù hợp cho Single Page Application
    * Amazon S3 cho phép cấu hình chính sách CORS ( Cross Origin Resource Sharing ) cho phép client web applications tương tác với các tài nguyên nằm ở domain khác

  * **Amazon Simple Storage Service (S3) – Control access**
    * Amazon S3 có 2 cơ chế kiểm soát quyền truy cập tới bucket
    * S3 Access Control List (ACL) là một cơ chế kiểm soát truy cập có trước IAM. Tuy nhiên, nếu bạn đã sử dụng S3 ACL và thấy đủ thì không cần thay đổi. ACL S3 được gắn bucket và object của S3. Nó xác định tài khoản hoặc nhóm AWS nào được cấp quyền truy cập và loại quyền truy cập
    * S3 Bucket Policy và IAM policy xác định quyền cấp đối tượng bằng cách cung cấp các đối tượng đó trong phần Resource trong policy của bạn. Câu lệnh sẽ áp dụng cho các đối tượng đó trong bucket. Việc hợp nhất các quyền dành riêng cho đối tượng thành một chính sách (trái ngược với nhiều ACL S3) giúp bạn dễ dàng hơn trong việc xác định các quyền truy cập
    * Mỗi object trong S3 đều ngang hàng, không phân cấp (hierarchy) và được gắn 1 object key. Ví dụ: /image/sample.jpg , sample.jpg
  
  * **Amazon Simple Storage Service (S3) – Endpoint & Versioning**
    * Điểm truy cập Amazon S3 (S3 Endpoint) là tính năng cho phép truy cập đến S3 bucket thông qua mạng riêng của AWS. Mặc định, việc truy cập tới S3 là thông qua internet
    * Chúng ta có thể kích hoạt tính năng lập phiên bản (Versioning) cho phép bạn khôi phục đối tượng sau khi vô tình xóa hay ghi đè, có thể hỗ trợ trước việc bị tấn công ransomware / encryption attack:
    * Nếu xóa một đối tượng, thay vì xóa đối tượng đó, thì Amazon S3 sẽ đánh dấu tập tin đã xóa
    * Nếu ghi đè đối tượng, thì một phiên bản đối tượng mới sẽ xuất hiện trong bucket
    * => Trong cả 2 trường hợp chúng ta đều có thể khôi phục phiên bản trước đó
    * (Versioning) cho phép bạn khôi phục đối tượng sau khi vô tình xóa hay ghi đè, có thể hỗ trợ trước việc bị tấn công ransomware / encryption attack

  * **Amazon Simple Storage Service (S3) – Object Key & Performance**
    * Mỗi object trong S3 đều ngang hàng, không phân cấp (hierarchy) và được gắn 1 object key. Ví dụ: /image/sample.jpg , sample.jpg
    * Sâu bên dưới S3 chia ra các Partitions, Partitions sẽ được chia ra tự động khi lượng request tăng cao hoặc số lượng S3 object keys lớn (làm chậm tốc độ tìm kiếm object trong partition)
    * S3 lưu trữ key map (key map cũng được chia ra nhiều partition và được hash bởi prefix – tiền tố của object key)
    * Để tối ưu S3 performance có thể dùng random prefix ( /fscd/img/sample.jpg thay vì /img/sample.jpg ). Mục tiêu của việc làm này là khiến S3 lưu trữ các object trên nhiều partitions nhất có thể vì performance của S3 dựa trên số lượng partitions

  * **Amazon Simple Storage Service (S3) – Glacier**
    * Amazon S3 Glacier là lựa chọn lưu trữ có chi phí thấp, phù hợp với dữ liệu không yêu cầu truy suất trực tiếp, dữ liệu lưu trữ dài hạn. Nếu ứng dụng yêu cầu truy cập dữ liệu nhanh chóng hoặc thường xuyên, hãy chọn Amazon S3
    * Khi lưu trữ dữ liệu trong Amazon S3 Glacier bạn không thể truy xuất dữ liệu trực tiếp mà phải đưa ( retrieve ) dữ liệu về lại một S3 Bucket
    * Có ba tùy chọn để truy xuất dữ liệu với thời gian truy cập và chi phí khác nhau:
      * Truy xuất Nhanh ( Expedited ) thường hoàn tất trong vòng 1 – 5 phút
      * Truy xuất Tiêu chuẩn ( Standard ) thường hoàn tất trong vòng 3 – 5 giờ
      * Truy xuất Hàng loạt ( Bulk ) thường hoàn tất trong vòng 5 – 12 giờ
    * Amazon S3 Glacier là lựa chọn lưu trữ có chi phí thấp, phù hợp với dữ liệu không yêu cầu truy suất trực tiếp, dữ liệu lưu trữ dài hạn

  * **Snow Family - Storage Gateway - Backup**
    * **Snow Family - Snowball**
      * Dịch vụ hỗ trợ migrate dữ liệu từ môi trường on-premise tới AWS ở quy mô lên đến PetaByte (PB). Mỗi Snowball có thể chứa tới 80 TeraByte (TB)
      * Snowball sẽ được ship trở về AWS region mà chúng ta lựa chọn để lưu trữ dữ liệu và lưu trong dịch vụ chúng ta lựa chọn bao gồm S3 hoặc Glacier
      * Chúng ta sẽ cần cài Snowball Client tại máy local để thực hiện xác minh, nén, mã hóa và transfer dữ liệu
     
    * **Snow Family - Snowball Edge**
      * Dịch vụ hỗ trợ migrate dữ liệu từ môi trường on-premise tới AWS ở quy mô lên đến PetaByte (PB). Mỗi Snowball Edge có thể chứa tới 100 TeraByte (TB)
      * Snowball Edge sẽ được ship trở về AWS region mà chúng ta lựa chọn để lưu trữ dữ liệu và lưu trong dịch vụ chúng ta lựa chọn bao gồm S3 hoặc Glacier
      * Chúng ta sẽ cần cài Snowball Client tại máy local để thực hiện xác minh, nén, mã hóa và transfer dữ liệu
      * Snowball Edge là thiết bị đặc biệt có sẵn các tài nguyên tính toán để xử lý dữ liệu local trước khi import vào thiết bị

    * **Snow Family - Snowmobile**
      * Dịch vụ hỗ trợ migrate dữ liệu từ môi trường on-premise tới AWS ở quy mô lên đến Exabyte. Mỗi Snowmobile có thể chứa tới 100 PB
      * Snowmobile sẽ trở về AWS region mà chúng ta lựa chọn để lưu trữ dữ liệu và lưu trong dịch vụ chúng ta lựa chọn bao gồm S3 hoặc Glacier

    * **AWS Storage Gateway**
      * AWS Storage Gateway là giải pháp lưu trữ Hybrid, kết hợp dung lượng lưu trữ trên AWS với dung lượng lưu trữ tại chỗ (on-premise)
      * Chúng ta có thể tận dụng quy mô và giá thành hợp lý của các dịch vụ lưu trữ trên cloud để giúp lưu trữ các dữ liệu lớn có thời gian yêu cầu lưu trữ lâu
      * AWS Storage Gateway hỗ trợ ba phương thức lưu trữ chính: tập tin, ổ đĩa và băng từ
        * Cổng kết nối tập tin (File Gateway): cho phép bạn lưu trữ và truy xuất đối tượng trong Amazon S3 bằng cách sử dụng các giao thức tập tin NFS và SMB. Đối tượng được ghi thông qua cổng kết nối tập tin có thể được truy cập trực tiếp trong S3
        * Cổng kết nối ổ đĩa (Volume Gateway): cung cấp lưu trữ dạng khối cho ứng dụng của bạn bằng cách sử dụng giao thức iSCSI. Dữ liệu trên ổ đĩa được lưu trữ trong Amazon S3. Để truy cập ổ đĩa iSCSI trong AWS, bạn có thể tạo EBS snapshot (tự động bằng AWS Backup) từ đó tạo ra thành EBS Volumes
        * Cổng kết nối băng từ (Tape Gateway): cung cấp cho ứng dụng sao lưu của bạn một giao diện thư viện băng từ ảo (VTL) iSCSI, các ổ tape drive ảo và tape ảo. Dữ liệu tape ảo được lưu trữ trong Amazon S3 hoặc có thể được lưu trữ vào Amazon Glacier
      * AWS Storage Gateway là giải pháp lưu trữ Hybrid, kết hợp dung lượng lưu trữ trên AWS với dung lượng lưu trữ tại chỗ ( on-premise )

    * **Disaster Recovery on AWS**
      * **RTO / RPO**
        * Thời gian phục hồi mục tiêu (Recovery Time Objective - RTO) là thời gian cần thiết để phục hồi một dịch vụ trở lại trạng thái hoạt động bình thường
          * Ví dụ: Nếu một thảm họa xảy ra lúc 2:00 giờ chiều và RTO là 4 giờ, quá trình DR phải phục hồi dịch vụ trễ nhất vào thời điểm 6:00 giờ tối
        * Thời điểm phục hồi mục tiêu (Recovery Point Objective - RPO) là khoảng thời gian tối đa mà dữ liệu có thể bị mất
          * Ví dụ: Nếu chúng ta thực hiện backup mỗi ngày 1 lần thì trong trường hợp xấu nhất chúng ta có thể mất dữ liệu 24 giờ, RPO = 24 hours

      * **Disaster Recovery on AWS**
        * Các dịch vụ, ứng dụng có độ phức tạp khác nhau và có mức cam kết dịch vụ (Service Level Agreement - SLA) trong đó bao gồm RTO/RPO khác nhau. Tùy theo loại dịch vụ và mức cam kết, chúng ta sẽ lựa chọn chiến lược phục hồi sau thảm họa tương ứng
        * Có 4 chiến lược phục hồi sau thảm họa trên AWS bao gồm:
          * Sao lưu và khôi phục
          * Pilot Light (Active – Standby)
          * Low Capacity Active - Active
          * Full Capacity Active - Active

      * **AWS Backup**
        * AWS Backup là một dịch vụ quản lý các tác vụ sao lưu. Chúng ta có thể cấu hình và lập lịch (backup schedule), chính sách sao lưu (backup retention) và giám sát hoạt động sao lưu cho các tài nguyên trên AWS bao gồm:
          * Amazon EBS
          * Amazon EC2
          * Cơ sở dữ liệu Amazon RDS
          * Cơ sở dữ liệu DynamoDB
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

## Thứ 4: Thiết lập Hybrid DNS với Route 53 Resolver
  * **Giới thiệu**
    * **Tổng quan**
      * Hầu hết doanh nghiệp đều có hệ thống DNS on-premise riêng
      * Khi di chuyển lên AWS, cần tích hợp DNS hai chiều giữa on-premise và AWS
      * Workshop sử dụng AWS Managed Microsoft AD để mô phỏng DNS on-premise

    * **Khả năng của Amazon Route 53**
      * Đăng ký miền công cộng
      * Tạo Private Hosted Zone
      * DNS Hybrid Resolution
      * Recursive DNS Resolver

    * **Ba công cụ chính của Route 53 Resolver**
      * **Outbound Endpoints**: Gửi truy vấn DNS từ AWS ra on-premise
      * **Inbound Endpoints**: Nhận truy vấn DNS từ on-premise vào AWS
      * **Resolver Rules**: Quy tắc forward DNS cho tên miền cụ thể

  * **Kết nối đến RDGW (Remote Desktop Gateway)**
    * **Mô tả**
      * Kết nối RDP vào máy chủ Remote Desktop Gateway để quản trị

    * **Các bước thực hiện chi tiết**
      * Truy cập EC2 Console → Chọn instance RDGW
      * Chọn Connect → RDP Client
      * Tải file Remote Desktop
      * Chọn Get Password → Upload key pair để decrypt password
      * Mở file RDP và đăng nhập bằng password vừa lấy
      * Xác nhận kết nối thành công

  * **Triển khai Microsoft AD**
    * **Mục tiêu**
      * Triển khai AWS Managed Microsoft Active Directory để mô phỏng DNS on-premise

    * **Các bước thực hiện**
      * Truy cập Directory Service Console
      * Chọn AWS Managed Microsoft AD → Create directory

      * **Directory Information**
          * Edition: Standard Edition
          * Directory DNS name: onprem.example.com
          * Directory NetBIOS name: onprem
          * Description: This is to simulate the on-prem AD
          * Admin Password: Nhập mật khẩu mạnh

      * **VPC and subnets**
          * Chọn VPC: Hybrid-DNS-VPCStack
          * Chọn hai Private Subnets

      * Tạo Directory (thời gian khoảng 20-40 phút)
      * Ghi lại hai DNS IP của Domain Controllers

  * **Thiết lập DNS**
    * **Tổng quan**
      * Sử dụng ba công cụ của Route 53 Resolver để thiết lập hybrid DNS hai chiều

    * **Kiến trúc tổng thể**
      * Mũi tên đỏ: Outbound Endpoint + Resolver Rule (AWS → On-prem)
      * Mũi tên xanh dương: Inbound Endpoint (On-prem → AWS)
      * Mũi tên xanh lá: EC2 sử dụng VPC DNS Resolver (VPC CIDR + 2)

    * **Tạo Route 53 Outbound Endpoint**
      * **Mô tả**
        * Tạo điểm cuối để Route 53 Resolver forward query ra ngoài on-premise

    * **Tạo Route 53 Resolver Rules**
      * **Mô tả**
        * Tạo rule forward truy vấn cho domain onprem.example.com đến DNS IP của Microsoft AD

    * **Tạo Route 53 Inbound Endpoints**
      * **Mô tả**
        * Tạo điểm cuối để on-premise forward query vào AWS

    * **Thử nghiệm kết quả**
      * **Mô tả**
        * Kiểm tra resolve tên miền hai chiều
        * Ping và truy vấn DNS giữa AWS và mô phỏng on-premise

  * **Dọn dẹp tài nguyên**
    * **Thứ tự xóa quan trọng (phải theo đúng thứ tự)**

      * **Xóa Inbound Endpoint**
        * Route 53 Console → Inbound endpoints → Delete

      * **Xóa Resolver Rule**
        * Disassociate VPC trước
        * Sau đó mới Delete rule

      * **Xóa Outbound Endpoint**
        * Route 53 Console → Outbound Endpoints → Delete

      * **Xóa AWS Managed Microsoft AD**
        * Directory Service → Delete directory

      * **Xóa CloudFormation Stack**
        * CloudFormation Console → Chọn stack HybridDNS → Delete
        * Stack sẽ xóa toàn bộ hạ tầng mạng (VPC, Subnets, RDGW...)