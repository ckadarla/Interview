```markdown
### DevOps Interview Questions and Answers

#### Infrastructure Design & Automation

**Q1: How do you design a highly available architecture on AWS?**  
**A:** Use multiple Availability Zones for redundancy, Elastic Load Balancers for traffic distribution, Auto Scaling groups for scalability, and Route 53 for DNS failover.

**Q2: What is Infrastructure as Code (IaC)?**  
**A:** IaC is the process of managing and provisioning infrastructure through code instead of manual processes. Tools include Terraform, CloudFormation, etc.

**Q3: How do you implement IaC with Terraform?**  
**A:** Write `.tf` files to define infrastructure, use `terraform init`, `plan`, and `apply` to provision resources, and manage state files securely.

**Q4: Difference between Terraform and CloudFormation?**  
**A:** Terraform is open-source and supports multiple cloud providers, while CloudFormation is AWS-native. Terraform has better modularity and state management.

**Q5: How do you manage state in Terraform?**  
**A:** Use remote backends like S3 with state locking via DynamoDB. This allows team collaboration and state consistency.

## Containerization & Orchestration

**Q6: What is Docker and how does it work?**  
**A:** Docker is a containerization platform that packages applications with dependencies into containers, ensuring consistency across environments.

**Q7: How do you create and run a Docker container?**  
**A:** Create a `Dockerfile`, build with `docker build`, and run with `docker run`. Push images to Docker Hub or ECR for reuse.

**Q8: What is Kubernetes?**  
**A:** Kubernetes is an open-source container orchestration platform for automating deployment, scaling, and operations of containerized applications.

**Q9: What is AWS EKS?**  
**A:** Amazon Elastic Kubernetes Service (EKS) is a managed Kubernetes service that simplifies cluster operations and integrates with other AWS services.

**Q10: How do you monitor Kubernetes clusters?**  
**A:** Use Prometheus for metrics collection, Grafana for visualization, and tools like Fluentd/ELK for log aggregation.

## CI/CD Pipeline Development

**Q11: What is CI/CD?**  
**A:** Continuous Integration (CI) is automating code integration, and Continuous Delivery/Deployment (CD) automates application delivery to staging/production.

**Q12: How do you implement CI/CD with Jenkins?**  
**A:** Create Jenkins pipelines using declarative or scripted syntax. Integrate with Git, Docker, and Kubernetes for build-test-deploy automation.

**Q13: What is a Jenkinsfile?**  
**A:** It is a text file containing the pipeline as code, defining stages like build, test, and deploy.

**Q14: What are GitLab CI stages?**  
**A:** Stages like `build`, `test`, and `deploy` define the flow of the pipeline and each job execution order.

**Q15: How do you handle secrets in CI/CD pipelines?**  
**A:** Use secrets managers (AWS Secrets Manager, Vault) and environment variable encryption to avoid hardcoding sensitive data.

## Blue-Green Deployments & Release Management

**Q16: What is Blue-Green deployment?**  
**A:** It involves two identical environments. Blue is live; Green is idle. Deploy to Green, test, then switch traffic. Rollback by switching back to Blue.

**Q17: Difference between Blue-Green and Canary deployments?**  
**A:** Blue-Green switches 100% traffic at once; Canary gradually shifts traffic to the new version while monitoring metrics.

**Q18: How do you implement Blue-Green deployment on AWS?**  
**A:** Use Route 53 for DNS-based traffic switch, or ALB/Target Groups with ECS/EKS for seamless transition.

**Q19: How do you ensure zero-downtime deployment?**  
**A:** Use Blue-Green or Rolling deployment with readiness checks, auto-scaling, and health probes.

**Q20: How do you manage rollback in deployments?**  
**A:** Store previous versions as artifacts, use tags or versioning, and automate re-deployment of stable versions.

## Disaster Recovery & Backup Strategy

**Q21: What is Disaster Recovery (DR)?**  
**A:** DR is a strategy to recover from system failures with minimal downtime and data loss. Includes backups, failovers, and recovery plans.

**Q22: What are RTO and RPO?**  
**A:** RTO: time to restore service. RPO: acceptable data loss in time. Both define DR objectives.

**Q23: How do you implement DR on AWS?**  
**A:** Use cross-region backups, replication (e.g., RDS Multi-AZ), and Route 53 failover routing for quick recovery.

**Q24: What is the difference between Backup and DR?**  
**A:** Backup is data protection; DR is full system recovery. DR includes infrastructure restoration.

**Q25: Tools used for cloud backup?**  
**A:** AWS Backup, AWS DLM, third-party tools like Veeam, Rubrik, etc.

## Security & Compliance

**Q26: What are IAM roles?**  
**A:** IAM roles define temporary permissions for users/services. Used for secure access control in AWS.

**Q27: How do you enforce least privilege?**  
**A:** Define IAM policies granting only necessary permissions and review regularly.

**Q28: What is KMS?**  
**A:** AWS Key Management Service (KMS) manages encryption keys for securing data at rest and in transit.

**Q29: How do you implement compliance checks?**  
**A:** Use tools like AWS Config, GuardDuty, and CloudTrail. Implement automated security scans in CI/CD.

**Q30: How do you handle vulnerability scanning?**  
**A:** Use tools like Trivy, Clair, or commercial scanners (e.g., Snyk) integrated into pipelines.

## Collaboration & Mentorship

**Q31: How do you mentor junior engineers?**  
**A:** Through pair programming, code reviews, knowledge sharing sessions, and documentation.

**Q32: How do you promote DevOps culture?**  
**A:** Advocate for automation, continuous feedback, cross-team collaboration, and shared responsibility.

**Q33: How do you handle cross-functional collaboration?**  
**A:** Conduct regular syncs, use common tools (Jira, Confluence), and promote transparency in goals and blockers.

**Q34: What’s your approach to documentation?**  
**A:** Maintain runbooks, architecture diagrams, IaC comments, and wiki pages to ensure clarity and continuity.

**Q35: How do you stay updated in DevOps?**  
**A:** Follow tech blogs, attend webinars, contribute to open source, and experiment in lab environments.

## Core Competency & Tools

**Q36: What is VPC and how do you design it?**  
**A:** Virtual Private Cloud enables isolated networking in AWS. Design includes subnets, route tables, IGWs, and NATs.

**Q37: How do you secure data in transit and at rest in AWS?**  
**A:** Use TLS for in-transit, and KMS/SSE for at-rest encryption.

**Q38: How do you manage Kubernetes manifests?**  
**A:** Use YAML files, Helm charts, and Kustomize for configuration management and templating.

**Q39: What are Helm charts?**  
**A:** Helm charts are Kubernetes packages that define, install, and manage applications.

**Q40: How do you manage secrets in Kubernetes?**  
**A:** Use Kubernetes Secrets, integrate with external managers like AWS Secrets Manager or HashiCorp Vault.

**Q41: What’s your Git branching strategy?**  
**A:** Use GitFlow or trunk-based development. Feature branches, pull requests, and protected branches.

**Q42: What is your experience with Prometheus and Grafana?**  
**A:** Use Prometheus for metrics scraping and alerting. Grafana for dashboards and visualization.

**Q43: How do you automate scaling in Kubernetes?**  
**A:** Use HPA (Horizontal Pod Autoscaler), Cluster Autoscaler, and custom metrics.

**Q44: What’s your process for debugging production issues?**  
**A:** Analyze logs, monitor metrics, inspect pod/container health, and correlate deployments with issues.

**Q45: What is Canary deployment?**  
**A:** Gradual traffic shift to a new version to catch issues early without full rollout.

**Q46: What’s your scripting experience?**  
**A:** Proficient in Bash and Python. Used for automation scripts, data parsing, and integration tasks.

**Q47: How do you manage multi-environment deployments?**  
**A:** Use variables and workspaces in Terraform, or Helm values. Maintain separate config files.

**Q48: What’s your experience with GitOps?**  
**A:** Use Git as the single source of truth for declarative infrastructure and application deployments.

**Q49: How do you ensure code quality in DevOps?**  
**A:** Implement linters, automated testing, peer reviews, and enforce coding standards.

**Q50: What tools do you use for ticketing and collaboration?**  
**A:** Jira for issue tracking, Confluence for documentation, Slack/MS Teams for communication.
