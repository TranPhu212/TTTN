---
title: "Event 2"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 4.2. </b> "
---

# Summary Report: “AWS Vietnam Community Day 2026”

### Event Objectives
- Sharing real-world case studies on building enterprise-grade AI/ML systems
- Introducing Multi-Agent architectures, GenAI optimization, and production best practices
- Discussing LLM non-determinism, security, performance, and ROI in AI adoption
- Encouraging community knowledge sharing from hackathons to production-grade systems

### Speakers
- Vy Lam - Senior Business Systems Analyst, VPBank
- Duc Dao - Solution Architect, Cloud Kinetics
- Team VIB - LotusHacks 2026 participants (UTMorpho project)
- Nguyen Tuan Thinh - DevOps Engineer
- Pham Ng Hai Anh - AWS Community Builder, G-AsiaPacific Vietnam
- Tinh Truong - Platform Engineer, GoTymeX

### Key Highlights
#### Enterprise-Grade Multi-Agent System – The Case of Startup Credit Scoring (Vy Lam)
- Structural Mismatch: Traditional credit systems are not suitable for startup data (lack of history, intangible assets, non-linear growth)
- Single Agent vs Multi-Agent: Single agents are limited in context handling, suffer from expertise dilution, and lack checks & balances. Multi-agent systems act as a Virtual Credit Committee
- Multi-Agent Architecture: Manager + Financial Analyst + Market Analyst + Team Evaluator + Risk Assessor + Compliance → consensus output (Score, Risk Rating, Confidence, Audit Trail)
- Enterprise Pillars: Security, Data Governance, Network, Operations, Human Factors, Compliance
- Guardrails & Deployment: Bedrock, AgentCore, ECR, API Gateway, Terraform, Cognito, IAM
- ROI: 95% reduction in time and cost, and 2x increase in approval rate

#### Non-Determinism of “Deterministic” LLM Settings (Duc Dao)
- Root Cause: Floating-point non-associativity on GPUs + inference batching
- Reality: Even with temperature = 0, outputs are not fully reproducible. Accuracy variance can reach up to 15%, and TAR@10 isoften near 0% on hard tasks
- Mitigation: Multiple runs + majority voting, structured output (JSON mode), self-hosted models, designing for variance (temperature 0.1 sweet spot)
- Key Takeaway: Always test thoroughly and design systems that can tolerate the probabilistic nature of LLMs

#### UTMorpho – LotusHacks 2026 Winning Project (Team VIB)
- Problem: AI UI generators produce outputs that are hard to edit and suffer from drift when re-prompted
- Solution: UI-generating agent + inline WYSIWYG editing, token-aware diffing, React export
- Key Learnings: Real frustration → real ideas, team chemistry > individual skill, token economy is a design constraint, AI is a teammate
- 36-hour sprint: Idea validation → core build → polish → pitch

#### CloudFront as Your Foundation (Nguyen Tuan Thinh)
- Cost Optimization: Free data transfer from AWS origins, reduced Load Balancer & EC2 costs, HTTP compression (80%+ size reduction)
- Security: Origin cloaking (VPC + OAC), Signed URLs, mTLS, geo restriction, WAF + Shield
- Performance & Reliability: Multi-layer caching, HTTP/3 (QUIC), origin failover, edge computing (CloudFront Functions, Lambda@Edge)
- Use Cases: Small websites, business applications, scalable workloads

#### Friendly AI Assistant with Amazon Quick (Pham Ng Hai Anh)
- Agentic AI: Combines company data, world knowledge, and actions into a unified experience
- Use Cases: PM Assistant (auto-generated meeting minutes, scheduling), research, automation
- Capabilities: 40+ data connectors, Bedrock models, guardrails, governance

#### Context Is Everything (Tinh Truong)
- Core Message: AI is powerful, but poor outputs often come from weak context
- Common Mistakes: Internet pulling, redundant information, lack of goals/constraints
- Best Practices: Goal + relevant information + constraints + success criteria. Build a “Second AI Brain” (memory + retrieval)
- Evolution: Prompt → Context → Memory → AgentOps

### Key Takeaways
#### Design & Architecture Thinking
- Multi-agent systems provide specialized expertise, checks & balances, and strong auditability compared to single-agent systems
- Context quality is more important than context quantity; systems must be designed to handle LLM variance
- Enterprise AI must start with security, guardrails, compliance, and observability from day one
- Real-world pain points are the strongest source of ideas (as shown by UTMorpho)

#### Technical Skills & Tools
- Using Bedrock + AgentCore, Terraform, Cognito, and CloudFront for production-ready systems
- CloudFront is not just a CDN but also a powerful layer for security, cost optimization, and performance
- Context engineering and memory systems are becoming core engineering skills

#### Business & ROI
- Multi-agent credit scoring systems can deliver 200–300% ROI over 3 years
- Hackathons help build endurance, focus, and the ability to cut features for demo success

### Applying to Work

- Build Multi-Agent Systems for internal use cases (credit assessment, customer support, document processing)
- Optimize prompt & context design for LLMs using structured outputs and majority voting in production
- Deploy CloudFront to reduce cost and improve security/performance of existing applications
- Build a Second AI Brain for individuals/teams to improve productivity in research and development
- Participate in / organize hackathons to rapidly test ideas and strengthen team collaboration
- Pilot Amazon Quick or Bedrock Agents for business users

### Event Experience
Attending AWS Vietnam Community Day 2026 was an inspiring and highly practical experience. The sessions were not purely theoretical but included real-world case studies, failures, lessons learned, and production-grade solutions

#### Learning from highly skilled speakers
- Speakers shared hands-on experience from banking, hackathons, DevOps, and platform engineering environments

#### Hands-on technical exposure
- Gained insight into building a Virtual Credit Committee using multi-agent systems
- Learned how to handle LLM non-determinism and the importance of context engineering
- Observed the journey from a 36-hour hackathon idea to a scalable, demo-ready product

#### Networking and discussions
- Opportunity to interact with AWS community members and learn how to apply CloudFront, Agentic AI, and modern architecture in Vietnam’s context

#### Lessons learned
- Enterprise AI ≠ just making it work, but making it secure, reliable, and scalable
- Context truly is everything. Strong architecture + strict guardrails + production-first mindset create sustainable value

#### Some event photos
* ![Event](/images/Event2.png)