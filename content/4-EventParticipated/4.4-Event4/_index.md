---
title: "Event 4"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 4.4. </b> "
---

# Reflection Report: “FCAJ Community Day - June 2026”

### Purpose of the Event
- Connect the Cloud & AI community, sharing real-world experiences from working professionals to final-year students
- Discuss career journeys (Career Path) in Cloud computing and the transition from on-premise to Cloud environments
- Introduce practical technical solutions: Hybrid connectivity, PrivateLink, and AWS security best practices
- Encourage students to pursue early internships, gain hands-on experience, and prepare for a job market rapidly evolving due to AI
- Create a space for networking, Q&A, and knowledge exchange within the FCAJ (First Cloud AI Journey) community

### Main Speakers

- **Steve Tran** – Clouder / CTO, Cloud Thinker
- MC / Representatives from AWS Study Group & FCAJ Community (opening and closing)

### Highlighted Sessions

#### Career Journey from Student to Clouder – Steve Tran (Cloud Thinker)

- **Early Background**: Part-time job at a Contact Center at age 19 → Frequently visiting server rooms (on-premise) → Realized the complexity, high cost, and difficulty in scaling traditional infrastructure
- **Cloud Learning Path**: Failed multiple times with Azure → Switched to AWS → Obtained Developer/Solution Architect certifications in under a year while studying and working
- **Boom Period**: 2020-2021 (COVID era) → Surge in Cloud demand as businesses migrated en masse → Abundant job opportunities
- **Career Progression**: Developer → Solution Architect at AWS Vietnam → Current role at Cloud Thinker
- **Advice for Students**:
  - Start internships early at startups or companies to accumulate real-world experience
  - The developer job market is changing rapidly due to AI tools → Combine Cloud + AI + business acumen
  - Focus on “real-world experience” rather than just degrees

#### Secure Private Connectivity Solution (Live Demo)

- **Challenge**: Securely connect public cloud with private servers (MCP) with low latency and no public exposure
- **Proposed Architecture**:
  - Amazon VPC + PrivateLink / Interface Endpoint
  - Route 53 Resolver for internal DNS
  - Application Load Balancer (ALB) + AWS Certificate Manager (ACM)
  - Secret Manager + strict IAM permissions
- **Live Demo**: Querying logs, checking latency, calling APIs from private server via private connection → Achieved zero public exposure
- **Cost Estimation**: Approximately $250–350 USD/month for a basic setup (depending on data transfer). Suitable for production workloads
- **Benefits**: Enhanced security, operational stability, and easier scaling

### Key Takeaways

#### Mindset & Thinking
- Cloud is not just technology — it’s a **long-term career journey**. Start early, persist, and stay adaptable (e.g., switching from Azure to AWS)
- The job market is evolving quickly due to AI → Pure developers must upgrade with Cloud + AI + practical thinking
- **Real pain points** from daily work (such as managing physical servers) are the strongest sources of business ideas and improvements
- Production-first mindset: Security, private connectivity, and cost optimization must be considered from day one

#### Technical Skills & Tools
- Hybrid connectivity on AWS: VPC, PrivateLink, Route 53 Resolver, ALB, Secret Manager
- Best practices for private resource connections: Internal DNS, TLS encryption, least-privilege IAM
- Monitoring & observability: Logs, latency tracking, and real-time health checks for private servers

#### Business & Career Insights
- Cloud skills provide a significant competitive advantage in Vietnam and ASEAN
- Early internships greatly improve post-graduation job opportunities and compensation
- Cost awareness: Always estimate and control expenses (data transfer, EC2, ALB) when designing architectures

### Application to Work and Studies
- **Students**: Prioritize learning AWS Cloud, obtain certifications early, and seek internships for real-world exposure
- **Developers/Engineers**: Apply PrivateLink + VPC patterns in hybrid projects to reduce security risks when connecting to on-premise systems
- **Teams/Projects**: Use the demonstrated architecture for designing secure hybrid systems with clear latency and cost monitoring
- Build a personal **Second Brain**: Combine Cloud knowledge with AI tools to boost productivity
- Regularly attend monthly FCAJ Community Days to stay updated on trends and expand your network

### Event Experience
Participating in **FCAJ Community Day - June 2026** was highly inspiring for beginners and working professionals alike. The event perfectly balanced authentic career storytelling with practical technical deep-dives.

#### Learning from Experienced Speakers
- Steve Tran shared his journey openly and honestly — from early struggles to success with AWS and his current role.

#### Hands-on Technical Insights
- Witnessed a live demo of private connectivity and gained clear understanding of building secure hybrid architectures on AWS.

#### Networking and Interaction
- Friendly atmosphere, open Q&A, opportunities to scan QR codes for giveaways, and group photos with the community. Looking forward to the next monthly event.

#### Key Lessons Learned
- **Career journey** matters more than grades. Start early, learn from failures, and always aim for production-grade solutions.
- Cloud + Security + Cost optimization form the foundation for sustainable growth in the AI era.
