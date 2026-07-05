---
title: "Event 4"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 4.4. </b> "
---

# Bài thu hoạch “FCAJ Community Day - June 2026”
### Mục Đích Của Sự Kiện
- Kết nối cộng đồng Cloud & AI, chia sẻ kinh nghiệm thực tế từ người đi làm đến sinh viên năm cuối
- Thảo luận hành trình sự nghiệp (Career Path) trong lĩnh vực Cloud và cách chuyển tiếp từ on-premise sang Cloud
- Giới thiệu các giải pháp kỹ thuật thực tiễn: Hybrid connectivity, PrivateLink, security best practices trên AWS
- Khuyến khích sinh viên tham gia internship sớm, tích lũy kinh nghiệm thực tế và chuẩn bị cho thị trường việc làm đang thay đổi mạnh vì AI
- Tạo không gian trao đổi, Q&A và networking trong cộng đồng FCAJ (First Cloud AI Journey)

### Danh Sách Diễn Giả

- Steve Tran – Clouder / CTO, Cloud Thinker
- MC / Đại diện AWS Study Group & FCAJ Community

### Nội Dung Nổi Bật

#### Hành Trình Sự Nghiệp Từ Sinh Viên Đến Clouder – Steve Tran (Cloud Thinker)

- Bối cảnh ban đầu: Làm part-time Contact Center năm 19 tuổi → Thường xuyên phải ra server room (on-premise) → Nhận ra sự phức tạp, tốn kém, khó scale và vận hành của hạ tầng truyền thống
- Hành trình học Cloud: Thử Azure thất bại vài lần → Chuyển sang AWS → Thi chứng chỉ Developer/Solution Architect trong chưa đầy 1 năm (vừa học vừa làm)
- Thời điểm bùng nổ: 2020-2021 (Covid) → Nhu cầu Cloud tăng mạnh, doanh nghiệp migrate ồ ạt → Cơ hội việc làm lớn
- Quá trình thăng tiến: Developer → Solution Architect tại AWS Vietnam → Vai trò hiện tại tại Cloud Thinker
- Lời khuyên cho sinh viên:
  - Tham gia internship sớm tại startup hoặc công ty để tích lũy kinh nghiệm thực tế
  - Thị trường developer đang thay đổi mạnh do AI tools → Cần kết hợp Cloud + AI + tư duy thực tiễn
  - Tập trung vào “real-world experience” thay vì chỉ bằng cấp

#### Giải Pháp Kết Nối An Toàn Private Connectivity (Demo Thực Tế)
- Vấn đề: Kết nối public cloud với private server (MCP) một cách an toàn, low-latency, không expose public
- Kiến trúc đề xuất:
  - Amazon VPC + PrivateLink / Interface Endpoint
  - Route 53 Resolver cho internal DNS
  - Application Load Balancer (ALB) + AWS Certificate Manager (ACM)
  - Secret Manager + IAM permissions chặt chẽ
- Demo thực tế: Query logs, kiểm tra latency, gọi API từ private server qua private connection → Zero public exposure
- Chi phí ước tính: Khoảng 250-350 USD/tháng cho setup cơ bản (tùy data transfer). Phù hợp cho production workload
- Lợi ích: Tăng security, ổn định vận hành, dễ scale

### Những Gì Học Được
#### Tư Duy Thiết Kế & Kiến Trúc
- Cloud không chỉ là công nghệ mà là hành trình sự nghiệp dài hạn. Bắt đầu sớm, kiên trì và linh hoạt thay đổi (từ Azure sang AWS)
- Thị trường lao động đang thay đổi nhanh do AI → Developer thuần cần nâng cấp kỹ năng Cloud + AI + Business understanding
- Real pain points từ công việc hàng ngày (như ra server room) là nguồn ý tưởng kinh doanh và cải tiến mạnh mẽ nhất
- Production-first mindset: Security, Private connectivity và Cost optimization phải được cân nhắc từ sớm

#### Kỹ Thuật & Công cụ
- Hybrid connectivity trên AWS: VPC, PrivateLink, Route 53 Resolver, ALB, Secret Manager
- Best practices khi kết nối private resources: DNS internal, TLS encryption, IAM least privilege
- Quan sát và monitor: Logs, latency tracking, real-time health check của private server

#### Business & Career
- Cloud skills mang lại lợi thế cạnh tranh lớn tại Việt Nam và ASEAN
- Internship sớm giúp tăng cơ hội việc làm sau tốt nghiệp với mức lương và vị trí tốt hơn
- Cost awareness: Luôn ước tính và kiểm soát chi phí (data transfer, EC2, ALB) khi thiết kế architecture

### Ứng Dụng Vào Công Việc
- Sinh viên: Ưu tiên học AWS Cloud, thi chứng chỉ sớm và tìm internship để trải nghiệm môi trường thực tế
- Developer/Engineer: Áp dụng PrivateLink + VPC cho các dự án hybrid, giảm rủi ro bảo mật khi kết nối on-premise
- Team/Project: Sử dụng kiến trúc demo của Steve để thiết kế hệ thống kết nối an toàn, monitor latency và chi phí rõ ràng
- Xây dựng Second Brain cá nhân: Kết hợp kiến thức Cloud với AI tools để tăng productivity
- Tham gia đều đặn các Community Day hàng tháng của FCAJ để cập nhật xu hướng và mở rộng network

### Trải nghiệm trong event
Tham gia **AWS Vietnam Community Day 2026** là một ngày đầy cảm hứng và kiến thức thực tiễn. Các session không chỉ mang tính lý thuyết mà còn chia sẻ rất nhiều case study, thất bại, bài học và giải pháp production-grade

#### Học hỏi từ diễn giả
- Anh Steve Tran chia sẻ rất gần gũi, chân thành từ hành trình cá nhân, thất bại (Azure) đến thành công với AWS và vai trò hiện tại

#### Trải nghiệm kỹ thuật thực tế
- Được xem demo live về private connectivity, hiểu rõ cách xây dựng hybrid architecture an toàn trên AWS

#### Kết nối và trao đổi
- Không khí thân thiện, Q&A cởi mở, cơ hội scan QR nhận quà và chụp ảnh kỷ niệm cộng đồng. Hẹn gặp lại ở event tháng sau

#### Bài học rút ra
- Hành trình sự nghiệp quan trọng hơn điểm số. Bắt đầu sớm, học từ sai lầm và luôn hướng tới production-grade solutions
- Cloud + Security + Cost optimization là nền tảng để phát triển bền vững trong kỷ nguyên AIrything. Kiến trúc tốt + guardrails chặt chẽ + mindset production-first mới tạo ra giá trị bền vững

