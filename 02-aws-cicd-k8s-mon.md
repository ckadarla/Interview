Alright — here’s your **Interview Quick Card** — a **one-page cheat sheet** combining the **rapid-fire essentials + 3 high-impact STAR stories** + **keywords from your JD** so you can glance at it during a virtual interview.

---

# **DevOps Engineer Interview Quick Card**

---

## **🚀 Rapid-Fire Essentials (Top 15)**

1. **AWS Durability (S3)** – 11 nines (99.999999999%).
2. **EKS Control Plane** – AWS-managed, HA, multi-AZ.
3. **Service Types** – ClusterIP, NodePort, LoadBalancer, ExternalName.
4. **HPA Metrics** – CPU, memory, custom metrics.
5. **Rolling Update** – `maxUnavailable`, `maxSurge`.
6. **Terraform Backend** – S3 + DynamoDB for lock.
7. **GitOps Tools** – Argo CD, Flux.
8. **CI vs CD** – CI = build/test, CD = deploy.
9. **CrashLoopBackOff** – Logs, probes, limits, config.
10. **Secrets Management** – AWS Secrets Manager / Sealed-Secrets.
11. **StatefulSet Use** – Persistent, ordered workloads.
12. **Image Scanning Tools** – Trivy, AquaSec.
13. **Multi-AZ vs Multi-Region** – HA vs DR.
14. **WAF Function** – Block malicious requests at L7.
15. **Drift Detection** – Argo CD sync status, `terraform plan`.

---

## **📌 STAR Stories (Ultra-Short)**

**1. Automated EKS Provisioning**

* **S:** Needed secure multi-tenant clusters for banks.
* **T:** Automate & ensure compliance.
* **A:** Terraform + Helm + Argo CD + image scanning.
* **R:** 3 days → 4 hours, 90% fewer errors, 100% audit pass.

**2. AWS Cost Optimization**

* **S:** High AWS spend due to overprovisioning.
* **T:** Cut costs without SLA impact.
* **A:** Karpenter, Spot, right-sizing, Savings Plans.
* **R:** 35% savings (\~\$240K/year).

**3. Deployment Reliability Fix**

* **S:** Frequent rollbacks in banking apps.
* **T:** Improve success rate.
* **A:** DB migration checks, readiness probes, canary deploy.
* **R:** 70% → 96% success rate, 60% fewer rollbacks.

---

## **🔑 Keywords from JD (Weave Into Answers)**

AWS (EC2, VPC, S3, RDS, Lambda, SNS, ECR)
EKS / Kubernetes / Helm / Ingress / HPA / Network Policy
Terraform / Ansible / AWS SAM
Argo CD / GitOps / RBAC / Rollback
CI/CD – Jenkins / Bitbucket / Jira Integration
Bash / Python Scripting
Linux (Ubuntu, RHEL, CentOS)
Datastores – MySQL / PostgreSQL / Redis
Security – IAM, KMS, Secrets Manager, Image Scanning
Monitoring – Prometheus, Grafana, Fluent Bit

---

✅ **Usage Tip:**

* Keep answers **crisp, keyword-rich, and confident**.
* For technical questions → 3-step: **Concept → Example → Tool Used**.
* For scenario questions → **S-T-A-R** in 30–45 seconds.

---
Perfect — here’s your **High-Impact STAR Stories Sheet** tailored to your resume and the DevOps Engineer JD.
These are **ready-made success stories** for “Tell me about a time when…” questions — you can adapt wording based on interviewer style.

---

## **1. Automating Kubernetes Cluster Provisioning**

**Situation:**
At LTI Mindtree, we needed to provision multiple secure Kubernetes clusters for banking clients (EKS, AKS, GKE) with strict compliance requirements.
**Task:**
Deliver fully automated, compliant, multi-tenant clusters with minimal manual intervention.
**Action:**

* Built modular **Terraform/Terragrunt** templates for multi-cloud cluster creation.
* Integrated **Helm** for workload deployment with RBAC, network policies, and pod security.
* Automated image scanning with **Trivy/AquaSec** in CI/CD.
* Implemented GitOps with **Argo CD** for continuous sync and rollback.
  **Result:**
  Provisioning time reduced from **3 days to 4 hours**, compliance audit pass rate improved to **100%**, and reduced manual errors by **90%**.

---

## **2. Reducing AWS Cloud Costs**

**Situation:**
Client’s AWS costs were rising due to overprovisioned EC2/EKS nodes and unused resources.
**Task:**
Optimize AWS cloud spend without impacting performance.
**Action:**

* Right-sized EC2 instances and EKS node groups.
* Introduced **Karpenter** for dynamic scaling.
* Applied **AWS Compute Savings Plans** and moved non-critical workloads to **Spot Instances**.
* Automated **off-hours scale-down** with Lambda.
  **Result:**
  Achieved **35% monthly cost savings** (\~\$240K/year) while maintaining SLA compliance.

---

## **3. Disaster Recovery Implementation for EKS Workloads**

**Situation:**
A major financial services client required DR capability for Kubernetes workloads.
**Task:**
Implement a disaster recovery plan ensuring minimal downtime.
**Action:**

* Deployed **Velero** for EKS backups and restores.
* Enabled **cross-region replication** for RDS, S3, and Terraform state.
* Automated DR failover testing in staging environments.
* Documented runbooks for the operations team.
  **Result:**
  RTO reduced from **12 hours to under 1 hour**, with zero data loss in DR drills.

---

## **4. Improving Deployment Reliability in Banking Apps**

**Situation:**
Frequent deployment rollbacks due to DB schema mismatches and readiness probe failures.
**Task:**
Increase deployment success rate while ensuring compliance.
**Action:**

* Integrated **Liquibase** DB migration checks in CI/CD pipelines.
* Enforced readiness/liveness probes before service routing.
* Introduced **canary deployments** for early failure detection.
  **Result:**
  Deployment success rate increased from **70% to 96%**, with 60% fewer rollbacks.

---

## **5. Securing Container Images Across Environments**

**Situation:**
Security audits found vulnerabilities in production container images.
**Task:**
Ensure all container images are secure before deployment.
**Action:**

* Built an **image security pipeline** using Trivy + AquaSec + Cosign signing.
* Enforced policy that only signed, vulnerability-free images can be deployed via Argo CD.
* Set up alerts for new CVEs affecting existing workloads.
  **Result:**
  Zero critical CVEs in production images for **12 consecutive months**.

---

## **6. Multi-Cloud GitOps Implementation**

**Situation:**
Needed a unified deployment strategy across AWS EKS, Azure AKS, and GCP GKE.
**Task:**
Implement GitOps for all clusters to ensure consistency.
**Action:**

* Designed Argo CD apps for each environment with branch-based separation.
* Automated sync with manual approvals for production.
* Applied RBAC to restrict who can promote deployments.
  **Result:**
  Deployment consistency improved across all environments; **mean time to deploy reduced by 50%**.

---

## **7. Handling a Major Production Outage**

**Situation:**
A production EKS cluster outage due to CoreDNS crash caused service downtime.
**Task:**
Restore services quickly and prevent recurrence.
**Action:**

* Identified root cause: misconfigured ConfigMap after a manual change.
* Restored previous ConfigMap from Argo CD history.
* Implemented drift detection to block manual config changes.
  **Result:**
  Services restored in **18 minutes**, and no similar outages in the following year.

---

Here’s your **Rapid-Fire Interview Sheet** — designed so you can respond **quickly and confidently** in interviews.
Answers are **short, keyword-heavy, and to the point**, aligned with **your JD + resume**.

---

## **Rapid-Fire DevOps / AWS / Kubernetes Q\&A**

### **AWS**

1. **Default VPC CIDR?** – `172.31.0.0/16`
2. **EC2 stop vs terminate?** – Stop keeps EBS, terminate deletes.
3. **S3 durability?** – `99.999999999%` (11 nines).
4. **IAM role vs user?** – Role = temp credentials, User = permanent.
5. **EKS control plane hosted where?** – AWS-managed.
6. **ALB vs NLB?** – ALB = L7, NLB = L4.
7. **Spot instance use case?** – Batch, non-critical workloads.
8. **CloudFormation vs Terraform?** – CF = AWS native, TF = multi-cloud.
9. **AWS Secrets Manager vs SSM Parameter Store?** – Secrets rotation vs static config.
10. **RDS Multi-AZ purpose?** – High availability failover.

---

### **Kubernetes / EKS**

11. **kubectl get pods -A?** – Lists all namespace pods.
12. **Pod vs Deployment?** – Pod = 1+ containers, Deployment = manages pods.
13. **Service types?** – ClusterIP, NodePort, LoadBalancer, ExternalName.
14. **HPA metric?** – CPU, memory, custom metrics.
15. **Readiness probe purpose?** – Traffic only to ready pods.
16. **ConfigMap vs Secret?** – Plain text vs base64 encoded & secure.
17. **Rolling update strategy?** – `maxUnavailable` / `maxSurge`.
18. **StatefulSet use case?** – Persistent, ordered pods.
19. **Ingress controller role?** – Route external traffic into cluster.
20. **CrashLoopBackOff fix?** – Logs, events, resource limits, probe check.

---

### **Terraform / IaC**

21. **terraform init?** – Initialize backend & plugins.
22. **terraform plan?** – Show changes before apply.
23. **terraform state purpose?** – Track infra resources.
24. **Variables.tf usage?** – Input parameterization.
25. **Drift detection?** – `terraform plan` vs state.
26. **Terraform backend?** – Store state remotely (S3/DynamoDB).
27. **TF module use case?** – Reusable infra blocks.
28. **taint command?** – Force recreate resource.
29. **tfsec purpose?** – IaC security scanning.
30. **Terraform vs Ansible?** – Provision infra vs configure infra.

---

### **GitOps / CI-CD**

31. **GitOps key tools?** – Argo CD, Flux.
32. **Argo CD sync policies?** – Auto-sync, manual.
33. **Rollback in Argo CD?** – Select previous revision.
34. **CI vs CD?** – CI = build/test, CD = deploy.
35. **Bitbucket Pipeline file?** – `bitbucket-pipelines.yml`.
36. **Jenkins pipeline type?** – Scripted, declarative.
37. **SonarQube purpose?** – Code quality scanning.
38. **Artifact repo example?** – Nexus, Artifactory, ECR.
39. **Blue-Green deployment?** – Zero downtime switch.
40. **Canary deployment?** – Partial traffic rollout.

---

### **Linux / Scripting**

41. **Check disk usage?** – `df -h`
42. **Find top CPU process?** – `top` / `ps -aux --sort=-%cpu`
43. **Make script executable?** – `chmod +x script.sh`
44. **Crontab syntax?** – `minute hour day month weekday`
45. **Shebang meaning?** – Script interpreter declaration.
46. **Log rotation tool?** – `logrotate`
47. **Check open ports?** – `netstat -tulnp` / `ss -tuln`
48. **Kill process by name?** – `pkill -f process`
49. **SSH key generation?** – `ssh-keygen -t rsa`
50. **Archive folder?** – `tar -czvf archive.tar.gz folder`

---

### **Security / Best Practices**

51. **Least privilege principle?** – Minimum access needed.
52. **Kubernetes secret encryption?** – Enable envelope encryption.
53. **Image vulnerability scan tools?** – Trivy, AquaSec.
54. **IAM inline vs managed policy?** – Inline = single entity, managed = reusable.
55. **Pod Security Policy status?** – Deprecated → use OPA/Gatekeeper.
56. **EKS IRSA use case?** – Fine-grained IAM for pods.
57. **TLS termination?** – At ingress or load balancer.
58. **RDS encryption?** – KMS-based at rest.
59. **S3 public access block?** – Prevent accidental exposure.
60. **Drift in GitOps?** – Out-of-sync detected by Argo CD.

---

### **Troubleshooting**

61. **Pipeline failed at build stage?** – Check logs, dependencies, environment.
62. **EKS pod Pending?** – Node resources, scheduling, taints/tolerations.
63. **Service not reachable?** – DNS, endpoints, firewall.
64. **Terraform apply stuck?** – API limits, lock state check.
65. **AWS bill spike?** – Cost Explorer, unused resources, rightsizing.
66. **Argo CD app out-of-sync?** – Manual change outside Git.
67. **Pod OOMKilled?** – Increase memory limits.
68. **Slow website on ALB?** – Health checks, backend latency.
69. **Secret not injected in pod?** – Check mounts, RBAC, namespace.
70. **DNS not resolving in pod?** – CoreDNS, network policy.

---

### **Cloud Patterns & Governance**

71. **Multi-AZ vs Multi-Region?** – HA vs DR.
72. **S3 lifecycle policy?** – Move to cheaper storage/expire.
73. **Cloud tagging use case?** – Cost allocation, governance.
74. **VPC peering vs Transit Gateway?** – 1:1 vs hub-spoke.
75. **CloudFront purpose?** – CDN + caching.
76. **WAF function?** – Block malicious traffic.
77. **KMS CMK vs AWS-managed key?** – Customer control vs AWS managed.
78. **Cost optimization tool?** – AWS Trusted Advisor.
79. **Blue/Green DNS switch?** – Route53 weighted routing.
80. **Service quota increase?** – AWS Support request.

---
Alright — here’s an **extended set of Q\&A** focusing on **scenario-based, troubleshooting, and deep-dive** questions for your JD + resume alignment.

---

## **Advanced & Scenario-Based Q\&A**

### **11. How would you design a highly available EKS cluster for production workloads?**

**Answer:**
I’d provision an EKS cluster across at least 3 Availability Zones for HA. Worker nodes would be in multiple subnets (private for workloads, public for ingress). I’d enable cluster autoscaler, set up managed node groups, and integrate an ALB Ingress Controller for routing. For persistence, I’d use EBS or EFS depending on workloads. Security would include network policies, RBAC, IRSA for pods, and Secrets Manager for sensitive data. Monitoring via Prometheus + Grafana, and logging via Fluent Bit to CloudWatch.

---

### **12. How do you manage secrets in your pipelines?**

**Answer:**
I avoid hardcoding secrets — instead, I integrate AWS Secrets Manager or SSM Parameter Store with pipelines. For Kubernetes, I use sealed-secrets or external-secrets operator to inject secrets at runtime. Access is controlled via IAM roles, ensuring least privilege. For example, in one project, we replaced all plain Kubernetes secrets with sealed-secrets encrypted via KMS, reducing exposure risks.

---

### **13. If a pod in EKS is in `CrashLoopBackOff`, how do you troubleshoot?**

**Answer:**

1. `kubectl describe pod` → check events & last exit code.
2. `kubectl logs` → review application logs.
3. Check readiness/liveness probe configurations.
4. Validate image pull secrets & container registry access.
5. If OOMKilled, adjust `resources.requests/limits`.
6. If config-related, fix environment variables or ConfigMaps.
   I also check node conditions (`kubectl get nodes`) to ensure no resource pressure.

---

### **14. How would you implement GitOps in a multi-environment setup?**

**Answer:**
I’d maintain separate Git branches or directories for `dev`, `stage`, and `prod` manifests. Argo CD would be configured with an application per environment, each pointing to the respective path/branch. Sync policies would differ — auto-sync for dev, manual approval for prod. Rollbacks would be handled via Argo CD’s revision history.

---

### **15. What’s your approach for disaster recovery in AWS?**

**Answer:**
For EKS workloads, I’d back up etcd snapshots (via Velero) and persistent volumes (EBS/EFS). For databases, I’d enable automated RDS snapshots and cross-region replication. S3 buckets would have versioning and replication enabled. Terraform state would be stored in S3 with cross-region replication for infra restore.

---

### **16. How do you optimize AWS costs for Kubernetes workloads?**

**Answer:**

* Use spot instances for non-critical workloads with mixed node groups.
* Apply right-sizing recommendations for EC2 and RDS.
* Schedule node scale-down during off-hours.
* Implement AWS Compute Savings Plans.
* In one project, I cut EKS costs by 35% using Karpenter for dynamic node provisioning.

---

### **17. If a Terraform apply fails halfway, what’s your next step?**

**Answer:**
First, I’d check the error logs to see if it’s a syntax error, API rate limit, or dependency issue. I’d run `terraform plan` again to see the drift, then either fix the code or use `terraform taint` on failed resources before re-applying. For state corruption, I’d lock and manually adjust the S3 state file with DynamoDB lock table.

---

### **18. How do you ensure container image security before deployment?**

**Answer:**

* Build images from minimal base images.
* Run vulnerability scans with Trivy/AquaSec.
* Sign images using Cosign.
* Store in a private registry (ECR) with lifecycle policies.
* At LTI, I enforced image scanning as a mandatory pipeline stage before pushing to ECR.

---

### **19. How do you handle Kubernetes config drift?**

**Answer:**
Using GitOps with Argo CD prevents drift — any out-of-band changes trigger a “diff” alert. We can auto-sync or revert changes to match Git. For Terraform, I use drift detection via `terraform plan` in a scheduled pipeline.

---

### **20. Describe a time when you improved deployment reliability.**

**Answer:**
In one client’s banking application, deployments often failed due to schema mismatches. I introduced database migration checks in CI/CD, health probes for early failure detection, and pre-prod canary testing. This reduced deployment rollbacks by 60% and improved release confidence.

---
Got it — I’ll prepare **interview Q\&A tailored to the JD** you shared, but aligned with **your resume strengths** so your answers sound both technically deep and experience-backed.

---

## **Interview Q\&A for DevOps Engineer (AWS, EKS, IaC, GitOps)**

### **1. Tell me about your experience with AWS cloud infrastructure.**

**Answer:**
I have over a decade of hands-on AWS experience, provisioning and managing services like EC2, VPC, S3, RDS, EKS, Lambda, and SNS. I’ve implemented these via both AWS CLI and Terraform, ensuring compliance with IAM policies, security groups, tagging standards, and cost optimization dashboards. For example, at LTI Mindtree, I provisioned multi-account AWS environments with Terraform/Terragrunt modules, integrated AWS KMS for encryption, and maintained cost visibility through AWS Cost Explorer and custom Grafana dashboards.

---

### **2. How have you managed Kubernetes deployments on EKS or equivalent?**

**Answer:**
I’ve deployed and managed Kubernetes workloads on AWS EKS, Azure AKS, and GCP GKE. My experience covers authoring Helm charts, configuring ingress controllers like NGINX and ALB Ingress, implementing HPA/VPA for autoscaling, setting resource quotas, and defining liveness/readiness probes. In banking projects, I applied network policies and Pod Security Policies to meet strict compliance, integrated image scanning tools like Trivy and AquaSec into pipelines, and resolved CVEs before deployments.

---

### **3. How do you approach Infrastructure as Code (Terraform / Ansible / AWS SAM)?**

**Answer:**
I follow a modular IaC approach — creating reusable Terraform modules with remote state management (S3 + DynamoDB locking), enforcing linting with TFLint, and ensuring drift detection via Terraform Cloud or Atlantis. I’ve used Ansible for OS patching and configuration management, and AWS SAM for packaging and deploying serverless workloads like Lambda + API Gateway. For example, I automated EKS cluster provisioning with Terraform, Ansible-based node configuration, and integrated them into a CI/CD workflow.

---

### **4. What’s your experience with GitOps?**

**Answer:**
I’ve implemented GitOps using Argo CD across multi-environment Kubernetes deployments. This included configuring automated and manual sync policies, setting rollback strategies, and applying RBAC for deployment control. At LTI, GitOps enabled zero-touch deployments for microservices — developers committed changes to Git, Argo CD synced them to EKS, and security scans ran pre-deployment.

---

### **5. Can you explain a CI/CD pipeline you’ve built?**

**Answer:**
I’ve built pipelines using Jenkins, Bitbucket Pipelines, and Azure DevOps. A typical flow involved:

* Build & Unit Test → Container Image Build (Kaniko or Docker) → Image Scan (Trivy/AquaSec) → Deploy to Dev via Argo CD → Automated Functional Tests → Manual Approval for Staging/Prod.
  At Excelra, I integrated Jira for issue tracking and Bitbucket for version control, ensuring traceability from commit to deployment.

---

### **6. How comfortable are you with scripting?**

**Answer:**
I regularly write Bash and Python scripts for automation tasks like log rotation, backup scheduling, automated failover checks, and validation scripts for Kubernetes deployments. For example, I wrote a Python script to validate Kubernetes RBAC policies against a compliance matrix before deployment.

---

### **7. What’s your Linux administration experience?**

**Answer:**
I’m proficient with Ubuntu, RHEL, and CentOS. My tasks have included package installation, performance tuning, configuring NGINX/Apache for SSL termination, setting up reverse proxies, and implementing security hardening. I also automate Linux server provisioning via Ansible.

---

### **8. How have you managed databases in your DevOps work?**

**Answer:**
I’ve managed MySQL, PostgreSQL, and Redis — including provisioning, backups (mysqldump, pg\_dump, RDS snapshots), replication setup, and performance tuning. I’ve also integrated database migrations into CI/CD pipelines to avoid downtime during deployments.

---

### **9. How do you ensure security and compliance in your deployments?**

**Answer:**
Security is integrated at every stage — from IaC scanning (tfsec, checkov) to container image scanning, IAM least privilege policies, and encryption (AWS KMS, Secrets Manager). I also work closely with SOC teams to perform vulnerability scans and meet industry regulations, particularly in banking and finance.

---

### **10. Describe a challenging DevOps problem you solved.**

**Answer:**
In one project, we faced failed EKS rollouts due to resource quota exhaustion in the staging namespace. I identified unused deployments consuming resources, implemented namespace-specific quotas, and optimized HPA settings. This reduced deployment failures by 80% and improved environment stability.

---
