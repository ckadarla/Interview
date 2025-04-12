```markdown
Design and implement CI/CD pipelines using Azure DevOps (YAML pipelines preferred) for microservices-based applications.

Deploy, manage, and monitor applications in AKS (Azure Kubernetes Service).

Create and maintain Helm charts or Kubernetes manifests for application deployment.

Automate infrastructure provisioning using ARM templates, Bicep, or Terraform.

Collaborate with development and operations teams to ensure smooth deployments and reliable releases.

Configure and manage Kubernetes resources such as pods, deployments, services, ingress, and config maps.

Monitor system health, availability, and performance using Azure Monitor, Log Analytics, or Prometheus/Grafana.

Manage secrets and credentials using Azure Key Vault and Kubernetes secrets.

Ensure security best practices across build, release, and runtime environments.

Troubleshoot and resolve deployment and environment issues quickly and effectively.


```

# 🚀 Azure DevOps + AKS Engineer – Interview Q&A

A curated list of **50 technical interview questions and answers** specifically crafted for roles involving Azure DevOps, AKS, Infrastructure as Code (ARM/Bicep/Terraform), monitoring, security, and Kubernetes-based deployments.

---

## 📂 Table of Contents

1. [CI/CD with Azure DevOps](#cicd-with-azure-devops)
2. [Azure Kubernetes Service (AKS)](#azure-kubernetes-service-aks)
3. [Infrastructure as Code (Terraform / Bicep / ARM)](#infrastructure-as-code-terraform--bicep--arm)
4. [Kubernetes Resources & Helm](#kubernetes-resources--helm)
5. [Monitoring & Observability](#monitoring--observability)
6. [Security & Secrets Management](#security--secrets-management)
7. [Troubleshooting & Best Practices](#troubleshooting--best-practices)

```markdown
## CI/CD with Azure DevOps

**Q1. What are the key benefits of using YAML pipelines over Classic in Azure DevOps?**  
**A:** YAML pipelines are version-controlled, reusable, and portable. They support CI/CD as code and enable better collaboration and traceability.

**Q2. How do you trigger a pipeline on branch push or pull request in YAML?**  
```yaml
trigger:
  branches:
    include:
      - main

pr:
  branches:
    include:
      - main
```

**Q3. How do you pass variables between pipeline stages in Azure DevOps YAML?**  
**A:** Use `output variables`. Example:
```yaml
- task: Bash@3
  name: SetVar
  script: echo "##vso[task.setvariable variable=myVar;isOutput=true]Hello"
```

**Q4. How do you secure secrets in Azure DevOps pipelines?**  
**A:** Use variable groups linked to Azure Key Vault, mark secrets as sensitive, and avoid echoing them.

**Q5. How do you implement a multi-stage deployment pipeline in Azure DevOps YAML?**  
**A:** Define stages like `build`, `deploy-dev`, `deploy-prod`. Use approvals and conditions between them.

---

## Azure Kubernetes Service (AKS)

**Q6. What are the key components of AKS architecture?**  
**A:** Control plane (managed by Azure), node pools, kubelet, kube-proxy, Container Runtime (e.g., containerd).

**Q7. How do you deploy an application to AKS?**  
**A:** Use `kubectl apply -f manifest.yaml` or `helm install`, post-authentication via `az aks get-credentials`.

**Q8. How do you expose services externally in AKS?**  
**A:** Use `LoadBalancer` service type or Ingress controller (NGINX, Application Gateway).

**Q9. How do you configure RBAC in AKS?**  
**A:** Use `Role`, `ClusterRole`, `RoleBinding`, and `ClusterRoleBinding`. Integrate with Azure AD for secure auth.

**Q10. How do you perform node pool scaling in AKS?**  
**A:** Use `az aks nodepool scale` or configure autoscaler in cluster settings.

---

## Infrastructure as Code (Terraform / Bicep / ARM)

**Q11. What are the advantages of Bicep over ARM templates?**  
**A:** Bicep is cleaner, easier to read, modular, and supports automatic conversion to ARM JSON.

**Q12. How do you manage environments in Terraform?**  
**A:** Use workspaces, separate variable files, or modules with dynamic inputs.

**Q13. How do you provision an AKS cluster using Terraform?**  
**A:** Use `azurerm_kubernetes_cluster` resource. Define node pools, identity, and network config.

**Q14. What is the use of `depends_on` in Terraform?**  
**A:** Ensures resources are created in a specific order when dependencies aren't automatically inferred.

**Q15. How do you pass secrets or sensitive data in Terraform securely?**  
**A:** Use `sensitive = true`, environment variables, or integrate with Key Vault.

---

## Kubernetes Resources & Helm

**Q16. What is a Helm chart and how is it structured?**  
**A:** A Helm chart is a package with templated Kubernetes YAML files. It has folders like `templates/`, `values.yaml`, and `Chart.yaml`.

**Q17. How do you override Helm chart values during install?**  
```bash
helm install myapp ./mychart -f custom-values.yaml
```

**Q18. How do you roll back a Helm release?**  
```bash
helm rollback <release-name> <revision>
```

**Q19. What is a ConfigMap and when do you use it?**  
**A:** A ConfigMap stores non-sensitive configuration as key-value pairs. Use it for app settings, env variables, etc.

**Q20. How does a Kubernetes Deployment differ from a StatefulSet?**  
**A:** Deployment is for stateless apps; StatefulSet is for apps that need stable identity, like databases.

---

## Monitoring & Observability

**Q21. How do you monitor AKS with Azure Monitor?**  
**A:** Enable Container Insights, use metrics/alerts in Azure Monitor, and integrate with Log Analytics.

**Q22. How does Prometheus work in Kubernetes?**  
**A:** It scrapes `/metrics` endpoints via service discovery. Deployed via Helm or Operator in AKS.

**Q23. What is Log Analytics Workspace used for?**  
**A:** It aggregates logs from Azure services and resources. Used in conjunction with Azure Monitor.

**Q24. How do you set up alerts in Azure Monitor?**  
**A:** Create metric/log-based alerts using action groups and thresholds for metrics (CPU, memory, etc.)

**Q25. How can you visualize metrics in Grafana for AKS?**  
**A:** Use Azure Monitor or Prometheus data source. Configure dashboards for custom visualization.

---

## Security & Secrets Management

**Q26. How do you store and retrieve secrets in Azure Key Vault?**  
**A:** Store via Azure CLI/Portal. Access using SDKs, `az keyvault secret show`, or pipeline variable groups.

**Q27. How do you integrate Key Vault with Azure DevOps pipelines?**  
**A:** Link a variable group to Key Vault in Library. Ensure access policies allow pipeline identity.

**Q28. How do you use Kubernetes secrets securely?**  
**A:** Use base64-encoded values, encrypt at rest, and access via environment variables or volume mounts.

**Q29. What is pod security context?**  
**A:** Defines privilege settings for pods/containers—like running as non-root, readOnlyRootFilesystem.

**Q30. How do you restrict external traffic in AKS?**  
**A:** Use Network Policies, disable public IPs, use Private AKS, and restrict Ingress with WAF.

---

## Troubleshooting & Best Practices

**Q31. How do you troubleshoot a failing Kubernetes pod?**  
**A:** Use `kubectl describe pod`, `kubectl logs`, and check events for error details.

**Q32. What steps do you take when a YAML deployment fails?**  
**A:** Validate syntax (`kubectl apply --dry-run=client`), check resource quotas, logs, and error events.

**Q33. How do you diagnose Azure DevOps pipeline failures?**  
**A:** Examine logs, retry failed tasks, enable debug mode, use diagnostic tasks like `System.Debug`.

**Q34. What are readiness and liveness probes in Kubernetes?**  
**A:**
- **Readiness**: Checks if pod is ready to receive traffic
- **Liveness**: Checks if pod should be restarted

**Q35. What is the importance of resource requests and limits in K8s?**  
**A:** Prevents resource contention and ensures fair scheduling. Helps in autoscaling decisions.

**Q36. What are some AKS upgrade best practices?**  
**A:** Use staging environments, take backup of workloads, use drain/cordon, test with `--node-image-only`.

**Q37. What is a rolling deployment?**  
**A:** Kubernetes updates pods one by one to minimize downtime.

**Q38. What is the difference between horizontal and vertical pod autoscaling?**  
**A:**
- **Horizontal**: Adds/removes pods
- **Vertical**: Adjusts CPU/memory requests of a pod

**Q39. How do you handle Helm chart versioning?**  
**A:** Increment chart version in `Chart.yaml` and app version for semantic releases.

**Q40. What is a DaemonSet?**  
**A:** Ensures that a pod runs on every (or selected) node. Used for monitoring, logging agents.

---

## Bonus & Conceptual

**Q41. What is the difference between AKS and self-managed K8s?**  
**A:** AKS abstracts control plane management, integrates with Azure tools, and offers built-in scaling and monitoring.

**Q42. How do you ensure high availability in AKS?**  
**A:** Use multiple node pools across zones, autoscaling, multi-region deployments, and health probes.

**Q43. What’s the difference between `az aks get-credentials` and `kubectl config use-context`?**  
**A:** `az aks get-credentials` retrieves and adds cluster context. `kubectl config use-context` switches between them.

**Q44. How does Azure Policy work with AKS?**  
**A:** Enforces governance using built-in policies (e.g., restrict container images, enforce tags).

**Q45. What’s the purpose of using private container registries like ACR with AKS?**  
**A:** Improves security, performance, and compliance. Easily integrates via managed identities.

**Q46. What is an Ingress Controller and which ones are used in AKS?**  
**A:** Handles HTTP/HTTPS traffic routing. Common ones: NGINX, Application Gateway Ingress Controller (AGIC), Traefik.

**Q47. How do you apply a patch to a live K8s deployment?**  
```bash
kubectl patch deployment my-deploy -p '{"spec":{"replicas":4}}'
```

**Q48. What is KEDA and how is it used in AKS?**  
**A:** Kubernetes-based Event Driven Autoscaler. Scales workloads based on external triggers like queues.

**Q49. How do you audit changes in Azure resources?**  
**A:** Use Azure Activity Logs, Diagnostic Settings, and Log Analytics.

**Q50. How do you ensure smooth collaboration between Dev and Ops teams?**  
**A:** Use shared pipelines, clear documentation, DevOps culture, cross-functional syncs, and feedback loops.

### Advanced AKS, DevSecOps & Governance

**Q51. How does Azure AD integrate with AKS for authentication?
A:** AKS can be integrated with Azure AD using OIDC, enabling fine-grained RBAC control using Azure AD groups mapped to Kubernetes roles.

**Q52. What are Pod Security Admission policies?
A:** They enforce pod security standards (e.g., privileged, baseline, restricted) and replace PodSecurityPolicies in newer Kubernetes versions.

**Q53. How can you secure traffic between microservices in AKS?
A:** Use mTLS with service mesh (Istio/Linkerd), network policies, and secure service-to-service authentication.

**Q54. How do you implement container image scanning in the pipeline?
A:** Integrate tools like Trivy, Aqua, or Microsoft Defender for Containers as a pipeline task.

**Q55. What is Azure Defender for Kubernetes?
A:** A security solution that detects threats, misconfigurations, and suspicious behaviors in AKS.

**Q56. How can you control resource quotas and limits for namespaces?
A:** Use ResourceQuota and LimitRange objects to enforce boundaries and defaults.

**Q57. What are Kubernetes PSP alternatives?
A:** Use OPA/Gatekeeper, Kyverno, and Pod Security Admission (PSA).

**Q58. How do you implement DevSecOps in Azure DevOps pipelines?
A:** Incorporate static code analysis, container scanning, secret detection, and IaC validation tools.

**Q59. What is the difference between Cluster Autoscaler and HPA?
A:** Cluster Autoscaler adds/removes nodes; HPA scales pods horizontally based on CPU/memory.

**Q60. How do you handle AKS cost optimization?
A:** Use autoscaling, spot nodes, right-size workloads, and schedule non-prod shutdowns.

### CI/CD Deep Dive & Templates

**Q61. What are reusable templates in Azure DevOps YAML?
A:** Templates allow modular, reusable pipeline logic using extends, steps, jobs, or stages.

**Q62. How do you conditionally execute stages in YAML?
A:** Use condition: property. Example: condition: eq(variables['Build.SourceBranch'], 'refs/heads/main')

**Q63. How do you manage approvals in multi-stage pipelines?
A:** Use environments and configure pre/post-deployment approvals in the UI.

**Q64. How do you cache dependencies in Azure DevOps?
A:** Use Cache@2 task to store/reuse dependencies between runs.

**Q65. What are self-hosted agents and why use them?
A:** Custom VMs used as build agents, often for performance, security, or custom software needs.

**Q66. How do you publish Helm charts in Azure DevOps?
A:** Use pipeline to package with helm package and push to ACR or an OCI registry.

**Q67. How do you use secureFile in Azure DevOps?
A:** Upload sensitive files (e.g., certs) to Library > Secure Files and reference in YAML.

**Q68. What is pipeline artifact vs build artifact?
A:** Pipeline artifacts are newer, faster, and support multi-stage sharing; build artifacts are legacy.

**Q69. How do you manage parallel deployments in YAML?
A:** Use dependsOn and matrix strategy to define parallel jobs or stages.

**Q70. How do you handle secrets in pipeline templates?
A:** Reference variables from Key Vault/Library groups. Avoid inlining secrets in template code.

### Real World Scenarios & Design Questions

**Q71. Describe how you would build a complete CI/CD workflow for a microservice in AKS.
A:** Build: lint → unit test → build Docker → scan → push to ACR → Helm package → deploy to AKS (dev → QA → prod with approvals).

**Q72. How do you implement blue/green or canary deployments in AKS?
A:** Use Kubernetes deployments with selectors, Ingress routing or service meshes like Istio for traffic splitting.

**Q73. How would you handle AKS logging and troubleshooting in production?
A:** Centralized logging with Azure Monitor, Prometheus/Grafana dashboards, alerts, and kubectl for local debug.

**Q74. How do you handle downtime during upgrades?
A:** Use rolling updates, pod disruption budgets, readiness probes, and avoid single-node pools.

**Q75. How do you recover from a broken deployment in AKS?
A:** Rollback via Helm/Kubernetes, check logs/events, scale replicas, or redeploy from previous version.

**Q76. What design considerations would you make for a multi-tenant AKS cluster?
A:** Namespace isolation, RBAC per tenant, resource quotas, network policies, and audit logging.

**Q77. How would you ensure image provenance and integrity in AKS?
A:** Use image signing (Cosign), ACR tasks, and only allow trusted registries.

**Q78. How do you audit changes made to Kubernetes resources?
A:** Use Azure Policy, audit logs from Kubernetes API server, and integrate with SIEM.

**79. How do you support developers with preview environments per PR?
A:** Use ephemeral environments via dynamic namespaces or Terraform preview with short TTL.

**Q80. How do you implement zero-downtime upgrades in AKS?
A:** Use rolling updates, health probes, keep min replicas running, and maintain session affinity.

### Final Concepts & Best Practices

**Q81. What is the difference between cluster-wide and namespace-wide RBAC?
A:** ClusterRole/ClusterRoleBinding is for global scope; Role/RoleBinding is namespace-scoped.

**Q82. What is a Kubernetes Job vs CronJob?
A:** Job runs once to completion; CronJob runs on a scheduled time.

**Q83. How do you handle node draining safely?
A:** Use kubectl drain --ignore-daemonsets --delete-emptydir-data, followed by workload rescheduling.

**Q84. What are affinity and anti-affinity rules?
A:** Define pod placement policies based on co-location (affinity) or separation (anti-affinity).

**Q85. How do you restrict pod execution on specific nodes?
A:** Use nodeSelectors, taints/tolerations, or affinity rules.

**Q86. How do you clean up unused resources in AKS
A:** Use TTL controllers, resource pruning scripts, and scheduled jobs.

**Q87. What is the benefit of using Azure CNI vs Kubenet?
A:** Azure CNI assigns VNet IPs for pods (more integration); Kubenet is simple but limited in IP management.

**Q88. How do you create a private AKS cluster?
A:** Use --enable-private-cluster in Terraform or CLI and ensure private DNS setup.

**Q89. What is the difference between DaemonSet and ReplicaSet?
A:** DaemonSet runs one pod per node; ReplicaSet maintains a defined number of replicas.

**Q90. What is workload identity in AKS?
A:** Allows Kubernetes workloads to authenticate with Azure services using federated identity instead of secrets.

**Q91. How do you test your Helm charts locally before deploying?
A:** Use helm lint, helm template, and helm install --dry-run.

**Q92. What is the purpose of .helmignore file?
A:** Excludes files from being packaged in Helm charts (like .git, README, etc.).

**Q93. What is the difference between Helm2 and Helm3?
A:** Helm3 removed Tiller, improved security, uses native K8s APIs, and supports better lifecycle hooks.

**Q94. What is Azure Container Apps vs AKS?
A:** Azure Container Apps is serverless and simpler for microservices; AKS is full K8s with more control and complexity.

**Q95. How do you encrypt secrets at rest in Kubernetes?
A:** Enable secret encryption providers in kube-apiserver config (handled by AKS automatically).

**Q96. What are mutating and validating admission controllers?
A:** Webhooks that modify (mutate) or validate resource specs before they are persisted.

**Q97. What is the use of a service mesh in AKS?
A:** Manages traffic, retries, observability, and security (e.g., Istio, Linkerd, Open Service Mesh).

**Q98. How do you perform backup and restore in AKS?
A:** Use tools like Velero for backing up volumes and resource definitions.

**Q99. How do you manage GitOps in AKS?
A:** Use Flux or ArgoCD to sync Git state to the cluster for declarative K8s management.

**Q100. What is your strategy for handling AKS incident response?
A:** Use runbooks, observability stack, diagnostics, audit logs, chaos testing, and documented procedures.
```
