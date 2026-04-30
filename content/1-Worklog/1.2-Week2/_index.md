---
title: "Week 2 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.2. </b> "
---
{{% notice warning %}} 
⚠️ **Note:** The following information is for reference purposes only. Please **do not copy verbatim** for your own report, including this warning.
{{% /notice %}}


### Week 2 Objectives:

* Connect and get acquainted with members of First Cloud Journey.
* Understand basic AWS services, how to use the console & CLI.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
|  6  | - Agentic AI Development (Kiro) & AWS Cost Optimization | 24/04/2026 | 24/04/2026 | <https://www.youtube.com/watch?v=uAQCm4sm_1c&t=2s> <br> <https://www.youtube.com/watch?v=UIw8UxGZCHA&t=3s> |
|  2  | - VPC Deep Dive, Hybrid Connectivity & Elastic Load Balancing (ELB) | 27/04/2026 | 27/04/2026 | <https://youtu.be/O9Ac_vGHquM> <br> <https://youtu.be/BPuD1l2hEQ4> <br> <https://youtu.be/CXU8D3kyxIc> |
|  3  | - EC2 Fundamentals, Storage & Auto Scaling | 28/04/2026 | 28/04/2026 | <https://youtu.be/-t5h4N6vfBs> <br> <https://youtu.be/e7XeKdOVq40> <br> <https://youtu.be/yAR6QRT3N1k> <br> <https://youtu.be/hKr_TfGP7NY> <br> <https://youtu.be/6IHNDJ85aoQ> <br> <https://youtu.be/_v_43Wi7zjo> <br> <https://youtu.be/Ew3QRaKJQSA> <br> <https://youtu.be/bbLcPitXJSY> |

### Week 2 Achievements:

## Friday: Gen AI on AWS & Cost Optimization with Kiro

### Gen AI on AWS - Kiro
  * **Agentic changing the SDLC**
    * The rise of Agentic AI in software development is shifting how developers approach their work. We went from task-specific code generation assistance, to end-to-end AI driven feature or app development
    * In 2024, AI primarily acted as a support tool to help developers build applications faster
    * By 2025, the concept of AI agents emerged, enabling developers to assign more complex tasks to AI. These agents could handle end-to-end workflows, going beyond simple code completion or prediction to execute more sophisticated operations
    * As of 2026, the concept of autonomous systems has taken shape, where fully autonomous agents can work end-to-end and collaborate with each other without requiring human intervention

  * **Spec-driven development**
    * **Challenge with AI Development**
      * AI coding tools excel at small tasks but can fail with complex project
      * Existing tools make it difficult to collaborate with and manage agents
      * Getting a project from proof-of-concept to production while maintaining quality control becomes increasingly difficult

    * **Spec Driven Development**
      * Vibe coding ships the prototype, traditional SDLC practices ship the product
      * Vibe-based (inspiration-driven) coding tends to produce prototypes, while traditional software development methods aim to deliver complete, production-ready products
      * When using AI agents or AI coding tools, there are certain limitations: they perform very well for small-scale projects, but as project complexity increases, relying solely on simple interactions makes it difficult to manage and can easily lead to project failure
      * Additionally, when multiple agents or team collaboration are involved, current AI tools still face challenges in coordination and teamwork
      * A project at the POC (Proof of Concept) or MVP (Minimum Viable Product) stage—built to demonstrate technical feasibility—must go through many additional, more detailed requirements before reaching production. A working demo alone is not sufficient for deployment; significant additional work is required, which leads to the need for spec-driven development
      * Spec-driven development means defining detailed specifications, preparing clear requirements, and thorough documentation before starting the coding process
      * Similarly, when using AI coding tools, detailed descriptions of application requirements are essential
      * To build an application, it is necessary to go through structured steps such as planning, implementation, testing, and deployment. When all of these are consolidated into a specification (“spec”), it enables the development of more complex and scalable products

  * **Kiro**
    * The AI IDE for prototype to production. Kiro helps you do your best work by bringing structure to AI coding with spec-driven development

    * **Kiro IDE**
      * Built to support application development from prototype to production environments  
      * The number of Pro Kiro users in Vietnam has exceeded 2,000  
      * Enables building AI applications leveraging GPC-driven development  
      * Kiro offers two usage modes:
        * Vibe Coding: Purely interact with Kiro using natural language. For example, you can ask Kiro to build applications such as note-taking apps, planning tools, expense management systems, etc., based on platforms like Python Web or Python Flux. Kiro will automatically generate and plan the application.
        * Kiro Spec-driven: Designed for more complex applications that require detailed specifications and validation of requirements. Instead of interacting with Kiro via chat or vibe coding from the start, Kiro transforms your input into clear requirements, system designs, and structured tasks. You collaborate with Kiro to refine specifications and system architecture. Kiro agents will implement the specifications while still allowing you to maintain full control.

    * **Kiro IDE - Agent Hook**
      * Delegate tasks to AI agents that trigger on events such as 'file save'
      * Agents autonomously excute in the background based on your pre-defined prompts
      * Agent hooks help you scale your work by generating documentation, unit tests, or optimizing code performance

    * **Kiro IDE - Advenced Context Management**
      * Connect to docs, databases, APIs, and more with native MCP integration
      * Configure how you want Kiro agents to interact with each project via steering files
      * Drop an image of your UI design, or a photo of your architecture whiteboarding session, and Kiro can use it to guide its implementation
    
    * **Kiro IDE – Timeline Checkpointing**
      * Rollback to existing points in the execution log
      * Safety net to safely explore multiple approaches to a problem
      * Snapshots the contents of each modified file and then restores that snapshot when reverting to the checkpoint

    * **Kiro Spec Correctness – Property Based Testing (PBT)**
      * **The Problem with Traditional Testing**
        * Unit tests only validate specific examples — they're limited by the tester's imagination. When AI writes both the code and the tests, it's no guarantee the code matches the requirements

      * **What is Property-Based Testing (PBT)?**
        * Instead of checking individual examples, PBT validates universal properties — rules that must hold true across hundreds or thousands of randomly generated inputs. It shifts the question from "does this example work?" to "does this code always behave correctly?"

      * **How Kiro Implements PBT**
        * Kiro reads your requirements document (written in **EARS** format), extracts testable correctness properties, generates hundreds of test cases, and runs them to surface edge cases and bugs

      * **When Does Kiro Run PBT?**
        * On demand: Triggered manually after code generation
        * Automatically via Agent Hooks: On file save, create, or delete
        * During spec task execution: As the agent implements each component
      
      * **Kiro CLI – AI-Powered Development in Your Terminal**
        * Brings Kiro's AI agent capabilities directly to the command line
        * Build features, automate workflows, analyze errors, and trace bugs — all in natural language
        * Read/write files, call APIs, run bash commands, and interact with MCP tools
        * Custom agents: define tools, permissions, and context for specific tasks
        * MCP integrations: connect to external systems (OpenSearch, Slack, internal tools, etc.)
        * Shares the same steering files and MCP config as Kiro IDE — consistent across environments

      * **Kiro CLI – Custom Agents**
        * Pre-configured AI agents tailored for specific tasks or workflows
        * Define which tools, permissions, and context each agent gets
        * Eliminate repetitive setup

        * **Custom Agents Benefit**
          * Custom agents load only what's needed
          * Optimizes context window usage -> better performance, less noise
          * Enables team-wide consistency
      
      * **Kiro Powers**
        * A unified bundle: MCP tools + steering files + hooks — loaded dynamically, zero baseline context overhead
        * Mechanism to share powers with the community

      * **Kiro Autonomous Agent**
        * Describe a change you need, and execute up to 10 tasks concurrently. It independently figures out how to execute
        * Kiro autonomous agent takes on time-consuming and context-heavy work in the background, from design documentation to new features
      
      * **Kiro – Team Governance**
        * Understand and track usage with the advanced dashboards
        * Manage settings with administrative controls
        * Subscriptions available in AWS IAM Identity Center

      * **Kiro – Pricing**
        **Access the Kiro IDE and CLI with one subscription:**
          * **Pro Tier: $20/month**
              * 1,000 credits
          * **Pro+ Tier: $40/month**
              * 2,000 credits
          * **Power Tier: $200/month**
              * 10,000 credits
        **Additional Information:**
          * Pay-per-use overages available for paid plans at $0.04 per additional credit
          * Free Tier available with 50 credits per month, available for social-sign ins

### Cost optimization on AWS
  * Choose the appropriate configuration of computing resources and data storage
  * Use discounted payment methods such as reserved, savings plans, spot
  * Delete unused resources and turn on automatic shutdown of resources that do not need to run 24/7
  * Use serverless or fully managed service
  * Design well-architecture addresses the proposed requirements
  * Install and use AWS Budget
  * Manage costs by department/application with cost allocation tags
  * Continuously monitor and optimize costs
  * Create a Cost Optimization check list for [your service] using Kiro

  * **AWS Pricing Calculator**
    * Allows creation of estimated service information
    * Estimates can be shared with others
    * Costs will vary by region

  * **Work with AWS Support**
    * **AWS has 4 main support packages:**
      * Basic ( Explore )
      * Developer ( Test / Dev )
      * Business ( Production )
      * Enterprise ( Large Enterprise )

    * The support package can be upgraded in a short time to support faster speeds when there are problems that need to be handled faster

  * **Hands-on**
    * **Create an AWS account**
      * **000001**
        * Create an AWS account
        * Setting MFA for AWS account (Root)
        * Account and group admin
        * Support account authentication
      
    * **Get started with AWS Budgets**
      * **000007**
        * Create an expense budget
        * Create a usage budget
        * Create a preset budget
        * Create a budget savings plan
      
    * **Kiro Spec Driven Development**
      * **000180**
        * Installing Kiro
        * Sign in to Kiro IDE
        * Building Applications with Kiro SDD
        * Hands-on with Kiro SDD
        * Introduction to Kiro CLI
      
    * **Support requests with AWS Support**
      * **000009**
        * AWS support packages
        * Visit AWS Support
        * Handle support requests
      
  * **Additional research**
    * **AWS Well Architected Framework**
      * Concepts, design principles, and architectural best practices for designing and operating your systems in the cloud
      * We use the Framework by answering questions, so you know how your architecture aligns with recommended best practices
      * Additionally, when you use the AWS Well-Architected Framework integration tool on the AWS Management Console, you will receive guidance to improve your current architecture

## Monday: Networking & Content Delivery trên AWS
  * Amazon Virtual Private Cloud (VPC)
  * VPC Peering & Transit Gateway
  * VPN & Direct Connect
  * Elastic Load Balancing
  * **Amazon Virtual Private Cloud (VPC)**
    *  It is a service that provides a private virtual network environment, logically isolated from other networks on the AWS cloud
    * VPC allows us to launch AWS resources, such as virtual servers, databases, and load balancers, within a private virtual network environment where we have complete control
    * VPC (Private Cloud) on AWS is entirely different from the traditional Private Cloud concept
    * Traditional Private Cloud is understood as businesses building a centralized virtualization system in a local or on-premises environment, with features that simulate those of major hyperscale cloud providers like AWS
    * Amazon Virtual Private Cloud (Amazon VPC) allows you to launch AWS resources into a virtual network that you've defined
    * VPC resides within 1 Region; when creating a VPC, it is mandatory to declare an IPv4 CIDR block (IPv6 is optional)
    * The current limit for VPCs is 5 VPCs per AWS Region per AWS Account
    * The main purpose of using VPCs is often to isolate environments (Production / Dev / Test / Staging).
    * **Note:** If you want resources to be completely separate (e.g., a User cannot see a specific resource), you must separate them into multiple AWS accounts; having multiple VPCs does not resolve this issue
  
    * **Amazon Virtual Private Cloud (VPC) – Subnet**
      * Amazon VPC allows the creation of multiple virtual networks and divides these virtual networks into subnets
      * A VPC Subnet resides within 1 specific Availability Zone
      * When creating a Subnet, we specify a CIDR for that subnet, and this is a subset of the VPC CIDR block
      * Within each Subnet, AWS reserves 5 IP addresses. For example, if a Subnet has a CIDR of 10.10.1.0/24:
        * Network address (10.10.1.0)
        * Broadcast address (10.10.1.255)
        * Address for the router (10.10.1.1)
        * Address for DNS (10.10.1.2)
        * Address for future features (10.10.1.3)

    * **Amazon Virtual Private Cloud (VPC) – Route table**
      * Route table, a set of routes used to determine where network traffic is directed
      * When a VPC is created, AWS automatically creates a Default Route table. This table cannot be deleted and initially contains only one route that allows all subnets within the VPC to communicate with each other
      * A Route table is assigned to a Subnet
      * We can create Custom Route tables; however, the default local route (VPC CIDR – Local) cannot be deleted

    * **Amazon Virtual Private Cloud (VPC) – Elastic Network Interface (ENI)**
      * Elastic Network Interface ( ENI ) is a virtual network card that we can transfer to other EC2 Instances
      * When transferred to a new server, a virtual network card will maintain:
        * Private IP address
        * Elastic IP address
        * MAC address

    * **Amazon Virtual Private Cloud (VPC) – Elastic IP address (EIP)**
      * Elastic IP address (EIP) is a static public IPv4 address that can be associated with an Elastic Network Interface
      * When not in use, it will incur charges (to avoid waste)

    * **Amazon Virtual Private Cloud (VPC) – VPC Endpoint**
      * VPC Endpoint allows us to connect resources within a VPC to supported AWS services (AWS PrivateLink – traveling through AWS's private network) without requiring an internet connection
      * There are 2 types of VPC Endpoints:
        * Interface Endpoint: Uses an Elastic Network Interface (ENI) within the VPC along with a Private IP address to connect to a supported service
        * Gateway Endpoint: Uses a route table to direct traffic to the endpoint of a supported service (specifically S3 and DynamoDB)

    * **Amazon Virtual Private Cloud (VPC) – Internet Gateway**
      * Internet Gateway is a component of Amazon VPC that scales horizontally (scale out), allowing EC2 Instances within the VPC to communicate with the outside Internet
      * Internet Gateway is managed by AWS; we do not need to configure autoscale or high availability
    
    * **Amazon Virtual Private Cloud (VPC) – NAT Gateway**
      * NAT Gateway allows EC2 instances in a subnet to access the internet or other AWS services. It only accepts outbound connections and does not accept inbound connections

    * **Amazon Virtual Private Cloud (VPC) – Security Group**
      * Security Group (SG) is a stateful virtual firewall that helps control inbound and outbound traffic for AWS resources
      * Security Group rules are restricted by protocol, source address, port, or another Security Group
      * Security Group rules only support allow rules
      * Security Groups are applied to Elastic Network Interfaces
    
    * By default, Security Groups block all inbound traffic and allow all outbound traffic

    * **Network Access Control List (NACL)**
      * Network Access Control List (NACL) is a stateless virtual firewall that helps control inbound and outbound traffic for AWS resources
      * NACL is restricted by protocol, source address, and port
      * NACL is applied to Amazon VPC Subnets
      * By default, NACL allows all inbound and outbound traffic

    * Rules are read from top to bottom (numerically). If a traffic flow matches a rule, that rule is applied immediately, and subsequent rules are ignored
    * By default, NACL allows all incoming and outgoing access

    * **Amazon Virtual Private Cloud (VPC) – VPC Flow Logs**
      * VPC Flow Logs is a feature that enables you to capture information about the IP traffic going to and from network interfaces in your VPC
      * Log files can be published to Amazon CloudWatch Logs or Amazon S3
      * VPC Flow Logs does not capture the actual content of the network packets (payload)
  
  * **VPC Peering & Transit Gateway**
    * **VPC Peering**
      * VPC Peering is a feature that connects two or more VPCs so that resources within those VPCs can communicate directly with each other without going through the Internet, contributing to increased security for the VPC
      * VPC Peering is a 1 : 1 connection between member VPCs and does not support transitive routing
      * VPC Peering is not supported when two VPCs have overlapping IP address spaces

    * **Transit Gateway**
      * Transit Gateway is used to connect VPCs and on-premises networks through a central hub. This simplifies networking and ends complex peering relationships
      * Transit Gateway Attachment is a tool to attach subnets from each VPC that needs to be connected to an initialized TGW. Transit Gateway Attachment operates at the Availability Zone (AZ-level)
      * Within a VPC, when a subnet in an AZ has a Transit Gateway Attachment to a TGW, all other subnets in the same AZ can connect to that TGW

  * **VPN & Direct Connect**
    * ** VPN Site to Site**
      * VPN Site to Site is used in hybrid models to establish continuous connectivity between traditional data center environments and the AWS VPC environment. Setting up this connection requires two endpoints on the AWS side and the customer side:
        * Virtual Private Gateway: Fully managed by AWS (divided into 2 endpoints at 2 different AZs)
        * Customer Gateway: The endpoint on the customer side, which can be a hardware device or a software appliance

    * **VPN Client to Site**
      * VPC Client to Site: Allows a single host to access resources within a VPC
      * It is recommended to use VPN Client to Site solutions available in the AWS Marketplace

    * **AWS Direct Connect**
      * AWS Direct Connect is a service that allows you to create a private connection from a traditional data center to AWS
      * Latency is approximately 20 ms – 30 ms
      * AWS Direct Connect in Vietnam is currently provided through AWS Direct Connect partners and operates as Hosted Connections. (A direct connection to AWS is known as a Dedicated Connection)
      * Direct Connect bandwidth can be scaled up or down based on demand

  * **Elastic Load Balancing**
    * Elastic Load Balancing (ELB) is a load balancing service managed by AWS, which functions to distribute traffic across multiple EC2 Instances or Containers
    * Uses HTTP, HTTPS, TCP, and SSL (Secure TCP) protocols
    * Can be located in a public or private subnet
    * Each ELB will be provided with a DNS name and connected via DNS. Only Network Load Balancer supports assigning a static IP
    * ELB has a health check feature; it does not send traffic to Instances that fail the health check
    * There are 4 types:
      * Application Load Balancer
      * Network Load Balancer
      * Classic Load Balancer
      * Gateway Load Balancer
    * Sticky session (session affinity): A feature that allows connections to be assigned to a specific target. This ensures that requests from a user within a session will be sent to the same target. Sticky sessions are necessary in cases where application servers store user state information locally on the server
      * Compatibility: Operates on Network Load Balancer, Application Load Balancer, and Classic Load Balancer
    * ELB provides an access log storage feature (access logs). We can use access logs to analyze traffic and troubleshoot. Access logs will be stored in an object storage service, Amazon S3 (Simple Storage Service)

    * **Elastic Load Balancing – Application Load Balancer**
      * Application Load Balancer (ALB) is a load balancing service managed by AWS, operating at Layer 7 (Application Layer)
      * Uses HTTP and HTTPS protocols
      * Supports path-based routing feature (e.g., /mobile and /desktop requests can be routed to two different target groups)
      * Allows routing traffic to various targets including those outside the VPC (via IP address), EC2, Lambda, and Containers (ECS, EKS)

    * **Elastic Load Balancing – Network Load Balancer**
      * Network Load Balancer (NLB) is a load balancing service managed by AWS, operating at Layer 4 (Transport Layer)
      * Uses TCP and TLS protocols
      * Supports static IP (Elastic IP) assignment
      * Offers the highest performance among Load Balancer types, capable of handling millions of requests per second
      * Allows routing traffic to targets including those outside the VPC (via IP address), EC2, and Containers (ECS, EKS)

    * **Elastic Load Balancing – Classic Load Balancer**
      * Classic Load Balancer (CLB) is a load balancing service managed by AWS, operating at both Layer 4 and Layer 7
      * Uses HTTP, HTTPS, TCP, and TLS protocols
      * Higher costs compared to ALB and NLB
      * Fewer advanced features than ALB and NLB; currently rarely used
      * Allows routing traffic to EC2 instances

    * **Elastic Load Balancing – Gateway Load Balancer**
      * Gateway Load Balancer (GLB) is a load balancing service managed by AWS, operating at Layer 3. GLB listens to all IP packets and forwards them to a specified target group
      * Uses the GENEVE protocol on port 6081
      * Allows routing traffic to supported AWS virtual appliances
      * List of supported vendors: https://aws.amazon.com/vi/elasticloadbalancing/partners/
    
    * Common patterns when using Gateway Load Balancers

  * **Hands-on**
    * **Initialize VPC**
      * 000003
        * Introduction to Amazon VPC
        * Firewalls in VPC
        * Practice creating a VPC
        * Configure Site to Site VPN

    * **Systems Manager – Session Manager**
      * 000058
        * Preparation steps
        * Create connection to EC2 instances
        * Manage session logs
        * Port Forwarding

    * **Set up VPC Peering**
      * 000019
        * Preparation steps
        * Update Network ACL
        * Create Peering connection
        * Configure Route tables
        * Enable Cross-Peer DNS
    
    * **Set up Transit Gateway**
      * 000020
        * Infrastructure Setup
        * Create Transit Gateway
        * Transit Gateway Attachments
        * Create Route Table for TGW
        * Add Gateway to Route Tables & Verify results

    * **Hybrid DNS**
      * 000010
        * Set up Hybrid DNS
        * Create Outbound Endpoint
        * Create Route 53 Resolver Rule
        * Create Inbound Endpoint

## Tuesday: AWS Compute Services: EC2, Instance Storage, and Auto Scaling
  * Amazon Elastic Compute Cloud (EC2)
  * Amazon Lightsail
  * Amazon EFS / FSx
  * AWS Application Migration Service (MGN)
  * **Amazon Elastic Compute Cloud (EC2)**
    * Amazon EC2 is similar to a virtual server or a traditional physical server. EC2 has the ability to initialize quickly, with powerful, flexible resource scalability
    * Amazon EC2 can support workloads such as web hosting, applications, databases, authentication services, and any other tasks that a standard server can handle
    * Traditional Environment: When purchasing hardware, you use it until the end of its lifecycle. Replacing a new server incurs very high replacement costs
    * Using EC2 Service: Similar to renting a house where you can upgrade to a better, more modern one over time. After a few years, AWS upgrades CPUs, chipsets, and more powerful server versions. Notably, the cost of newer versions can be lower than the old ones currently in use
    * Cost Efficiency: The cost for a specific feature within a service generally decreases over time rather than increasing
    * Elasticity: This refers to the ability to automatically scale resources up or down based on actual demand
    * When the number of users increases, the number of servers increases accordingly
    * When users leave the application, the number of servers decreases to minimize costs
    * Pay-as-you-go: Since the cloud operates on a "pay for what you use" model, increasing or decreasing resources based on real-time needs saves significant costs
    * Modern Design: Previously, in local environments, the focus was primarily on Scalability (the ability to expand). Today, applications are designed for Elasticity to ensure resources match actual user traffic while optimizing expenses
    * Workload Support: EC2 instances function similarly to virtual machines in traditional environments. They support various workloads such as web applications, databases, authentication services, and any other tasks a standard server can handle

    * **Amazon Elastic Compute Cloud (EC2) – Instance Type**
      * Amazon EC2 configurations are not arbitrarily customizable; instead, configurations are selected by choosing EC2 Instance types. ( https://aws.amazon.com/ec2/instance-types/?nc1=h_ls )
      * The Instance type determines the following factors:
        * CPU ( Intel / AMD / ARM (Graviton 1 / 2 / 3) / GPU)
        * Memory
        * Network
        * Storage

    * **Amazon Elastic Compute Cloud (EC2) – AMI / Backup / Key Pair**
      * Using an AMI (Amazon Machine Image), you can provision one or many EC2 Instances simultaneously. AMIs are available from AWS, on the AWS Marketplace, or as custom AMIs created from your own EC2 Instances
      * An AMI includes root OS volumes, AMI permissions that specify which AWS accounts can use it, and block device mapping that determines the EBS volumes to be created and attached to the EC2 Instances
      * EC2 instances can be backed up by creating snapshots
      * A Key pair (public key and private key) is used to encrypt the login information for an EC2 Instance
      * AMI (Amazon Machine Image) can provision one or many EC2 Instances simultaneously
      * Key pair (including 1 public key and 1 private key) is used to encrypt login information for an EC2 Instance
    
    * **Amazon Elastic Compute Cloud (EC2) – Elastic Block Store**
      * Amazon EBS provides block storage and is attached directly to an EC2 Instance. Although it is attached directly like a RAW device, EBS essentially operates independently of the EC2 and is connected through a private EBS network
      * EBS has two main groups of disks: HDD and SSD. It is designed to achieve 99.999% availability by replicating data across 3 Storage Nodes within a single Availability Zone (AZ)
      * EBS essentially operates independently of EC2 and is connected through a private EBS network within the same AZ. EC2 cannot operate without EBS
      * There are specific EC2 Instances that are performance-optimized for EBS. (EBS-Optimized Instances)  
      * By default, EBS volumes can only be attached to a single EC2 Instance. However, EC2 Instances running on the Nitro Hypervisor can use a single EBS volume attached to multiple EC2 Instances. (EBS Multi-attach)  
      * EBS is backed up by taking snapshots to S3 (Simple Storage Service):  
        * The first snapshot is a full copy; all subsequent snapshots are incremental

    * **Amazon Elastic Compute Cloud (EC2) – Instance Store**
      * Instance store is a high-speed NVME disk area located on the physical node running the EC2 virtual machines
        * All data on an Instance store will be deleted when the EC2 instance is stopped
        * Data on an Instance store is not deleted when the machine is restarted or in the event of a crash
        * Instance store does not replicate data for backup, so it is generally not recommended for storing critical data
          * It is used in cases requiring extremely high performance, up to millions of IOPS
            * When used, data is typically replicated to an EBS volume to ensure safety
      * Used in cases requiring extremely high performance, up to millions of IOPS:
        * swap
        * paging
        * buffer / cache
        * log

    * **Amazon Elastic Compute Cloud (EC2) – User data**
      * EC2 user data is a script that runs once when provisioning an EC2 Instance from an AMI
      * Depending on the operating system, we use bash shell scripts (Linux) or PowerShell (Windows)
        * You can check the EC2 user data at: http://169.254.169.254/latest/user-data

    * **Amazon Elastic Compute Cloud (EC2) – Meta data**
      * EC2 Metadata is information related to the EC2 instance itself, such as Private IP address, Public IP, Hostname, Security groups, etc
      * Link to access: http://169.254.169.254/latest/meta-data/
      * Use EC2 Metadata information to configure the hostname for a Linux EC2 Instance using EC2 user data

    * **Amazon Elastic Compute Cloud (EC2) – EC2 Auto Scaling**
      * EC2 Auto Scaling is a feature that supports increasing or decreasing the number of EC2 Instances based on specific conditions (scaling policy)
      * EC2 Auto Scaling can automatically register EC2 Instances with an Elastic Load Balancer
      * EC2 Auto Scaling operates across multiple AWS Availability Zones
      * EC2 Auto Scaling can support various Pricing options