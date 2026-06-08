---
title: "Event 2"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 4.2. </b> "
---

# Bài thu hoạch “AWS Vietnam Community Day 2026”

### Mục Đích Của Sự Kiện
- Chia sẻ các case study thực tế về việc xây dựng hệ thống AI/ML cấp doanh nghiệp
- Giới thiệu kiến trúc Multi-Agent, tối ưu hóa GenAI và các best practices vận hành production
- Thảo luận về non-determinism của LLM, bảo mật, performance và ROI khi áp dụng AI
- Khuyến khích cộng đồng chia sẻ kinh nghiệm từ hackathon đến production-grade systems

### Danh Sách Diễn Giả

- **Vy Lam** - Senior Business Systems Analyst, VPBank
- **Duc Dao** - Solution Architect, Cloud Kinetics
- **Team VIB** - LotusHacks 2026 participants (UTMorpho project)
- **Nguyen Tuan Thinh** - DevOps Engineer
- **Pham Ng Hai Anh** - AWS Community Builder, G-AsiaPacific Vietnam
- **Tinh Truong** - Platform Engineer, GoTymeX

### Nội Dung Nổi Bật

#### Enterprise-Grade Multi-Agent System – The Case of Startup Credit Scoring (Vy Lam)

- **Structural Mismatch**: Hệ thống tín dụng truyền thống không phù hợp với dữ liệu startup (thiếu lịch sử, tài sản vô hình, tăng trưởng không tuyến tính)
- **Single Agent vs Multi-Agent**: Single agent gặp hạn chế về context, expertise dilution, thiếu checks & balances. Multi-agent hoạt động như **Virtual Credit Committee**
- **Kiến trúc Multi-Agent**: Manager + Financial Analyst + Market Analyst + Team Evaluator + Risk Assessor + Compliance → Consensus output (Score, Risk Rating, Confidence, Audit Trail)
- **Enterprise Pillars**: Security, Data Governance, Network, Operations, Human Factors, Compliance
- **Guardrails & Deployment**: Bedrock, AgentCore, ECR, API Gateway, Terraform, Cognito, IAM
- **ROI**: Giảm 95% thời gian và chi phí, tăng gấp đôi approval rate

#### Non-Determinism of “Deterministic” LLM Settings (Duc Dao)

- **Root Cause**: Floating-point non-associativity trên GPU + inference batching
- **Thực tế**: Ngay cả temp=0 cũng không đảm bảo reproducible outputs. Accuracy biến động lên đến 15%, TARr@10 thường gần 0% trên task khó
- **Mitigation**: Multiple runs + majority voting, structured output (JSON mode), self-hosted models, design for variance (temp=0.1 sweet spot)
- **Key Takeaway**: Luôn test thoroughly và xây dựng hệ thống chịu được probabilistic nature của LLM

#### UTMorpho – LotusHacks 2026 Winning Project (Team VIB)

- **Problem**: AI UI generators tạo output khó chỉnh sửa, drift khi re-prompt
- **Solution**: Agent sinh UI + **inline WYSIWYG editing**, token-aware diffing, export React
- **Key Learnings**: Real frustration → real idea, team chemistry > skill, token economy là design constraint, AI là teammate
- **36-hour sprint**: Idea validation → core build → polish → pitch

#### CloudFront as Your Foundation (Nguyen Tuan Thinh)

- **Cost Optimization**: Free DTO từ AWS origins, giảm chi phí Load Balancer & EC2, HTTP compression (giảm 80%+ size)
- **Security**: Origin cloaking (VPC + OAC), Signed URL, mTLS, Geo restriction, WAF + Shield
- **Performance & Reliability**: Multi-layer caching, HTTP/3 (QUIC), origin failover, edge computing (CloudFront Functions, Lambda@Edge)
- **Use Cases**: Small sites, business apps, scaling workloads

#### Friendly AI Assistant with Amazon Quick (Pham Ng Hai Anh)

- **Agentic AI**: Kết hợp company data, world knowledge và actions trong một unified experience
- **Use Cases**: PM Assistant (tự động tạo MoM, schedule meeting), research, automation
- **Capabilities**: 40+ data connectors, Bedrock models, guardrails, governance

#### Context Is Everything (Tinh Truong)

- **Core Message**: AI mạnh nhưng output kém thường do **context yếu**
- **Common Mistakes**: Internet Puller, redundant info, no goal/constraints
- **Best Practices**: Goal + Relevant info + Constraints + Success criteria. Xây dựng “Second AI Brain” (memory + retrieval)
- **Evolution**: Prompt → Context → Memory → AgentOps

### Những Gì Học Được
#### Tư Duy Thiết Kế & Kiến Trúc
- Multi-agent mang lại **specialized expertise**, checks & balances và auditability vượt trội so với single agent
- Context quality quan trọng hơn context quantity. Phải design system chịu được variance của LLM
- Enterprise-grade AI phải bắt đầu từ **security, guardrails, compliance và observability** ngay từ ngày đầu
- Real pain points từ công việc hàng ngày là nguồn ý tưởng mạnh mẽ nhất (UTMorpho)

#### Kỹ Thuật & Công cụ
- Sử dụng **Bedrock + AgentCore**, Terraform, Cognito, CloudFront để xây dựng production-ready system
- CloudFront không chỉ là CDN mà còn là lớp security, cost optimization và performance mạnh mẽ
- Context engineering và memory systems là kỹ năng cốt lõi tương lai

#### Business & ROI
- Multi-agent credit scoring mang lại **200-300% ROI** trong 3 năm
- Hackathon rèn luyện endurance, focus và khả năng cắt feature để bảo vệ demo

### Ứng Dụng Vào Công Việc
- **Xây dựng Multi-Agent System** cho các use case nội bộ (credit assessment, customer support, document processing)
- **Tối ưu prompt & context** khi dùng LLM, áp dụng structured output và majority voting cho production
- **Triển khai CloudFront** để giảm chi phí, tăng security và performance cho các web/app hiện tại
- **Xây dựng Second AI Brain** cá nhân/team để tăng productivity trong research và development
- **Tham gia/ tổ chức hackathon** để test ý tưởng nhanh và rèn luyện team chemistry
- Pilot **Amazon Quick** hoặc Bedrock Agents cho business users

### Trải nghiệm trong event
Tham gia **AWS Vietnam Community Day 2026** là một ngày đầy cảm hứng và kiến thức thực tiễn. Các session không chỉ mang tính lý thuyết mà còn chia sẻ rất nhiều case study, thất bại, bài học và giải pháp production-grade

#### Học hỏi từ các diễn giả có chuyên môn cao
- Các anh/chị speaker đều chia sẻ chân thực từ kinh nghiệm thực chiến tại ngân hàng, hackathon, DevOps đến platform engineering

#### Trải nghiệm kỹ thuật thực tế
- Hiểu rõ cách xây dựng **Virtual Credit Committee** bằng multi-agent, cách xử lý non-determinism của LLM, và sức mạnh của context engineering
- Thấy rõ hành trình từ ý tưởng hackathon 36 giờ thành sản phẩm có thể demo và mở rộng

#### Kết nối và trao đổi
- Cơ hội trao đổi với các anh/chị trong cộng đồng AWS, học hỏi cách áp dụng CloudFront, Agentic AI và modern architecture vào môi trường Việt Nam

#### Bài học rút ra
- **Enterprise AI ≠ làm cho nó chạy**, mà là làm cho nó **chạy an toàn, đáng tin cậy và scalable**
- Context thực sự là everything. Kiến trúc tốt + guardrails chặt chẽ + mindset production-first mới tạo ra giá trị bền vững

#### Một số hình ảnh khi tham gia sự kiện
* ![Event](images/Event2.png)
