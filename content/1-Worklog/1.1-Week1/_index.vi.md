---
title: "Worklog Tuần 1"
date: 2026-04-17
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---


### Mục tiêu tuần 1:

* Kết nối, làm quen với các thành viên trong First Cloud Journey.
* Hiểu tổng quan về AWS và các nhóm dịch vụ chính, đồng thời làm quen với AWS Management Console và AWS CLI.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 6 | - Làm quen với các thành viên FCJ <br> - Đọc và lưu ý các nội quy, quy định của chương trình thực tập <br> - Tạo tài khoản AWS Free Tier | 17/04/2026 | 17/04/2026 | <https://000001.awsstudygroup.com/> |
| 2 | - Thiết lập AWS Budgets để quản lý chi phí | 20/04/2026 | 20/04/2026 | <https://000007.awsstudygroup.com/>  |
| 3 | - Tìm hiểu AWS và các loại dịch vụ <br>&emsp; + Compute <br>&emsp; + Storage <br>&emsp; + Networking <br>&emsp; + Database <br>&emsp; + ... <br> - Học về Access Management với AWS IAM (User, Group, Policy, Role) | 21/04/2026 | 21/04/2026 | <https://000002.awsstudygroup.com/> |
| 4 | - Học Networking với Amazon VPC | 22/04/2026 | 22/04/2026 | <https://000003.awsstudygroup.com/> |
| 5 | - Introduction to AWS <br> - Management Console | 23/04/2026 | 23/04/2026 | <https://www.youtube.com/watch?v=qVCF7UjYC5s&t=146s> <br> <https://www.youtube.com/watch?v=95quNuhvMT0> |


### Kết quả đạt được tuần 1:

## Thứ 6: Khởi tạo hạ tầng & Làm quen môi trường

* **Hòa nhập môi trường:** 
    * Kết nối đội ngũ: Kết nối và làm quen với các thành viên trong cộng đồng First Cloud Journey (FCJ).
        * Thiết lập kênh giao tiếp (Whapsapp/Linkedin) và nhận diện các Mentor hỗ trợ kỹ thuật.
    * Nghiên cứu nội quy: Đọc và phân tích kỹ các điều khoản thực tập, quy trình báo cáo Worklog (Daily/Weekly).
        * Cam kết: Đảm bảo tính bảo mật của dữ liệu và tuân thủ các nguyên tắc an toàn thông tin khi thực hành trên môi trường Cloud.

* **Quản trị tài khoản AWS:**
    * Khởi tạo tài khoản AWS Free Tier:
        * Thực hiện đăng ký tài khoản tại AWS Free Tier.
        * Yêu cầu kỹ thuật: Sử dụng thẻ thanh toán quốc tế (Visa/Mastercard) có sẵn ít nhất $1 để xác thực tài khoản.
        * Lựa chọn Region: Ưu tiên chọn các Region gần Việt Nam như Singapore (ap-southeast-1) để có độ trễ (latency) thấp nhất khi thực hành.
    ![Minh chứng: Tài khoản AWS đã kích hoạt thành công](/images/1-Worklog/1.1-Week1/Day6/Create_Account.png)
    * Bảo mật tài khoản gốc (Root Account Hardening):
        * Kích hoạt MFA (Multi-Factor Authentication): Đây là bước bắt buộc ngay sau khi tạo tài khoản. Sử dụng các ứng dụng như Google Authenticator hoặc Authy để tạo lớp bảo mật thứ hai cho tài khoản Root.
    ![Minh chứng: Kích hoạt MFA cho tài khoản thành công](/images/1-Worklog/1.1-Week1/Day6/MFA_success.png)

* **Nhận diện và Phân loại dịch vụ miễn phí:**
    * Dựa trên tài liệu hướng dẫn tại https://000001.awsstudygroup.com/, thực hiện phân loại 3 nhóm ưu đãi của AWS:
    * Always Free: Các dịch vụ như AWS Lambda (1 triệu request/tháng), Amazon DynamoDB (25GB storage).
    * 12 Months Free: * Amazon EC2: 750 giờ/tháng (loại instance t2.micro hoặc t3.micro tùy region).
    * Amazon S3: 5GB dung lượng lưu trữ Standard.
    * Amazon RDS: 750 giờ/tháng cho các database micro instance.
    * Trials: Các dịch vụ cao cấp có thời gian dùng thử ngắn từ 30-60 ngày (như Amazon SageMaker hoặc GuardDuty).

* **Nhận diện "Credit Killers" (Cảnh báo rủi ro chi phí):**
    * Ghi chú lại các dịch vụ dễ phát sinh phí ngoài ý muốn dù đang trong thời gian Free Tier:
    * Elastic IP (EIP): Sẽ bị tính phí nếu bạn đăng ký nhưng không gắn (attach) vào một máy chủ EC2 đang chạy.
    * NAT Gateway: Không nằm trong danh mục Free Tier. Phí duy trì khoảng $0.045/giờ (rất dễ làm cạn kiệt số dư tài khoản nếu quên xóa).
    * EBS Volumes: Chỉ miễn phí tối đa 30GB tổng dung lượng. Nếu tạo nhiều ổ đĩa thừa sẽ bị tính phí lưu trữ.

## Thứ 2: Quản lý chi phí với AWS Budgets

* **Quản lý chi phí (AWS Budgets - Cơ sở kiến thức)**
    * Mô hình Trách nhiệm dùng chung về Chi phí: AWS cung cấp công cụ, nhưng người dùng chịu trách nhiệm theo dõi và thiết lập các giới hạn để tránh lãng phí tài nguyên.
    * Các loại Ngân sách (Budget Types):
        * Cost Budget: Theo dõi dựa trên số tiền (USD) thực tế phát sinh.
        * Usage Budget: Theo dõi dựa trên định mức sử dụng tài nguyên (giờ chạy, dung lượng lưu trữ) - cực kỳ quan trọng để kiểm soát giới hạn của Free Tier.
        * Reservation Budget: Theo dõi hiệu quả của việc mua trước tài nguyên (dành cho doanh nghiệp).
    * Cơ chế Cảnh báo (Alerting Mechanisms):
        * Actual (Thực tế): Cảnh báo khi chi phí đã xảy ra.
        * Forecasted (Dự báo): Cảnh báo dựa trên thuật toán máy học của AWS, dự đoán chi phí cuối tháng dựa trên thói quen sử dụng hiện tại. (Giúp ngăn chặn rủi ro từ sớm).
    * Độ trễ dữ liệu (Data Latency): Hiểu rằng dữ liệu Billing thường trễ từ 8 - 12 tiếng, do đó cần thiết lập ngưỡng cảnh báo thấp hơn mức mong muốn một chút.

* **Quản lý chi phí (AWS Budgets - Quy trình thiết lập)**
    * **Tạo Cost Budget (Ngân sách chi phí)**
        * Thiết lập ngân sách dựa trên chi phí hóa đơn thực tế. 
        * Đặt ngưỡng cảnh báo tại **$0.01** để kiểm soát tuyệt đối các phát sinh.
        * Áp dụng cho toàn bộ dịch vụ AWS.
        * Đăng nhập vào AWS Management Console và tìm dịch vụ Billing and Cost Management tại thanh tìm kiếm.
        * ![Minh chứng: Chọn dịch vụ AWS Billing and Cost Management](/images/1-Worklog/1.1-Week1/Day2/AWS_Billing_and_Cost_Management.png)
        * Tại trang quản trị, chọn Budgets từ menu bên trái. Nhấn vào nút Create budget.
        * ![Minh chứng: Tạo budget](/images/1-Worklog/1.1-Week1/Day2/Create_a_budget.png)
        * Chọn Customize (tùy chỉnh)
        * Tại Budget types, chọn Cost budget
        * Nhấn Next
        * ![Minh chứng: Phần Budget setup](/images/1-Worklog/1.1-Week1/Day2/Budget_setup_1.png)
        * ![Minh chứng: Phần Budget setup](/images/1-Worklog/1.1-Week1/Day2/Budget_setup_2.png)
        * Tại Budget name, nhập Monthly
        * ![Minh chứng: Giao diện Set your budget](/images/1-Worklog/1.1-Week1/Day2/Set_your_budget.png)
        * Period: Chọn khoảng thời gian cho Budget:
            * Daily (Hàng ngày)
            * Monthly (Hàng tháng)
            * Quarterly (Hàng quý)
            * Annually (Hàng năm)
        * Budget effective dates:
            * Recurring Budget: Nếu bạn muốn Budget được lặp lại định kỳ
            * Expiring Budget: Nếu bạn chỉ muốn Budget được áp dụng một lần duy nhất.
        * Specify your monthly budget:
            * Fixed: Nếu bạn muốn ngân sách của mỗi kỳ hạn là giống nhau
            * Monthly Budget Planning: Nếu bạn muốn thiết lập ngân sách khác nhau cho từng tháng
            * Budgeted amount: Nhập số tiền tương ứng với ngân sách của bạn
        * ![Minh chứng: Set budget amount](/images/1-Worklog/1.1-Week1/Day2/Set_budget_amount.png)
        * Tại phần Budget scope, chọn All AWS services để áp dụng ngân sách cho tất cả dịch vụ AWS. Tại Aggregate costs by, chọn Unblended costs. Sau đó nhấn Next.
        * ![Minh chứng: Budget scope](/images/1-Worklog/1.1-Week1/Day2/Budget_scope.png)
        * Chọn Add an alert threshold để thiết lập ngưỡng cảnh báo.
        * ![Minh chứng: Thiết lập cảnh báo](/images/1-Worklog/1.1-Week1/Day2/Add_an_alert_threshold.png)
        * Thực hiện cấu hình chi tiết cho Alert và chọn Next.
        * ![Minh chứng: Cấu hình Alert](/images/1-Worklog/1.1-Week1/Day2/Alert.png)
        * Xem lại các thiết lập hành động (nếu có) và chọn Next.
        * ![Minh chứng: Xem lại các thiết lập](/images/1-Worklog/1.1-Week1/Day2/Check_Alert.png)
        * Xem lại toàn bộ cấu hình và chọn Create budget để hoàn tất.
        * ![Minh chứng: Create budget](/images/1-Worklog/1.1-Week1/Day2/Create_budget.png)
        * Xác nhận Budget đã được tạo thành công.
        * ![Minh chứng: Budget tạo thành công](/images/1-Worklog/1.1-Week1/Day2/Budget_tạo_thành_công.png)

    * **Tạo Usage Budget (Ngân sách sử dụng)**
        * Theo dõi định mức sử dụng tài nguyên (như giờ chạy EC2, dung lượng S3) để đảm bảo không vượt quá giới hạn của gói Free Tier.
        * Đăng nhập vào AWS Management Console và tìm dịch vụ Billing and Cost Management tại thanh tìm kiếm.
        * ![Minh chứng: Chọn dịch vụ AWS Billing and Cost Management](/images/1-Worklog/1.1-Week1/Day2/AWS_Billing_and_Cost_Management.png)
        * Tại trang quản trị, chọn Budgets từ menu bên trái. Nhấn vào nút Create budget.
        * ![Minh chứng: Tạo budget](/images/1-Worklog/1.1-Week1/Day2/Create_a_budget.png)
        * Chọn Customize (tùy chỉnh)
        * Tại Budget types, chọn Usage budget
        * Nhấn Next
        * ![Minh chứng: Budget setup](/images/1-Worklog/1.1-Week1/Day2/Budget_setup.png)
        * Trong giao diện Set your budget:
            * Tại Budget name, nhập tên cho budget của bạn
        * Tại phần Budget against:
            * Chọn Usage type groups
            * Chọn EC2: ELB - Running Hours để theo dõi số giờ chạy của EC2 instances
        * ![Minh chứng: Details Budgeting](/images/1-Worklog/1.1-Week1/Day2/Details_Budget.png)
        * Period: Chọn khoảng thời gian cho Budget (Hàng ngày/Hàng tháng/Hàng quý/Hàng năm)
        * Budget renewal type: Chọn loại gia hạn ngân sách (Recurring/Expiring)
        * Budgeting method: Chọn phương pháp lập ngân sách (Fixed/Planned)
        * Nhập số giờ sử dụng tối đa mà bạn muốn giới hạn
        * ![Minh chứng: Set budget amount](/images/1-Worklog/1.1-Week1/Day2/Set_budget_amount.png)
        * Tại phần Budget scope, giữ mặc định và chọn Next.
        * ![Minh chứng: Budget scope](/images/1-Worklog/1.1-Week1/Day2/Budget_scope.png)
        * Trong phần Configure alerts, chọn Add an alert threshold để thiết lập ngưỡng cảnh báo.
        * ![Minh chứng: Thiết lập cảnh báo](/images/1-Worklog/1.1-Week1/Day2/Add_an_alert_threshold.png)
        * Thiết lập ngưỡng cảnh báo (% của ngân sách)
        * Thêm địa chỉ email để nhận thông báo khi vượt ngưỡng
        * ![Minh chứng: Cấu hình Alert](/images/1-Worklog/1.1-Week1/Day2/Alert.png)
        * Nhấn Next để tiếp tục.
        * ![Minh chứng: Xem lại các thiết lập](/images/1-Worklog/1.1-Week1/Day2/Check_Alert.png)
        * Xem lại các thiết lập và chọn Create budget để hoàn tất.
        * ![Minh chứng: Create budget](/images/1-Worklog/1.1-Week1/Day2/Create_budget.png)
        * Sau khi tạo thành công, bạn sẽ thấy budget mới trong danh sách.
        * ![Minh chứng: Tạo Usage budget thành công](/images/1-Worklog/1.1-Week1/Day2/Tạo_Usage_budget_thành_công.png)
        * Kiểm tra Budget health (Tình trạng ngân sách) để theo dõi mức sử dụng hiện tại so với ngân sách đã thiết lập.
        * ![Minh chứng: Budget health](/images/1-Worklog/1.1-Week1/Day2/Budget_health.png)
        * Xem Budget history (Lịch sử ngân sách) để theo dõi xu hướng sử dụng qua thời gian.
        * ![Minh chứng: Budget history](/images/1-Worklog/1.1-Week1/Day2/Budget_history.png)

    * **Tạo RI & Savings Plans Budget**
        * Thiết lập giám sát cho các thực thể dự trữ và kế hoạch tiết kiệm nhằm tối ưu hóa chi phí cho các dự án dài hạn.
        * Đăng nhập vào trang quản trị AWS Management Console và chọn dịch vụ AWS Billing and Cost Management tại thanh tìm kiếm.
        * ![Minh chứng: Chọn dịch vụ AWS Billing and Cost Management](/images/1-Worklog/1.1-Week1/Day2/AWS_Billing_and_Cost_Management.png)
        * Tại trang quản trị, chọn Budgets từ menu bên trái. Nhấn vào nút Create budget.
        * ![Minh chứng: Tạo budget](/images/1-Worklog/1.1-Week1/Day2/Create_a_budget.png)
        * Chọn Customize
        * Chọn Reservation budget
        * Chọn Next
        * ![Minh chứng: Budget setup](/images/1-Worklog/1.1-Week1/Day2/Budget_setup_3.png)
        * Đặt tên budget.
        * ![Minh chứng: Name budget](/images/1-Worklog/1.1-Week1/Day2/Budget_name.png)
        * Cấu hình Coverage threshold.
        * ![Minh chứng: Coverage threshold](/images/1-Worklog/1.1-Week1/Day2/Coverage_threshold.png)
        * Cấu hình Budget scope.
        * ![Minh chứng: Budget scope](/images/1-Worklog/1.1-Week1/Day2/Budget_scope.png)
        * Tại phần Alert setting, nhập địa chỉ email. Chọn Next
        * ![Minh chứng: Alert setting](/images/1-Worklog/1.1-Week1/Day2/Alert_setting.png)
        * Chọn Create budget.
        * ![Minh chứng: Tạo budget](/images/1-Worklog/1.1-Week1/Day2/Create_RI_budget.png)
        * Hoàn thành tạo budget.
        * ![Minh chứng: Tạo RI budget thành công](/images/1-Worklog/1.1-Week1/Day2/Tạo_RI_Budget_thành_công.png)
        * Kiểm tra budget đã tạo.
        * ![Minh chứng: Kiểm tra budget RI](/images/1-Worklog/1.1-Week1/Day2/Check_RI_budget.png)

    * **Cấu hình Cảnh báo & Thông báo Email**
        * Cài đặt gửi thông báo tự động về email cá nhân khi chi phí thực tế hoặc dự báo (Forecasted) chạm ngưỡng thiết lập.
        * Đăng nhập vào trang quản trị AWS Management Console và tìm dịch vụ AWS Billing and Cost Management tại thanh tìm kiếm.
        * ![Minh chứng: Chọn dịch vụ AWS Billing and Cost Management](/images/1-Worklog/1.1-Week1/Day2/AWS_Billing_and_Cost_Management.png)
        * Tại trang quản trị, chọn Budgets từ menu bên trái. Nhấn vào nút Create budget
        * ![Minh chứng: Tạo budget](/images/1-Worklog/1.1-Week1/Day2/Create_a_budget.png)
        * Chọn Customize (tùy chỉnh)
        * Tại Budget types, chọn Savings Plans budget
        * Nhấn Next
        * ![Minh chứng: Budget setup](/images/1-Worklog/1.1-Week1/Day2/Budget_setup_3.png)
        * Tại phần Details, nhập tên cho budget của bạn trong trường Budget name.
        * Thực hiện cấu hình Utilization threshold - ngưỡng sử dụng cho Savings Plans.
        * ![Minh chứng: Details Budgeting](/images/1-Worklog/1.1-Week1/Day2/Details_saving_plan_budget.png)
        * Tại Budget scope giữ tùy chọn mặc định. Chọn Next
        * ![Minh chứng: Budget scope](/images/1-Worklog/1.1-Week1/Day2/Budget_scope.png)
        * Tại phần Alert setting, nhập địa chỉ email. Chọn Next
        * ![Minh chứng: Alert setting](/images/1-Worklog/1.1-Week1/Day2/Alert_setting.png)
        * Xem lại các thiết lập và nhấn Create budget để hoàn tất.
        * ![Minh chứng: Tạo budget](/images/1-Worklog/1.1-Week1/Day2/Create_saving_plan_budget.png)
        * Sau khi tạo thành công, bạn sẽ thấy thông báo xác nhận.
        * Kiểm tra chi tiết budget đã tạo trong danh sách budgets.
        * ![Minh chứng: Tạo saving plan budget thành công](/images/1-Worklog/1.1-Week1/Day2/Tạo_saving_plan_Budget_thành_công.png)

    * **Dọn dẹp tài nguyên (Resource Cleanup)**
        * Thực hiện kiểm tra và xóa bỏ các tài nguyên thử nghiệm không cần thiết để duy trì tài khoản ở trạng thái sạch, tránh phí duy trì ngầm.
        * Đăng nhập vào trang quản trị AWS Management Console và tìm dịch vụ AWS Billing and Cost Management tại thanh tìm kiếm.
        * ![Minh chứng: Chọn dịch vụ AWS Billing and Cost Management](/images/1-Worklog/1.1-Week1/Day2/AWS_Billing_and_Cost_Management.png)
        * Tại trang quản trị, chọn Budgets từ menu bên trái.
        * Thực hiện xóa budget:
            * Chọn Budget cần xóa
            * Chọn Action
            * Nhấn vào nút Delete
        * ![Minh chứng: Xóa budget](/images/1-Worklog/1.1-Week1/Day2/Delete_budget.png)
        * Trong hộp thoại xác nhận, nhấn Delete để hoàn tất việc xóa budget.
        * Lặp lại các bước trên với tất cả các Budget còn lại mà bạn đã tạo trong quá trình thực hành.

## Thứ 3: Quản trị định danh và Truy cập (AWS IAM)

* **Tổng quan các nhóm dịch vụ cốt lõi (Global Infrastructure & Core Services):**
    * Compute (Dịch vụ tính toán - "Bộ não")
        * Đây là nơi xử lý các dòng lệnh và chạy ứng dụng.
        * Amazon EC2 (Elastic Compute Cloud): Cung cấp máy chủ ảo hóa. Bạn có toàn quyền kiểm soát hệ điều hành.
        * AWS Lambda (Serverless): Chạy code theo sự kiện mà không cần quản lý máy chủ. Bạn chỉ trả tiền cho thời gian code thực sự chạy.
    * Storage (Dịch vụ lưu trữ - "Kho chứa")
        * Amazon S3 (Simple Storage Service): Lưu trữ dạng đối tượng (ảnh, video, file backup). Có độ bền dữ liệu lên tới 99.999999999% (11 con số 9).
        * Amazon EBS (Elastic Block Store): Giống như ổ cứng SSD/HDD rời để gắn vào máy chủ EC2.
    * Networking (Dịch vụ mạng - "Đường dẫn")
        * Amazon VPC (Virtual Private Cloud): Tạo ra một phân vùng mạng riêng biệt cho tài nguyên của bạn.
        * Amazon Route 53: Hệ thống phân giải tên miền (DNS) giúp điều hướng người dùng đến ứng dụng của bạn.
    * Database (Cơ sở dữ liệu - "Trí nhớ")
        * Amazon RDS (Relational Database Service): Dành cho dữ liệu có cấu trúc (MySQL, PostgreSQL, SQL Server).
        * Amazon DynamoDB: Dành cho dữ liệu phi cấu trúc, cần tốc độ cực nhanh và quy mô lớn.

* **AWS IAM (Identity and Access Management)**
    * Các khái niệm cốt lõi (The Big Four)
        * IAM Users: Đại diện cho con người hoặc một ứng dụng. Mỗi User có một bộ thông tin xác thực riêng (Mật khẩu hoặc Access Key).
        * IAM Groups: Tập hợp các User. Thay vì cấp quyền cho 10 kỹ sư, bạn tạo nhóm Developers và cấp quyền cho nhóm đó.
        * IAM Policies (Chính sách): Là một file JSON định nghĩa quyền hạn.
            * Managed Policies: Do AWS tạo sẵn (ví dụ: AdministratorAccess).
            * Customer Managed Policies: Do bạn tự viết để tùy chỉnh quyền.
        * IAM Roles: Giống như một "chiếc mũ" quyền lực. Một dịch vụ (như EC2) có thể "đội" chiếc mũ này để có quyền truy cập vào S3 mà không cần lưu trữ mật khẩu bên trong máy chủ.
    * Các nguyên tắc bảo mật "Kinh điển"
        * Principle of Least Privilege (Đặc quyền tối thiểu): Luôn bắt đầu bằng việc không cho phép gì cả (Deny all), sau đó chỉ cấp đúng những quyền cần thiết để hoàn thành công việc.
        * Shared Responsibility Model (Mô hình trách nhiệm chung):
            * AWS chịu trách nhiệm: Bảo mật "Của" đám mây (Hạ tầng vật lý, trung tâm dữ liệu).
            * Khách hàng chịu trách nhiệm: Bảo mật "Trong" đám mây (Dữ liệu, Cấu hình IAM, Hệ điều hành của EC2).
* **Quy trình làm việc an toàn (Best Practices)**
    * Dựa trên lý thuyết, quy trình chuẩn khi làm việc với AWS là:
        * Khóa tài khoản Root (chỉ dùng khi thực sự cần thiết).
        * Tạo IAM User cho bản thân và gán vào nhóm Admin.
        * Bật MFA cho tất cả các tài khoản.
        * Sử dụng Roles thay vì Access Keys bất cứ khi nào có thể để tránh lộ thông tin xác thực.

* **Tạo Admin Group:**
    * Tạo người dùng mới, thiết lập mật khẩu tùy chỉnh.
    * Thêm người dùng vào nhóm `admin` để kế thừa quyền hạn.
    * Truy cập AWS Management Console tại AWS Web Service page
    * Nhấn vào tên tài khoản AWS của bạn ở góc trên bên phải và chọn Security Credentials
    * ![Minh chứng: AWS Management Console](/images/1-Worklog/1.1-Week1/Day3/AWS_Management_Console.png)
    * Sử dụng thanh tìm kiếm (Search bar) trên AWS Management Console
    * Nhập “IAM”
    * Chọn dịch vụ IAM từ kết quả tìm kiếm
    * ![Minh chứng: Tìm kiếm IAM](/images/1-Worklog/1.1-Week1/Day3/Search_bar.png)
    * Trong thanh điều hướng bên trái (navigation pane), chọn User Groups và nhấn Create Group
    * ![Minh chứng: Tạo nhóm](/images/1-Worklog/1.1-Week1/Day3/Create_Group.png)
    * Tại mục Name the group, nhập tên group (ví dụ: AdminGroup)
    * ![Minh chứng: Đặt tên](/images/1-Worklog/1.1-Week1/Day3/Name_the_group.png)
    * Tìm kiếm AdministratorAccess
    * Chọn policy AdministratorAccess từ danh sách
    * Nhấn Create Group
    * ![Minh chứng: Attach permissions policies](/images/1-Worklog/1.1-Week1/Day3/Attach_permissions_policies.png)
    * Xác nhận việc tạo Admin Group đã hoàn tất thành công
    * ![Minh chứng: Tạo Admin Group thành công](/images/1-Worklog/1.1-Week1/Day3/Admin_group_created.png)

* **Tạo Admin User:**
    * Tạo người dùng mới, thiết lập mật khẩu tùy chỉnh.
    * Thêm người dùng vào nhóm `admin` để kế thừa quyền hạn.
    * ![Minh chứng: Tạo Admin User](/images/1-Worklog/1.1-Week1/Day3/Create_Admin_User.png)
    * ![Minh chứng: User details](/images/1-Worklog/1.1-Week1/Day3/Specify_user_details_1.png)
    * ![Minh chứng: User details](/images/1-Worklog/1.1-Week1/Day3/Specify_user_details_2.png)
    * ![Minh chứng: Permissions Options](/images/1-Worklog/1.1-Week1/Day3/Set_permissions.png)
    * ![Minh chứng: Review and create](/images/1-Worklog/1.1-Week1/Day3/Review_and_create.png)
    * ![Minh chứng: Retrieve pasword](/images/1-Worklog/1.1-Week1/Day3/Retrieve_pasword.png)
    * ![Minh chứng: Tải file .csv](/images/1-Worklog/1.1-Week1/Day3/Dowload_csv_file.png)
    * ![Minh chứng: Tạo Admin User thành công](/images/1-Worklog/1.1-Week1/Day3/Create_adminuser_success.png)

* **Đăng nhập và Kiểm tra:**
    * Sử dụng đường dẫn đăng nhập dành riêng cho IAM User để kiểm tra quyền hạn thực tế.
    * Mở URL đăng nhập đã lưu từ bước tạo user
    * Hoặc truy cập IAM Dashboard để lấy URL đăng nhập
    * ![Minh chứng: Truy cập URL](/images/1-Worklog/1.1-Week1/Day3/Truy_cập_URL.png)
    * Mở cửa sổ trình duyệt ẩn danh (Incognito/Private)
    * ![Minh chứng: Incognito/Private](/images/1-Worklog/1.1-Week1/Day3/Đăng_nhập_ẩn_danh.png)
    * Nhập Account ID hoặc alias (nếu có)
    * Nhập IAM Username
    * Nhập mật khẩu tạm thời từ file .csv
    * Làm theo hướng dẫn để đổi mật khẩu
    * ![Minh chứng: Đổi mật khẩu](/images/1-Worklog/1.1-Week1/Day3/Thay_đổi_mật_khẩu.png)
    * Xác nhận đăng nhập thành công
    * ![Minh chứng: Đăng nhập Admin User thành công](/images/1-Worklog/1.1-Week1/Day3/Đăng_nhập_thành_công.png)
    * Kiểm tra quyền Administrator
    * ![Minh chứng: Kiểm tra quyền Admin](/images/1-Worklog/1.1-Week1/Day3/Kiểm_tra_quyền.png)

* **Tạo Admin Role:**
    * Thiết lập Role với thực thể tin cậy (Trusted Entity) là chính tài khoản AWS hiện tại.
    * Gán quyền `AdministratorAccess` cho Role này.
    * Truy cập AWS Management Console và mở dịch vụ IAM
    * Trong thanh điều hướng bên trái, chọn Roles và nhấn Create role
    * ![Minh chứng: Khởi tạo Role](/images/1-Worklog/1.1-Week1/Day3/Create_role.png)
    * Chọn AWS account
    * Tùy chọn này cho phép role được sử dụng trong tài khoản AWS hiện tại hoặc tài khoản khác
    * ![Minh chứng: Select trusted entity](/images/1-Worklog/1.1-Week1/Day3/Select_trusted_entity.png)
    * Chọn Another AWS account
    * Nhập Account ID của tài khoản AWS hiện tại
    * Để xem Account ID, nhấp vào tên tài khoản ở góc trên bên phải
    * Nhấn Next
    * Tìm kiếm và chọn policy AdministratorAccess
    * Policy này cấp toàn quyền quản trị tài khoản AWS
    * Nhấn Next
    * ![Minh chứng: Add permissions](/images/1-Worklog/1.1-Week1/Day3/Add_permissions.png)
    * Nhập tên role (ví dụ: AdminRole)
    * Thêm mô tả chi tiết về mục đích sử dụng của role
    * ![Minh chứng:Role name](/images/1-Worklog/1.1-Week1/Day3/Role_name.png)
    * Xem lại cấu hình và nhấn Create role
    * ![Minh chứng: Add tag](/images/1-Worklog/1.1-Week1/Day3/Add_tag.png)
    * Xác nhận việc tạo role thành công
    * ![Minh chứng: Tạo Role thành công](/images/1-Worklog/1.1-Week1/Day3/Tạo_role_thành_công.png)
    * Kiểm tra thông tin chi tiết của role vừa tạo
    * ![Minh chứng: Xem thông tin Role](/images/1-Worklog/1.1-Week1/Day3/Kiểm_tra_role.png)

* **Tạo Operator User:**
    * Tạo một người dùng mới (ví dụ: `OperatorUser`) nhưng **không** gán quyền hạn trực tiếp nào.
    * Truy cập dịch vụ IAM thông qua thanh tìm kiếm
    * Nhập “IAM” và chọn dịch vụ từ kết quả
    * ![Minh chứng: Tìm kiếm IAM](/images/1-Worklog/1.1-Week1/Day3/Search_bar.png)
    * Chọn Users từ menu bên trái
    * Nhấn Add Users
    * ![Minh chứng: Tạo Operator User](/images/1-Worklog/1.1-Week1/Day3/Create_Admin_User.png)
    * Nhập tên user: OperatorUser
    * Chọn Provide user access to the AWS Management Console
    * Chọn I want to create an IAM user
    * Thiết lập mật khẩu:
        * Chọn Autogenerated password hoặc
        * Chọn Custom password để tự đặt mật khẩu
    * Bỏ chọn Users must create a new password at next sign-in
    * ![Minh chứng: Thông tin User](/images/1-Worklog/1.1-Week1/Day3/thông_tin_User.png)
    * Nhấn Next để tiếp tục
    * ![Minh chứng: Bỏ qua permission](/images/1-Worklog/1.1-Week1/Day3/Pass_permission.png)
    * Thêm các tags để phân loại và quản lý user
    * Ví dụ: Department = Operations, Environment = Production
    * Xem lại cấu hình và nhấn Create user
    * ![Minh chứng: Bỏ qua tag](/images/1-Worklog/1.1-Week1/Day3/Pass_add_tag.png)
    * Lưu trữ thông tin đăng nhập an toàn
    * Chuẩn bị cho việc cấu hình assume role
    * ![Minh chứng: Tạo OperatorUser thành công](/images/1-Worklog/1.1-Week1/Day3/Tạo_OperatorUser_thành_công.png)
    * Thiết lập MFA ngay sau khi tạo user
    * Lưu URL đăng nhập console vào bookmark
    * Chuẩn bị hướng dẫn assume role cho người dùng

* **Cho phép OperatorUser switch role**
    * **Khởi tạo Admin Role:** Tạo một IAM Role với chính sách `AdministratorAccess`, thiết lập thực thể tin cậy (Trust Entity) là chính tài khoản AWS đang sử dụng.
    * **Tạo OperatorUser:** Khởi tạo người dùng vận hành ban đầu không có quyền hạn. Sau đó, gắn một **Inline Policy** cho phép hành động `sts:AssumeRole` trỏ đến ARN của Admin Role đã tạo.
    * Click Users.
    * Click OperatorUser.
    * ![Minh chứng: Chọn Role](/images/1-Worklog/1.1-Week1/Day3/Chọn_role.png)
    * Click Add inline policy.
    * ![Minh chứng: Create inline policy](/images/1-Worklog/1.1-Week1/Day3/Add_inline_policy.png)
    * Điền vào nội dung policy dưới đây, nhớ thay thế bằng account ID mà bạn đang sử dụng và trước đó bạn đã tạo role AdminRole.
    * Policy này cho phép IAM User có thể đảm nhận role AdminRole nằm trong account ID mà bạn chỉ định.
    * Click Review Policy.
    * ![Minh chứng: Policy editor](/images/1-Worklog/1.1-Week1/Day3/Policy_editor.png)
    * Đặt tên cho inline policy là AllowSwitchAdminPolicy.
    * Click Create Policy.
    * ![Minh chứng: Create Policy](/images/1-Worklog/1.1-Week1/Day3/Create_Policy.png)

* **Đăng nhập OperatorUser**
    * Thực hiện đăng nhập vào Console bằng tài khoản `OperatorUser`. Tại thời điểm này, User không có quyền truy cập các dịch vụ như S3 hay Billing.
    * Trong tab Security credentials của OperatorUser
    * Copy đường dẫn đăng nhập console dành riêng cho tài khoản AWS của bạn
    * ![Minh chứng: Vào OperatorUser](/images/1-Worklog/1.1-Week1/Day3/Vào_operatoruser.png)
    * Mở cửa sổ trình duyệt mới
    * Dán URL đăng nhập vào thanh địa chỉ
    * Nhập thông tin đăng nhập:
        * IAM user name: OperatorUser
        * Password đã được cấp
    * Nhấn Sign in
    * ![Minh chứng: Đăng nhập OperatorUser](/images/1-Worklog/1.1-Week1/Day3/Đn_role_operator.png)
    * Truy cập thử dịch vụ IAM
    * Bạn sẽ thấy thông báo không có quyền truy cập
    * Điều này xác nhận OperatorUser chưa có quyền trực tiếp với các dịch vụ AWS
    * ![Minh chứng: Xem trạng thái](/images/1-Worklog/1.1-Week1/Day3/Xác_nhận_trạng_thái.png)

* **Chuyển đổi role (Switch Role)**
    * Sử dụng tính năng **Switch Role** trên thanh menu người dùng, nhập Account ID và Role Name (`AdminRole`).
    * Sau khi chuyển đổi thành công, định danh người dùng thay đổi và tài khoản có đầy đủ quyền quản trị để thao tác.
    * Click vào tên OperatorUser ở góc trên bên phải
    * Chọn Switch Roles
    * ![Minh chứng: Thao tác Switch Role](/images/1-Worklog/1.1-Week1/Day3/Switch_role.png)
    * Account: Nhập AWS Account ID của bạn
    * Role: Nhập AdminRole đã tạo trước đó
    * Color: Chọn màu để phân biệt role (tùy chọn)
    * Click Switch Role để xác nhận
    * ![Minh chứng: Thông tin chuyển role](/images/1-Worklog/1.1-Week1/Day3/Thông_tin_chuyển_role.png)
    * Tên role hiển thị sẽ chuyển thành AdminRole
    * Có thể quay lại OperatorUser bằng cách click Switch back
    * Bạn đã có đầy đủ quyền AdministratorAccess
    * ![Minh chứng: Thành công chuyển role](/images/1-Worklog/1.1-Week1/Day3/Chuyển_role_thành_công.png)

* **Dọn dẹp tài nguyên (Cleanup)**
    * Sau khi hoàn thành bài thực hành, tôi đã tiến hành xóa bỏ các IAM Users, Groups và Roles để đảm bảo an toàn bảo mật và duy trì tài khoản sạch.
    * Truy cập AWS Management Console
    * Điều hướng đến dịch vụ IAM
    * Chọn mục Users
    * Chọn user liên quan đến bài lab
    * Click Delete
    * ![Minh chứng: Xóa IAM User](/images/1-Worklog/1.1-Week1/Day3/Xóa_IAM_User.png)
    * Kiểm tra kỹ thông tin user sẽ xóa
    * Nhập tên user để xác nhận
    * Click Delete để hoàn tất
    * ![Minh chứng: Xác nhận xóa IAM User](/images/1-Worklog/1.1-Week1/Day3/Xác_nhận_xóa_IAM_User.png)
    * Quay lại dịch vụ IAM
    * Chọn mục User groups
    * Chọn group liên quan đến bài lab
    * Click Delete
    * ![Minh chứng: Xóa IAM User Group](/images/1-Worklog/1.1-Week1/Day3/Xóa_IAM_User_Group.png)
    * Kiểm tra kỹ thông tin group sẽ xóa
    * Click Delete để hoàn tất
    * ![Minh chứng: Xác nhận xóa IAM User Group](/images/1-Worklog/1.1-Week1/Day3/Xác_nhận_xóa_IAM_User_Group.png)

## Thứ 4: Hạ tầng Mạng Chuyên sâu AMAZON VPC

### Tổng quan về Amazon VPC
**Amazon Virtual Private Cloud (VPC)** là một mạng ảo dành riêng cho tài khoản AWS của bạn. Nó cho phép bạn khởi tạo các tài nguyên AWS trong một mạng ảo được cách ly logic, mang lại sự kiểm soát toàn diện đối với môi trường mạng.

* **Đặc điểm cốt lõi:**
    * **Tính cách ly:** Hoàn toàn tách biệt với các mạng ảo khác trên hạ tầng AWS.
    * **Phạm vi (Scope):** Một VPC bao phủ toàn bộ một **Region** nhưng được chia nhỏ vào các **Availability Zones (AZs)** thông qua Subnets.
    * **Quyền kiểm soát:** Tự định nghĩa dải IP, bảng định tuyến (Route Tables), và thiết lập các tầng bảo mật (Security Groups/NACLs).

### Các thành phần cấu tạo chính
* **CIDR Block & Địa chỉ IP**
    * VPC sử dụng phương pháp **CIDR** để xác định dải địa chỉ IP.
    * **VPC CIDR:** Thường dùng dải `/16` (65,536 IP) để tối ưu khả năng mở rộng.
    * **Subnet CIDR:** Chia nhỏ từ VPC CIDR (thường dùng `/24` - 256 IP).
    * **5 IP dành riêng của AWS:**
        * `.0`: Network address.
        * `.1`: VPC Router (Cổng mặc định).
        * `.2`: Amazon Provided DNS.
        * `.3`: Dành riêng cho mục đích tương lai.
        * `.255`: Network broadcast address (mặc dù VPC không hỗ trợ broadcast).

* **Subnets (Phân vùng mạng)**
    * **Public Subnet:** Có Route trỏ đến **Internet Gateway (IGW)**. Chứa các tài nguyên cần giao tiếp trực tiếp với Internet (Web Server, NAT Gateway).
    * **Private Subnet:** Không có Route đến IGW. Chứa các tài nguyên cần bảo mật cao (Database, Backend App).

* **Điều phối luồng dữ liệu (Routing)**
    * **Internet Gateway (IGW):** Cổng kết nối VPC với Internet. Là đối tượng cần thiết để các Public Subnet có thể "ra ngoài".
    * **Route Table:** Chứa tập hợp các quy tắc định tuyến. 
        * *Local Route:* Cho phép các tài nguyên trong cùng một VPC nói chuyện với nhau.
        * *Public Route:* `0.0.0.0/0 -> IGW`.
    * **NAT Gateway:** Thiết bị đặt tại Public Subnet giúp tài nguyên ở Private Subnet truy cập Internet (để cập nhật patch, tải thư viện) nhưng ngăn chặn Internet truy cập ngược vào.

### Bảo mật đa lớp (Security Layers)
* **Hệ thống bảo mật của VPC hoạt động dựa trên hai lớp tường lửa chính:**
    * **Security Groups (Cấp độ Instance)**
    * Hoạt động như tường lửa cho máy chủ (EC2).
    * **Stateful:** Nếu bạn cho phép lưu lượng vào (Inbound), lưu lượng phản hồi (Outbound) tự động được cho phép.
    * Chỉ hỗ trợ luật **Allow**.

    * **Network ACLs (Cấp độ Subnet)**
    * Hoạt động như tường lửa cho toàn bộ phân vùng (Subnet).
    * **Stateless:** Phải cấu hình tường minh cả chiều vào (Inbound) và chiều ra (Outbound).
    * Hỗ trợ cả luật **Allow** và **Deny**.

### Tư duy thiết kế High Availability (HA)
* **Để đảm bảo hệ thống không bị gián đoạn khi một trung tâm dữ liệu gặp sự cố:**
    * Triển khai tài nguyên trên ít nhất **2 Availability Zones**.
    * Tại mỗi AZ, thiết lập các cặp Public/Private Subnet tương ứng.
    * Sử dụng các dịch vụ có tính sẵn sàng cao của AWS như **ELB (Elastic Load Balancing)** để điều phối lưu lượng.

## Thứ 5: 
* **Introduction to AWS:**
    * Giới thiệu về dịch vụ mới và sự xuất hiện của agent AI trong học tập và công việc
    * **Cloud Computing**
        * Cloud Computing là cách chúng ta cung cấp dịch vụ về IT thông qua internet với mô hình "Sài bao nhiêu tính bấy nhiêu"

        * **Sự khác biệt giữa mô hình truyền thống và hiện đại:**
            * **Truyền thống (On-premises):**
                * Muốn xây dựng hệ thống, sản phẩm hay dịch vụ cho rất nhiều người sử dụng cần phải xây dựng hạ tầng ở môi trường on-premises, hạ tầng trung tâm dữ liệu, in house, tức là mỗi doanh nghiệp tự xây khu trung tâm dữ liệu, phải mua sắm các thiết bị phần cứng, đầu tư trung tâm dữ liệu với chi phí rất lớn.
                * Nếu dự án, sản phẩm, dịch vụ đó ko thành công thì chi phí sau thất bại rất cao

            * **Hiện đại (Cloud):**
                * Còn điện toán đám mây hiểu đơn giản là đi thuê tài nguyên thay vì mua đứt 1 căn nhà thì có thể thuê các phòng khách sạn chẳng hạn, mô hình tính phí sẽ là "Pay as you go"

        * **Lợi ích**
            * Tối ưu chi phí: Loại bỏ chi phí duy trì phần cứng không cần thiết
            * Tốc độ & Linh hoạt: Triển khai tài nguyên chỉ trong vài phút
            * Tính bảo mật & AI: Tận dụng các công cụ bảo mật và trí tuệ nhân tạo có sẵn từ nhà cung cấp
            * Quy mô toàn cầu: Khả năng mở rộng ứng dụng để phục vụ khách hàng trên khắp thế giới dễ dàng

    * **AWS global infrastructure**
        * **AWS Data Center**
            * Tập trung toàn bộ thiết bị, phần cứng của AWS với quy mô cực lớn lên tới hàng chục ngàn máy chủ
            * Toàn bộ thiết bị của AWS ở trong AWS data center đều được customiz dựa trên tiêu chuẩn vận hành của AWS
            * Bo mạnh chủ, máy chủ, hệ thống network, hệ thống bảo mật, những dòng GPU cũng được AWS thiết kế

        * **Availability Zone (AZ)**
            * Bao gồm 1 hoặc nhiều trung tâm dữ liệu của AWS
            * Được thiết kế để đảm bảo nếu có sự cố xảy ra thì sẽ không ảnh hưởng 2 AZ đồng thời gọi lại fault isolation
            * Các sự cố: sự cố về điện, thiên tai
            * Khoảng cách giữa 2 AZ đủ lớn để tránh những cái sự cố xảy ra ảnh hưỡng đồng thời giữa 2 AZ
            * Về hệ thống điện năng hệ thống về mạng cũng được thiết kế độc lập ở mức cao nhất
            * Tiêu chuẩn thiết kế trung tâm dữ liệu , tiêu chuẩn thiết kế AG Region của AWS là ở mức cao nhất, cao hơn tiêu chuẩn chung của industry

        * **Region**
            * 1 Region tối thiểu là 3 AZ, một số có nhiều hơn 3 AZ
            * Tất cả các Region được kết nối với nhau thông qua mạng backbond của AWS
            * Những dữ liệu, dịch vụ không phụ thuộc lẫn nhau giữa các Region
            * Một số dịch vụ được thiết kế ở global scale nhu dịch vụ DNS sẽ nằm ngoài Region

        * **Edge Locations (POP)**
            * Những trung tâm dữ liệu mạng bin Edge Location
            * Là một mạng lưới, những cái trung tâm dữ liệu được sử dụng để cung cấp các dịch vụ bin
            * Dịch vụ bin phổ biến: 
                * CloudFront (CDN) đóng vai trò là content delivery network CDN, caching các dữ liệu mà khác hàng thường xuyên truy cập tới
                * Web Application Firewall (WAF) tường lửa cho những ứng dụng web
                * Route 53(DNS Service) có thể host domain, phân giải domain và hỗ trợ phân giải những domain public lần domain trong môi trường private
                
        * **Local Zone**
            * Giống như 1 phiên bản nhỏ hơn của Availability Zone của AG

* **Management Console:**
    * **Root Login**
        * Chúng ta có thể đăng nhập bằng tài khoản người dùng root hoặc bằng tài khoản người dùng IAM (một tài khoản người dùng phụ giúp quản lý việc xuất tài nguyên AWS)

    * **IAM User Login**
        * Khi đăng nhập bằng tài khoản IAM, chúng ta cần cung cấp thêm thông tin ID tài khoản (chuỗi 12 chữ số) để xác định tài khoản AWS

    * **Service Search**
        * Sau khi đăng nhập vào giao diện Bảng điều khiển quản trị AWS, chúng ta có thể tìm kiếm các dịch vụ AWS
        * Mỗi dịch vụ sẽ có hệ thống quản lý trang web riêng, cho phép chúng ta truy cập các tính năng của dịch vụ đó
    
    * **Support Center**
        * Ở bên trái là menu Hỗ trợ, người dùng có thể vào Trung tâm Hỗ trợ để tạo yêu cầu hỗ trợ và nhận được sự trợ giúp từ nhóm AWS
    
    * **AWS Command Line Interface (CLI)**
        * Giao diện dòng lệnh AWS (AWS CLI) là một công cụ lập trình mã nguồn mở cho phép bạn tương tác với các dịch vụ AWS bằng các lệnh
        * AWS CLI cho phép bạn chạy các chức năng phát triển lệnh tương thích với các chức năng được cung cấp bởi Bảng điều khiển quản lý AWS dựa trên trình duyệt
    
    * **AWS SDK**
        * AWS SDK đơn giản hóa việc sử dụng các dịch vụ AWS cho các ứng dụng bằng cách cung cấp một thư viện hàng đầu, quen thuộc với các nhóm phát triển ứng dụng.
        * AWS SDK hỗ trợ các tác vụ quản lý vòng đời API cho các dịch vụ AWS như quản lý thông tin xác thực, thử lại, xử lý dữ liệu, tuần tự hóa và giải tuần tự hóa.