---
title: "Worklog Tuần 7"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.7. </b> "
---

### Mục tiêu tuần 7:

* Tìm hiểu các dịch vụ cơ sở dữ liệu trên AWS và kiến thức nền tảng về hệ quản trị cơ sở dữ liệu
* Thực hành quản lý truy cập và phân quyền trên AWS bằng IAM User, IAM Role và Permission Boundary
* Nghiên cứu các giải pháp bảo mật dữ liệu trên AWS sử dụng Amazon S3, AWS KMS và CloudTrail
* Nâng cao hiểu biết về các cơ chế bảo mật, giám sát và kiểm soát quyền truy cập trong môi trường Cloud
* Hoàn thiện và mở rộng hệ thống SOC Dashboard với các module AI Threat Detection, Attack Surface, MITRE ATT&CK và Case Management

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
|  6  | - Tổng Quan về Cơ Sở Dữ Liệu và Các Dịch Vụ Cơ Sở Dữ Liệu AWS | 29/05/2026 | 29/05/2026 | <https://youtu.be/OOD2RwWuLRw> <br> <https://youtu.be/qbrobQZrokY> <br> <https://youtu.be/UvdiRW34aNI> |
|  2  | - Thực hành AWS IAM, EC2 Instance Role và các cơ chế kiểm soát truy cập bảo mật | 01/06/2026 | 01/06/2026 | <https://000048.awsstudygroup.com/> <br> <https://000044.awsstudygroup.com/> |
|  3  | - Thực hành quản lý quyền AWS IAM bằng Permission Boundary, IAM Role và Resource Tag | 02/06/2026 | 02/06/2026 | <https://000030.awsstudygroup.com/> <br> <https://000028.awsstudygroup.com/> |
|  4  | - Xây dựng giải pháp bảo vệ dữ liệu trên Amazon S3 bằng AWS KMS kết hợp giám sát nhật ký và tối ưu chi phí vận hành EC2 | 03/06/2026 | 03/06/2026 | <https://000033.awsstudygroup.com/> <br> <https://000022.awsstudygroup.com/> |
|  5  | - Mở rộng hệ thống Routing, cập nhật Sidebar Navigation và tích hợp các trang chuyên sâu (AI Threat Detection, Attack Surface, MITRE ATT&CK, Case Management) | 04/06/2026 | 04/06/2026 |


### Kết quả đạt được tuần 7:

## Thứ 6: Tổng Quan về Cơ Sở Dữ Liệu và Các Dịch Vụ Cơ Sở Dữ Liệu AWS
* **Database Concepts**
  * Database / Cơ sở dữ liệu là một hệ thống các thông tin có cấu trúc / bán cấu trúc, được lưu trữ trên các thiết bị lưu trữ nhằm thỏa mãn yêu cầu khai thác thông tin đồng thời của nhiều người sử dụng hay nhiều chương trình ứng dụng chạy cùng một lúc với những mục đích khác nhau
	* Session / Phiên là khoảng thời gian tính từ thời gian bắt đầu kết nối vào hệ thống CSDL (time start) và thời gian kết thúc (time end) là khoảng thời gian bạn ngắt kết nối
  * Primary Key / Khóa chính là một cột trong bảng cơ sở dữ liệu quan hệ đặc biệt (hoặc kết hợp các cột) được chỉ định để xác định duy nhất mỗi bản ghi trong bảng
  * Foreign Key / Khóa ngoại là một cột hoặc nhóm cột trong bảng cơ sở dữ liệu quan hệ cung cấp liên kết giữa dữ liệu trong hai bảng. Nó hoạt động như một tham chiếu chéo giữa các bảng vì nó tham chiếu đến khóa chính của một bảng khác, do đó thiết lập liên kết giữa chúng
  * Index / Chỉ mục cơ sở dữ liệu là một cấu trúc dữ liệu cải thiện tốc độ của các hoạt động truy xuất dữ liệu (read) trên bảng cơ sở dữ liệu tuy nhiên sẽ làm tăng chi phí ghi thêm (write) và không gian lưu trữ (storage) để duy trì cấu trúc dữ liệu chỉ mục
  * Các chỉ mục được sử dụng để định vị dữ liệu một cách nhanh chóng mà không cần phải tìm kiếm mọi hàng trong bảng cơ sở dữ liệu mỗi khi truy cập bảng cơ sở dữ liệu. Chỉ mục có thể được tạo bằng cách sử dụng một hoặc nhiều cột của bảng cơ sở dữ liệu
  * Partitions / Phân vùng là quá trình cơ sở dữ liệu trong đó các bảng rất lớn được chia ra và lưu trữ dưới dạng nhiều phần nhỏ hơn. Bằng cách tách một bảng lớn thành các bảng nhỏ hơn, riêng lẻ, các truy vấn chỉ truy cập một phần dữ liệu có thể chạy nhanh hơn vì có ít dữ liệu hơn để quét
  * Execution Plan - Query Plan / Kế hoạch thực thi truy vấn - Kế hoạch truy vấn là một chuỗi các bước được sử dụng để truy cập dữ liệu trong hệ quản trị cơ sở dữ liệu quan hệ SQL. ... Khi một truy vấn được gửi đến cơ sở dữ liệu, trình tối ưu hóa truy vấn sẽ đánh giá một số phương án có thể khác nhau, chính xác để thực hiện truy vấn và trả về những gì nó cho là tùy chọn tốt nhất
  * Database Log là một phần quan trọng trong thiết kế giải pháp cơ sở dữ liệu sẵn có của bạn vì nhật ký cơ sở dữ liệu giúp bạn có thể khôi phục sau khi bị lỗi và chúng giúp đồng bộ hóa cơ sở dữ liệu chính và phụ. Tất cả các cơ sở dữ liệu đều có hệ thống log được liên kết với chúng
  * Buffers / Bộ đệm là một vùng lưu trữ tạm thời trong bộ nhớ chính. Nó cho phép lưu trữ dữ liệu tạm thời khi di chuyển từ nơi này sang nơi khác. Bộ đệm cơ sở dữ liệu lưu trữ một bản sao của các khối đĩa. Thường được dùng để tăng tốc độ truy xuất ( đọc dữ liệu từ buffer ) cũng như tốc độ ghi (ghi dữ liệu vào buffer , sau đó buffer sync vào vùng lưu trữ CSDL)
  * RDBMS (SQL) Hệ quản trị cơ sở dữ liệu (DBMS) kết hợp mô hình dữ liệu-quan hệ, thường bao gồm giao diện lập trình ứng dụng Ngôn ngữ truy vấn có cấu trúc (SQL – Structured Query Language)
  * Cơ sở dữ liệu được tổ chức và truy cập theo mối quan hệ giữa các mục dữ liệu. Trong cơ sở dữ liệu quan hệ, mối quan hệ giữa các mục dữ liệu được thể hiện bằng các bảng. Sự phụ thuộc lẫn nhau giữa các bảng này được thể hiện bằng các giá trị dữ liệu
  * NOSQL Cơ sở dữ liệu NoSQL (hay còn gọi là "không chỉ SQL") thường không phải dạng bảng và lưu trữ dữ liệu khác với bảng quan hệ. Cơ sở dữ liệu NoSQL có nhiều loại dựa trên mô hình dữ liệu của chúng
  * Các loại chính là tài liệu (document), khóa-giá trị (key-value), wide-column và graph - biểu đồ. Chúng cung cấp các lược đồ linh hoạt và mở rộng quy mô dễ dàng với lượng lớn dữ liệu và tải lượng người dùng cao
  * OLTP – Online Transaction Processing - Hệ thống OLTP nắm bắt và duy trì dữ liệu giao dịch trong cơ sở dữ liệu. Mỗi giao dịch liên quan đến các bản ghi cơ sở dữ liệu riêng lẻ được tạo thành từ nhiều trường hoặc cột
  * Ví dụ bao gồm hoạt động ngân hàng và thẻ tín dụng hoặc quét thanh toán bán lẻ. Trong OLTP, trọng tâm là xử lý nhanh, vì cơ sở dữ liệu OLTP được đọc, ghi và cập nhật thường xuyên. Nếu một giao dịch không thành công, logic hệ thống tích hợp đảm bảo tính toàn vẹn của dữ liệu
  * OLAP – Online Analytical Processing - OLAP áp dụng các truy vấn phức tạp cho một lượng lớn dữ liệu lịch sử, được tổng hợp từ cơ sở dữ liệu OLTP và các nguồn khác, cho các dự án khai thác dữ liệu, phân tích và kinh doanh thông minh. Trong OLAP, trọng tâm là thời gian phản hồi cho các truy vấn phức tạp này. Mỗi truy vấn liên quan đến một hoặc nhiều cột dữ liệu được tổng hợp từ nhiều hàng
  * Ví dụ bao gồm hiệu suất tài chính hàng năm hoặc xu hướng tạo khách hàng tiềm năng tiếp thị. Cơ sở dữ liệu và kho dữ liệu (data warehouse) OLAP cung cấp cho các nhà phân tích khả năng sử dụng các công cụ báo cáo tùy chỉnh để biến dữ liệu thành thông tin

* **Amazon RDS & Aurora**
  * **Amazon RDS**
    * Là cơ sở dữ liệu được quản lý trên AWS, chúng ta chỉ truy cập và quản lý ở mức RDBMS, không thể truy cập và quản lý ở mức hệ điều hành. Bao gồm Aurora, MySQL, Postgres SQL, MSSQL, Oracle, Maria
    * Amazon RDS cung cấp các tính năng:
      * Tự động sao lưu. (cả log và database – max 35 ngày)
      * Tạo bản sao chỉ đọc (Read Replica) phục vụ cho các Read workload. (reporting)
      * Read Replica có thể được tách ra và chuyển thành một Primary node
      * Chạy với cơ chế tự động fail over , Primary / Standby , hay còn gọi là cơ chế Multi- AZ
      * RDS thường được sử dụng cho các ứng dụng OLTP
      * RDS cung cấp tính năng mã hóa dữ liệu at rest và in transit
      * RDS cũng được bảo vệ bởi tính năng tường lửa giống như EC2 (Security Group và NACL)
      * Thay đổi quy mô (Thay đổi instance size)
      * Tự động tăng dung lượng lưu trữ (Storage Auto scaling)
    * Cơ chế tự động fail over , Primary / Standby , hay còn gọi là cơ chế Multi- AZ

  * **Amazon RDS > Aurora**
    * Amazon Aurora là một công cụ cơ sở dữ liệu quan hệ được tối ưu lại hạ tầng lưu trữ bên dưới, cho hiệu năng đọc ghi song song cao. Nền tảng RDBMS có 2 lựa chọn là MySQL và PostgreSQL
    * Aurora cũng là một RDBMS thuộc Amazon RDS nên thừa hưởng các tính năng của RDS
    * Ngoài ra Amazon Aurora cung cấp các tính năng:
      * Back Track – Phục hồi lại DB về thời điểm trước đó
      * Clone – Tạo bản sao
      * Global Database – 1 Master và Multi Read nằm ở các Region khác nhau
      * Multi Master – Multi Master database

* **Amazon Redshift**
  * Amazon Redshift là dịch vụ Data warehouse được quản lý bởi AWS. Lõi là PostgreSQL nhưng được tối ưu cho OLAP
  * Redshift sử dụng kiến trúc Massively-Parallel Processing (MPP) Database, dữ liệu được chia (partition) và lưu trữ tại các Compute node (bao gồm cả compute / storage). Leader node nhận vai trò điều phối và tổng hợp truy vấn
  * Redshift lưu trữ dữ liệu dưới dạng columnular storage, phù hợp cho ứng dụng OLAP
  * Redshift sử dụng SQL và các driver JDBC, ODBC thông dụng
  * Hỗ trợ những tính năng để tối ưu hóa chi phí (Transient cluster, Redshift spectrum)

* **Amazon ElastiCache**
  * Amazon ElastiCache là một dịch vụ được quản lý bởi AWS giúp tạo ra các cluster caching engines. Hiện ElastiCache hỗ trợ 2 engine là Redis và Memcached
  * Amazon ElastiCache sẽ trách nhiệm phát hiện và thay thế các node bị failed
  * Amazon ElastiCache thường được đặt trước lớp CSDL để cache dữ liệu, giảm tải cho lớp CSDL
  * Với các workload và ứng dụng mới, ưu tiên sử dụng Redis. (tính năng đa dạng, hiệu năng tốt)
  * Sử dụng ElastiCache yêu cầu phải viết và quản lý caching logic trên ứng dụng

## Thứ 2: AWS IAM – Quản lý truy cập, IAM Role và Bảo mật phân quyền
* **Tổng quan**
  * Mục tiêu của bài học nhằm giúp người dùng:
    * Biết cách cấp quyền cho ứng dụng thông qua Access Key / Secret Access Key và hiểu lý do tại sao không nên sử dụng phương pháp này trong môi trường thực tế (vì lý do bảo mật)
    * Biết cách cấp quyền cho ứng dụng một cách an toàn thông qua IAM Role gắn trực tiếp trên EC2 instance

* **Nội dung chi tiết các bước thực hiện**
  * **Chuẩn bị tài nguyên**
    * Trước khi cấu hình quyền, bạn cần khởi tạo môi trường thử nghiệm bao gồm:
      * * Khởi tạo EC2 Instance: Tạo một máy chủ ảo EC2, đây sẽ là nơi ứng dụng của bạn chạy và cần quyền để thao tác với dịch vụ AWS khác
      * Khởi tạo S3 bucket: Tạo một kho lưu trữ Amazon S3, đây là dịch vụ đích mà ứng dụng trên EC2 cần truy cập để đọc/ghi dữ liệu

    * Sử dụng Access Key (Use access key) – Phương pháp không khuyến khích

    * Phần này minh họa cách làm truyền thống nhưng kém an toàn:
      * Tạo IAM User và Access Key: Người dùng tạo một tài khoản IAM user, cấp quyền truy cập S3 và xuất ra cặp mã mã hóa Access Key ID và Secret Access Key
      * Sử dụng Access Key: Cấu hình cặp key này trực tiếp vào trong EC2 để ứng dụng có thể gọi dữ liệu từ S3

  * **Sử dụng IAM Role trên EC2**
    * Đây là nội dung cốt lõi của bài workshop nhằm thay thế cho Bước 2:
      * Tạo IAM Role: Tạo một vai trò (IAM Role) có đính kèm chính sách (Policy) cho phép tương tác với S3 bucket
      * Sử dụng IAM Role: Gán (Attach) IAM Role vừa tạo vào EC2 instance. Sau khi gán, ứng dụng chạy trên EC2 tự động có quyền truy cập S3 một cách an toàn mà hoàn toàn không cần phải lưu trữ bất kỳ cặp Access Key / Secret Access Key nào trong mã nguồn hay máy chủ

  * **Dọn dẹp tài nguyên**
    * Hướng dẫn người học cách xóa bỏ các tài nguyên đã tạo (EC2, S3 bucket, IAM Role, IAM User) sau khi hoàn thành bài thực hành để tránh phát sinh chi phí ngoài ý muốn trên tài khoản AWS

* **Tạo EC2 Instance**
  * Làm theo bước 1.1.1 trong workshop giới thiệu về Amazon EC2 để tạo EC2 instance
    * Bạn hãy tạo một instance Amazon Linux với cấu hình t2.micro được miễn phí bởi free tier để dùng cho workshop này

  * Sử dụng putty để kết nối tới máy ảo bạn vừa tạo theo hướng dẫn ở bước 1.1.2
    * Tiếp theo chúng ta sẽ tạo một S3 bucket để cho ứng dụng trong máy chủ EC2 của chúng ta kết nối tới

* **Tạo S3 bucket**
  * Truy cập vào giao diện quản trị dịch vụ S3
    * Click Create bucket

  * Đặt tên s3 bucket của chúng ta là s3-instancerole-001 ( bạn có thể thêm số suffix phía sau ví dụ s3-instancerole-1000 vì tên s3 bucket phải đảm bảo không bị trùng)

  * Kéo màn hình xuống dưới, sau đó click Create bucket

  * Đảm bảo bucket được tạo thành công như hình dưới, trước khi qua các bước tiếp theo

* **Tạo IAM user và access key**
  * Truy cập vào giao diện quản trị dịch vụ IAM
    * Click Users
  * Click Add users
  * Đặt tên User name là iamaccesskey
    * Click chọn Programmatic access. ( Tùy chọn này cho phép sử dụng access key và secret access key cho AWS API , CLI , SDK )
    * Click Next: Permissions

  * Click chọn Attach existing policies directly
    * Tại ô Filter policies , điền S3
    * Click chọn AmazonS3FullAccess, chúng ta sẽ cấp quyền full access để truy cập và upload file lên S3 bucket chúng ta đã tạo ở bước trước
    * Click Next: Tags

  * Click Next: Review, sau đó click Create user

  * Sau khi tạo user thành công , click Show để hiển thị giá trị Secret access key
    * Bạn hãy lưu cặp giá trị Access key ID + Secret access key để phục vụ cho các bước sau của workshop
    * Bạn cũng có thể click Download .csv để down load Access key ID + Secret access key dưới dạng csv

  * Tiếp theo chúng ta sẽ dùng access key và secret access key đã tạo để upload 1 file lên S3 bucket

* **Sử dụng access key**
  * Quay lại giao diện của máy chủ EC2 chúng ta đã kết nối tới
    * Chạy câu lệnh sau để cài đặt AWS SDK cho Python
  * Sau khi quá trình cài đặt hoàn tất , chạy lệnh sau để tạo ra file test.txt để chúng ta thử nghiệm upload
  * Chạy lệnh sau để tạo file ứng dụng python
    * Lưu ý thay các giá trị , và phù hợp với giá trị của bạn
  * Thực hiện chạy ứng dụng python của chúng ta để upload file lên S3 bucket
  * Truy cập vào giao diện dịch vụ S3
    * Click S3 bucket s3-instancerole-001
    * Kiểm tra file đã được upload thành công lên S3 bucket

  * Khi chúng ta sử dụng access key thì chúng ta đang chạy ứng dụng với quyền quản trị full dịch vụ S3 được cấp cho IAM user iamaccesskey mà chúng ta đã tạo. Việc sử dụng access key như trên sẽ rất nguy hiểm vì dễ bị lộ thông tin access key khi chúng ta upload code lên những public repo như GitHub chẳng hạn. Việc đưa trực tiếp access key vào trong code không được khuyến khích vì dẫn tới các rủi ro trong việc bảo mật, ở phần tiếp theo thay vì sử dụng access key , chúng ta sẽ thử sử dụng IAM role nhé

* **Tạo IAM role**
  * Truy cập vào giao diện quản trị dịch vụ IAM
    * Click Roles
  * Click Create role
  * Tại mục **Choose a use case ** chúng ta click chọn EC2 để tạo một IAM role sử dụng cho ứng dụng chạy bên trong EC2
    * Click Next:Permissions
    * Tại ô Filter policies , điền S3
    * Click chọn AmazonS3FullAccess, chúng ta sẽ cấp quyền full access để truy cập và upload file lên S3 bucket chúng ta đã tạo
    * Click Next: Tags
  * Click Next: Review
  * Đặt Role name là ec2roles3upload
    * Click Create role

  * Tiếp theo chúng ta sẽ dùng role này để gán vào EC2 instance và giúp ứng dụng của chúng ta có thể upload file lên S3 mà không cần sử dụng access key và secret access key trong code

* **Sử dụng IAM role**
  * Truy cập vào giao diện quản trị EC2
    * Click chọn EC2 instance chúng ta đã tạo
    * Click Actions
    * Click Security
    * Click Modify IAM role
  * Click chọn role ec2roles3upload
    * Click Save
  * Quay trở lại giao diện dòng lệnh của EC2 instance
    * Chạy lệnh sau để tạo file ứng dụng python
    * Lưu ý thay giá trị phù hợp với giá trị của bạn
  * Thực hiện chạy ứng dụng python của chúng ta để upload file lên S3 bucket
  * Truy cập vào giao diện dịch vụ S3
    * Click S3 bucket s3-instancerole-001
    * Kiểm tra file đã được upload thành công lên S3 bucket

  * Chúng ta có thể kiểm tra thông tin xác thực bảo mật được tạo ra cho IAM role ec2roles3upload bằng câu lệnh sau . Chúng ta có thể thấy thông tin chứng thực có thời gian hết hạn ( Expiration ) và sẽ được tự động làm mới sau khoản thời gian hết hạn này
  * Chạy câu lệnh sau để liệt kê S3 bucket trong account

* **Dọn dẹp tài nguyên**
  * **Xoá S3 bucket**
    * Truy cập vào giao diện quản lý của dịch vụ S3
      * Click chọn S3 bucket s3-instancerole-001
      * Click Empty
    * Điền permanently delete để xác nhận, sau đó click Empty để xóa toàn bộ dữ liệu trong S3 bucket
      * Click Exit để trở lại giao diện S3
    * Click chọn S3 bucket s3-instancerole-001 , sau đó click Delete
    * Điền tên bucket sau đó click Delete bucket để xóa S3 bucket

  * **Xoá EC2 Instance**
    * Truy cập vào giao diện quản lý dịch vụ EC2
      * Click chọn Instance chúng ta tạo cho bài lab
      * Click Instance state
      * Click Terminate instance , sau đó click Terminate để xác nhận
    * Truy cập vào giao diện quản lý dịch vụ IAM
      * Click Users
      * Click chọn user iamaccesskey
      * Click Delete. Điền tên user iamaccesskey và click Delete
    * Click Roles
      * Điền ec2 để tìm role chúng ta đã tạo
      * Click chọn role ec2roles3upload
      * Click Delete. Điền tên role ec2roles3upload và click Delete để xóa IAM Role

* **Tổng quan**
  * Bài học tập trung vào nguyên tắc phân quyền tối thiểu (least privilege) trong AWS IAM, thay vì cấp toàn quyền Admin cho một User. Nội dung hướng dẫn cách tạo User/Group có quyền Admin giới hạn cho từng dịch vụ cụ thể (EC2 và RDS), sau đó cấu hình IAM Role kết hợp các điều kiện ràng buộc (Condition) về địa chỉ IP và thời gian để tăng cường bảo mật

* **Cấu trúc nội dung chi tiết**
  * Tài liệu được chia thành 5 phần chính:
    * Giới thiệu về IAM (Introduction about IAM):
      * Request to AWS service: Cách các yêu cầu gửi đến dịch vụ AWS được xử lý
      * Authenticate requests: Cơ chế xác thực thực thể
      * Assume Role Process: Quy trình một thực thể giả lập (assume) một IAM Role để lấy quyền hạn tạm thời
    * Tạo IAM Group (Create IAM Group): Hướng dẫn tạo nhóm người dùng để quản lý quyền tập trung
    * Tạo IAM User (Create IAM User):
      * Create IAM Users: Cấp tài khoản cho nhân sự
      * Check permissions: Kiểm tra và xác thực lại các quyền đã cấp để đảm bảo không bị thừa/thiếu quyền
    * Cấu hình Điều kiện cho Role (Configure Role Condition):
      * Create Admin IAM Role: Tạo một IAM Role có quyền Admin
      * Configure Switch role: Cấu hình để User có thể chuyển đổi (Switch) sang Role này khi cần
      * Restrict role access: Thêm các lớp bảo mật nâng cao bao gồm:
        * Limit switch role by IP: Chỉ cho phép chuyển đổi Role khi người dùng truy cập từ các dải IP được chỉ định (ví dụ: IP của công ty)
        * Limit switch role by Time: Giới hạn khung giờ thiết lập/sử dụng Role
    * Dọn dẹp tài nguyên (Clean up resources): Hướng dẫn xóa các User, Group, Role đã tạo sau khi hoàn thành bài thực hành để tránh phát sinh chi phí hoặc rủi ro bảo mật

* **Request tới AWS service**
  * Request: Khi một principal cố gắng thực hiện một thao tác sử dụng AWS Console, AWS API hoặc AWS CLI, principal đó sẽ phải gửi đi một request. Thông tin Request bao gồm
    * Action or Operation: hành động mà principal muốn thực hiện
    * Resource: thông tin tài nguyên sẽ bị tác động
    * Principal: thông tin về người hoặc ứng dụng gửi đi yêu cầu, bao gồm cả thông tin policy đã được attach với principal đó
    * Environment data: thông tin về địa chỉ IP, user agent, trạng thái enable SSL và thời điểm gửi request
    * Resource data: thông tin liên quan đến tài nguyên mà có thể đc request. Ví dụ tên của bảng dữ liệu DynamoDB, hay tên tag của máy ảo EC2

* **Chứng thực các request**
  * Authentication: Một principal phải có khả năng xác thực truy cập để có thể gửi request tới AWS
    * Với Root user: khi login cần thông tin địa chỉ email và password. (thông tin chứng thực dài hạn)
    * Với IAM user: cần thông tin account ID hoặc alias, và user + password tương ứng. (thông tin chứng thực dài hạn)
    * Để xác thực IAM user qua AWS API hay CLI, chúng ta có thể sử dụng Access key và Secret access key ( thông tin chứng thực dài hạn) hoặc sử dụng IAM Role và thông tin chứng thực tạm thời được cấp khi chúng ta thực hiện thao tác assume role thông qua dịch vụ AWS Security Token Service (AWS STS)

* **Quá trình assume role**
  * Trong phần này chúng ta sẽ cùng tìm hiểu quá trình một IAM User thực hiện assume role và lấy thông tin chứng thực tạm thời như thế nào nhé
  * IAM user sẽ có thông tin chứng thực dài hạn (password / acccesskey & secretaccesskey) và sẽ dùng thông tin chứng thực dài hạn đó để request tới AWS Security Token Service (AWS STS) và thực hiện action sts:AssumeRole
  * STS sẽ thực hiện kiểm tra xem IAM user có quyền để thực hiện action này hay không thông qua kiểm tra Trust Relationship (gán vào Role) và Identity Policy (gán vào IAM User)
  * Nếu quá trình STS kiểm tra thành công, STS sẽ trả về thông tin chứng thực tạm thời
  * IAM user sẽ sử dụng thông tin chứng thực tạm thời để thực hiện các request (API call) tới các dịch vụ của AWS.(IAM User ở thời điểm này sẽ có các quyền hạn được gán vào IAM role mà IAM User đã assume)

* **Tạo IAM Group**
  * Truy cập trang IAM console ở link https://console.aws.amazon.com/iam/home#/home
  * Tại thanh điều hướng bên trái, chọn User groups, sau đó bấm Create group
  * Tại trang Create user group, nhập các thông tin sau:
    * User group name: ec2-rds-admin-group
    * Cuốn xuống mục Attach permissions policies - Optional, tìm và chọn các policy AmazonEC2FullAccess, AmazonRDSFullAccess và DatabaseAdministrator
    * Kiểm tra và bấm Create group
    * Như vậy, bạn đã tạo thành công IAM Group

* **Tạo các IAM User**
  * Log in to the IAM console using the link: https://console.aws.amazon.com/iam/home#/home
  * In the left navigation pane, select Users, and then click Add User
  * On the Set user details page, enter the following information:
    * User name: EC2-admin-user
    * Access type: Check AWS Management Console access to allow user access to the AWS Management Console
    * Console password: Choose Custom password and set a password of your choice for the user
    * Require password reset: Uncheck this option to avoid the user changing their password on the first login
    * Review and click Next: Permissions
  * On the Set permissions page, perform the following steps:
    * Select Attach existing policies directly to assign permissions directly to the user
    * In the search box next to Filter Policies, search for and select AmazonEC2FullAccess
    * Review and click Next: Tags
  * On the Add tags (optional) page, leave the defaults and click Next: Review
  * On the Review page, review the information and click Create user
  * Once the user creation process is complete, click Close to return to the IAM Console

  * You have successfully created the user. To create other users, follow the same procedure with different settings for Step 3 and 4:
    * RDS-admin-user:
      * Step 3: On the Set user details page, enter the following information:
        * User name: RDS-admin-user
      * Step 4: On the Set permissions page, do the following:
        * Select Attach existing policies directly
        * Choose AmazonRDSFullAccess and DatabaseAdministrator
    * Group-user:
      * Step 3: On the Set user details page, enter the following information:
        * User name: Group-user
      * Step 4: On the Set permissions page, do the following:
        * Select Add user to group
        * Check the group ec2-rds-admin-group
    * No-permission-user:
      * Step 3: On the Set user details page, enter the following information:
        * User name: No-permission-user
      * Step 4: Skip the permissions and click Next: Tags

* **Kiểm tra quyền**
  * Đăng nhập vào IAM console theo link https://console.aws.amazon.com/iam/home#/home
  * Ở thanh điều hướng bên trái, chọn User
  * Chọn vào EC2-admin-user
  * Chọn vào tab Security credentials, copy đường link để đăng nhập cho user ở bên cạnh Summary
  * Mở một tab broswer ở chế độ ẩn danh hoặc mở một broswer khác với broswer bạn đang sử dụng. Sau đó, truy cập vào đường link vừa copy ở trên
  * Sử dụng username và password cho user EC2-admin-user để đăng nhập
  * Lặp lại bước 1-6 để lần lượt đăng nhập vào các user khác
  * Sau khi đăng nhập thành công, bạn sẽ làm các bài kiểm tra sau để chắc chắn các user đã được cấu hình chính xác:
    * EC2-admin-user: khởi chạy thành công một EC2 instance
    * RDS-admin-user: khởi chạy thành công một RDS instance
    * Group-user: khởi chạy thành công một EC2 instance và một RDS instance
    * No-permission-user: không sử dụng được bất kỳ dịch vụ nào

* **Tạo Admin IAM Role**
  * Đăng nhập vào IAM console theo link https://console.aws.amazon.com/iam/home#/home
  * Tại thanh điều hướng bên trái, chọn Roles, sau đó bấm Create role
  * Ở mục Select type of trusted entity, chọn AWS Service. Ở mục Choose a use case, chọn EC2. Sau đó, chọn Next: Permissions
  * Tại mục Attach permissions policies, tìm và chọn AdministratorAccess. Sau đó, chọn Next: Tags
  * Bỏ qua bước gán tag và bấm Next: Review
  * Tại trang Review, nhập tên của Role là lab44-RoleFullAccess. Sau đó, bấm Create role để kết thúc quá trình tạo Role

* **Cấu hình Switch role**
  * Truy cập trang IAM console ở link https://console.aws.amazon.com/iam/home#/home
  * Ở thanh điều hướng bên trái, chọn Users
  * Bấm vào user No-permission-user, sao chép thông tin User ARN
  * Tại thanh điều hướng bên trái, bấm chọn Roles, rồi chọn IAM Role mới tạo lab44-RoleFullAccess
  * Chọn tab Trust relationships và chọn Edit trust relationship
  * Bổ sung AWS với thông tin là User ARN của user No-permission-user như hình bên dưới. Sau đó bấm Update Trust Policy
  * Như vậy, user No-permission-user đã có thể sử dụng role lab44-RoleFullAccess. Để kiểm tra assume role, ta thao tác như sau:
    * Thực hiện log in user No-permission-user, sau đó bấm vào tên của user ở góc phải màn hình, chọn Switch Role
    * Tại màn hình Switch Role, nhập các thông tin theo yêu cầu
    * Bấm Switch role để thực hiện assume role cho user No-permission-user
    * Thực hiện truy cập các dịch vụ cơ bản như EC2 hoặc RDS để xác nhận cấu hình Switch role thành công. Với quyền truy cập AdministratorAccess, user No-permission-user giờ đây có thể sử dụng bất kỳ dịch vụ nào

* **Giới hạn truy cập theo IP**
  * Truy cập trang IAM console ở link https://console.aws.amazon.com/iam/home#/home với quyền user Admin
  * Tại thanh điều hướng bên trái, bấm chọn Roles, rồi chọn IAM Role mới tạo lab44-RoleFullAccess
  * Ở tab Trust relationships, bấm Edit trust relationship, bổ sung Condition như bên dưới, sau đó bấm Update Trust Policy
  * Sau khi cập nhật trust policy, phần Condition được bổ sung thông tin IP được phép thực hiện switch role
  * Trở lại phiên log in của user No-permission-user, thực hiện lại việc switch role ta sẽ nhận được thông báo lỗi như hình bên dưới do ta đang truy cập dịch vụ từ thiết bị không có IP như trong điều kiện

* **Giới hạn theo thời gian**
  * Truy cập trang IAM console ở link https://console.aws.amazon.com/iam/home#/home với quyền user Admin
  * Tại thanh điều hướng bên trái, bấm chọn Roles, rồi chọn IAM Role mới tạo lab44-RoleFullAccess
  * Ở tab Trust relationships, bấm Edit trust relationship, bổ sung Condition như bên dưới, sau đó bấm Update Trust Policy
  * Sau khi cập nhật trust policy, phần Condition được bổ sung thông tin Date time được phép thực hiện switch role
  * Trở lại phiên log in của user No-permission-user, thực hiện lại việc switch role ta sẽ nhận được thông báo lỗi như hình bên dưới do thời điểm mà ta thực hiện Switch đã ngoài khoảng thời gian cho phép

* **Dọn dẹp tài nguyên**
  * Xóa role lab44-RoleFullAccess
    * Truy cập vào IAM Console
    * ở thanh bên trái, chọn Roles
    * Tìm và tick vào role lab44-RoleFullAccess
    * Chọn Delete

  * Xóa IAM user bao gồm EC2-admin-user, RDS-admin-user, Group-user, và No-permission-user
    * Truy cập vào IAM Console
    * ở thanh bên trái, chọn Users
    * Tick vào các user liên quan tới bài lab
    * Chọn Delete user

  * Xóa User Group ec2-rds-admin-group
  * Truy cập vào IAM Console
  * ở thanh bên trái, chọn User groups
  * Tick vào user group liên quan tới bài lab
  * Chọn Delete

## Thứ 3: Quản lý quyền IAM với Permission Boundary và Resource Tag
* **Tổng quan & Khái niệm**
  * IAM Permission Boundary là gì? Là một tính năng nâng cao trong AWS IAM giúp thiết lập số quyền hạn tối đa (maximum permissions) mà một IAM User hoặc Role có thể đạt được. Ngay cả khi người dùng đó được gán một chính sách (Policy) có quyền cao hơn, họ cũng không thể vượt qua ranh giới được định sẵn bởi Permission Boundary. Quyền hạn thực tế của người dùng sẽ là phần giao (độ giao thoa) giữa Identity-based policy và Permission Boundary
  * Tại sao cần sử dụng? Khi số lượng người dùng tăng lên, việc quản lý các chính sách riêng lẻ trở nên phức tạp, dễ dẫn đến lỗ hổng leo thang đặc quyền (privilege escalation). Sử dụng Permission Boundary giúp đơn giản hóa việc quản lý và ngăn chặn lỗ hổng này một cách nhanh chóng và đồng loạt

* **Cấu trúc bài Lab**
  * Bài workshop được thiết kế theo lộ trình gồm 6 bước thực hiện:
    * Introduction (Giới thiệu): Đặt vấn đề và lý thuyết cốt lõi về Permission Boundary
    * Preparation (Các bước chuẩn bị): Khởi tạo môi trường cần thiết để làm lab
    * Create Restriction Policy (Tạo chính sách hạn chế): Hướng dẫn cấu hình chính sách định hình ranh giới quyền lực
    * Create IAM Limited User (Tạo người dùng IAM bị giới hạn): Tạo một tài khoản IAM User mới và áp dụng Permission Boundary vừa tạo
    * Test IAM User Limits (Kiểm tra giới hạn người dùng): Thực hiện kiểm tra thực tế để chứng minh tài khoản không thể làm các hành động vượt quá ranh giới, dù có được cấp quyền cao
    * Clean up resources (Dọn dẹp tài nguyên): Hướng dẫn xóa các tài nguyên đã tạo sau khi hoàn thành lab để tránh phát sinh chi phí AWS

* **Giới thiệu**
  * **IAM Permission Boundary là gì?**
    * IAM Permission Boundary là một tính năng cao cấp cho phép chúng ta giới hạn quyền tối đa với một User hoặc Group. Giả sử chúng ta áp dụng Permission Boundary chỉ cho phép user EC2admin quản trị dịch vụ EC2 thì anh ấy sẽ không thể có quyền trên một dịch vụ nào khác kể cả có được gán một Policy cấp quyền cao hơn
    * Do đó, quyền hạn có hiệu lực (effective permissions) của user EC2admin sẽ bao gồm những quyền được cho phép bởi cả Permission Boundary và chính sách quyền của user EC2admin (Identity-based policy)

  * **Tại sao sử dụng IAM Permission Boundary?**
    * Thông thường, khi bạn trao quyền cho các IAM user, bạn nghĩ rằng chỉ cần xây dựng chính sách quyền cho user một cách cẩn thận, bạn sẽ có thể bỏ qua bước sử dụng Permission Boundary
    * Tuy nhiên, khi số lượng user tăng lên và những thay đổi liên tục trong vai trò công việc của các user yêu cầu bạn phải tạo ra thêm nhiều chính sách quyền mới, thì việc quản lý quyền trở nên phức tạp, từ đó tạo những lỗ hổng cho leo thang đặc quyền (privilege escalation) trong các user
    * Để đơn giản hóa công tác quản lý quyền, thay vì bạn phải chỉnh sửa từng chính sách quyền, bạn có thể áp dụng Permission Boundary một cách nhanh chóng và đồng loạt để giúp bạn đóng những lỗ hổng về privilege escalation

* **Tạo Policy Giới hạn**
  * Đăng nhập vào IAM Management Console
  * Tại thanh bên trái, chọn Policies và chọn Create Policy
  * Trong trang Create policy, chọn vào tab JSON và copy đoạn JSON bên dưới vào khung. Đoạn JSON có ý nghĩa rằng mọi hành động đối với tất cả dịch vụ EC2 từ mọi tài nguyên đều được cho phép với điều kiện rằng dịch vụ EC2 đó phải ở region ap-southeast-1 (Singapore)
    * Kiểm tra và chọn Next: Tags
  * Bỏ qua bước gán tag và chọn Next: Review
  * Đặt tên policy là ec2-admin-restrict-region. (Vì chúng ta đang chỉ cho phép User EC2 Admin chỉ được quyền thao tác trên Region Singapore ap-southeast-1.) Sau đó, chọn Create Policy
  * Như vậy chúng ta đã hoàn thành việc tạo policy để sử dụng nhằm giới hạn quyền tối đa mà một IAM user có thể có. Ở bước tiếp theo chúng ta sẽ áp đặt policy chúng ta vừa tạo ở bước này

* **Tạo IAM User giới hạn**
  * Đăng nhập vào IAM Management Console
  * Tại thanh bên trái chọn Users rồi chọn Add user
  * Tại trang Set user details, nhập những thông số sau rồi chọn Next Permissions:
    * User name: ec2-admin
    * Access type: Chọn AWS Management Console access để cho phép user login vào AWS Management Console
    * Chọn Custom Password và đặt password tùy ý bạn
    * Bỏ chọn “User must create a new password at next sign-in”
  * Tại mục Set permissions, bạn cần làm những thao tác sau:
    * Chọn Attach existing policies directly để gán policy trực tiếp vào IAM user
    * Tìm và tick vào AmazonEC2FullAccess để gán quyền quản trị EC2 cho IAM user
  * Sau đó, mở rộng mục Set permissions boundary:
    * Chọn Use a permissions boundary to control the maximum user permissions
    * Ở ô Search, gõ “ec2-admin-restrict-region” để tìm và chọn policy giới hạn chúng ta đã tạo
    * Kiểm tra và chọn Next: Tags
  * Tại trang Add tags (optional), giữ mặc định và chọn Next-Review
  * Tại trang Review, kiểm tra kỹ và chọn Create user
  * Như vậy, user đã được tạo thành công, ở bước tiếp theo chúng ta sẽ login bằng user ec2-admin vừa tạo để kiểm tra xem user đó có thể tạo ra các EC2 instance ở Region khác với Region chúng ta đã giới hạn hay không
  * Chúng ta sẽ sử dụng IAM user này cho bước tiếp theo

* **Kiểm tra IAM User Giới Hạn**
  * Ở thanh bên trái, chọn Users và chọn vào user ec2-admin mà bạn vừa tạo
  * Chọn tab Security credentials, copy link login vào IAM user ở Summary, và khởi chạy link ấy ở trong browser của bạn với chế độ ấn danh hoặc sử dụng một broswer khác
  * Tại trang Sign in as IAM user, nhập các thông tin sau để đăng nhập vào user ec2-admin:
    * IAM User name: ec2-admin
    * Password: password mà bạn chọn
    * Click Sign in
  * Nhắc nhở: Permission Boundary ec2-admin-restrict-region mà bạn đã tạo chỉ cho phép user truy cập vào dịch vụ EC2 khi đang ở region ap-southeast-1 (Singapore)
  * Tại AWS Management Console của user ec2-admin, chọn region ap-southeast-1 (Singapore) và truy cập vào dịch vụ EC2 bằng thanh tìm kiếm. Bạn sẽ thấy dịch vụ EC2 sẽ hoạt động bình thường
  * Thay đổi Region ở góc trên tay phải sang ap-southeast-2 (Sydney), bạn có thể thấy, dù được cấp quyền quản trị dịch vụ EC2 ở mức cao nhất, nhưng do chúng ta đã áp giới hạn quyền chỉ cho phép quản trị EC2 trên Region Singapore, nên IAM user chúng ta tạo ra sẽ không có quyền gì về EC2 trên Region Sydney

* **Dọn dẹp tài nguyên**
  * **Xóa user ec2-admin**
    * Quay lại user chính của bạn
    * Truy cập vào IAM Management Console
    * Ở thanh bên trái, chọn Users
    * Tick vào user liên quan tới bài lab
    * Chọn Delete user
    * Tick vào box trong pop-up và chọn Yes, delete|

  * **Xóa IAM Policy**
    * Truy cập vào IAM Management Console
    * Ở thanh bên trái, chọn Policies
    * Ở thanh tìm kiếm trong trang Policies, tìm ec2-admin-restrict-region
    * Tick vào policy và chọn Actions
    * Chọn Delete
    * Trong pop-up, nhập tên của policy vào ô trống và chọn Delete

* **Tổng quan**
  * Bài thực hành này sẽ đưa chúng ta qua quá trình quản lý quyền truy cập dịch vụ EC2 với Resource Tag thông qua cấu hình chi tiết của các chính sách và IAM role với quyền cụ thể. Việc sử dụng Resource Tag sẽ cực kỳ hữu ích khi chúng ta mở rộng trong việc quản trị phi tập trung
  * Trong bài thực hành này, chúng ta sẽ tạo các chính sách với các role có thể được sử dụng bởi một số người dùng nhất định, chẳng hạn như Quản trị viên EC2. Các chính sách (policy) này sẽ chỉ cho phép Quản trị viên EC2 tạo các tài nguyên liên quan khi nó đáp ứng các yêu cầu đã nêu và dựa trên một số Resource Tag nhất định

* **Mục tiêu**
  * Áp dụng phương pháp đặc quyền IAM tối thiểu
  * Đặc tả chính sách IAM kèm theo các điều kiện chi tiết (Điều kiện chính sách IAM)

* **Tạo IAM user**
  * **Tạo Admin Group**
    * Đăng nhập vào Bảng điều khiển ở trang AWS Web Service page
    * Nhấn vào tên tài khoản ở góc trên bên phải và chọn Security Credentials
    * Ở thanh bên trái, chọn User Groups sau đó chọn Create Group
    * Dưới mục Name the group, nhập tên Group (Ví dụ: AdminGroup) và cuộn chuột xuống dưới
    * Ở phần Attach permissions policies, gõ AdministratorAccess vào thanh tìm kiếm và nhấn enter. Từ danh sách hiện ra, bạn chọn AdministratorAccesss. Cuối cùng, chọn Create Group
    * Hoàn thành tạo admin group

  * **Tạo Admin User**
    * Ở thanh bên trái, chọn Users sau đó chọn Add User

    * Trên trang Specify user details, dưới phần User details, trong ô User name, nhập tên cho người dùng mới. Đây là tên đăng nhập cho AWS của họ. Ví dụ: AdminUser
      * Chọn Provide user access to the – AWS Management Console (tuỳ chọn) này tạo ra thông tin đăng nhập AWS Management Console cho người dùng mới
      * Bạn được hỏi liệu bạn có cung cấp quyền truy cập vào bảng điều khiển cho một người không. Chúng tôi khuyến nghị bạn tạo người dùng trong IAM Identity Center thay vì IAM
      * Để chuyển sang việc tạo người dùng trong IAM Identity Center, chọn Specify a user in Identity Center
      * Nếu bạn chưa bật IAM Identity Center, việc chọn tùy chọn này sẽ đưa bạn đến trang dịch vụ trong bảng điều khiển để bạn có thể bật dịch vụ này. Để biết chi tiết về quy trình này, xem https://docs.aws.amazon.com/singlesignon/latest/userguide/getting-started.html trong Hướng dẫn người dùng AWS IAM Identity Center (kế thừa từ AWS Single Sign-On)
      * Nếu bạn đã bật IAM Identity Center, việc chọn tùy chọn này sẽ đưa bạn đến trang “Chỉ định chi tiết người dùng” trong IAM Identity Center. Để biết chi tiết về quy trình này, xem https://docs.aws.amazon.com/singlesignon/latest/userguide/addusers.html trong Hướng dẫn người dùng AWS IAM Identity Center (kế thừa từ AWS Single Sign-On)
      * Nếu bạn không thể sử dụng IAM Identity Center, chọn I want to create an IAM user

    * Đối với Console password, hãy chọn một trong các lựa chọn sau:
      * Autogenerated password - Người dùng sẽ nhận được một mật khẩu được tạo ngẫu nhiên và đáp ứng chính sách mật khẩu tài khoản. Bạn có thể xem hoặc tải xuống mật khẩu khi bạn đến trang Lấy mật khẩu
      * Custom password - Người dùng sẽ được gán mật khẩu mà bạn nhập vào ô
      * (Tùy chọn) Users must create a new password at next sign-in (recommended) được chọn mặc định để đảm bảo người dùng bị buộc phải thay đổi mật khẩu lần đầu tiên khi đăng nhập
      * Chọn Next

    * Trên trang Set permissions, xác định cách bạn muốn gán quyền cho người dùng này. Chọn một trong ba tùy chọn sau:
      * Chọn Add user to group - Chọn tùy chọn này nếu bạn muốn gán người dùng vào một hoặc nhiều nhóm đã có các chính sách quyền. IAM hiển thị danh sách các nhóm trong tài khoản của bạn, cùng với các chính sách đã được gắn kết. Bạn có thể chọn một hoặc nhiều nhóm hiện có hoặc chọn Tạo nhóm để tạo một nhóm mới. Để biết thêm thông tin, xem Hướng dẫn thay đổi quyền cho một người dùng IAM
      * Copy permissions - Chọn tùy chọn này để sao chép tất cả các thành viên của nhóm, chính sách quản lý đã gắn kết, chính sách nội tuyến nhúng và bất kỳ ranh giới quyền hiện có nào từ người dùng hiện tại sang người dùng mới. IAM hiển thị danh sách các người dùng trong tài khoản của bạn. Chọn người dùng có quyền phù hợp nhất với nhu cầu của người dùng mới của bạn
      * Attach policies directly - Chọn tùy chọn này để xem danh sách các chính sách do AWS quản lý và chính sách do khách hàng quản lý trong tài khoản của bạn. Chọn các chính sách mà bạn muốn gắn vào người dùng hoặc chọn Tạo chính sách để mở một tab trình duyệt mới và tạo chính sách mới. Để biết thêm thông tin, xem bước 4 trong thủ tục Tạo chính sách IAM. Sau khi tạo chính sách, đóng tab đó và quay lại tab ban đầu để thêm chính sách vào người dùng
      
    * (Tùy chọn) Trên Review and create, dưới mục Tags, chọn Add new tag để thêm dữ liệu về người dùng bằng cách gắn thẻ dưới dạng cặp khóa-giá trị
      * Xem xét tất cả các lựa chọn mà bạn đã chọn đến thời điểm này. Khi bạn sẵn sàng tiếp tục, chọn Create user

    * Trên trang Lấy lại mật khẩu, lấy mật khẩu đã được chỉ định cho người dùng:
      * Chọn Show bên cạnh mật khẩu để xem mật khẩu của người dùng, từ đó bạn có thể ghi lại mật khẩu theo cách thủ công
      * Chọn Download.csv để tải xuống thông tin đăng nhập của người dùng dưới dạng tệp .csv mà bạn có thể lưu vào một vị trí an toàn

    * Kiểm tra User tạo thành công

    * Kiểm tra group của user

    * Sao chép console-sigin link

* **Tạo IAM Policy**
  * **Các bước tạo IAM Policy**
    * Đăng nhập vào AWS Management Console và truy cập đến IAM Management Console
    * Ở thanh điều hướng bên tay trái, chọn Policies và nhấn nút Create policy
    * Ở màn hình tạo mới, chúng ta chọn JSON và điền đặc tả chính sách của mình vào
      * Trong ví dụ này, chúng ta sử dụng chính sách ec2-list-read
      * Chọn Next: Tags
    * Để cấu hình mặc định. Chọn Next: Review để tiến hành kiểm tra
    * Điền tên cùng với miêu tả cụ thể
      * Name: ec2-list-read
      * Description: ec2-list-read
      * Tiến hành tạo bằng cách nhấn Create Policy
    * Tạo Policy thành công

* **Chính sách - ec2-create-tags**
  * Ở thanh điều hướng bên tay trái, chọn Policies và nhấn nút Create policy
  * Ở màn hình tạo mới, chúng ta chọn JSON và điền đặc tả chính sách của mình vào. Trong ví dụ này, chúng ta sử dụng chính sách ec2-create-tags
  * Chọn Next: Tags
  * Để cấu hình mặc định. Chọn Next: Review để tiến hành kiểm tra
  * Thông tin:
    * Name: ec2-create-tags
    * Description: ec2-create-tags
    * Mô tả: Chính sách này sẽ cho phép tạo ra các thẻ dành cho dịch vụ EC2, kèm với điều kiện thực thi là khi chúng ta tiến hành tạo một EC2 instance
    * Tiến hành tạo bằng cách nhấn Create Policy
  * Tạo Policy thành công

* **Chính sách - ec2-create-tags-existing**
  * Thông tin:
    * Name: ec2-create-tags-existing
    * Description: ec2-create-tags-existing
    * Mô tả: Chính sách này cho phép user gán thẻ cho các tài nguyên thuộc dịch vụ EC2 khi thỏa cả ba điều kiện:
      * Thẻ được gán trên tài nguyên EC2 là cặp giá trị “Key=Team,Value=Alpha”
      * Tag key được gán của tài nguyên EC2 bao gồm Team và Name
      * Thẻ được yêu cầu gán phải là cặp giá trị “Key=Team,Value=Alpha”

* **Chính sách - ec2-run-instances**
  * Thông tin:
    * Name: ec2-run-instances
    * Description: ec2-run-instances
    * Mô tả: Chính sách này sẽ được chia làm 2 phần:
    * Phần đầu tiên: Cho phép tạo ra EC2 instance khi và chỉ khi các điều kiện về AWS Regions và Resource Tags được thoả mãn
    * Phần còn lại: Cho phép tạo ra các tài nguyên liên quan tại thời điểm chúng ta tiến hành tạo EC2 instance, kèm với điều kiện về AWS Regions

* **Chính sách - ec2-manage-instances**
  * Thông tin:
    * Name: ec2-manage-instances
    * Description: ec2-manage-instances
    * Mô tả: Chính sách này cho phép thực hiện những thao tác cơ bản (reboot, terminate, start, stop) đối với EC2 instances, kèm với điều kiện AWS Regions và Resource Tags phải được thoả mãn
  * Sau khi hoàn tất, bạn sẽ có 5 EC2 policies

* **Tạo IAM Role**
  * Đăng nhập vào AWS Management Console và truy cập đến IAM Management Console
  * Ở thanh điều hướng bên tay trái, chọn Role và nhấn nút Create role
  * Ở màn hình tạo mới, chúng ta chọn Another AWS account và điền account ID của mình vào (bạn có thể tìm Account ID ở phần My Account), bên cạnh đó Require MFA như là một sự lựa chọn bắt buộc (best practice)
  * Ở khu vực Attach permissions policies, chúng ta sẽ lần lượt chọn các chính sách dưới đây:
    * ec2-list-read
    * ec2-create-tags
    * ec2-create-tags-existing
    * ec2-run-instances
    * ec2-manage-instances
  * Chọn Next: Tags
  * Để cấu hình tự động. Chọn Next: Review để tiến hành xem xét
    * Điền tên (ví dụ: ec2-admin-team-alpha) cùng với miêu tả cụ thể
  * Tiến hành tạo bằng cách nhấn Create role
  * Sau khi tạo thành công, trong danh sách các IAM roles, chúng ta chọn ec2-admin-team-alpha và cần lưu lại 2 thứ:
    * Role ARN
    * Switch Role URL
  * Sử dụng ARN IAM user để cấu hình Trust relationships
  * Thực hiện chỉnh sửa trust policy
  * Hoàn thành cập nhật

* **Chuyển Role**
  * Đăng nhập vào AWS Management Console
    * Chọn Users
    * Chọn Admin user đã tạo
    * Chọn Add user
  * Chọn Security credentials
    * Sao chép đường dẫn đăng nhập
  * Sử dụng đường dẫn đăng nhập với tab trình duyệt mới
    * Nhập thông tin về Account ID và user name - password
    * Sau đó, chọn Sign in
  * Hoàn thành đăng nhập
  * Sau khi đăng nhập thành công, nhấn vào Username hiển thị ở góc trên bên phải, Console sẽ hiển thị tương ứng như sau @<ACCOUNT_ID_NUMBER_or_ACCOUNT_ID_ALIAS>, sau đó tiến hành nhấn nút Switch Role. Một cách khác, chúng ta có thể copy/paste đường dẫn mà đã lưu lại
  * Chọn Switch Role
  * Ở trang Switch Role, chúng ta sẽ nhập như sau:
    * Ở ô Account: <ACCOUNT_ID_NUMBER>
    * Ở ô Role: ec2-admin-team-alpha
    * Ở ô Display Name (Optional): Tuỳ ý nhập tên gợi nhớ cho các lần sử dụng kế tiếp
    * Tiến hành nhấn nút Switch Role, đối với lần đầu tiên sẽ có một số thông tin thêm
  * Trình duyệt Web của chúng ta sẽ được điều hướng sang một trang mới

* **Tiến hành truy cập EC2 console ở AWS Region - Tokyo**
  * Đăng nhập vào AWS EC2 Console và truy cập dịch vụ EC2 ở ap-northeast-1 (Tokyo) theo đường dẫn - https://ap-northeast-1.console.aws.amazon.com/ec2/v2/home?region=ap-northeast-1
  * Khi truy cập vào Dashboard, chúng ta sẽ nhận thấy một loạt các lỗi chứa cụm sau API Error
    * Như vậy bài kiểm tra đầu tiên đã được thông qua bởi ap-northeast-1 không nằm trong AWS Regions được cho phép

* **Tiến hành truy cập EC2 console ở AWS Region - North Virginia**
  * Đăng nhập vào AWS EC2 Console và truy cập dịch vụ EC2 ở us-east-1 (North Virginia) theo đường dẫn - https://us-east-2.console.aws.amazon.com/ec2/v2/home?region=us-east-1
  * Khi truy cập vào Dashboard, chúng ta sẽ chỉ nhận thấy một lỗi chứa cụm sau API Error ở phần Load Balancing
    * Như vậy bài kiểm tra đầu tiên đã được thông qua bởi us-east-1 nằm trong AWS Regions được cho phép

* **Tiến hành tạo EC2 instance khi không có và có Tags thỏa điều kiện**
  * Trong bước này , chúng ta sẽ tạo EC2 mà không đáp ứng yêu cầu về tag theo policy(chính sách) ec2-create-tags-existing đã tạo. Điều này sẽ khiến việc tạo instance bị fail. Sau đó chúng ta sẽ sửa lại tag theo đúng yêu cầu và tạo instance thành công
    * Đăng nhập vào AWS EC2 Console và truy cập dịch vụ EC2 ở us-east-1 (North Virginia) theo đường dẫn - https://us-east-2.console.aws.amazon.com/ec2/v2/home?region=us-east-1
    * Ở thanh điều hướng bên tay trái, chọn Instances và nhấn nút Launch instances
  * Thử sử dụng SAI Resource Tag để kiểm tra:
    * Key = Name và Value = Example
    * Key = Team và Value = Beta
  * Sử dụng cấu hình mặc định t2.micro. Chọn Keypair
  * Tiến hành cấu hình Network
    * Sau khi cấu hình xong, kiểm tra lại và chọn Launch instance
  * Ở trang Launch Status, chúng ta sẽ nhận được lỗi là Launch Failed
    * Như vậy bài kiểm tra thứ 3 đã được thông qua
  * Bây giờ, chúng ta sẽ thử sử dụng ĐÚNG Resource Tag để kiểm tra
    * Chọn Back to Review Screen
    * Chúng ta thực hiển sửa tag đúng
    * Key = Name và Value = Example
    * Key = Team và Value = Alpha
    * Chọn Launch instance
  * Và lần này chúng ta khởi tạo thành công

* **Chỉnh sửa Resource Tag trên EC2 Instance**
  * Trong bước này , chúng ta sẽ cố ý thay đổi tag của EC2 Instance đã tạo ở bước trước
    * Đăng nhập vào AWS EC2 Console và truy cập dịch vụ EC2 ở us-east-1 (North Virginia) theo đường dẫn - https://us-east-2.console.aws.amazon.com/ec2/v2/home?region=us-east-1
    * Truy cập vào mục Running Instances và kiếm EC2 instance với tên là Example
    * Ở mục Tags, chúng ta nhấn chọn nút Manage tags
  * Ở ô Key = Team, để tiến hành kiểm tra, chúng ta sẽ sửa Value = Alpha thành Value = Test, sau đó nhấn Save
  * Bạn sẽ nhận được thông báo lỗi ở bước này
    * Như vậy, bài kiểm tra thứ 4 đã được thông qua

* **Kiểm tra chính sách**
  * Đăng nhập vào AWS EC2 Console và truy cập dịch vụ EC2 ở us-east-1 (North Virginia) theo đường dẫn - https://us-east-2.console.aws.amazon.com/ec2/v2/home?region=us-east-1
  * Chúng ta truy cập vào mục Running Instances và kiếm EC2 instance với tên là Example
    * Ở góc trên bên tay phải, chúng ta sẽ nhấn nút Instance State
    * Chúng ta sẽ tiến hành nhấn chọn Terminate
  * Xác nhận Terminate
    * Bạn sẽ nhận được thông báo thành công
    * Như vậy bài kiểm tra thứ 5 đã được thông qua

* **Don dẹp tài nguyên**
  * Từ AWS Console của IAM role - ec2-admin-team-alpha, chọn vào tên của role ở góc trên bên phải và chọn Back to <Account_của_bạn>
  * Truy cập đến dịch vụ IAM theo đường dẫn - https://console.aws.amazon.com/iam/
  * Ở thanh điều hướng bên tay trái, chọn Roles và tìm ec2-admin-team-alpha
  * Chọn ec2-admin-team-alpha và nhấn nút Delete role
  * Ở thanh điều hướng bên tay trái, chọn Policies và tìm lần lượt các chính sách dưới đây, sau đó nhất nút Delete policy
    * ec2-list-read
    * ec2-create-tags
    * ec2-create-tags-existing
    * ec2-run-instances
    * ec2-manage-instances

## Thứ 4: Xây dựng giải pháp bảo vệ dữ liệu trên Amazon S3 bằng AWS KMS kết hợp giám sát nhật ký và tối ưu chi phí vận hành EC2
* **Giới thiệu**
  * Tổng quan về kiến trúc hệ thống và luồng đi của dữ liệu: Mã hóa các đối tượng (Object) trên S3 bằng khóa KMS, cấu hình Amazon CloudTrail để ghi lại toàn bộ nhật ký (logs) tương tác, và sử dụng Amazon Athena để truy vấn các tệp log đó

* **Các bước chuẩn bị**
  * Create Policy and Role: Hướng dẫn tạo các chính sách (IAM Policy) định nghĩa quyền hạn và vai trò (IAM Role) để cho phép các dịch vụ AWS hoặc thực thể tương tác bảo mật với nhau
  * Create Group and User: Hướng dẫn tạo nhóm người dùng (IAM Group) và người dùng cụ thể (IAM User) phục vụ cho việc phân quyền trong bài thực hành

* **Tạo dịch vụ quản lý khóa**
  * Các bước cấu hình và khởi tạo khóa quản lý (KMS Customer Managed Key) để thiết lập cơ chế mã hóa và giải mã dữ liệu tùy chỉnh

* **Tạo Amazon S3**
  * Create Bucket: Cách khởi tạo một phân vùng lưu trữ (S3 Bucket) trên AWS
  * Upload data to S3: Hướng dẫn tải dữ liệu lên bucket và áp dụng cơ chế mã hóa tại chỗ (at-rest) vừa cấu hình bằng khóa KMS

* **Tạo AWS CloudTrail và Amazon Athena**
  * Create CloudTrail: Cấu hình CloudTrail nhằm ghi vết toàn bộ hoạt động (API calls) liên quan đến S3 và KMS
  * Logging to CloudTrail: Theo dõi và kiểm tra quá trình ghi nhật ký tự động
  * Create Amazon Athena: Thiết lập môi trường Amazon Athena (định nghĩa cấu trúc bảng dựa trên định dạng log của CloudTrail)
  * Retrieve data with Athena: Sử dụng các câu lệnh truy vấn SQL trên Athena để lọc và tìm kiếm thông tin từ file log.

* **Kiểm tra và chia sẻ dữ liệu mã hóa trên S3**
  * Thực hiện kiểm tra tính toàn vẹn của dữ liệu sau mã hóa, giả lập các tình huống truy cập hợp lệ/không hợp lệ và hướng dẫn cách chia sẻ dữ liệu đã mã hóa một cách an toàn cho các đối tượng được cấp quyền

* **Dọn dẹp tài nguyên**
  * Hướng dẫn xóa các tài nguyên đã tạo (S3 Bucket, CloudTrail, Athena, KMS Key, IAM Users/Roles) để tránh phát sinh chi phí ngoài ý muốn sau khi hoàn thành bài thực hành

* **Tạo Policy và Role**
  * **Tạo Role**
    * Truy cập AWS Management Console
      * Tìm IAM
      * Chọn IAM
    * Trong giao diện IAM
      * Chọn Policies
      * Chọn Create policy
    * Trong phần Specify permissions
      * Chọn JSON xóa đoạn mã cũ và sao chép đoạn mã mới ở dưới vào
    * Sau khi hoàn tất bước ở trên, chúng ta kéo xuống cuối trang và ấn Next
    * Trong phần Review and create
      * Policy name nhập kms-key-policy
    * Sau khi nhập Policy name chúng ta kéo xuống cuối trang và ấn Create policy
    * Thông báo tạo Policy thành công

  * **Bước tiếp theo chúng ta sẽ tạo Role**
    * Trong giao diện IAM
      * Chọn Roles
      * Chọn Create role
    * Trong phần Select trusted entity
      * Chọn AWS service
    * Kéo xuống phần Use case
      * Phần Service or use case chọn S3
      * Phần Use case chọn S3
      * Và ấn Next
    * Trong phần Add permissions
      * Chọn và thanh tìm kiếm và tìm policy kms mới vừa tạo
      * Tích chọn vào policy vừa tạo
      * Ấn Next
    * Trong phần Name, review, and create
      * Role name nhập kms-key-role
    * Kéo xuống dưới và ấn Create role
    * Thông báo tạo role thành công

* **Tạo Group và User**
  * **Tạo Group**
    * Truy cập AWS Management Console
      * Tìm IAM
      * Chọn IAM
    * Trong giao diện IAM
      * Chọn User groups
      * Chọn Create group
    * Trong phần Create user group
      * User name group nhập GroupLimit
    * Kéo xuống phần Attach permissions polices
      * Nhấp vào thanh tìm kiếm và chọn S3
      * Tích chọn AmazonS3FullAccess
      * Ấn Create group
    * Thông báo tạo thành công

  * **Bước tiếp theo chúng ta tạo User**
    * Trong giao diện IAM
      * Chọn Users
      * Chọn Create user
    * Trong phần Specify user details
      * User name nhập User-S3
      * Tích chọn Provide user access to the AWS Management Console
      * Tích chọn I want to create an IAM user
    * Kéo xuống phần Console password
      * Nhập Password của bạn
      * Bỏ tích Users must create a new password at next sign-in (Mình sẽ không cần đổi mật khẩu khi đăng nhập lần đầu)
      * Ấn Next
    * Trong phần Permissions options
      * Chọn Add user to group
      * Tích chọn vào GroupLimit mới vừa tạo
      * Ấn Next
    * Kéo xuống dưới và ấn Create user
    * Thông báo tạo thành công
      * Sau khi tạo thành công thì bạn sao chép đường đẫn và mở trang ẩn danh hoặc một trình duyệt mới và dán vào
    * Đăng nhập các thông tin mà bạn vừa tạo
    * Thành công đăng nhập vào User-S3

* **Tạo Key Management Service**
  * Truy cập AWS Management Console
    * Tìm KMS
    * Chọn Key Management Service
  * Trong giao diện KMS
    * Chọn Customer managed keys
    * Chọn Create
  * Trong phần Configure key
    * Ở phần này chúng ta sẽ tạo ra một khóa đối xứng để mã hóa dữ liệu, bạn có thể tham khảo thêm khóa đối xứng và bất đối xứng tại AWS Key Management Service
    * Key type chọn Symmectric
    * Key usage chọn Encrypt and decrypt
    * Ấn Next
  * Trong phần Add lables
    * Alias nhập kms-key-encrypt-decrypt
  * Bước tiếp theo chúng ra kéo xuống và ấn Next
  * Trong phần Define key administrative permissions
    * Key administrator tìm kms
    * Tích chọn kms-key-role
    * Key deletion tích chọn dòng Allow key administrators to delete this key
    * Ấn Next
  * Trong phần Define key usage permissions
    * Key usage tìm kms
    * Tích chọn kms-key-role
    * Ấn Next
  * Bước tiếp theo chúng ta kéo xuống và ấn Finish
  * Thông báo tạo thành công
  
  * Tự động xoay khóa trong AWS KMS là một tính năng giúp bạn tự động thay đổi khóa mã hóa của mình sau một khoảng thời gian nhất định (Từ 90 ngày và lên đến 2560 ngày). Điều này giúp tăng cường bảo mật cho dữ liệu của bạn bằng cách giảm thiểu nguy cơ khóa của bạn bị lộ hoặc xâm phạm. Đường dẫn tham khảo thêm Rotating AWS KMS keys
  * Các bạn trở lại giao diện KMS
    * Chọn vào Key vừa mới tạo
  * Tiếp theo
    * Chọn Key rotation
    * Chọn Edit
  * Trong phần Edit automaitic key rotation
    * Chọn Ebale
    * Phần Rotation period (in days) bạn có thể tùy chỉnh tự động thay đổi khóa mã hóa của bạn bạn sau bao nhiêu ngày 1 lần nhé

* **Tạo Bucket**
  * Truy cập AWS Management Console
    * Tìm S3
    * Chọn S3
  * Trong giao diện S3
    * Chọn Buckets
    * Chọn Create bucket
  * Trong giao diện Create bucket
    * Bucket type chọn General purpose
    * Bucket name nhập kms-key-s3
  * Bước tiếp theo chúng ta kéo xuống phần Object Ownership
    * Chọn ACLs enabled
    * Object ownership chọn Object writer8
  * Bước tiếp theo chúng ta kéo xuống phần Block Public Access settings for this bucket
    * Bỏ tích Block all public acces
    * Tích chọn I acknowledge that the current settings might result in this bucket and the objects within becoming public
  * Bước tiếp theo chúng ta kéo xuống phần Default encryption
    * Encryption type chọn Server-side encryption with AWS Key Management Service keys (SSE-KMS)
    * AWS kMS Key chọn Choose fromy your AWS KMS keys
    * Availiable AWS KMS keys chọn kms-key-encrypt-decrypt
  * Bước tiếp theo chúng ta kéo xuống và ấn Create bucket
  * Thông báo tạo thành công

* **Đăng tải dữ liệu lên S3**
  * Truy cập AWS Management Console
    * Tìm S3
    * Chọn S3
  * Trong giao diện S3
    * Chọn Buckets
    * Chọn kms-key-s3
  * Bước tiếp theo chúng ta chọn Upload
  * Bước tiếp theo trong phần Upload
    * Chọn Add files
    * Chọn File vừa mới tải về và chọn Open
  * Bước tiếp theo
    * Bạn sẽ thấy File đã được Upload
    * Tiếp theo chúng ta sẽ chọn vào phần Properties
  * Chúng ta kéo xuống phần Server-side encryption
    * Server-side encryption chọn Specify an encryption key
    * Encryption settings chọn Override bucket settings for default encryption
    * Encryption type chọn Server-side encryption with AWS Key Management Service keys (SSE-KMS)
  * Chúng ta kéo xuống phần AWS KMS key
    * Chọn Choose from your AWS KMS key
    * Available AWS KMS keys chọn kms-key-encrypt-decrypt
  * Bước tiếp theo chúng ta kéo xuống và chọn Upload
  * Thông báo đăng tải dữ liệu thành công

* **Tạo CloudTrail**
  * Truy cập AWS Management Console
    * Tìm CloudTrail
    * Chọn CloudTrail
  * Trong giao diện CloudTrail
    * Chọn Trails
    * Chọn Create trail
  * Trong phần Choose trail attributes
    * Trail name nhập kms-key-cloudtrail
    * Storage location chọn Use existing S3 bucket
    * Chọn Browse
  * Bước tiếp theo
    * Chọn kms-key-s3
    * Ấn Choose
  * Trong phần Prefix - optional
    * Nhập cloudtrail
  * Chúng ta kéo xuống phần và ấn Next
  * Trong phần Choose log events
    * Event type tích chọn Management events
    * Tích chọn Data evntes
  * Bước tiếp theo chúng ta kéo xuống phần Data events
    * Chọn vào dòng chữ Switch to basic event selector để chuyển đổi chế độ
    * Bước tiếp theo ấn Continue
  * Trong phần Data event: S3
    * Data event source chọn S3
    * S3 bucket bỏ chọn Read và Write
    * Individual bucket selection ấn Browse
  * Bước tiếp theo
    * Chọn kms-key-s3
    * Ấn Choose
  * Bước tiếp theo ấn Next
  * Bước tiếp theo kéo xuống dưới ấn Create trail
  * Thông báo tạo thành công
  * Truy cập vào lại S3
  * Chọn Buckets chọn kms-key-s3
  * Chúng ta sẽ thấy một thư mục được tạo ra có tên là cloudtrail/, thư mục này sẽ chứa tất cả nhật ký liên quan đến kms-key-s3

* **Ghi nhật ký vào CloudTrail**
  * Truy cập AWS Management Console
    * Tìm S3
    * Chọn S3
  * Trong giao diện S3
    * Chọn Buckets
    * Chọn kms-key-s3
  * Tiếp theo chúng ta chọn vào thư mục cloudtrail/
  * Bước tiếp theo
    * Chọn theo đường dẫn và thấy ở trong thư mục cloudtrail/ chưa có nhật ký nào được ghi lại
  * Quay trở lại phần kms-key-s3
    * Chọn Upload
  * Trong phần Upload
    * Chọn Add files
    * Chọn File tải về ở phần 4.2
    * Ấn Open
  * Bước tiếp theo
    * Chọn vào Properties
  * Chúng ra kéo xuống phần Server-side encryption
    * Server-side encryption chọn Specify an encryption key
    * Encryption settings chọn Override bucket settings for default encryption
    * Encryption type chọn Server-side encryption with AWS Key Management Service keys (SSE-KMS)
    * AWS KMS key chọn Choose from your AWS KMS keys
  * Chúng ta kéo xuống phần Available AWS KMS keys
    * Chọn kms-key-encrypt-decrypt
  * Kéo xuống và ấn Upload
  * Thông báo upload thành công
  * Quay trở lại và chọn vào thư mục cloudtrail/
  * Chọn theo đường đẫn và thấy nhật ký đã được ghi lại vào trong thư mục cloudtrail/

* **Tạo Amazon Athena**
  * Truy cập AWS Management Console
    * Tìm CloudTrail
    * Chọn CloudTrail
  * Trong giao diện CloudTrail
    * Chọn Event history
    * Chọn Create Athena table
  * Trong phần Create a table in Amazon Athena
    * Storage location chọn kms-key-s3/cloudtrail
  * Bước tiếp theo
    * Chọn Create table
  * Thông báo tạo thành công

* **Truy xuất dữ liệu với Athena**
  * Truy cập AWS Management Console
    * Tìm Athena
    * Chọn Athena
  * Trong giao diện Athena
    * Chọn Query editor
    * Chọn Edit settings
  * Trong phần Manage settings
    * Chọn Browse S3
  * Bước tiếp theo
    * Chọn kms-key-s3
    * Ấn Choose
  * Bước tiếp theo ấn Save
  * Chúng ta quay trở lại phần Query editor
    * Chọn Editor
    * Chọn dấu 3 chấm ở bảng cloudtrail-log-kms-key-s3-cloudtrail
    * Chọn Preview table
  * Kéo xuống bên dưới sẽ thấy các nhật ký đã xuất hiện
  * Truy xuất thử thử eventname của nhật ký kms-key-s3
    * Nhập vào bảng câu lệnh truy xuất SELECT eventname FROM "default". "cloudtrail_logs_kms_key_s3_cloudtrail" limit 100;
    * Sau đó ấn Run để chạy câu lệnh
  * Kéo xuống và sẽ thấy đã truy xuất eventname thành công

* **Kiểm thử và chia sẻ dữ liệu mã hóa trên S3**
  * Truy cập AWS Management Console
    * Tìm S3
    * Chọn S3
  * Trong giao diện S3
    * Chọn Buckets
    * Chọn kms-key-s3
  * Trong phần kms-key-s3
    * Tích chọn vào dữ liệu awsstudygroup.jpg
    * Ấn Open
  * Như đã thấy, sau khi ấn Open thì dữ liệu sẽ được mở lên. Tại vì mình đã tạo quyền truy cập cho tài khoản là chủ sở hữu nên sẽ được truy cập vào dữ liệu
  * Tiếp theo chúng ta Make public mục đích là để cho phép mọi người truy cập thử dữ liệu trên S3
  * Quay trở lại giao diện kms-key-s3
    * Tích chọn dữ liệu awsstudygroup
    * Chọn Actions
    * Chọn Make public using ACL
  * Trong phần Make public
    * Ấn Make public
  * Thông báo thành công
  * Quay trở lại phần kms-key-s3
    * Tích chọn awsstudygroup
    * Ấn Copy URL
  * Sau khi dán đường dẫn URL vào một tab mới. Bạn sẽ không thể mở được dữ liệu phía AWS các yêu cầu chỉ định mã hóa phía máy chủ bằng khóa được quản lý AWS KMS yêu cầu AWS Signature Phiên bản 4
  * Tiếp theo các bạn quay lại tab ẩn danh và đăng nhập thông tin user đã tạo ở phần 2.2 Tạo Group và User
    * Sau đó truy cập vào S3
    * Chọn Buckets
    * Chọn awsstudygroup
    * Chọn Open
  * Ở User-S3 bạn sẽ nhận được thông báo truy cập bị từ chối và không được phép giải mã vì không có chính sách nào được áp dụng trên User-S3 này (Ở bước này cho thấy chủ sở hữu mới có quyền hạn để xem và mở dữ liệu)
  * Vẫn ở User-S3 trở lại phần kms-key-s3
    * Tích chọn awsstudygroup
    * Copy URL
  * Sau khi dán đường dẫn URL vào một tab mới. Bạn sẽ không thể mở được dữ liệu phía AWS các yêu cầu chỉ định mã hóa phía máy chủ bằng khóa được quản lý AWS KMS yêu cầu AWS Signature Phiên bản 4
  * Quay lại User lúc đầu của bạn
    * Truy cập vào S3
    * Tích chọn qrcode_facebook_awsstudygroup
    * Chọn Actions
  * Chọn Share with a presigned URL
  * Bước tiếp theo
    * Time interval until the presigned URL expires chọn Minutes
    * Mumber of minutes chọn 2 (Phần này mình để demo là 2 phút)
    * Ấn Create persigned URL
  * Thông báo thành công và ấn Copy persigned URL
  * Tất cả ai có được đường dẫn này đều có thể mở để xem dữ liệu trong vòng 2 phút
  * Sau hết 2 phút thì sẽ có thông báo Truy cập bị từ chối và hết hạn truy cập

* **Dọn dẹp tài nguyên**
  * **Xóa tài nguyên KMS**
    * Truy cập AWS Management Console
      * Tìm KMS
      * Chọn KMS
    * Trong giao diện KMS
      * Tích chọn kms-key-encrypt-decrypt
      * Chọn Key actions
      * Chọn Disable
    * Bước tiếp theo
      * Tích chọn Comfirm that you want to disable this key
      * Ấn Disable key
    * Quay trở lại giao diện KMS
      * Tích chọn kms-key-encrypt-decrypt
      * Chọn Key actions
      * Chọn Schedule key deletion
    * Tiếp theo
      * Waiting period (in days) nhập 7
      * Tích chọn Confirm that you want to schedule these keys for deletion after a 7 day waiting period
      * Ấn Schedule deletion
    * Thông báo thành công

  * **Xóa tài nguyên CloudTrail**
    * Truy cập AWS Management Console
      * Tìm CloudTrail
      * Chọn CloudTrail
    * Trong giao diện CloudTrail
      * Chọn Trail
      * Chọn kms-key-cloudtrail
    * Bước tiếp theo
      * Ấn Stop logging
    * Tiếp theo
      * Chọn Stop logging
    * Sau khi Stop logging thì quay trở lại ấn Delete
    * Tiếp theo
      * Ấn Delete
    * Thông báo thành công

  * **Xóa tài nguyên S3**
    * Truy cập AWS Management Console
      * Tìm S3
      * Chọn S3
    * Trong giao diện S3
      * Tích chọn aws-athena-query-results-058264191537-us-east-1
      * Chọn Empty
    * Bước tiếp theo
      * Nhập vào permanently delete
      * Ấn Empty
    * Thông báo Empty thành công
    * Tiếp tục quay lại giao diện CloudTrail
      * Tích chọn aws-athena-query-results-058264191537-us-east-1
      * Chọn Delete
    * Bước tiếp theo
      * Nhập vào aws-athena-query-results-058264191537-us-east-1
      * Ấn Delete bucket
    * Tiếp tục quay lại giao diện CloudTrail
      * Tích chọn vào kms-key-s3
      * Chọn Empty
    * Bước tiếp theo
      * Nhập vào permanently delete
      * Ấn Empty
    * Thông báo thành công
    * Quay lại giao diện CloudTrail
      * Tích chọn vào kms-key-s3
      * Chọn Delete
    * Tiếp theo chúng ta ấn Empty một lần nữa
    * Bước tiếp theo
      * Nhập vào permanently delete
      * Ấn Empty
    * Chúng ta quay lại giao diện CloudTrail
      * Tích chọn vào kms-key-s3
      * Chọn Delete
    * Tiếp theo
      * Nhập kms-key-s3
      * Ấn Delete bucket
    * Xóa thành công

  * **Xóa tài nguyên User và Group**
    * Truy cập AWS Management Console
      * Tìm IAM
      * Chọn IAM
    * Trong giao diện IAM
      * Tích chọn User-S3
      * Chọn Delete
    * Bước tiếp theo
      * Nhập vào User-S3
      * Ấn Delete user
    * Thông báo thành công
    * Quay trở lại giao diện IAM
      * Tích chọn GroupLimit
      * Chọn Delete
    * Tiếp theo
      * Nhập vào GroupLimit
      * Ấn Delete
    * Thông báo thành công

* **Tối ưu chi phí EC2 với Lambda**
  * **Tạo VPC**
    * Truy cập AWS Management Console
      * Tìm VPC
      * Chọn VPC
    * Trong giao diện VPC
      * Chọn Your VPCs
      * Chọn Create VPC
    * Trong giao diện Create VPC
      * Chọn VPC, subnets, etc
      * Nhập lambda-lab
    * Chọn Create VPC
    * Chọn View VPC
    * Hoàn thành tạo VPC
    * Trong giao diện VPC
      * Chọn Subnets
      * Chọn public subnet
      * Chọn Actions
      * Chọn Edit subnet settings
    * Chọn Enable auto-assign public IPv4 address, chọn Save

  * **Tạo Security Group**
    * Trong giao diện VPC:
      * Chọn Security Group
      * Chọn Create security group
      * Trong trường Security group name, nhập lambda-lab
      * Trong trường Description, nhập security group for lambda lab
      * Chọn VPC vừa tạo
    * Trong giao diện Create security group:
      * Cấu hình Inbound rules
      * Cấu hình Outbound rules
    * Chọn Create security group

  * **Tạo EC2 instance**
  * Truy cập giao diện AWS Management Console
    * Tìm EC2
    * Chọn EC2
  * Trong giao diện EC2
    * Chọn Instances
    * Chọn Launch instances
  * Tiếp theo trong giao diện Launch instance
    * Name, nhập lambda-lab-instance
    * Chọn Quick Start
    * Chọn Amazon Linux
    * Chọn Amazon Linux 2 AMI
  * Chọn Instance type và chọn Create new key pair
  * Trong giao diện Create key pair
    * Key pair name, nhập lambda-lab-key
    * Chọn Create key pair
  * Trong phần Network settings
    * Chọn Edit
  * Trong phần Network settings
    * Chọn VPC vừa tạo
    * Chọn public subnet
    * Chọn Enable đối với Auto-assign public IP
    * Chọn Select existing security group
    * Chọn Security group vừa tạo
  * Tạo ec2 instance thành công

  * **Hướng dẫn sử dụng Incoming Web-hooks trên Slack**
    * Trước tiên, đăng nhập vào Slack.com thông qua trình duyệt của bạn
    * Sau khi đăng nhập thành công, bạn sẽ thấy giao diện
    * Bây giờ, truy cập vào Incoming WebHooks
      * Nếu bạn chưa đăng nhập ở bước trước, hãy chọn Sign in to install
    * Sau khi đăng nhập thành công, hãy chọn Add to Slack
    * Tiếp theo, bạn sẽ được yêu cầu chọn Create Another Workspace
    * Nhập tên là aws-lambda-labs và sau đó chọn Next
    * Tiếp theo, nhập tên là aws-lambda và chọn Next
    * Hoàn tất quá trình tạo Workspace trên Slack
    * Trong giao diện Slack App Directory, chọn workspace bạn vừa tạo và sau đó chọn Add to Slack
    * Tiếp theo, chọn create a new channel
    * Trong giao diện Create a Channel:
      * Đặt tên cho kênh là notification
      * Nhập mô tả là notification for lambda
      * Cuối cùng, chọn Create
    * Sau khi hoàn tất các bước trên, bạn sẽ cần sao chép Webhook URL để sử dụng

  * **Tạo Tag cho Instance**
    * Trong giao diện EC2
      * Chọn Instances
      * Chọn lambda-lab-instance
      * Chọn Actions
      * Chọn Instance settings
      * Chọn Manage tags
    * Trong giao diện Manage tags
      * Key, nhập environment_auto
      * Value, nhập true
      * Chọn Save

  * **Tạo Role cho Lambda**
    * Truy cập giao diện AWS Management Console
      * Tìm IAM
      * Chọn IAM
    * Trong giao diện IAM
      * Chọn Roles
      * Chọn Create role
    * Trong giao diện Select trusted entity
      * Chọn AWS service
      * Chọn Lambda
      * Chọn Next
    * Trong giao diện Add permissions
      * Tìm AmazonEC2FullAccess
      * Chọn AmazonEC2FullAccess
    * Tiếp theo, tương tự bước trên
      * Tìm CloudWatchFullAccess
      * Chọn CloudWatchFullAccess
      * Chọn Next
    * Trong phần Name, review, and create
      * **Nhập dc-common-lambda-role cho Role name
    * Kiểm tra lại và chọn Create role
    * Hoàn thành tạo role cho Lamda Function

  * **Tạo Lambda Function thực hiện chức năng Stop instances**
    * Truy cập AWS Management Console
      * Tìm Lambda
      * Chọn Lambda
    * Trong giao diện AWS Lambda
      * Chọn Function
      * Chọn Create function
    * Trong giao diện Create function
      * Chọn Author from scratch
      * Function name, nhập dc-common-lambda-auto-stop
      * Runtime, chọn Python 3.8
      * Chọn x86_64
    * Tiếp tục trong giao diện Create function
      * Chọn Change default execution role
      * Chọn Use an existing role
      * Chọn dc-common-lambda-role
      * Chọn Create function
    * Sau khi tạo function thành công
      * Chọn Configuration
      * Chọn Environment variables
      * Chọn Edit
    * Trong giao diện Edit environment variables
      * Chọn Add environment variable
    * Trong giao diện Edit environment variables
      * Key, nhập environment_auto
      * Value, nhập true
    * Sau khi tạo môi trường xong
      * Chúng ta chọn Code
    * Trong giao diện Code source
      * Import source code: Bạn cần phải thay đổi webhook_url để nhận thông báo đến Slack.
    * Sau đó lưu lại và chọn Deploy
    * Truy cập AWS Management Console
      * Tìm CloudWatch
      * Chọn CloudWatch
    * Trong giao diện CloudWatch
      * Chọn Events
      * Chọn Rules
      * Chọn Go to Amazon EvenBridge
    * Trong giao diện Rules
      * Chọn Create rule
    * Trong giao diện create rule
      * Name, nhập dc-common-lambda-auto-stop
      * Description, nhập dc-common-lambda-auto-stop
      * Chọn Schedule
      * Chọn Next
    * Trong Schedule pattern
      * Có 2 Schedule pattern để lựa chọn:
        * Lịch trình chi tiết chạy vào một thời điểm cụ thể, chẳng hạn như 8 giờ sáng theo giờ PST vào Thứ Hai đầu tiên của mỗi tháng
        * Lịch trình chạy với tốc độ đều đặn, chẳng hạn như 10 phút một lần
      * Chọn A schedule that runs at a regular rate, such as every 10 minutes
      * Đặt rate, value là 9 hours
      * Chọn Next
    * Trong giao diện Target
      * Chọn AWS service
      * Chọn Lambda function
      * Function, chọn dc-common-lamda-auto-stop
      * Chọn Next
    * Chọn Next
    * Kiểm tra lại và chọn Create rule
    * Hoàn thành tạo rule cho stop insatance

  * **Tạo Lambda Function thực hiện chức năng Start instances**
    * Trong giao diện Lambda Function
      * Chọn Create function
    * Trong giao diện Create function
      * Chọn Author from scratch
      * Function name, nhập dc-common-lambda-auto-start
      * Runtime, chọn Python 3.8
      * Chọn x86_64
    * Trong giao diện Create function
      * Chọn Change default execution role
      * Chọn Use an existing role
      * Chọn dc-common-lambda-role
      * Chọn Create function
    * Trước khi import code , hãy tạo Environment variables như sau:
      * Chọn Configuration
      * Chọn Environment variables
      * Chọn Edit
    * Trong giao diện Edit environment variables
      * Key, nhập environment_auto
      * Value, nhập true
      * Chọn Save
    * Sau khi tạo môi trường
      * Chọn Code
      * Import source code: Bạn cần phải thay đổi webhook_url để nhận thông báo đến Slack
      * Lưu lại và chọn Deploy
    * Tiếp theo tạo rule CloudWatch
      * Trong phần rule details, Name, nhập dc-common-lambda-auto-start
      * Description, nhập dc-common-lambda-auto-start
      * Chọn Schedule
      * Chọn Next
    * Trong giao diện Schedule pattern
      * Có 2 Schedule pattern để lựa chọn:
        * Lịch trình chi tiết chạy vào một thời điểm cụ thể, chẳng hạn như 8 giờ sáng theo giờ PST vào Thứ Hai đầu tiên của mỗi tháng
        * Lịch trình chạy với tốc độ đều đặn, chẳng hạn như 10 phút một lần
      * Chọn A schedule that runs at a regular rate, such as every 10 minutes
      * Đặt rate, value là 8 hours
      * Chọn Next
    * Trong giao diện Target
      * Chọn AWS service
      * Chọn Lambda function
      * Function, chọn dc-common-lambda-auto-start
      * Chọn Next
    * Chọn Next
    * Kiểm tra lại và chọn Create rule

  * **Kiểm tra kết quả**
    * Kiểm tra giao diện EC2 và trạng thái instance
    * Vào Lambda Function thực hiện chức năng start instance
      * Chọn Test
      * Chọn Create new event
      * Event name, nhập instance-start
      * Chọn Save
      * Chọn Test
    * Trong workspace của slack nhận được thông báo Starting instance
    * Tương tự, trong Lambda function thực hiện chức năng stopping instance
      * Chọn Test
      * Chọn Create new envent
      * Event name, nhập instance-stop
      * Chọn Save
      * Chọn Test
    * Kiểm tra instance đã chuyển sang trạng thái Stopped
    * Trong workspace của slack nhận được thông báo Stopping Instance

  * **Dọn dẹp tài nguyên**
    * **Xóa Lambda function**
      * Truy cập vào trang AWS Lambda
      * Chọn các function liên quan bài lab
      * Chọn Delete

    * **Xóa CloudWatch Events Rule**
      * Truy cập vào trang CloudWatch
      * Chọn Rules
      * Chọn các rule liên quan bài lab
      * Chọn Actions
      * Chọn Delete

## Thứ 5: Cập nhật Routing, Navigation và Các Trang SOC Mới
* **Mô tả tổng quát**
  * Tập trung vào việc mở rộng và hoàn thiện routing + tích hợp các trang chuyên sâu mới cho phần Frontend SOC Dashboard.
  * Đây là bước quan trọng để nâng cao khả năng điều hướng và chuẩn bị cho các module AI Threat Intelligence, Attack Surface Management, MITRE ATT&CK Framework và Case Management.

* **Các thay đổi cụ thể**
  * **Cập nhật routing chính (src/App.tsx)**
    * Thêm import cho 4 trang mới:
      * AIThreatDetectionPage
      * AttackSurfacePage
      * MitreAttackPage
      * CaseManagementPage

    * Cải tiến type của state currentView:
      * Trước: Union type cứng ("dashboard" | "alerts" | ...)
      * Sau: Sử dụng AppView (được định nghĩa trong types/views.ts) — giúp code sạch hơn, dễ bảo trì và mở rộng.

    * Mở rộng logic render conditional (AnimatePresence) để hỗ trợ render các trang mới dựa trên currentView.
    * Cập nhật Sidebar navigation để liên kết với các view mới.

  * **Cập nhật Mock Server (frontend/server.ts)**
    * Thay đổi port mặc định từ 3000 thành 3001 (hoặc lấy từ biến môi trường process.env.PORT).
    * Điều này giúp tránh conflict port khi chạy đồng thời với các service khác (backend FastAPI thường chạy ở 8000).

  * **Thêm mới / Cập nhật các file cấu hình và trang**
    * Các trang mới được thêm:
      * AIThreatDetectionPage.tsx — Trang giám sát phát hiện mối đe dọa bằng AI.
      * AttackSurfacePage.tsx — Trang quản lý bề mặt tấn công.
      * MitreAttackPage.tsx — Trang tích hợp khung MITRE ATT&CK.
      * CaseManagementPage.tsx — Trang quản lý vụ việc (Case).
      * EndpointPage.tsx — Trang quản lý Endpoint.

    * Các file config hỗ trợ:
      * aiThreatDetectionConfig.ts
      * attackSurfaceConfig.ts
      * caseManagementConfig.ts
      * mitreConfig.ts

    * Cập nhật components chung:
      * IncidentsFeed.tsx
      * MultiColorDonut.tsx
      * Sidebar.tsx
      * ReportStats.tsx
      * Cập nhật CSS và types (views.ts)

* **Nội dung chi tiết các trang mới (Mock Data)**
  * AI Threat Detection Page bao gồm:
    * KPI cards: Total Detections, Avg Accuracy, False Positive Rate, Active Models, Avg Latency.
    * Detection Timeline (24h) với dữ liệu mock.
    * Model Performance Radar Chart (so sánh nhiều model).
    * Accuracy Trend Line Chart.
    * Multi-color Donut Chart phân bố loại tấn công.
    * Recent Detections list.
    * Active Models status.

  * Attack Surface Page, MITRE ATT&CK Page, Case Management Page cũng được xây dựng với cấu trúc tương tự, sử dụng mock data phong phú để mô phỏng giao diện thực tế.

* **Tình trạng tổng thể nhánh devphu sau cập nhật**
  * Frontend đã khá hoàn chỉnh với nhiều trang chuyên sâu.
  * Hỗ trợ Dark/Light mode ổn định.
  * Realtime WebSocket (mock server).
  * Sidebar navigation đầy đủ.
  * Nhiều chart, KPI widgets, alert feed, modal chi tiết sự kiện.
  * Chuẩn bị tốt cho việc tích hợp backend sau này (Track A).