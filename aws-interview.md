# AWS Architect Interview Questions & Answers

## **Core AWS Services**

### **1. What is AWS and its key components?**
**Answer:**  
AWS (Amazon Web Services) is a cloud computing platform offering over 200 services, including computing, storage, databases, networking, AI, and security.  
Key components:  
- **Compute:** EC2, Lambda  
- **Storage:** S3, EBS, EFS  
- **Database:** RDS, DynamoDB  
- **Networking:** VPC, Route 53  
- **Security:** IAM, KMS  

---

### **2. Explain AWS Global Infrastructure.**
**Answer:**  
AWS operates in:  
- **Regions** (geographical areas, e.g., `us-east-1`)  
- **Availability Zones (AZs)** (isolated data centers within a region)  
- **Edge Locations** (CDN endpoints for CloudFront)  

---

### **3. What is an AWS VPC?**  
**Answer:**  
A **Virtual Private Cloud (VPC)** is a logically isolated network in AWS where you can launch resources.  
- Uses subnets (public/private), route tables, and security groups.  
- Supports peering and VPN connections.  

---

### **4. Difference between Security Groups and NACLs?**  
| **Security Group** | **NACL (Network ACL)** |  
|---------------------|-----------------------|  
| Stateful (return traffic allowed) | Stateless (explicit rules needed) |  
| Applied at instance level | Applied at subnet level |  
| Supports allow rules only | Supports allow/deny rules |  

---

## **Compute Services**

### **5. What is EC2 and its instance types?**  
**Answer:**  
**EC2 (Elastic Compute Cloud)** provides scalable virtual servers.  
- **Instance Types:**  
  - General Purpose (`t3`, `m5`)  
  - Compute Optimized (`c5`)  
  - Memory Optimized (`r5`)  
  - GPU (`p3`)  

---

### **6. What is AWS Lambda?**  
**Answer:**  
Lambda is a **serverless** compute service that runs code in response to events (e.g., S3 upload, API Gateway request).  
- No servers to manage, scales automatically.  
- Pay per execution time.  

---

### **7. When to use ECS vs. EKS?**  
**Answer:**  
- **ECS (Elastic Container Service):** AWS-managed Docker container orchestration.  
- **EKS (Elastic Kubernetes Service):** Managed Kubernetes for complex microservices.  

---

## **Storage Services**

### **8. Difference between S3, EBS, and EFS?**  
| **S3** | **EBS** | **EFS** |  
|--------|---------|--------|  
| Object storage | Block storage (attached to EC2) | File storage (NFS) |  
| 99.999999999% durability | Single AZ (unless replicated) | Multi-AZ |  

---

### **9. What is S3 Glacier?**  
**Answer:**  
Low-cost storage for **cold data** (archival).  
- Retrieval times: **Minutes to hours**.  
- Use cases: Compliance, backups.  

---

## **Database Services**

### **10. RDS vs. DynamoDB?**  
| **RDS** | **DynamoDB** |  
|---------|-------------|  
| SQL (MySQL, PostgreSQL) | NoSQL (key-value) |  
| Vertical scaling | Horizontal scaling |  
| Good for structured data | Good for high-speed, unstructured data |  

---

### **11. What is Amazon Aurora?**  
**Answer:**  
A MySQL/PostgreSQL-compatible **high-performance RDS** database.  
- 5x faster than standard MySQL.  
- Auto-scaling storage.  

---

## **Networking & Content Delivery**

### **12. What is CloudFront?**  
**Answer:**  
AWS’s **CDN** (Content Delivery Network) caches content at Edge Locations for low-latency delivery.  

---

### **13. What is Route 53?**  
**Answer:**  
AWS’s **DNS service** for domain registration and traffic routing (e.g., weighted, latency-based).  

---

## **Security & Identity**

### **14. What is IAM?**  
**Answer:**  
**Identity and Access Management (IAM)** controls AWS user/role permissions.  
- Policies define permissions (e.g., `AmazonS3FullAccess`).  

---

### **15. Explain KMS.**  
**Answer:**  
**Key Management Service (KMS)** manages encryption keys for AWS services.  
- Supports **CMKs (Customer Master Keys)**.  

---

## **DevOps & Automation**

### **16. What is CloudFormation?**  
**Answer:**  
**Infrastructure as Code (IaC)** tool to define AWS resources in JSON/YAML templates.  

---

### **17. AWS CodePipeline vs. CodeDeploy?**  
**Answer:**  
- **CodePipeline:** CI/CD orchestration.  
- **CodeDeploy:** Deploys code to EC2/Lambda.  

---

## **High Availability & Disaster Recovery**

### **18. What is Multi-AZ in RDS?**  
**Answer:**  
Automatically replicates RDS databases to a standby **AZ** for failover.  

---

### **19. Difference between ASG and ELB?**  
**Answer:**  
- **Auto Scaling Group (ASG):** Scales EC2 instances.  
- **Elastic Load Balancer (ELB):** Distributes traffic.  

---

## **Serverless & Advanced Services**

### **20. What is API Gateway?**  
**Answer:**  
Managed service to create, publish, and secure APIs.  
- Integrates with **Lambda** for serverless backends.  

---

## **Monitoring & Logging**

### **21. What is CloudWatch?**  
**Answer:**  
AWS’s monitoring service for logs, metrics, and alarms.  

---

### **22. CloudWatch vs. CloudTrail?**  
**Answer:**  
- **CloudWatch:** Performance monitoring.  
- **CloudTrail:** Logs API calls for auditing.  

---

## **Cost Optimization**

### **23. How to reduce AWS costs?**  
**Answer:**  
- Use **Reserved Instances** (long-term discounts).  
- Delete unused **EBS volumes**.  
- Enable **S3 Lifecycle Policies**.  

---

## **Migration & Hybrid Cloud**

### **24. What is AWS Snowball?**  
**Answer:**  
Physical device for **large-scale data migration** (petabyte-scale).  

---

## **Advanced Architecting**

### **25. Explain Well-Architected Framework.**  
**Answer:**  
AWS best practices for:  
- **Operational Excellence**  
- **Security**  
- **Reliability**  
- **Performance Efficiency**  
- **Cost Optimization**  
---

### **26. What is AWS Direct Connect?**  
**Answer:**
**Dedicated network connection from on-premises to AWS (bypasses public internet).  
---
### **27. What is AWS WAF?**  
**Answer:**  
**Web Application Firewall** protects against SQL injection, XSS.  
---
### **28. What is AWS Shield?**  
**Answer:**  
DDoS protection service (Standard & Advanced tiers).  
---
### **29. What is AWS Organizations?**  
**Answer:**  
Manages multiple AWS accounts under a single master account.  
---
### **30. What is AWS Config?**  
**Answer:**  
Tracks resource configurations and compliance.  
---

### **Networking & Hybrid Cloud**

### **31. What is AWS Transit Gateway?**  
**Answer:**  
A hub-and-spoke model for connecting multiple VPCs and on-premises networks centrally.  
- Simplifies network management (replaces VPC peering).  

---

### **32. Difference between NAT Gateway and NAT Instance?**  
| **NAT Gateway** | **NAT Instance** |  
|------------------|------------------|  
| Managed by AWS (no maintenance) | Self-managed EC2 instance |  
| Scales automatically | Manual scaling required |  

---

### **33. What is AWS PrivateLink?**  
**Answer:**  
Securely exposes services to other VPCs **without using public internet/VPN**.  
- Uses **VPC Endpoints**.  

---

### **34. Explain VPC Flow Logs.**  
**Answer:**  
Captures IP traffic metadata in a VPC (for security/network monitoring).  
- Logs stored in **S3/CloudWatch**.  

---

## **Security & Compliance**

### **35. What is AWS Secrets Manager?**  
**Answer:**  
Stores and rotates **database credentials, API keys** securely.  
- Alternative: **Parameter Store (SSM)** for non-secret configs.  

---

### **36. What is AWS GuardDuty?**  
**Answer:**  
AI-powered **threat detection** service (monitors VPC, S3, DNS logs).  

---

### **37. Difference between IAM Roles and Policies?**  
**Answer:**  
- **Policy:** JSON document defining permissions (e.g., `S3ReadOnly`).  
- **Role:** Temporary credentials assigned to AWS services/users.  

---

### **38. What is AWS Artifact?**  
**Answer:**  
Portal for **compliance reports** (e.g., SOC, ISO).  

---

## **Database & Analytics**

### **39. What is Amazon Redshift?**  
**Answer:**  
Fully managed **data warehouse** for analytics (SQL-based).  

---

### **40. When to use ElastiCache?**  
**Answer:**  
In-memory caching (Redis/Memcached) for **low-latency apps** (e.g., session stores).  

---

### **41. What is AWS Athena?**  
**Answer:**  
Serverless **SQL query service** for S3 data (uses Presto).  

---

### **42. What is AWS Glue?**  
**Answer:**  
ETL (Extract, Transform, Load) service for **data preparation**.  

---

## **DevOps & CI/CD**

### **43. What is AWS CodeBuild?**  
**Answer:**  
Fully managed **build service** (compiles code, runs tests).  

---

### **44. What is AWS Systems Manager (SSM)?**  
**Answer:**  
Manages EC2 instances at scale (patch management, run commands).  

---

### **45. What is AWS OpsWorks?**  
**Answer:**  
Managed **Chef/Puppet** for configuration automation.  

---

## **Serverless & Event-Driven**

### **46. What is Amazon EventBridge?**  
**Answer:**  
Serverless **event bus** for connecting AWS services/SaaS apps.  

---

### **47. What is Step Functions?**  
**Answer:**  
Orchestrates **Lambda functions** into workflows (state machines).  

---

### **48. What is SQS vs. SNS?**  
| **SQS (Queue)** | **SNS (Pub/Sub)** |  
|-----------------|------------------|  
| Pull-based (consumers poll) | Push-based (fanout) |  
| 1:1 messaging | 1:many messaging |  

---

## **Migration & Storage**

### **49. What is AWS Storage Gateway?**  
**Answer:**  
Hybrid storage service (connects on-premises to S3/Glacier).  

---

### **50. What is AWS DataSync?**  
**Answer:**  
High-speed **data transfer** between on-premises and AWS.  

---

### **51. What is AWS Backup?**  
**Answer:**  
Centralized backup for **EBS, RDS, DynamoDB, etc.**  

---

## **Advanced Architecting**

### **52. What is the CAP Theorem?**  
**Answer:**  
Distributed systems can only guarantee 2 of 3:  
- **Consistency**  
- **Availability**  
- **Partition Tolerance**  

---

### **53. Explain Blue/Green Deployment.**  
**Answer:**  
- **Blue:** Live environment.  
- **Green:** New deployment (traffic switched after testing).  

---

### **54. What is Circuit Breaker Pattern?**  
**Answer:**  
Stops requests to a failing service (prevents cascading failures).  

---

## **Monitoring & Performance**

### **55. What is AWS X-Ray?**  
**Answer:**  
Traces requests in **microservices** for debugging latency issues.  

---

### **56. What is AWS Trusted Advisor?**  
**Answer:**  
Provides **cost/security/performance** recommendations.  

---

## **Cost Optimization**

### **57. What is AWS Cost Explorer?**  
**Answer:**  
Visualizes **cost/spending trends** with filters.  

---

### **58. What are Spot Instances?**  
**Answer:**  
Discounted EC2 instances (up to 90% off) with **interruptible** capacity.  

---

## **Disaster Recovery Strategies**

### **59. Explain Pilot Light DR.**  
**Answer:**  
Minimal version of core systems runs in AWS (scales up during failover).  

---

### **60. What is AWS Elastic Disaster Recovery (DRS)?**  
**Answer:**  
Automates **lift-and-shift** DR for on-premises apps to AWS.  

---

## **AI/ML Services**

### **61. What is Amazon SageMaker?**  
**Answer:**  
Fully managed **machine learning** service (build/train/deploy models).  

---

### **62. What is Amazon Rekognition?**  
**Answer:**  
AI service for **image/video analysis** (object detection, facial recognition).  

---

## **IoT & Edge Computing**

### **63. What is AWS IoT Core?**  
**Answer:**  
Managed service for **IoT device connectivity** (MQTT/HTTP).  

---

### **64. What is AWS Greengrass?**  
**Answer:**  
Extends AWS to **edge devices** (run Lambda locally).  

---

## **Containers & Kubernetes**

### **65. What is Amazon ECR?**  
**Answer:**  
**Docker container registry** (integrated with ECS/EKS).  

---

### **66. What is AWS Fargate?**  
**Answer:**  
Serverless **container runtime** (no EC2 management).  

---

## **Hybrid Cloud**

### **67. What is AWS Storage Gateway?**  
**Answer:**  
Connects on-premises apps to **S3, EBS, Glacier**.  

---

### **68. What is AWS Outposts?**  
**Answer:**  
AWS hardware **deployed in your data center** (hybrid cloud).  

---

## **Security & Identity**

### **69. What is AWS Cognito?**  
**Answer:**  
Managed **user authentication** for apps (supports OAuth/SAML).  

---

### **70. What is AWS Inspector?**  
**Answer:**  
Automated **security assessments** for EC2 instances.  

---

## **Database & Analytics**

### **71. What is Amazon Neptune?**  
**Answer:**  
Managed **graph database** (for social networks, fraud detection).  

---

### **72. What is Amazon Timestream?**  
**Answer:**  
Serverless **time-series database** (IoT, monitoring).  

---

## **Serverless**

### **73. What is AWS AppSync?**  
**Answer:**  
Managed **GraphQL** service (real-time data sync).  
---
### **74. What is Amazon MQ?**  
**Answer:**  
Managed **message broker** (Apache ActiveMQ/RabbitMQ).  
---
## **Migration**
### **75. What is AWS Migration Hub?**  
**Answer:**  
Tracks **application migrations** across AWS tools.  
---
### **76. What is AWS Server Migration Service (SMS)?**  
**Answer:**  
Automates **VM migration** from on-premises to AWS.  
---
## **Advanced Networking**
### **77. What is AWS Global Accelerator?**  
**Answer:**  
Improves performance by routing traffic over AWS’s **global network**.  
---
### **78. What is AWS VPN CloudHub?**  
**Answer:**  
Connects multiple sites via **hub-and-spoke VPN**.  
---
## **Governance**
### **79. What is AWS Control Tower?**  
**Answer:**  
Sets up **multi-account AWS environments** with best practices.  
---
### **80. What is AWS Service Catalog?**  
**Answer:**  
Manages approved **IT service portfolios** for users.  
---
## **Cost Optimization**

### **81. What is AWS Compute Optimizer?**  
**Answer:**  
Recommends **EC2 instance types** for cost/performance.  
---
### **82. What are Savings Plans?**  
**Answer:**  
Commitment-based discounts (like RIs but flexible).  
---
## **Disaster Recovery**
### **83. What is AWS Backup?**  
**Answer:**  
Centralized **backup management** across services.  
---
### **84. What is AWS Resilience Hub?**  
**Answer:**  
Assesses **application resilience** against failures.  
---
## **AI/ML**
### **85. What is Amazon Comprehend?**  
**Answer:**  
NLP service for **text analysis** (sentiment, entities).  
---
## **86. What is Amazon Lex?**  
**Answer:**  
Builds **chatbots** (powers Alexa).  
---
## **IoT**
## **87. What is AWS IoT Analytics?**  
**Answer:**  
Processes **IoT device data** at scale.  
---
### **88. What is AWS IoT Greengrass?**  
**Answer:**  
Runs **Lambda functions** on edge devices.  

---

## **Containers**

### **89. What is Amazon EKS Anywhere?**  
**Answer:**  
Run **EKS on-premises**.  
---
### **90. What is AWS App Runner?**  
**Answer:**  
Deploys **containerized apps** without infra management.  
---
## **Hybrid Cloud**
## **91. What is AWS Local Zones?**  
**Answer:**  
Extends AWS regions to **metro areas** (low-latency apps).  
---
### **92. What is AWS Wavelength?**  
**Answer:**  
Embeds AWS in **5G networks** (ultra-low latency).  
---
## **Security**
### **93. What is AWS Macie?**  
**Answer:**  
Discovers/protects **sensitive data** in S3 (PII, credentials).  
---
### **94. What is AWS Firewall Manager?**  
**Answer:**  
Central **WAF/Security Groups** management.  
---
## **Database**
### **95. What is Amazon DocumentDB?**  
**Answer:**  
MongoDB-compatible **document database**.  
---
### **96. What is Amazon Keyspaces?**  
**Answer:**  
Managed **Apache Cassandra** service.  
---
## **Serverless**
### **97. What is AWS Lambda Edge?**  
**Answer:**  
Runs Lambda at **CloudFront Edge Locations**.  
---
### **98. What is Amazon EventBridge Schemas?**  
**Answer:**  
Discovers/creates **event schemas** for apps.  
---
## **Migration**
### **99. What is AWS Database Migration Service (DMS)?**  
**Answer:**  
Migrates databases to AWS **with minimal downtime**.  
---
### **100. What is AWS Application Discovery Service?**  
**Answer:**  
Collects **on-premises app data** for migration planning.  
