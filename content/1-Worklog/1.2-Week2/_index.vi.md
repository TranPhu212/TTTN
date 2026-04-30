---
title: "Worklog Tuần 2"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.2. </b> "
---
{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}


### Mục tiêu tuần 2:

* Kết nối, làm quen với các thành viên trong First Cloud Journey.
* Hiểu dịch vụ AWS cơ bản, cách dùng console & CLI.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
|  6  | - Phát triển phần mềm bằng Agentic AI (Kiro) & Tối ưu chi phí AWS | 24/04/2026 | 24/04/2026 | <https://www.youtube.com/watch?v=uAQCm4sm_1c&t=2s> <br> <https://www.youtube.com/watch?v=UIw8UxGZCHA&t=3s> |
|  2  | - Quản trị Mạng chuyên sâu (VPC), Kết nối Hybrid & Cân bằng tải (ELB) | 27/04/2026 | 27/04/2026 | <https://youtu.be/O9Ac_vGHquM> <br> <https://youtu.be/BPuD1l2hEQ4> <br> <https://youtu.be/CXU8D3kyxIc> |
|  3  | - AWS Compute: EC2, Storage & Auto Scaling | 28/04/2026 | 28/04/2026 | <https://youtu.be/-t5h4N6vfBs> <br> <https://youtu.be/e7XeKdOVq40> <br> <https://youtu.be/yAR6QRT3N1k> <br> <https://youtu.be/hKr_TfGP7NY> <br> <https://youtu.be/6IHNDJ85aoQ> <br> <https://youtu.be/_v_43Wi7zjo> <br> <https://youtu.be/Ew3QRaKJQSA> <br> <https://youtu.be/bbLcPitXJSY> |

### Kết quả đạt được tuần 2:

## Thứ 6: Gen AI trên AWS & Tối ưu hóa chi phí với Kiro

### Gen AI on AWS - Kiro
  * **Agentic changing the SDLC**
    * Sự trỗi dậy của Trí tuệ nhân tạo tác động (Agentic AI) trong phát triển phần mềm đang làm thay đổi cách các nhà phát triển tiếp cận công việc của họ. Chúng ta đã chuyển từ việc hỗ trợ tạo mã cho từng tác vụ cụ thể, sang phát triển tính năng hoặc ứng dụng hoàn chỉnh dựa trên AI từ đầu đến cuối
    * Thời điểm 2024, đóng vai trò là người hỗ trợ giúp cho lập trình viên phát triển ứng dụng nhanh hơn
    * Tới 2025, có các khái niệm về các agent, các agent cho thể đưa cho AI, đưa cho các AI agent những cái task phức tạp hơn để agent có thể làm việc end-to-end chứ ko đơn thuần là hoàn tất code hoặc đoán xem sẽ viết code gì nữa mà sẽ làm những cái tác vụ phức tạp hơn có bên trong đó
    * Tới thời điểm hiện tại (2026), có khái niệm về autonomous, những agent tự động hoàn toàn, có thể làm việc end-to-end và làm việc với nhau được không cần con người can thiệp

  * **Spec-driven development**
    * **Challenge with AI Development**
      * Các công cụ lập trình AI hoạt động xuất sắc trong các tác vụ nhỏ nhưng có thể thất bại với các dự án phức tạp
      * Các công cụ hiện có gây khó khăn trong việc cộng tác và quản lý các tác nhân
      * Việc đưa một dự án từ giai đoạn chứng minh ý tưởng đến sản xuất trong khi vẫn duy trì kiểm soát chất lượng ngày càng trở nên khó khăn

    * **Spec Driven Development**
      * Lập trình theo cảm hứng tạo ra bản mẫu, trong khi các phương pháp phát triển phần mềm truyền thống tạo ra sản phẩm hoàn chỉnh
      * Với cái việc sử dụng AI agent, những công cụ AI coding tool thì nó cũng sẽ gặp những trở ngại nhất định là đối với dự án quy mô nhỏ thì công cụ AI làm rất là tốt. Khi mà cái quy mô dự án  phức tạp  thì sử dụng công cụ AI một cách đơn thuần tức là tương tác với nó thì nó sẽ rất khó để quản lý và dễ gây tới fail dự án
      * Ngoài ra, nếu có nhiều agent hoặc muốn collaborate, muốn phối hợp với nhiều người thì những công cụ đó hiện tại cũng khá khó khăn
      * Việc 1 cái project đang ở cái mô hình là BOC, tức là những cái MVP, những cái minimum viable product, những sản phẩm nhỏ build ra để thể hiện tính khả thi về kỹ thuật mà muốn đưa lên production cũng sẽ trải qua rất là nhiều yêu cầu khó khăn khác, những yêu cầu chi tiết hơn chứ ko phải là sản phẩm chạy được, demo được thì đưa lên môi trường production, giữa 2 cái đó thì phải làm thêm nhiều việc khác nữa mới dẫn tới một việc đó là spec-driven development
      * Spec-driven development có ý nghĩa là phải đưa ra những mô tả chi tiết, chuẩn bị những requiment, những mô tả chi tiết trước khi bắt tay vào code
      * Với công cụ AI coding tool cũng vậy, cũng sẽ có mô tả chi tiết về những yêu cầu của cái ứng dụng xây dựng nên
      * Để xây dụng được cái ứng dụng thì phải trải qua từng bước thiết lập kế hoạch, về triển khai, về implementation, về testing, về deployment, gom lại thành một cái gọi là spec thì nó sẽ giúp cho mình có thể xây dựng  ra được những cái sản phẩm phức tạp hơn

  * **Kiro**
    * Môi trường phát triển tích hợp (IDE) dành cho AI, từ nguyên mẫu đến sản phẩm hoàn chỉnh. Kiro giúp bạn làm việc hiệu quả nhất bằng cách tạo cấu trúc cho việc lập trình AI thông qua phát triển dựa trên đặc tả kỹ thuật

    * **Kiro IDE**
      * Được xây dựng để có thể phát triển  được những ứng dụng  từ mức prototype cho tới môi trường production
      * Số lượng Pro Kiro user VN cũng đã hơn 2000
      * Giúp xây dựng được những cái ứng dụng AI leverage GPC Riven Development
      * Khi sử dụng Kiro sẽ có 2 hình thức:
        * Dạng vibe coding: thuần túy tương tác với Kiro thông qua ngôn ngữ tự nhiên. Ví dụ yêu cầu Kiro xây dựng  một cái ứng dụng  ghi chú, lập kế hoạch, ứng dụng quản lý chi tiêu, ... xây dựng dựa trên nền tảng  ngôn ngữ là Python Web, Python Flux, Kiro sẽ tự động xây, tự động plan
        * Kiro Spec-driven: Đối với  những cái ứng dụng  cần phức tạp hơn, cần chi tiết hơn, cần xem những cái yêu cầu có rõ ràng hay không, có đúng theo nhu cầu thực tế hay không. Không tương tác với Kiro bằng chat, bằng vibe ngay từ đầu. Kiro chuyển yêu cầu của bạn thành các yêu cầu rõ ràng, thiết kế hệ thống và các nhiệm vụ riêng biệt. Cùng Kiro cải tiến đặc tả và kiến ​​trúc hệ thống của bạn. Các tác nhân Kiro sẽ triển khai đặc tả trong khi vẫn cho phép bạn kiểm soát mọi thứ
    
    * **Kiro IDE - Agent Hook**
      * Giao nhiệm vụ cho các tác nhân AI được kích hoạt bởi các sự kiện như 'file save'
      * Các tác nhân tự động thực thi trong nền dựa trên các lời nhắc được xác định trước của bạn
      * Các hook tác nhân giúp bạn mở rộng quy mô công việc bằng cách tạo tài liệu, kiểm thử đơn vị hoặc tối ưu hóa hiệu suất mã
    
    * **Kiro IDE - Advenced Context Management**
      * Kết nối với tài liệu, cơ sở dữ liệu, API và nhiều hơn nữa với tích hợp MCP gốc
      * Cấu hình cách bạn muốn các tác nhân Kiro tương tác với từng dự án thông qua các tệp điều khiển
      * Chỉ cần kéo thả hình ảnh thiết kế giao diện người dùng của bạn, hoặc ảnh chụp buổi phác thảo kiến ​​trúc trên bảng trắng Kiro có thể sử dụng chúng để hướng dẫn quá trình triển khai
    
    * **Kiro IDE – Timeline Checkpointing**
      * Quay lại các điểm hiện có trong nhật ký thực thi
      * Mạng lưới an toàn để thử nghiệm nhiều cách tiếp cận khác nhau cho một vấn đề
      * Chụp lại nội dung của từng tệp đã sửa đổi và khôi phục bản chụp đó khi quay trở lại điểm kiểm tra

    * **Kiro Spec Correctness – Property Based Testing (PBT)**
      * **The Problem with Traditional Testing**
        * Kiểm thử đơn vị (Unit tests) chỉ xác thực các ví dụ cụ thể — chúng bị giới hạn bởi trí tưởng tượng của người kiểm thử. Khi AI viết cả mã nguồn và các bài kiểm thử, không có gì đảm bảo mã đó khớp với yêu cầu thực tế
        
      * **What is Property-Based Testing (PBT)?**
        * Thay vì kiểm tra từng ví dụ riêng lẻ, PBT xác thực các thuộc tính phổ quát — những quy tắc phải luôn đúng trên hàng trăm hoặc hàng nghìn dữ liệu đầu vào được tạo ngẫu nhiên. Nó chuyển câu hỏi từ "ví dụ này có chạy không?" thành "mã này có luôn hoạt động đúng hay không?"

      * **How Kiro Implements PBT**
        * Kiro đọc tài liệu yêu cầu của bạn (được viết dưới định dạng **EARS**), trích xuất các thuộc tính chính xác có thể kiểm thử, tạo ra hàng trăm trường hợp kiểm thử và chạy chúng để phát hiện các trường hợp biên và lỗi

      * **When Does Kiro Run PBT?**
        * Theo yêu cầu (On demand): Được kích hoạt thủ công sau khi tạo mã
        * Tự động qua Agent Hooks: Khi lưu, tạo hoặc xóa tệp
        * Trong quá trình thực thi nhiệm vụ: Khi các Agent (tác nhân AI) triển khai từng thành phần
      
      * **Kiro CLI – AI-Powered Development in Your Terminal**
        * Đưa khả năng của các tác nhân AI (AI agents) từ Kiro trực tiếp vào dòng lệnh
        * Xây dựng tính năng, tự động hóa quy trình, phân tích lỗi và truy vết bug — tất cả bằng ngôn ngữ tự nhiên
        * Đọc/ghi tệp, gọi API, chạy lệnh bash và tương tác với các công cụ MCP
        * Tác nhân tùy chỉnh (Custom agents): xác định công cụ, quyền hạn và ngữ cảnh cho các tác vụ cụ thể
        * Tích hợp MCP: kết nối với các hệ thống bên ngoài (OpenSearch, Slack, các công cụ nội bộ, v.v.)
        * Chia sẻ cùng tệp điều hướng (steering files) và cấu hình MCP với Kiro IDE — đảm bảo tính nhất quán trên mọi môi trường
      
      * **Kiro CLI – Custom Agents**
        * Các tác nhân AI được cấu hình sẵn, tối ưu riêng cho các nhiệm vụ hoặc quy trình làm việc cụ thể
        * Xác định các công cụ, quyền hạn và ngữ cảnh mà mỗi tác nhân được phép tiếp cận
        * Loại bỏ việc thiết lập lặp đi lặp lại
        
        * **Custom Agents Benefit**
          * Các tác nhân tùy chỉnh chỉ tải những gì thực sự cần thiết
          * Tối ưu hóa việc sử dụng cửa sổ ngữ cảnh (context window) -> hiệu suất tốt hơn, ít nhiễu hơn
          * Cho phép sự nhất quán trong toàn bộ đội ngũ làm việc
        
      * **Kiro Powers**
        * Một gói hợp nhất: Công cụ MCP + tệp điều hướng + hooks — được tải động, không gây tiêu tốn tài nguyên ngữ cảnh cơ sở
        * Cơ chế chia sẻ sức mạnh với cộng đồng

      * **Kiro Autonomous Agent**
        * Mô tả thay đổi bạn cần và thực thi tối đa 10 tác vụ đồng thời. Hệ thống sẽ tự động tìm cách để thực hiện các tác vụ đó một cách độc lập
        * Tác nhân tự hành Kiro đảm nhận các công việc tốn thời gian và nặng về ngữ cảnh ở chế độ chạy ngầm, từ việc viết tài liệu thiết kế cho đến phát triển các tính năng mới.   

      * **Kiro – Team Governance**
        * Thấu hiểu và theo dõi mức độ sử dụng thông qua các bảng điều khiển (dashboards) nâng cao
        * Quản lý các thiết lập bằng các quyền kiểm soát quản trị
        * Các gói đăng ký có sẵn trong AWS IAM Identity Center

      * **Kiro – Pricing**
        **Truy cập Kiro IDE và CLI chỉ với một gói đăng ký:**
          * **Gói Pro: $20/tháng**
              * 1.000 credits
          * **Gói Pro+: $40/tháng**
              * 2.000 credits
          * **Gói Power: $200/tháng**
              * 10.000 credits
        **Thông tin bổ sung:**
          * Phí sử dụng vượt mức cho các gói trả phí là $0.04 cho mỗi credit bổ sung
          * *Gói Miễn phí (Free Tier) có sẵn với 50 credits mỗi tháng, áp dụng cho đăng nhập qua mạng xã hội

### Cost optimization on AWS
  * Chọn cấu hình tài nguyên tính toán và lưu trữ dữ liệu phù hợp
  * Sử dụng các phương thức thanh toán chiết khấu như: đặt trước (reserved), gói tiết kiệm (savings plans), hoặc phiên bản dư thừa (spot)
  * Xóa các tài nguyên không sử dụng và bật tính năng tự động tắt đối với các tài nguyên không cần chạy 24/7
  * Sử dụng dịch vụ không máy chủ (serverless) hoặc dịch vụ được quản lý hoàn toàn (fully managed)
  * Thiết kế kiến trúc tối ưu (well-architected) nhằm giải quyết các yêu cầu đã đề ra
  * Cài đặt và sử dụng AWS Budget
  * Quản lý chi phí theo bộ phận/ứng dụng bằng các thẻ phân bổ chi phí (cost allocation tags)
  * Liên tục theo dõi và tối ưu hóa chi phí
  * Tạo danh sách kiểm tra (check list) tối ưu hóa chi phí cho [dịch vụ của bạn] bằng cách sử dụng Kiro

  * **AWS Pricing Calculator**
    * Cho phép tạo thông tin ước tính về dịch vụ
    * Các bản ước tính có thể được chia sẻ với người khác
    * Chi phí sẽ thay đổi tùy theo khu vực (region)

  * **Work with AWS Support**
    * **AWS có 4 gói hỗ trợ chính:**
      * Cơ bản - Basic ( Khám phá )
      * Nhà phát triển - Developer ( Thử nghiệm / Phát triển )
      * Doanh nghiệp - Business ( Môi trường vận hành thực tế )
      * Tập đoàn - Enterprise ( Doanh nghiệp quy mô lớn )

    * Gói hỗ trợ có thể được nâng cấp trong thời gian ngắn để có tốc độ phản hồi nhanh hơn khi phát sinh các vấn đề cần xử lý gấp
    
  * **Hands-on**
    * **Create an AWS account**
      * **000001**
        * Tạo tài khoản AWS
        * Thiết lập xác thực đa yếu tố (MFA) cho tài khoản AWS (Root)
        * Quản trị viên tài khoản và nhóm (Account and group admin)
        * Hỗ trợ xác thực tài khoản
  
    * **Bắt đầu với AWS Budgets**
      * **000007**
        * Tạo ngân sách chi phí (expense budget)
        * Tạo ngân sách sử dụng (usage budget)
        * Tạo ngân sách thiết lập sẵn (preset budget)
        * Tạo kế hoạch tiết kiệm ngân sách (budget savings plan)

    * **Kiro Spec Driven Development
      * **000180**
        * Cài đặt Kiro
        * Đăng nhập vào Kiro IDE
        * Xây dựng ứng dụng với Kiro SDD
        * Thực hành với Kiro SDD
        * Giới thiệu về Kiro CLI

    * **Support requests with AWS Support**
      * **000009**
        * Các gói hỗ trợ của AWS
        * Truy cập AWS Support
        * Xử lý các yêu cầu hỗ trợ

  * **Additional research**
    * **AWS Well-Architected Framework**
      * Các khái niệm, nguyên tắc thiết kế và các thực hành kiến trúc tốt nhất để thiết kế và vận hành hệ thống của bạn trên đám mây
      * Chúng ta sử dụng Khung này bằng cách trả lời các câu hỏi, từ đó bạn biết được kiến trúc của mình phù hợp như thế nào với các thực hành tốt nhất được khuyến nghị
      * Ngoài ra, khi sử dụng công cụ tích hợp AWS Well-Architected Framework trên Bảng điều khiển quản trị (AWS Management Console), bạn sẽ nhận được các hướng dẫn để cải thiện kiến trúc hiện tại của mình

## Thứ 2: Networking & Content Delivery trên AWS (Mạng và Truyền tải nội dung)
  * Mạng đám mây riêng ảo của Amazon (VPC)
  * Kết nối ngang hàng VPC & Cổng chuyển tiếp
  * Mạng riêng ảo & Kết nối trực tiếp
  * Cân bằng tải đàn hồi
  * **Amazon Virtual Private Cloud (VPC)**
    * Là một dịch vụ cung cấp môi trường mạnh ảo riêng tư được cô lập về mặt logic khỏi các mạng khác ở trên aws cloud
    * VPC cho phép chúng ta có thể khởi tạo các tài nguyên của aws như máy chủ Ảo cơ sở dữ liệu các thiết bị cân bằng tải trong một cái môi trường Mạng ảo riêng mà chúng ta có quyền kiểm soát hoàn toàn
    * VPC Private cloud ở trên aws hoàn toàn khác biệt với khái niệm về Private cloud truyền thống
    * Private cloud truyền thống được hiểu là các doanh nghiệp họ sẽ xây dựng một hệ thống Ảo hóa tập trung ở môi trường local và on-premises với các tính năng mô phỏng theo tính năng của các nhà cung cấp dịch vụ cloud lớn hay còn gọi là hyperscale cloud provider như aws
    * Amazon Virtual Private Cloud (Amazon VPC) cho phép bạn khởi chạy các tài nguyên AWS vào một mạng ảo mà bạn đã xác định
    * VPC nằm trong 1 Region, khi tạo VPC cần khai báo 1 lớp mạng CIDR IPv4 (bắt buộc) và IPv6 tùy chọn
    * Giới hạn của VPC hiện tại là 5 VPC trên 1 AWS Region trên 1 AWS Account
    * Mục đích chính sử dụng VPC thường dùng để phân tách các môi trường (Production / Dev / Test / Staging)
    * **Lưu ý:** Nếu muốn các tài nguyên tách biệt hẳn (User không thể nhìn thấy một tài nguyên cụ thể thì cần tách thành nhiều AWS account, nhiều VPC không giải quyết được vấn đề này)

    * **Amazon Virtual Private Cloud (VPC) – Subnet**
      * Amazon VPC cho phép tạo nhiều mạng ảo và chia các mạng ảo này thành các mạng con (subnet) 
      * VPC Subnet sẽ nằm trong 1 Availability Zone cụ thể
      * Khi tạo Subnet, chúng ta chỉ định CIDR cho mạng con đó và đây là một tập hợp con của khối VPC CIDR
      * Trong mỗi Subnet, AWS sẽ giữ 5 địa chỉ IP. Ví dụ nếu Subnet có CIDR là 10.10.1.0/24:  
        * Địa chỉ network (10.10.1.0)  
        * Địa chỉ broadcast (10.10.1.255)  
        * Địa chỉ cho bộ định tuyến (10.10.1.1)  
        * Địa chỉ cho DNS (10.10.1.2)  
        * Địa chỉ cho tính năng tương lai (10.10.1.3)

    * **Amazon Virtual Private Cloud (VPC) – Route table**
      * Route table ( Bảng định tuyến ), tập hợp các Route, để xác định đường đi cho mạng
      * Khi tạo VPC, AWS sẽ tạo một Default Route table, Default Route table không thể bị xóa và chỉ chứa 1 Route duy nhất là Route cho phép tất cả các Subnet trong VPC liên lạc với nhau
      * Route table sẽ được gán vào Subnet
      * Chúng ta có thể tạo Custom Route table (bảng định tuyến tùy chỉnh), tuy nhiên sẽ không thể xóa default route(VPC CIDR – Local)
    
    * **Amazon Virtual Private Cloud (VPC) – Elastic Network Interface (ENI)**
      * Elastic Network Interface (ENI) là một card mạng ảo, chúng ta có thể chuyển sang các EC2 Instance khác
      * Khi chuyển sang một máy chủ mới, một card mạng ảo sẽ vẫn duy trì:  
        * Địa chỉ IP Private  
        * Địa chỉ Elastic IP address  
        * Địa chỉ MAC

    * **Amazon Virtual Private Cloud (VPC) – Elastic IP address (EIP)**
      * Elastic IP address (EIP) là một địa chỉ public IPv4 tĩnh, có thể liên kết với một Elastic Network Interface
      * Khi không sử dụng, sẽ bị charge phí (tránh lãng phí)

    * **Amazon Virtual Private Cloud (VPC) – VPC Endpoint**
      * VPC Endpoint cho phép chúng ta kết nối các tài nguyên nằm trong VPC tới các dịch vụ AWS được hỗ trợ (AWS PrivateLink – đi qua mạng private của AWS) mà không cần thông qua kết nối internet
      * Có 2 kiểu VPC Endpoint:  
        * Interface Endpoint: Sử dụng một Elastic Network Interface (ENI) trong VPC cùng với một địa chỉ IP Private để kết nối tới 1 dịch vụ hỗ trợ
        * Gateway Endpoint: Sử dụng một route table để định tuyến tới endpoint của dịch vụ hỗ trợ (cụ thể là S3 và DynamoDB)
    
    * **Amazon Virtual Private Cloud (VPC) – Internet Gateway**
      * Internet Gateway là một thành phần của Amazon VPC có khả năng mở rộng quy mô theo chiều ngang (scale out) cho phép các EC2 Instance trong VPC có thể truyền thông tin ra ngoài Internet
      * Internet Gateway được quản lý bởi AWS, chúng ta không cần cấu hình autoscale hoặc high availability

    * **Amazon Virtual Private Cloud (VPC) – NAT Gateway**
      * NAT Gateway cho phép các EC2 instance trong subnet truy cập tới internet hoặc các dịch vụ AWS khác. Chỉ chấp nhận kết nối chiều ra và không chấp nhận kết nối chiều vào

    * **Amazon Virtual Private Cloud (VPC) – Security Group**
      * Security Group (SG) là một tường lửa ảo có lưu giữ trạng thái (stateful) giúp kiểm soát lượng truy cập đến và đi trong tài nguyên của AWS
      * Security Group rule được hạn chế theo giao thức, địa chỉ nguồn, cổng kết nối, hoặc một Security Group khác
      * Security Group rule chỉ cho phép rule allow
      * Security Group được áp dụng lên các Elastic Network Interface

    * Mặc định Security Group chặn mọi truy cập đến và cho phép mọi truy cập đi

    * **Network Access Control List (NACL)**
      * Network Access Control List (NACL) là một tường lửa ảo không lưu giữ trạng thái (stateless) giúp kiểm soát lượng truy cập đến và đi trong tài nguyên của AWS
      * NACL được hạn chế theo giao thức, địa chỉ nguồn, cổng kết nối
      * NACL được áp dụng lên các Amazon VPC Subnets
      * Mặc định NACL cho phép mọi truy cập đến và đi
    
    * Rule được đọc theo thứ tự từ trên xuống dưới. Nếu lưu lượng mạng thỏa mãn (match) quy tắc nào thì hệ thống sẽ lấy quy tắc đó và thực thi ngay lập tức
    * Mặc định NACL cho phép mọi truy cập đến và đi

    * **Amazon Virtual Private Cloud (VPC) – VPC Flow Logs**
      * VPC Flow Logs là một tính năng cho phép bạn nắm bắt thông tin về lưu lượng IP đến và đi từ các giao diện mạng trong VPC của bạn
      * Các tập tin logs có thể được xuất bản lên Amazon CloudWatch Logs hoặc Amazon S3
      * VPC Flow Logs không capture (ghi lại) nội dung bên trong của gói tin

  * **VPC Peering & Transit Gateway**
    * **VPC Peering**
      * VPC Peering là tính năng giúp kết nối hai hay nhiều VPC để các tài nguyên bên trong hai VPC đó có thể liên lạc trực tiếp với nhau không cần phải thông qua Internet, góp phần gia tăng tính bảo mật cho VPC
      * VPC Peering là kết nối cần tạo 1 : 1 giữa hai VPC thành viên, không hỗ trợ transitive routing (tuyến đường bắc cầu)
      * VPC Peering không hỗ trợ khi 2 VPC bị overlap (trùng lặp) IP address space

    * **Transit Gateway**
      * Transit Gateway được dùng để kết nối các VPC và mạng on-premises thông qua một hub trung tâm. Điều này đơn giản hóa mạng và kết thúc các mối quan hệ định tuyến phức tạp
      * Transit Gateway Attachment là một công cụ để gán các subnet của từng VPC cần kết nối với nhau vào một TGW đã được khởi tạo. Transit Gateway Attachment hoạt động ở quy mô Availability Zone (AZ-level)
      * Trong VPC, khi một subnet ở một AZ có Transit Gateway Attachment với một TGW, các subnet khác trong cùng AZ đều có thể kết nối tới TGW đó

  * **VPN & Direct Connect**
    * **VPN Site to Site**
      * VPN Site to Site dùng trong mô hình hybrid để thiết lập kết nối liên tục giữa môi trường trung tâm dữ liệu truyền thống tới môi trường VPC của AWS. Việc thiết lập kết nối sẽ cần 2 đầu endpoint ở phía AWS và phía khách hàng:  
        * Virtual Private Gateway: Được quản lý hoàn toàn bởi AWS (chia 2 endpoints ở 2 đầu AZ)
        * Customer Gateway: Đầu endpoint phía khách hàng, có thể là thiết bị phần cứng hoặc software appliance
      
    * **VPN Client to Site**
      * VPC Client to Site: cho phép một host truy cập tới tài nguyên trong VPC
      * Khuyến khích sử dụng VPN Client to Site trong AWS Market Place

    * **AWS Direct Connect**
      * AWS Direct Connect là dịch vụ cho phép tạo kết nối riêng từ trung tâm dữ liệu truyền thống tới AWS
      * Độ trễ khoảng 20 ms – 30 ms
      * AWS Direct Connect ở Việt Nam hiện tại sẽ thông qua AWS Direct Connect partners và hoạt động dưới dạng Hosted Connections. (Nếu trực tiếp tới AWS thì là Dedicated Connections)
      * Băng thông Direct Connect có thể thay đổi lên / xuống tùy nhu cầu
  
  * **Elastic Load Balancing**
    * Elastic Load Balancing (ELB) là một dịch vụ cân bằng tải được quản lý bởi AWS, có chức năng phân phối lưu lượng cho nhiều EC2 Instance hoặc Container
    * Sử dụng giao thức HTTP, HTTPS, TCP và SSL (TCP bảo mật)
    * Có thể nằm ở public hoặc private subnet
    * Mỗi ELB sẽ được cấp tên DNS và kết nối thông qua DNS. Chỉ có Network Load Balancer hỗ trợ gán IP tĩnh
    * ELB có tính năng health check, không gửi lưu lượng đến các Instance không đạt health check
    * Bao gồm 4 loại:  
      * Application Load Balancer  
      * Network Load Balancer  
      * Classic Load Balancer  
      * Gateway Load Balancer
    * Sticky session (session affinity): Tính năng cho phép các kết nối được gán vào một target nhất định. Việc này đảm bảo các requests từ một user trong một session sẽ được gửi tới cùng một target. Sticky session là cần thiết trong trường hợp các máy chủ ứng dụng lưu trữ thông tin trạng thái của người dùng tại server
      * Hoạt động: Trên Network Load Balancer, Application Load Balancer, Classic Load Balancer
    * ELB cung cấp tính năng lưu trữ logs truy cập (access logs). Chúng ta có thể sử dụng access logs để phân tích truy cập, troubleshoot. Log truy cập sẽ được lưu trữ vào một dịch vụ lưu trữ đối tượng là Amazon S3 (Simple Storage Service)

    * **Elastic Load Balancing – Application Load Balancer**
      * Application Load Balancer (ALB) là một dịch vụ cân bằng tải được quản lý bởi AWS, hoạt động ở Layer 7
      * Sử dụng giao thức HTTP, HTTPS
      * Hỗ trợ tính năng path-based routing (Ví dụ: các request /mobile hoặc /desktop sẽ được route tới 2 target group khác nhau)
      * Cho phép route traffic tới cả target nằm ngoài VPC (thông qua IP address), EC2, Lambda, Container (ECS, EKS)

    * **Elastic Load Balancing – Network Load Balancer**
      * Network Load Balancer (NLB) là một dịch vụ cân bằng tải được quản lý bởi AWS, hoạt động ở Layer 4
      * Sử dụng giao thức TCP, TLS
      * Hỗ trợ tính năng set IP tĩnh
      * Hỗ trợ hiệu năng cao nhất trong các loại Load Balancer, có khả năng xử lý lên đến hàng triệu request
      * Cho phép route traffic tới cả target nằm ngoài VPC (thông qua IP address), EC2, Container (ECS, EKS)

    * **Elastic Load Balancing – Classic Load Balancer**
      * Classic Load Balancer (CLB) là một dịch vụ cân bằng tải được quản lý bởi AWS, hoạt động ở Layer 4 và Layer 7
      * Sử dụng giao thức HTTP, HTTPS, TCP, TLS
      * Chi phí cao hơn so với ALB và NLB
      * Ít tính năng cao cấp hơn ALB và NLB, hiện tại rất ít được sử dụng
      * Cho phép route traffic tới EC2

    * **Elastic Load Balancing – Gateway Load Balancer**
      * Gateway Load Balancer (GLB) là một dịch vụ cân bằng tải được quản lý bởi AWS, hoạt động ở Layer 3. Gateway Load Balancer lắng nghe toàn bộ IP packets và forward tới target group được chỉ định
      * Sử dụng GENEVE protocol trên port 6081
      * Cho phép route traffic tới các virtual appliance được AWS hỗ trợ
      * Danh sách vendor hỗ trợ: https://aws.amazon.com/vi/elasticloadbalancing/partners/

    * Mô hình thường thấy khi sử dụng Gateway Load Balancer

  * **Thực hành**
    * **Khởi tạo VPC**
      * 000003
        * Giới thiệu Amazon VPC
        * Tường lửa trong VPC
        * Thực hành tạo 1 VPC
        * Cấu hình Site to Site VPN
    
    * **Systems Manager – Session Manager**
      * 000058
        * Các bước chuẩn bị
        * Tạo kết nối đến máy chủ EC2
        * Quản lý session logs
        * Port Forwarding

    * **Thiết lập VPC Peering**
      * 000019
        * Các bước chuẩn bị
        * Cập nhật Network ACL
        * Tạo kết nối Peering
        * Cấu hình Route tables
        * Kích hoạt Cross-Peer DNS

    * **Thiết lập Transit Gateway**
      * 000020
        * Thiết lập Hạ tầng
        * Tạo Transit Gateway
        * Transit Gateway Attachments
        * Tạo Route Table cho TGW
        * Thêm Gateway vào Route Tables & Kiểm tra kết quả

    * **Hybrid DNS**
      * 000010
        * Thiết lập Hybrid DNS
        * Tạo Outbound Endpoint
        * Tạo Route 53 Resolver Rule
        * Tạo Inbound Endpoint

## Thứ 3: Dịch vụ Máy chủ ảo EC2 và Cơ sở hạ tầng tính toán (Compute & Storage)
  * Amazon Elastic Compute Cloud (EC2)
  * Amazon Lightsail
  * Amazon EFS / FSx
  * AWS Application Migration Service (Dịch vụ di chuyển ứng dụng AWS - MGN)
  * **Amazon Elastic Compute Cloud (EC2)**
    * Amazon EC2 giống với máy chủ ảo hoặc máy chủ vật lý truyền thống. EC2 có khả năng khởi tạo nhanh, khả năng co giãn tài nguyên mạnh mẽ, linh hoạt
    * Amazon EC2 có thể hỗ trợ các workload như lưu trữ web, ứng dụng, cơ sở dữ liệu, dịch vụ xác thực và bất cứ công việc nào khác mà máy chủ thông thường có thể đáp ứng
    * Môi trường truyền thống: khi chúng ta mua một cái phần cứng thì chúng ta xài hết vòng đời của cải sản phẩm của mình và chúng ta thay thế một cái máy chủ mới thì chúng ta phải trả cái chi phí  thay thế máy chủ khá là cao
    * Sử dụng dịch vụ EC2 thì giống như đi thuê 1 cái nhà và cái hay là sau vài năm chúng ta có thể có một cái nhà đẹp hơn, xịn hơn. Sau vài năm, nhà cung cấp dịch vụ AWS sẽ nâng cấp CPU, chipset, những phiên bản máy chủ mạnh mẽ hơn và chi phí phiên bản mới có thể thấp hơn so với phiên bản cũ đang sử dụng
    * Chi phí bỏ ra cho một cái dịch vụ trong một cái tính năng sẽ chỉ có giảm đi theo thời gian, không tăng lên
    * Khả năng co giãn tài nguyên gọi là Elasticcity, có thể hiểu là khi xây dựng một cái ứng dụng dịch vụ, muốn cái ứng dụng dịch vụ có thể phục vụ một cái lượng người dùng lớn
    * Thì khi phục vụ lượng người dùng lớn thì cái số lượng máy chủ sẽ tăng lên, ta có 1 máy chủ thì khi mà sử dụng dịch vụ, khi có rất nhiều người dùng thì nó sẽ tăng số lượng máy chủ lên
    * Sau đó, giả sử người dùng sủ dụng xong, họ không có vào cái ứng dụng của chúng ta nữa thì chúng ta có thể giảm bớt số máy chủ để chúng ta phải trả tiền ít hơn, bởi vì mô hình trả phí của chúng ta ở trên môi trường cloud, môi trường xài bao nhiêu tính bấy nhiêu, cho nên là nếu như chúng ta có tăng khả năng co giãn, khả tăng tăng giảm số lượng tài nguyên tùy theo nhu cầu thực dụng của chúng ta sẽ tiết kiệm chi phí rất nhiều thì nó gọi là thuật ngữ elasticcity
    * Ngày xưa ở môi trường local thì chúng ta khá lạc quan, chỉ quan tâm  cái gọi là scalable, tức là ứng dụng của chúng ta có  khả năng mở rộng hay không
    * Thời điểm hiện tại thì không phải lúc nào cũng suôn sẻ cho nên ứng dụng của chúng ta thiết kế có khả năng co giãn để cái tài nguyên  của chúng ta đáp ứng được lượng người dùng thực tế và tiết kiệm chi phí
    * Máy ảo EC2 sẽ tương tự như máy ảo ở môi trường truyền thống, hỗ trợ được những cái công việc, những cái worklog như là ứng dụng web rồi cơ sở dữ liệu, những cái dịch vụ xác thực hay bất cứ một cái gì khác mà máy chủ thông thường có thể đáp ứng

    * **Amazon Elastic Compute Cloud (EC2) – Instance Type**
      * Cấu hình của Amazon EC2 không được tùy chọn tùy ý, mà lựa chọn cấu hình thông qua việc lựa chọn các EC2 Instance type. ( https://aws.amazon.com/ec2/instance-types/?nc1=h_ls )
      * Instance type quyết định các yếu tố:
        * CPU ( Intel / AMD / ARM (Graviton 1 / 2 / 3) / GPU)
        * Memory
        * Network
        * Storage

    * **Amazon Elastic Compute Cloud (EC2) – AMI / Backup / Key Pair**
      * Sử dụng AMI (Amazon Machine Image) có thể provision ra một hoặc nhiều EC2 Instances cùng lúc. AMI có sẵn của AWS, trên AWS Marketplace và custom AMI tự tạo từ EC2 Instances
      * AMI bao gồm root OS volumes, quyền sử dụng AMI quy định tài khoản AWS được sử dụng và mapping EBS volume sẽ được tạo và gắn vào EC2 Instances
      * EC2 instance có thể được backup bằng cách tạo snapshot
      * Key pair (public key và private key) dùng để mã hóa thông tin đăng nhập cho EC2 Instance
      * AMI (Amazon Machine Image) có thể provision ra một hoặc nhiều EC2 Instances cùng lúc
      * Key pair (bao gồm 1 public key và 1 private key) dùng để mã hóa thông tin đăng nhập cho EC2 Instance

    * **Amazon Elastic Compute Cloud (EC2) – Elastic Block Store**
      * Amazon EBS cung cấp block storage và được gán trực tiếp vào EC2 Instance. Tuy được gán trực tiếp như 1 RAW device, EBS về bản chất hoạt động độc lập với EC2 và được kết nối thông qua mạng riêng của EB
      * EBS có hai nhóm đĩa chính là HDD và SSD, được thiết kế để đạt độ sẵn sàng 99.999% bằng cách replicate dữ liệu giữa 3 Storage Node trong 1 AZ
      * EBS về bản chất hoạt động độc lập với EC2 và được kết nối thông qua mạng riêng của EBS trong cùng 1 AZ. EC2 không thể hoạt động mà không có EBS
      * Có một số EC2 Instances đặc thù được tối ưu hóa hiệu năng của EBS. (Optimized EBS Instances)  
      * EBS volumes, mặc định chỉ được gắn vào 1 EC2 Instances. Các EC2 Instances chạy trên Hypervisor Nitro có thể dùng 1 EBS volume gắn vào nhiều EC2 Instances. (EBS Multi-attach)  
      * EBS được backup bằng cách thực hiện snapshot vào S3 (Simple Storage Service):  
        * Snapshot đầu tiên là full, tất cả các snapshot tiếp theo là incremental

    * **Amazon Elastic Compute Cloud (EC2) – Instance Store**
      * Instance store là vùng đĩa NVME tốc độ cực cao, nằm trên physical node chạy các máy ảo EC2
        * Instance store sẽ bị xóa hết dữ liệu khi chúng ta thực hiện stop EC2 instance
        * Instance store không bị xóa dữ liệu khi chúng ta thực hiện restart máy, hoặc bị crash
        * Instance store không replicate dữ liệu dự phòng nên thường không khuyến khích lưu trữ dữ liệu quan trọng
          * Sử dụng trong các trường hợp cần hiệu năng cực cao lên tới hàng triệu IOPS
            * Khi sử dụng thường được replicate dữ liệu vào một EBS volume để bảo đảm an toàn
      * Sử dụng trong các trường hợp cần hiệu năng cực cao lên tới hàng triệu IOPS:
        * swap
        * paging
        * buffer / cache
        * log

    * **Amazon Elastic Compute Cloud (EC2) – User data**
      * EC2 user data là đoạn script chạy một lần khi provision EC2 Instance từ AMI
      * Tùy hệ điều hành mà chúng ta sẽ sử dụng bash shell scripts (Linux) / powershell (Windows)
        * Bạn có thể kiểm tra user data của EC2 tại: http://169.254.169.254/latest/user-data

    * **Amazon Elastic Compute Cloud (EC2) – Meta data**
      * EC2 Metadata là các thông tin liên quan tới bản thân EC2 instances, ví dụ địa chỉ IP Private, Public, Hostname, Security groups....
      * Đường dẫn truy cập: http://169.254.169.254/latest/meta-data/
      * Dùng thông tin EC2 Metadata để thiết lập hostname cho EC2 Instance Linux với EC2 user data

    * **Amazon Elastic Compute Cloud (EC2) – EC2 Auto Scaling**
      * EC2 Auto Scaling là tính năng hỗ trợ tăng giảm số lượng EC2 Instance dựa theo các điều kiện cụ thể (scaling policy)
      * EC2 Auto Scaling có thể tự đăng ký các EC2 Instance vào Elastic Load Balancer
      * EC2 Auto Scaling hoạt động trên nhiều AWS Availability Zone
      * EC2 Auto Scaling có thể hỗ trợ nhiều Pricing options khác nhau