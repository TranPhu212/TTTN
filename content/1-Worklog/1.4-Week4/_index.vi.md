---
title: "Worklog Tuần 4"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
---

### Mục tiêu tuần 4:

* 

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
|  6  | - nội dung cần thay thế | 08/05/2026 | 08/05/2026 | <https://cloudjourney.awsstudygroup.com/> |
|  2  | - nội dung cần thay thế | 11/05/2026 | 11/05/2026 | <https://cloudjourney.awsstudygroup.com/> |
|  3  | - nội dung cần thay thế | 12/05/2026 | 12/05/2026 | <https://cloudjourney.awsstudygroup.com/> |
|  4  | - nội dung cần thay thế | 13/05/2026 | 13/08/2026 | <https://cloudjourney.awsstudygroup.com/> |
|  5  | - nội dung cần thay thế | 14/05/2026 | 14/05/2026 | <https://cloudjourney.awsstudygroup.com/> |


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

## Thứ 2: 
