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
    * 
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

  * **




## Thứ 2:
