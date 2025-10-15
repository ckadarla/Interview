
# DevOps/Kubernetes/SRE Interview Questions and Answers

## Section 1: Cloud Infrastructure & Kubernetes

### 1. Q: How do you provision a new Kubernetes cluster on a cloud provider like AWS or GCP?

A: You can provision Kubernetes using managed services like EKS (AWS), GKE (GCP), or AKS (Azure) via Infrastructure as Code tools like Terraform. The process includes defining the cluster specs (node pools, networking, IAM roles) and applying the configuration using Terraform CLI or automation pipelines.

### 2. Q: What is the role of kubeadm in Kubernetes provisioning?

A: kubeadm is a tool to bootstrap a Kubernetes cluster manually. It handles tasks like initializing the control plane, joining nodes, and setting up the required certificates.

### 3. Q: How do you troubleshoot a failing pod in Kubernetes?

A: Use kubectl describe pod <pod-name> and kubectl logs <pod-name> to examine events, container logs, and error messages. You can also exec into the pod to check the environment.

### 4. Q: How do you implement node auto-scaling in a Kubernetes cluster?

A: Use Cluster Autoscaler to automatically add or remove nodes based on pod resource requests and current usage.

### 5. Q: What is the difference between DaemonSet and Deployment in Kubernetes?

A: DaemonSet ensures a pod runs on all (or some) nodes, typically for system-level services like log collectors. Deployment manages stateless pods and ensures the desired number of replicas are running.

## Section 2: Observability and Monitoring

### 6. Q: What are the key components of Prometheus?

A: Prometheus consists of the core server, exporters, Alertmanager, and storage backend. It scrapes metrics from targets, stores time-series data, and triggers alerts based on defined rules.

### 7. Q: How does Grafana integrate with Prometheus?

A: Grafana uses Prometheus as a data source to visualize time-series data. Dashboards can be created using PromQL queries to provide insights into metrics.

### 8. Q: How would you monitor a Kubernetes cluster?

A: Deploy Prometheus Operator, kube-state-metrics, and node-exporter for metrics collection, and visualize them using Grafana. Use kubelet metrics and alerts to monitor node and pod health.

### 9. Q: What’s the difference between black-box and white-box monitoring?

A: Black-box monitoring checks the availability of services externally (e.g., ping, HTTP). White-box monitoring gathers internal metrics from applications or systems (e.g., CPU, memory).

### 10. Q: What types of alerts would you configure for Kubernetes?

A: Alert on high pod restart count, node disk pressure, CPU/memory usage, crash loops, and application-specific thresholds.

## Section 3: Security & Hardening

### 11. Q: How do you secure a Kubernetes cluster?

A: Enable RBAC, use network policies, encrypt etcd at rest, enable audit logging, run CIS benchmarks, and manage secrets using tools like Vault or Kubernetes Secrets.

### 12. Q: What is PodSecurityPolicy or PodSecurityAdmission?

A: These are mechanisms to control security-related aspects of pod specification such as privileged access, volume types, or host networking.

### 13. Q: How do you handle CVE patches in a Kubernetes environment?

A: Monitor CVE feeds, use image scanners (like Trivy), apply upstream patches, upgrade base images, and patch OS packages regularly via automation tools.

### 14. Q: How would you restrict access to the Kubernetes dashboard?

A: Disable the dashboard if not needed; otherwise, restrict access using RBAC, OAuth authentication, or proxy with access controls.

### 15. Q: What is mTLS and how is it used in service communication?

A: Mutual TLS (mTLS) is a mechanism to encrypt communication and authenticate clients and servers using certificates. In Kubernetes, it can be enforced via service meshes like Istio.

## Section 4: Infrastructure as Code (Terraform)

### 16. Q: How do you manage Terraform state?

A: Store it remotely using backends like AWS S3, Azure Storage, or GCP Cloud Storage. Use state locking mechanisms like DynamoDB or GCS locks to prevent race conditions.

### 17. Q: What are Terraform modules and why use them?

A: Modules are reusable Terraform components. They help in DRY (Don't Repeat Yourself) practices and managing infrastructure as logical units.

### 18. Q: What is the difference between terraform apply and terraform plan?

A: terraform plan shows a preview of changes; terraform apply executes those changes to provision/update infrastructure.

### 19. Q: How do you manage sensitive data in Terraform?

A: Avoid hardcoding. Use variable files, secret managers (like AWS Secrets Manager, Vault), and environment variables with secure backends.

### 20. Q: How do you implement drift detection in Terraform?

A: Use terraform plan regularly and compare state with actual infrastructure. Tools like Terraform Cloud/Enterprise or Atlantis can automate this.

## Section 5: Automation & Scripting

### 21. Q: What are some typical use cases for Bash scripting in DevOps?

A: Automating system tasks, log rotation, service restarts, backups, and file processing are common Bash use cases.

### 22. Q: Provide an example where Python was more effective than Bash.

A: Complex file parsing, REST API interactions, and structured data handling (e.g., JSON, YAML) are better handled in Python due to its readability and libraries.

### 23. Q: How do you automate patching of Linux systems?

A: Use cron jobs, Ansible playbooks, or package managers (apt/yum) with automation tools like AWS SSM Patch Manager or OS native schedulers.

### 24. Q: What’s your approach to writing idempotent scripts?

A: Ensure scripts can run multiple times without unintended side effects. Check for resource existence before creation and avoid duplicate operations.

### 25. Q: What are Python libraries you’ve used for DevOps automation?

A: boto3 (AWS), requests (API calls), subprocess (command execution), os/sys (system interaction), json/yaml (config parsing).

## Section 6: CI/CD Tooling

### 26. Q: What is a CI/CD pipeline?

A: A CI/CD pipeline automates code integration, testing, and deployment. It ensures faster feedback and reliable delivery.

### 27. Q: Describe a basic CI/CD pipeline structure.

A: Stages typically include source checkout, build, test, security scan, artifact storage, and deployment.

### 28. Q: How do you manage secrets in CI/CD pipelines?

A: Use secret managers (e.g., Azure Key Vault, HashiCorp Vault), or native CI secrets management with restricted access.

### 29. Q: What is canary deployment?

A: It gradually rolls out a new version to a small subset of users, reducing risk by monitoring before full rollout.

### 30. Q: How do you rollback a failed deployment?

A: Use versioned deployments (e.g., Helm), maintain stable artifacts, and automate rollback steps in the CI/CD workflow.

## Section 7: Advanced Kubernetes Topics

### 31. Q: What is an Ingress Controller in Kubernetes?

A: It manages external access to services using HTTP/S. Examples: NGINX, HAProxy, Traefik.

### 32. Q: What is OPA and how does it integrate with Kubernetes?

A: Open Policy Agent (OPA) enables policy-as-code. It can be integrated with Kubernetes via Gatekeeper to enforce admission policies.

### 33. Q: What is SUSE Rancher?

A: Rancher is a Kubernetes management platform that simplifies cluster provisioning, access control, and monitoring.

### 34. Q: What is Fleet in Rancher?

A: Fleet is a GitOps-based tool by Rancher to manage Kubernetes workloads across clusters using a centralized model.

### 35. Q: What are Kubernetes taints and tolerations?

A: Taints prevent pods from being scheduled on specific nodes unless they have matching tolerations.

## Section 8: Troubleshooting & Incident Response

### 36. Q: What steps do you follow during an incident?

A: Identify the alert, assess the impact, gather logs/metrics, mitigate the issue, communicate status, and perform post-mortem analysis.

### 37. Q: How do you debug high CPU usage in a pod?

A: Check resource limits, pod logs, profiling (using tools like py-spy or top), and Prometheus metrics.

### 38. Q: What tools help in log aggregation?

A: Elasticsearch, Fluentd/Fluent Bit, and Kibana (EFK stack), or Loki with Grafana for logs.

### 39. Q: What’s the role of liveness and readiness probes?

A: Liveness probes restart unhealthy containers; readiness probes control service availability in load balancers.

### 40. Q: What is a CrashLoopBackOff and how do you fix it?

A: It's a container crash loop. Use logs and probes to identify root cause, validate config/env vars, and adjust restart policy.

## Section 9: Soft Skills & Collaboration

### 41. Q: How do you collaborate with software engineers during deployments?

A: Use shared dashboards, ticketing systems, and Slack/Teams for real-time collaboration. Integrate CI/CD with feedback loops.

### 42. Q: How do you prioritize incidents vs feature work?

A: Based on impact and SLAs. Critical incidents take priority; automation helps in reducing firefighting.

### 43. Q: How do you document infrastructure?

A: Use version-controlled IaC, README files, wikis, and visual diagrams.

### 44. Q: How do you approach learning new tools?

A: Set up local labs, follow official docs, take hands-on tutorials, and participate in communities.

### 45. Q: How do you deal with cross-functional friction?

A: Communicate proactively, focus on shared goals, and hold regular syncs/retrospectives.

## Section 10: Miscellaneous

### 46. Q: What’s the role of OpenStack in cloud environments?

A: OpenStack is an open-source cloud platform used to manage compute, storage, and networking resources, especially in private clouds.

### 47. Q: What are StatefulSets in Kubernetes?

A: StatefulSets manage stateful applications, maintaining stable pod identity and storage.

### 48. Q: What is the role of namespaces in Kubernetes?

A: Namespaces isolate resources and access within a cluster, aiding multi-tenancy.

### 49. Q: What’s a use case for using Ansible in Kubernetes environments?

A: Bootstrap VM provisioning, manage kubeadm clusters, and deploy configs or custom apps outside Kubernetes.

### 50. Q: What tools do you recommend for Kubernetes cost monitoring?

A: Kubecost, CloudHealth, or native tools from cloud providers like AWS Cost Explorer or GCP Billing.

Would you like this content delivered as a downloadable file as well?
