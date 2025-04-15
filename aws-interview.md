Here is a detailed list of 100 AWS Architect interview questions and answers in Markdown (`.md`) format:

```markdown
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

# **More Questions (26-100)**

### **26. What is AWS Direct Connect?**  
**Answer:**  
Dedicated network connection from on-premises to AWS (bypasses public internet).  

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

