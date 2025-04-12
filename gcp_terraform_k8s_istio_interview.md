JD:

Experience with Google cloud and its offerings like VPCSC ,IAM, Project Hands on

Experience with Terraform for automating infrastructure deployment Hands on

Experience with GKE cluster management and deploying workloads in the cluster Hands on Experience with Kubernetes network policies, GKE RBAC Policies, Role Bindings, Kubernetes Jobs, Kubernetes Logging & Monitoring etc.

Hands on Experience with Istio service mesh with features like authentication , authorization , load balancing , routing ,virtual network route tables subnets , gateway , Configuring control plane , ingress gateway CI/CD - Hands-on experience with Jenkins or similar tools

Scripting - Bash or Python or Groovy



🔹 Google Cloud Platform (GCP) - VPCSC, IAM, Project

**Q1:** What is VPC Service Controls and how have you used it?
A: VPC Service Controls (VPCSC) is a GCP security feature that helps mitigate data exfiltration risks by creating a security perimeter around Google Cloud resources like BigQuery, Cloud Storage, etc. I’ve implemented VPCSC to enforce data boundaries, especially in sensitive environments, and defined service perimeters to allow access only from trusted networks and projects.

**Q2:** How do you manage IAM policies in GCP?
A: I manage IAM through Terraform modules and follow the principle of least privilege. I use custom roles where necessary and bind roles at project, folder, and resource levels using google_project_iam_binding, google_project_iam_member, and google_project_iam_policy Terraform resources.

**Q3:** How do you structure GCP projects in a multi-environment setup?
A: I usually adopt a hierarchy using GCP folders and separate projects for dev, test, and prod environments. This supports resource isolation and billing clarity. Projects are managed via Terraform using the google_project resource.

🔹 Terraform

**Q4:** Describe your experience automating infrastructure on GCP using Terraform.
A: I use Terraform to provision GCP infrastructure, including VPCs, subnets, IAM, GKE clusters, and firewall rules. I modularize the code to enable reusability and implement remote state with locking using GCS and Google Cloud IAM.

**Q5:** How do you manage Terraform state securely?
A: I use a GCS backend with versioning enabled and bucket-level IAM for access control. State locking is enabled via GCS object locking, and access is restricted via VPCSC and organization policies.



🔹 GKE and Kubernetes

**Q6:** How do you deploy workloads to GKE and manage the cluster?
A: I deploy workloads using Helm or Kustomize, manage manifests in Git repos, and use Terraform to provision GKE clusters. I configure auto-scaling, node pools, taints, and labels to optimize resource usage.

**Q7:** Explain how you manage RBAC in GKE.
A: I define Roles and RoleBindings using Kubernetes manifests. For cluster-wide access, I use ClusterRole and ClusterRoleBinding. For example, developers get namespace-scoped access while platform engineers might have cluster-admin roles.

**Q8:** How do you implement network policies in Kubernetes?
A: I define NetworkPolicy resources to restrict pod-level communication. I often apply namespace and label selectors to allow only required traffic (e.g., from frontend to backend). Policies are tested using tools like netshoot.

**Q9:** How do you handle logging and monitoring in GKE?
A: I use Cloud Logging and Monitoring integrations in GKE. Fluentd agents are used to ship logs. For metrics, I enable GKE's built-in monitoring or install Prometheus and Grafana with sidecar dashboards for custom metrics.

🔹 Istio Service Mesh

**Q10:** What are the key Istio features you’ve worked with?
A: I’ve worked on mTLS for service-to-service authentication, AuthorizationPolicies for access control, destination rules and virtual services for traffic routing, and Istio ingress gateways to expose services. I also configured the Istio control plane using Helm charts or istioctl.

**Q11:** How do you route traffic using Istio?
A: I define VirtualService and DestinationRule objects. For example, to implement canary deployments, I route 90% traffic to v1 and 10% to v2. This can be modified dynamically for A/B testing or gradual rollout.

**Q12:** How do you manage Istio ingress?
A: I create Gateway resources to expose services externally via Istio. The configuration includes TLS termination and host-based routing. I map services to the gateway using VirtualServices.

🔹 CI/CD (Jenkins or similar)

**Q13:** Describe your CI/CD pipeline setup.
A: I use Jenkins with pipeline-as-code (Jenkinsfiles). Pipelines include stages for code checkout, linting, unit tests, Docker image build and push, Terraform validation and apply, and finally deployment to GKE using Helm or kubectl.

**Q14:** How do you secure your CI/CD pipeline?
A: I use credential binding in Jenkins, restrict access to jobs, and integrate with secrets managers like Vault or Google Secret Manager. Artifacts are signed, and deployment environments use RBAC with least privilege.



🔹 Scripting - Bash / Python / Groovy

**Q15:** How do you use scripting in your workflow?
A: I use Bash for quick automation (like health checks, log collection), Python for API integration or writing custom utilities, and Groovy in Jenkinsfiles for pipeline logic (e.g., conditional stages, loops, error handling).

**Q16:** Give an example of a useful script you’ve written.
A: I wrote a Python script that automates IAM audit by listing all users and their roles across GCP projects using the Cloud Resource Manager and IAM APIs, and outputs it in CSV format for governance checks.





🔹 Google Cloud Platform (Advanced GCP Concepts)

**Q17:** How do you enforce organization-wide security policies in GCP?
A: I use Organization Policies (Org Policies) to enforce constraints like domain restriction, disabling service account key creation, and restricting external IPs. Combined with VPCSC and IAM Conditions, this creates a strong security posture.

**Q18:** How do you manage billing and cost optimization across projects?
A: I use labels and folder/project-level budgets to track costs. I enable cost exports to BigQuery for analysis and set alerts in GCP Billing. I also use committed use discounts and optimize autoscaling in GKE to reduce costs.



🔹 Terraform (Advanced)

**Q19:** How do you structure a large Terraform project for GCP?
A: I use a mono-repo with environment-specific directories (dev, staging, prod) and reusable modules for components like VPC, GKE, IAM. State is isolated per environment using workspaces or separate backend config.

**Q20:** How do you handle secrets in Terraform?
A: Secrets like service account keys or sensitive variables are stored in Secret Manager or passed via environment variables in CI/CD pipelines. I avoid storing secrets in state files and use data sources to read secrets securely at runtime.



🔹 GKE and Kubernetes (Advanced Scenarios)

**Q21:** How do you perform a blue-green deployment in GKE?
A: I deploy a new version in a separate namespace or behind a different label, configure the service to switch between selectors, monitor performance, and then decommission the old version if stable.

**Q22:** What’s your approach for auto-scaling in GKE?
A: I use Horizontal Pod Autoscaler (HPA) based on CPU, memory, or custom metrics, and Cluster Autoscaler to add/remove nodes based on pod demand. I also set resource requests/limits to help the scheduler make optimal decisions.

**Q23:** How do you troubleshoot a CrashLoopBackOff pod?
A: I use kubectl describe pod and kubectl logs to get events and logs. Common issues include bad configs, missing env vars, or liveness probe failures. If needed, I run an interactive pod in the same namespace for debugging.



🔹 Istio (Advanced Service Mesh Concepts)

**Q24:** How do you implement mutual TLS in Istio?
A: I enable mesh-wide mTLS via PeerAuthentication policies and ensure services have proper sidecar injection. I verify with istioctl authn tls-check and troubleshoot using Istio logs if necessary.

**Q25:** Can you explain how to control east-west and north-south traffic in Istio?
A: East-west traffic is managed via service-to-service policies (PeerAuth, AuthZ), while north-south is controlled at the ingress gateway with Gateway and VirtualService definitions, including TLS settings and rate limiting via Envoy filters.

**Q26:** How do you implement rate limiting in Istio?
A: I use Envoy rate-limiting via Istio’s EnvoyFilter CRD or external rate-limiting services. For example, I can limit requests per minute per client IP or user token by configuring HTTP filters at the gateway or workload level.



🔹 CI/CD (Advanced Jenkins)

**Q27:** How do you handle rollback in Jenkins pipelines?
A: I store Helm chart versions or Kubernetes manifests with Git tags. In case of failure, a rollback stage is triggered to deploy the last known good version. I also use kubectl rollout undo or helm rollback.

**Q28:** How do you ensure high availability of Jenkins?
A: I deploy Jenkins on Kubernetes with persistent volumes, use master-agent setup with horizontal scaling of agents, and backup configs/jobs regularly. I use plugins like Job DSL for job reproducibility.



🔹 Scripting (Advanced)

**Q29:** Describe a Bash script you wrote to improve operational efficiency.
A: I wrote a Bash script that automates namespace cleanup in GKE by checking inactive pods/services older than 7 days and archiving logs before deletion. It saved time and maintained cluster hygiene.

**Q30:** What’s a Python script you used with GCP APIs?
A: I created a Python script using google-api-python-client to list all IAM bindings across projects and output a report highlighting overly permissive roles like owner or editor to help with security audits.



🔹 Google Cloud Platform (GCP - Real-world Scenarios)

**Q31:** How do you securely expose a GCP Cloud Function only to internal services in your VPC?
A: I configure the Cloud Function to use a VPC connector, restrict ingress settings to internal traffic only, and use IAM roles (e.g., invoker) scoped to internal service accounts. If VPCSC is enabled, I ensure it’s within the same service perimeter.

**Q32:** How would you handle cross-project service access with IAM?
A: I create a service account in Project A, grant it required roles in Project B, and then allow Project A’s workloads to impersonate the account using IAM policies and Workload Identity Federation for least-privilege access.



🔹 Terraform (Troubleshooting & Patterns)

**Q33:** What would you do if a Terraform apply fails due to a quota issue?
A: I review the GCP quota in the affected region using the GCP console or CLI, submit a quota increase request, and re-run the plan. I also consider retry logic or conditional resources if the plan depends on quotas dynamically.

**Q34:** How do you manage drift in Terraform-managed resources?
A: I run terraform plan regularly and use tools like terraformer for auditing. If there’s drift, I evaluate whether to re-import (terraform import) or bring the configuration back in sync manually or via state manipulation.



🔹 GKE (Operations, Resiliency, and Policies)

**Q35:** How do you ensure application resiliency in GKE?
A: I define readiness/liveness probes, use HPA for load-based scaling, configure PodDisruptionBudgets, anti-affinity rules, and use regional clusters with node auto-repair and multi-zonal node pools.

**Q36:** How do you enforce security best practices for workloads in GKE?
A: I apply GKE Autopilot (or harden standard clusters), enforce PSPs (or OPA/Gatekeeper for policies), disable legacy metadata APIs, use workload identity for service account binding, and enable Binary Authorization for image verification.

**Q37:** What’s the difference between ClusterRole and Role in Kubernetes?
A: Role is namespace-scoped and grants permissions within a single namespace, while ClusterRole is cluster-scoped and can apply across all namespaces. ClusterRole is required for access to non-namespaced resources like nodes.

🔹 Istio (Advanced Troubleshooting & Config)

**Q38:** How do you debug routing issues in Istio?
A: I verify VirtualService and DestinationRule configurations using istioctl analyze, check for missing hosts or subset labels, validate gateway bindings, and inspect envoy proxy configuration using istioctl proxy-config.

**Q39:** How do you use Istio Authorization Policies to restrict traffic?
A: I define AuthorizationPolicy to specify source principals, namespaces, or IPs. For example, I can restrict access to a service only from a specific workload with a service account identity using from.source.principals.

**Q40:** How do you configure observability in Istio?
A: I enable telemetry v2 for metrics and use Prometheus/Grafana for visualizations. I also use Kiali for service graph visualization and Jaeger for distributed tracing, integrated via Helm or IstioOperator.



🔹 CI/CD (Security, Optimization, Real-World Pipelines)

**Q41:** How do you manage dynamic environments for PR validation in Jenkins?
A: I use Jenkins pipelines that dynamically spin up ephemeral namespaces or clusters for PRs, run tests/deployments using Helm/Kustomize, and destroy them post-validation. Resource naming is tagged with PR IDs and TTLs.

**Q42:** How do you prevent credentials leakage in pipelines?
A: I never hardcode secrets; instead, I use credentials binding plugins, restrict job access, and pull secrets from Secret Manager or Vault. I also audit logs and rotate credentials regularly.

**Q43:** What’s your strategy for managing Jenkins shared libraries?
A: I maintain common Groovy libraries in a central Git repo, version them with semantic tags, and use them for reusable pipeline logic (e.g., Docker build, Helm deploy). This ensures DRY principles across pipelines.



🔹 Scripting (Real-World and API Integrations)

**Q44:** Describe a Groovy script you've used inside Jenkins.
A: I wrote a Groovy script in a shared library that validates PR titles against JIRA ticket formats, enforces changelog updates, and sends Slack notifications post-deployment with build status and commit info.

**Q45:** How would you use Python to interact with GCP APIs?
A: Using the google-cloud Python libraries (like google.cloud.compute_v1 or googleapiclient.discovery), I automate tasks like spinning up Compute Engine VMs, updating firewall rules, or polling job statuses in BigQuery or Dataflow.



Would you like me to assemble all these questions into a formatted PDF or Notion-friendly template for quick review? Or should I create a mock interview script next so you can practice live responses?

Great! Let’s keep going with even more advanced, scenario-based questions and answers — touching on edge cases, real-life architecture decisions, security, and troubleshooting in each area from the JD:



🔹 Google Cloud Platform (Governance & Compliance)

**Q46:** How do you ensure compliance and auditability in a multi-project GCP setup?
A: I enforce organization policies (like disabling external service accounts, enforcing CMEK), enable Cloud Audit Logs across all services, use SCC (Security Command Center) for real-time findings, and export logs to BigQuery for audit trail analytics. I also tag resources with cost centers and environment labels.

**Q47:** What’s your approach to managing access for temporary contractors in GCP?
A: I create a separate group or identity pool with scoped roles and IAM Conditions (like time-bound access). Access is granted via gcloud or Terraform and revoked automatically using TTL policies or de-provisioning automation.



🔹 Terraform (Modules, CI/CD Integration, and Best Practices)

**Q48:** How do you promote Terraform changes across environments (Dev → Prod)?
A: I maintain a separate state per environment with the same module structure. CI/CD pipelines validate, plan, and apply changes in stages, using Git branches (like feature/, main, release/) to control environment-specific promotion.

**Q49:** What are some best practices for writing Terraform modules?
A: I follow:

Use of input/output variables

Validation rules

Clear resource naming conventions with locals

Avoid hardcoding

Support for overrides using for_each or dynamic blocks

Documentation via README.md and examples folder

**Q50:** How do you manage dependency across Terraform modules?
A: I use output variables and pass them as inputs between modules. CI/CD controls apply order, and depends_on is used only when absolutely necessary to avoid hidden coupling.



🔹 GKE (Security, Lifecycle, and Disaster Recovery)

**Q51:** How do you configure Workload Identity in GKE and why is it preferred?
A: Workload Identity binds a Kubernetes service account to a GCP IAM service account. Pods assume this identity without storing keys, reducing the risk of key leaks. I configure it via annotations and IAM bindings.

**Q52:** How do you handle GKE upgrades with zero downtime?
A: I enable surge upgrades (e.g., maxSurge, maxUnavailable) and ensure workloads are disruption-tolerant with pod anti-affinity and proper readiness probes. I test upgrades in non-prod before rolling out to production clusters.

**Q53:** What’s your disaster recovery plan for GKE?
A: I back up persistent data using Velero and Cloud Storage snapshots, maintain IaC for full infra rebuilds, and use multi-region failover strategies. Application configs and secrets are stored in Git or Secret Manager with versioning.



🔹 Istio (Edge Cases & Policy Enforcement)

**Q54:** How do you apply rate limiting per user or client in Istio?
A: I use the Envoy RateLimit service with descriptors like user ID or client IP. Policies are configured in EnvoyFilter resources or integrated with external rate-limiting services like Redis or Istio extensions.

**Q55:** What challenges have you faced when using Istio, and how did you resolve them?
A: Some challenges include high memory usage by sidecars, misconfigured mTLS leading to 503s, and complex YAMLs. I solved these using istioctl analyze, tweaking proxy resource limits, and adopting IstioOperator for consistent config management.

**Q56:** How do you safely introduce Istio into an existing GKE cluster?
A: I first install Istio without sidecar injection and test control plane health. Then I selectively label namespaces for injection, validate traffic using mirrored routes, and incrementally adopt features like mTLS and AuthorizationPolicies.



🔹 CI/CD (Resiliency, Delivery Patterns, and Observability)

**Q57:** How do you implement a secure image build pipeline?
A: I use Jenkins or GitLab CI to build images in a hardened container, scan them with tools like Trivy or Clair, sign them using Cosign or Notary (for SLSA compliance), push them to Artifact Registry, and use Binary Authorization in GKE.

**Q58:** How do you debug a flaky Jenkins pipeline job?
A: I examine Jenkins logs, agent capacity, network timeouts, and use retry and timeout steps to stabilize jobs. I also mock external services and isolate parallel stages to reduce contention.

**Q59:** How do you visualize CI/CD metrics?
A: I push build data to Prometheus (via Jenkins Prometheus plugin), visualize it in Grafana dashboards, and set alerts for failed builds, duration anomalies, and deployment frequency (for DORA metrics).



🔹 Scripting (Security, Automation, and Tooling)

**Q60:** How do you securely interact with GCP APIs in a Python script running in CI?
A: I use Workload Identity Federation or short-lived service account tokens stored in Jenkins credentials. The script uses google-auth or google-api-python-client with the token to authenticate. Tokens are never stored or logged.

**Q61:** Describe a Bash script you’ve used for cluster health reporting.
A: I wrote a Bash script using kubectl, jq, and awk to collect pod restarts, node resource usage, and pending pods. It generates a daily HTML report and sends it via Slack/email for proactive alerting.

**Q62:** How do you use Python to automate IAM role analysis across GCP projects?
A: I use the cloudresourcemanager and iam APIs to iterate over projects, fetch IAM policies, and parse role bindings. The script flags broad roles (like owner) and writes reports with CSV and email alerts for compliance.



Want a printable/markdown/PDF version of the full 60+ question set for your prep? Or a mock interview based on random picks from these topics with time limits and feedback?

You got it — let’s dive into even more ultra-practical, scenario-based interview questions and answers to round out your preparation for this JD. We’ll cover troubleshooting, scalability, advanced security, service meshes, and real-world challenges across all the focus areas.



🔹 Google Cloud Platform (Multi-Tenant, Networking, Identity)

**Q63:** How do you isolate environments (Dev/Test/Prod) in GCP while keeping shared VPC access?
A: I create separate projects for each environment and use a host project with Shared VPCs. Each service project connects to the shared network. IAM is scoped tightly per project, and firewall rules/namespaces isolate workloads.

**Q64:** How do you implement least-privilege access for GCP service accounts across multiple services?
A: I use dedicated service accounts per service, use IAM Conditions to scope access (e.g., resource.name or request.time), and remove overly permissive roles like Editor. I regularly audit using gcloud asset and SCC IAM findings.

**Q65:** How do you restrict data exfiltration using VPC Service Controls?
A: I configure service perimeters around projects accessing sensitive data and enable VPC-SC on services like BigQuery or Cloud Storage. I add access levels for trusted IPs, enforce egress restrictions, and test via dry-run mode.



🔹 Terraform (Advanced Patterns, Performance, Team Practices)

**Q66:** How do you structure Terraform code in a large, multi-team environment?
A: I split code into reusable modules, maintain a separate repo for each team/env, use remote state backends with state locking (e.g., GCS + DynamoDB), and run terraform plan via CI before merging changes. Pre-commit hooks ensure formatting and security checks.

**Q67:** What’s your approach when Terraform is stuck in a locked state?
A: I investigate the lock in the backend (e.g., GCS with DynamoDB), and if it’s a stale lock, I manually remove it. I avoid this by enabling timeouts and proper job cleanup in CI/CD.



🔹 GKE (Scalability, Cost, Lifecycle Management)

**Q68:** How do you optimize GKE clusters for cost without compromising reliability?
A: I enable Node Auto-Provisioning with spot VMs for non-critical workloads, use Vertical Pod Autoscaler and HPA to right-size resources, and restrict namespaces with ResourceQuotas. I also use kubecost to monitor usage patterns.

**Q69:** How do you roll back a faulty deployment in GKE?
A: I use kubectl rollout undo for quick rollback or restore a previous Deployment manifest from Git. I also use Helm’s versioned releases (helm rollback) or ArgoCD’s sync history when using GitOps.

**Q70:** How do you handle a failing Kubernetes Job that keeps retrying indefinitely?
A: I set backoffLimit and activeDeadlineSeconds to prevent runaway retries. I check pod logs, investigate resource limits or failed dependencies, and use ttlSecondsAfterFinished to clean up succeeded/failed jobs.



🔹 Istio (Edge Security, Zero Trust, Gateways)

**Q71:** How do you configure end-to-end TLS in Istio (mTLS + TLS)?
A: I enable strict mTLS inside the mesh and configure Ingress Gateway with a TLS secret using Gateway and VirtualService. External traffic uses HTTPS with a cert from Let's Encrypt or ACM. SNI routing is used for multi-domain ingress.

**Q72:** How do you expose multiple services under the same domain in Istio?
A: I define a Gateway with the shared domain and create multiple VirtualService resources with different path prefixes or SNI matches. I ensure the correct Host header routing and avoid overlapping match rules.

**Q73:** What’s your approach to troubleshooting 503 errors in Istio?
A: I use istioctl proxy-status and proxy-config to inspect listeners/routes, check for missing subsets in DestinationRules, and validate VirtualService configs. Envoy logs (kubectl logs istio-proxy) often reveal detailed errors.



🔹 CI/CD (Rollbacks, Testing, Multi-Cluster Deployment)

**Q74:** How do you promote tested artifacts between stages in Jenkins pipelines?
A: I tag Docker images with Git commit SHA, push them to Artifact Registry, and pass tags through environments. I use promotion jobs that only deploy already-tested tags, ensuring immutability and traceability.

**Q75:** How do you test Helm charts in CI before applying them to a cluster?
A: I use helm lint and helm template to validate templates, kubeval to validate output, and run dry-runs with --dry-run --debug. I may also deploy to a kind/minikube test cluster in CI using Docker-in-Docker.

**Q76:** How do you handle multi-cluster deployment in your pipelines?
A: I abstract cluster contexts using kubectl kubeconfig switching or ArgoCD applications per cluster. I parameterize the environment (via Helm or Kustomize) and define promotion logic between clusters in the CD stage.



🔹 Scripting (Cloud APIs, Monitoring, Scheduled Tasks)

**Q77:** How do you automate GKE node pool upgrades using Bash or Python?
A: I use gcloud container node-pools update in a loop through each pool/cluster, pause workload autoscaling, cordon & drain nodes, then trigger the upgrade. I validate the version before and after upgrade using gcloud APIs or Python SDK.

**Q78:** Describe a script you’ve used to clean up stale resources.
A: A Python script that lists stale disks, snapshots, or unused IPs from GCP APIs and deletes them after X days of no usage. I include a dry-run mode and Slack/email notifications before execution.

**Q79:** How do you monitor job statuses and trigger actions based on them in Bash?
A: I poll job status using kubectl get jobs -o json or jq on GCP batch/Cloud Build APIs, then use conditionals to trigger next steps like Slack alerts, retries, or deployments. Exit codes are captured and logged for CI.



Would you like me to:

✅ Bundle this full set (now over 80+ questions) into a PDF/Markdown?

🎯 Generate a mock interview simulation?

📄 Help create flashcards or a Notion page to quickly review these before your interview?

Let me know how you’d like to lock this down!

You're on fire! 🔥 Here's the next wave of ultra-detailed, scenario-based Q&A to take you to the top of any interview panel. These go even deeper into real-world challenges, optimization, cross-service orchestration, troubleshooting, and security hardening in GCP, GKE, Istio, Terraform, CI/CD, and scripting.



🔹 Google Cloud Platform (Billing, Governance, Multi-Org)

**Q80:** How do you implement budget alerts across multiple GCP projects?
A: I use Billing Budgets API to create budgets at the project or label level. Notifications are sent to Pub/Sub, then to email/Slack via Cloud Functions or workflows. I also use cost attribution via labels and BigQuery exports for cost analytics dashboards in Looker Studio.

**Q81:** How do you manage multiple GCP organizations and enforce security policies consistently?
A: I use Organization Policies (like disableServiceAccountKeyCreation, restrictVpcPeering) at the Org level and Policy Sets (in preview) to enforce them across orgs. I automate setup using Terraform and monitor via Security Command Center across orgs.



🔹 Terraform (State Management, Change Control, Secrets)

**Q82:** How do you protect sensitive variables and secrets in Terraform?
A: I use sensitive = true for variables, store secrets in Secret Manager or Vault, and fetch them dynamically in CI pipelines. I avoid committing secrets in state by using data sources and local-exec provisioners where necessary.

**Q83:** How do you handle state drift in Terraform?
A: I regularly run terraform plan in CI/CD pipelines to detect drift. If drift occurs, I use terraform refresh, validate the changes, and reconcile manually or via re-applying corrected IaC.

**Q84:** What’s your versioning strategy for Terraform modules?
A: I use semantic versioning (v1.2.0) with Git tags, and modules are pinned to exact versions in the calling code (ref = "v1.2.0"). Breaking changes trigger major version bumps, and a changelog is maintained.



🔹 GKE (Security Edge, Pod Management, Upgrades)

**Q85:** How do you secure communication between services inside GKE without Istio?
A: I use Network Policies to allow traffic only from specific namespaces or pods, use Pod-to-Pod mTLS via SPIRE or application-layer TLS, and limit access using service accounts and RBAC.

**Q86:** How do you manage GKE upgrades across multiple clusters in different regions?
A: I tag clusters and automate upgrades using Terraform + CI/CD or scripts calling gcloud container clusters upgrade. I perform staged rollouts, beginning in non-prod clusters. Health checks, backup validation, and rollback plans are pre-baked.

**Q87:** How do you ensure pod security in GKE?
A: I use PodSecurityAdmission to enforce restricted or baseline policies, OPA/Gatekeeper for fine-grained control (e.g., disallow host networking), and run vulnerability scans with GCP Container Analysis.



🔹 Istio (AuthN/AuthZ, Multi-Cluster, Canary Deployments)

**Q88:** How do you apply per-path authorization rules in Istio?
A: I define AuthorizationPolicies that match specific paths and methods (e.g., /api/admin/* with GET) and bind them to service accounts or JWT claims. I often combine with mTLS and JWT validation in RequestAuthentication.

**Q89:** How do you handle Istio multi-cluster setup across regions?
A: I use Istio’s replicated control plane model with shared root CA, mesh federation, and multi-network configs. Ingress gateways are exposed with DNS load balancing, and services are reachable cross-cluster using ServiceEntry + endpoint discovery.

**Q90:** How do you perform canary releases using Istio?
A: I use VirtualService to split traffic based on weight (e.g., 90% v1, 10% v2), or use header-based routing for power users. Metrics from Prometheus help determine success before shifting more traffic.



🔹 CI/CD (Release Engineering, Audits, Dynamic Environments)

**Q91:** How do you manage environment-specific configurations in CI/CD?
A: I use templating tools like Helm/Kustomize with overlays or env-specific values files. The pipeline chooses the correct config based on Git branch or tag, and secrets are injected securely via Secret Manager or CI vaults.

**Q92:** How do you track deployments and correlate them with incidents?
A: I include Git SHA and timestamp in each deployment via annotations/labels on pods. I export metadata to logging and monitoring platforms (e.g., GKE logs, Stackdriver). When incidents occur, I correlate logs and metrics by deployment tags.

**Q93:** How do you implement dynamic review environments?
A: I use ephemeral environments triggered by PRs, spinning up short-lived namespaces or GKE preview clusters. Jenkins or GitLab pipelines deploy builds automatically, label resources with PR IDs, and auto-teardown post-merge/close.



🔹 Scripting (Advanced Automation, Compliance, Data Handling)

**Q94:** How do you automate IAM audit reporting using Python?
A: I use the google-iam API to pull policies from all projects, parse bindings with Python (google-api-python-client), filter out risky roles (e.g., owner), and generate CSV reports with grouped views per user or role.

**Q95:** How do you build a custom metrics exporter for Kubernetes in Python?
A: I use the kubernetes Python client to query pod status, resource usage via metrics-server, and expose metrics using prometheus_client. I deploy it as a sidecar or daemonset depending on scope.

**Q96:** How do you build a compliance check tool for Terraform in Bash?
A: A script scans .tf files for non-compliant resources (e.g., public = true, missing versioning on buckets), outputs warnings, and blocks the PR via pre-commit hooks or CI job. Optionally, it runs tfsec or checkov.



We’re now up to 96 highly detailed questions. Ready for:

✅ A PDF/Markdown export of all 96 Q&A for offline prep?

💡 A custom interactive flashcard set or quiz app (I can generate one)?

🎙️ A mock interview session with timed rounds and real feedback?

Let me know how you’d like to put these to work!



