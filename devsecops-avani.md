Q: How do you integrate security into a CI/CD pipeline?

A: By embedding SAST, DAST, dependency scanning, and container image scanning tools like SonarQube, OWASP ZAP, Trivy, or Aqua into the pipeline stages (build, test, deploy).

Q: What tools have you used for static code analysis?

A: Tools like SonarQube, Checkmarx, and Fortify to detect code-level vulnerabilities early in development.

Q: What is the benefit of shifting security left?

A: It reduces cost and effort by identifying security flaws early in the SDLC, improving code quality and reducing risk.

Q: How do you automate secrets scanning in code?

A: Use tools like GitGuardian, Gitleaks, or TruffleHog integrated into commit hooks or pipelines to catch secrets in code.

Q: How would you secure third-party dependencies in the pipeline?

A: Use tools like OWASP Dependency-Check, Snyk, or JFrog Xray to identify known vulnerabilities (CVEs) in dependencies.

Q: How do you secure a GCP project?

A: Use IAM best practices, service perimeter with VPC-SC, organization policies, firewall rules, and centralized logging/monitoring with SCC.

Q: What is VPC-SC in GCP and its security role?

A: VPC Service Controls help isolate GCP resources and mitigate data exfiltration risks by defining service perimeters.

Q: How would you secure cloud storage buckets in GCP?

A: Use bucket-level IAM, uniform bucket-level access, enforce encryption (CMEK), and disable public access.

Q: What’s your approach to securing cloud networking?

A: Implement firewall rules (least privilege), restrict ingress/egress, use private service access, and configure subnets and routes securely.

Q: How do you enforce encryption in cloud resources?

A: Enable encryption at rest with CMEK or CSEK, use HTTPS/TLS for in-transit encryption, and ensure default encryption is turned on.
Q: How do you implement security in Terraform?

A: Use Sentinel or Open Policy Agent for policy as code, version modules, perform drift detection, and validate plans with terraform validate and tfsec.

Q: What tools do you use to scan IaC for security issues?

A: tfsec, Checkov, Terrascan, or Snyk IaC to detect misconfigurations and enforce secure defaults.

Q: How do you manage credentials in IaC workflows?

A: Avoid hardcoding secrets, use secure backends like Vault or cloud KMS, and manage state files securely (e.g., encryption + RBAC).

Q: How do you handle Terraform state securely?

A: Store in a secure backend (e.g., GCS bucket with CMEK + versioning + access control), and encrypt with KMS.

Q: How do you enforce compliance with IaC?

A: Use OPA or Sentinel policies in CI/CD to block non-compliant infrastructure changes before deployment.

Q: How do you differentiate SAST and DAST?

A: SAST analyzes source code without running it (early in SDLC), while DAST tests a running application (post-deployment)
.
Q: What tools have you used for container image scanning?

A: Trivy, Clair, Anchore, and Aqua Security to identify vulnerabilities in base images and packages.
Q: How do you secure Kubernetes workloads?

A: Implement PodSecurityPolicies/OPA/Gatekeeper, RBAC, network policies, secrets encryption, and scan manifests using Kubeaudit.

Q: How do you test APIs for security vulnerabilities?

A: Use tools like OWASP ZAP, Postman with security tests, or Burp Suite to test for issues like injection, auth flaws, and rate-limiting.

Q: How do you continuously monitor code for new vulnerabilities?

A: Use dependency scanning tools (e.g., Snyk, Dependabot), automated CVE feeds, and integrate alerts into developer tools like Slack or Jira.

Q: How do you implement compliance checks in the cloud?

A: Use tools like Forseti (GCP), AWS Config, Azure Policy, or custom scripts to check resources against security/compliance baselines.

Q: How do you ensure GDPR compliance in cloud applications?

A: Implement data encryption, user consent handling, data minimization, audit trails, and allow for data export/deletion.

Q: What is CIS Benchmark and how do you use it?

A: CIS Benchmark provides security best practices; tools like InSpec or Prisma Cloud can validate infrastructure against CIS benchmarks.

Q: How do you track compliance drift in cloud environments?

A: Use configuration management tools (Ansible, Terraform), cloud-native config tracking, and audit logs to detect unauthorized changes

Q: How do you manage audits across multi-cloud environments?

A: Use centralized logging, tagging standards, automation with policy-as-code, and cross-cloud compliance tools like Prisma or Dome9.

Q: How do you detect threats in cloud environments?

A: Use tools like GCP Security Command Center, Cloud Audit Logs, IDS/IPS, and set up real-time alerts with Pub/Sub or SIEM integration.

Q: How do you respond to a compromised cloud resource?

A: Isolate the resource, rotate credentials, analyze logs for scope, remediate vulnerabilities, and perform RCA and post-incident reviews.

Q: What is your incident response process?

A: Detection → Triage → Containment → Eradication → Recovery → Lessons Learned → Documentation.

Q: What tools support threat detection in GCP?

A: SCC, Cloud Armor (WAF), Cloud IDS, Chronicle SIEM, and VPC Flow Logs.

Q: How do you detect data exfiltration attempts?

A: Monitor unusual network egress using VPC Flow Logs, audit logs, DLP alerts, and behavior analytics tools.

________________________________________
Q: How do you handle zero-day vulnerabilities?

A: Identify impact, apply temporary mitigations, prioritize patching, and isolate affected systems while monitoring for exploitation.

Q: How do you manage vulnerability remediation in cloud?

A: Automate vulnerability scans, integrate findings into ticketing systems, assign SLAs, and verify remediation post-patch.

Q: How do you patch container images?

A: Rebuild images from updated base images, run scans before deployment, and use CI/CD automation to redeploy patched containers.

Q: How do you manage vulnerabilities in ephemeral infrastructure?

A: Bake updated AMIs/images regularly, rotate instances, and enforce immutable infrastructure practices.

Q: What is your process for vulnerability triage?

A: Assess CVSS score, exploitability, asset criticality, and prioritize based on business risk and compliance requirements

Q: How do you enforce least privilege access in GCP?

A: Use predefined roles, audit IAM bindings, apply constraints via org policies, and use service accounts with scoped permissions.
Q: What tools do you use for managing secrets?
A: HashiCorp Vault, GCP Secret Manager, AWS Secrets Manager, or sealed-secrets in Kubernetes.
Q: How do you secure API keys in a DevOps pipeline?
A: Store them in a secure vault or secret manager, access them at runtime via environment variables or secret injection.
Q: What is the principle of "Just-in-time" access and how do you implement it?
A: Temporary elevated access granted only when needed, implemented using tools like BeyondCorp or access approval workflows.
Q: How do you detect privilege escalations in cloud environments?
A: Monitor IAM logs, alert on new roles/permissions assigned, and use anomaly detection in audit logs.
Q: How do you promote security culture in DevOps teams?
A: Conduct regular training, include security KPIs, create security champions, and automate secure practices into workflows.
Q: How do you ensure security is treated as a shared responsibility?
A: Embed security in planning, involve security in sprint reviews, and democratize security tools and training.
Q: What KPIs do you track for DevSecOps success?
A: Vulnerability MTTR, compliance score, false positive rate, coverage of security tests, and number of critical issues prevented.
Q: How do you evaluate and adopt new security tools?
A: Use PoCs, assess compatibility, performance, ease of use, community support, and security features before full adoption.
Q: How do you stay up to date with cloud security threats?
A: Follow threat intelligence feeds, vendor advisories, security blogs, attend webinars, and participate in forums like OWASP.
Q: A developer pushed secrets to Git. How do you respond?
A: Revoke and rotate the secret, remove it from Git history (git filter-branch or BFG), alert the team, and scan repo for more issues.
Q: You found a critical CVE in a production service. What’s next?
A: Assess exploitability, isolate if needed, apply patch or mitigation, test and redeploy, monitor, and document incident.
Q: How do you secure a Kubernetes cluster in GCP?
A: Use private GKE cluster, shielded nodes, workload identity, RBAC, network policies, binary authorization, and audit logging.
Q: How do you handle compliance for a multi-region cloud deployment?
A: Tag and group resources by region, apply region-specific compliance policies, and use centralized tools for enforcement and auditing.
Q: How do you deal with resistance from developers towards security practices?
A: Educate on risks, show value through metrics, simplify tooling, involve them early, and make secure paths the default and easiest option.
Q: What is software supply chain security, and how do you enforce it?
A: It involves securing all components from code to deploy (including dependencies, CI/CD tools, artifacts). Use SBOM (Software Bill of Materials), sign artifacts, and verify provenance (e.g., with Sigstore, Cosign, or in-toto).
Q: What are signed builds and why are they important?
A: Signed builds ensure the integrity and authenticity of artifacts. Tools like Cosign can sign container images; GitHub Actions can use OIDC to sign workflows.
Q: How do you enforce security gates in CI/CD?
A: Define blocking stages in the pipeline using tools like Snyk, Checkov, or SonarQube that must pass before allowing promotion to staging or production.
Q: How do you manage secrets across environments (dev/test/prod)?
A: Use separate secret stores per environment with IAM-based access control. Use key rotation and environment-specific encryption keys.
Q: What’s your approach to detecting and preventing lateral movement in pipelines?
A: Restrict permissions, isolate runners, monitor lateral access attempts, and use network segmentation and Just-in-Time credentials.
Q: How does GCP Cloud Armor help with security?
A: It's a WAF that protects against DDoS, OWASP Top 10, and supports geo-blocking and rate limiting.
Q: What is the difference between GCP IAM and Organization Policies?
A: IAM manages permissions at resource level, Org Policies enforce constraints like disabling service usage or blocking public IPs at org/folder level.
Q: How do you protect against SSRF in a cloud environment?
A: Disable metadata endpoint access (where possible), use workload identity instead of metadata tokens, validate and whitelist URLs in app logic.
Q: In GCP, how would you detect and alert on anomalous behavior?
A: Use SCC, log-based metrics, Cloud Logging, and integrate alerts into Pub/Sub, PagerDuty, or SIEM.
Q: What is the difference between customer-managed and Google-managed encryption keys?
A: CMEK gives customers full control over encryption keys, while Google-managed keys are automatic but not directly managed by the customer.
Q: How do you prevent privilege escalation in Terraform-managed IAM roles?
A: Define strict IAM role boundaries, review policies for wildcard permissions, use OPA to block risky patterns.
Q: What are Sentinel and OPA? How do they compare?
A: Both enforce policy-as-code. Sentinel is Terraform-native (by HashiCorp); OPA is broader and supports many platforms including Kubernetes.
Q: How do you ensure only approved modules are used in Terraform?
A: Use a private Terraform registry, scan module sources, and enforce checks in CI/CD.
Q: How do you manage Terraform in a team securely?
A: Use remote backends (e.g., Terraform Cloud or GCS) with access controls, locking, and versioned state files.
Q: How do you detect and fix drift in IaC?
A: Use terraform plan in CI pipelines, use tools like DriftCTL or Terraform Cloud drift detection.
Q: What is PodSecurityAdmission and how does it replace PodSecurityPolicy?
A: PodSecurityAdmission is a built-in admission controller in Kubernetes v1.23+ that enforces pod security standards (restricted, baseline, privileged).
Q: How do you enforce runtime security in Kubernetes?
A: Use tools like Falco or Aqua Enforce to monitor syscalls and alert/block unauthorized behavior.
Q: How do you ensure image provenance in Kubernetes?
A: Use admission controllers like Kyverno or Gatekeeper to enforce signed images only.
Q: What are Kubernetes NetworkPolicies and how do they secure workloads?
A: They control ingress/egress between pods/namespaces. By default, all traffic is allowed; policies can isolate services.
Q: How do you implement RBAC securely in Kubernetes?
A: Follow least privilege, avoid binding cluster-admin, audit rolebindings, and review logs for excessive permissions.
Q: What do you audit in a DevSecOps pipeline?
A: Code commits, pipeline runs, approval logs, artifact changes, and secrets access events.
Q: How do you monitor failed login attempts in GCP?
A: Use Cloud Audit Logs → export to Cloud Logging → create alert policies with filters on authenticationInfo.
Q: What’s the role of SIEM in DevSecOps?
A: Collect, correlate, and analyze logs from CI/CD, cloud infrastructure, and applications to detect anomalies and threats.
Q: How do you reduce alert fatigue in security monitoring?
A: Use threshold-based alerts, prioritize based on severity, use deduplication, and route alerts to appropriate teams.
Q: How do you detect privilege escalation via logs?
A: Look for patterns like self-assigned IAM roles, service account impersonation, or use of admin-level APIs.
Q: A container in production is running with root privileges. What do you do?
A: Isolate it, analyze behavior/logs, update image to run as non-root, enforce PSP or OPA to prevent recurrence.
Q: Your team uses an outdated OS image. How do you handle it?
A: Tag it as deprecated, communicate risks, provide an updated secure image, enforce it via CI validation or admission control.
Q: Your Vault cluster is down. How does your system respond?
A: Applications using Vault should have TTL-based secrets and retry logic. Consider HA Vault setup with integrated storage or cloud backends.
Q: A developer requests access to production secrets. What’s your response?
A: Use break-glass access with approvals, log all access, and revoke immediately after task completion.
Q: Your CI runners are compromised. What’s your action plan?
A: Revoke secrets, rotate credentials, rebuild runners, analyze audit logs, enforce isolation of runners per project.
Q: How do you track DevSecOps maturity?
A: Use a maturity model (e.g., NIST, OWASP SAMM), score each domain (CI/CD, infra, monitoring), and drive initiatives based on gaps.
Q: What security SLAs do you define?
A: MTTR for vulnerabilities, patch timelines (e.g., critical in 24h), compliance coverage, and secrets rotation frequency.
Q: What’s the “secure defaults” principle?
A: Ensure new systems/applications are deployed with least-privilege, encrypted, locked-down configurations without requiring user tuning.
Q: How do you handle legacy systems with no CI/CD?
A: Isolate, monitor strictly, document risks, create CI/CD wrapper (if possible), and define a migration plan.
Q: What would you automate first in a new DevSecOps project?
A: Dependency scanning, secrets detection, and IaC misconfig detection — as they give immediate, high-value coverage.
Q: How do you work with dev teams that push insecure code?
A: Set up feedback loops (e.g., PR comments via security scans), educate on patterns, and ensure security is integrated into sprint goals.
Q: How do you convince leadership to invest in DevSecOps?
A: Use ROI metrics like reduced incident response time, compliance readiness, and show the cost of breaches.
Q: How do you align DevSecOps with agile practices?
A: Embed security tasks in backlog, track security debt, run security sprints, and include security in DoD (Definition of Done).
Q: What’s your approach to onboarding new developers to secure coding?
A: Provide secure code guidelines, run onboarding workshops, give hands-on labs, and integrate real-time feedback in IDE or PRs.
Q: What’s your incident playbook template?
A: Incident title, detection method, affected systems, severity, impact, timeline, actions taken, lessons learned, and prevention steps.
Q: How do you unify DevSecOps across GCP, AWS, and Azure?
A: Use policy-as-code tools like OPA or Bridgecrew, centralize monitoring, and abstract IaC with Terraform modules or Pulumi.
Q: What are cloud-agnostic security patterns?
A: Encryption in transit/rest, identity federation, role-based access control, secure boot, and centralized logging.
Q: What’s the difference between cloud-native and cloud-agnostic security?
A: Cloud-native uses platform-specific tools/features, cloud-agnostic uses generalized, portable security tools and policies.
Q: How do you manage identity across multiple clouds?
A: Use a central IdP with SSO/OIDC, integrate with each cloud’s IAM, and enforce MFA and conditional access policies.
Q: How do you ensure consistent tagging and classification of resources?
A: Enforce tagging policies in IaC, validate in CI/CD, and use scripts/tools to report/tag retroactively.
Q: What is Zero Trust Architecture and how does DevSecOps support it?
A: It assumes no trust by default. DevSecOps enforces this by integrating identity verification, continuous monitoring, and least privilege in pipelines and infra.
Q: How do you use chaos engineering to improve security?
A: Simulate attacks or misconfigurations (e.g., revoked secrets, broken auth) to improve system resilience and detection capabilities.
Q: How do you integrate SBOMs into your pipeline?
A: Generate SBOMs using Syft or CycloneDX and store with artifacts. Use them for dependency scanning and vulnerability analysis.
Q: How does DevSecOps help in achieving faster recovery in DR scenarios?
A: Automates infra provisioning, config validation, and secrets rotation, enabling faster, consistent recovery workflows.
Q: How do you stay updated with regulatory requirements like SOC2, HIPAA, or PCI-DSS?
A: Subscribe to updates, participate in audits, align controls with frameworks like NIST/ISO, and use compliance-as-code tools.
Q: What is DevSecOps and how does it integrate into CI/CD pipelines?
    A: DevSecOps integrates security into every stage of the CI/CD pipeline by embedding security tools (like SAST, DAST, dependency scanning) into the software development lifecycle, enabling early vulnerability detection and faster remediation.
Q: How would you integrate SAST into a CI/CD pipeline?
    A: Use tools like SonarQube, Checkmarx, or Fortify in the build phase to analyze source code for vulnerabilities and fail the build on policy violations.
Q: What tools can be used for DAST in pipelines?
    A: OWASP ZAP, Burp Suite, and AppSpider are common DAST tools used during functional testing or staging to scan running applications.
Q: How do you implement container scanning in CI/CD?  
   A: Tools like Trivy, Clair, or Aqua Security scan container images during the build phase before pushing to registries.
Q: What is shift-left security?  
   A: It means integrating security practices early in the development cycle to catch issues before they reach production.
Q: How would you secure an S3 bucket in AWS?  
   A: Enable encryption (SSE), block public access, use IAM policies for least privilege, and enable logging.
Q: How do you secure traffic in Azure VNets?  
   A: Use NSGs, Azure Firewall, route tables, and private endpoints. Enable DDoS protection and logging.
Q: What are best practices for GCP IAM?  
   A: Use least privilege, predefined roles, organization policies, and avoid using primitive roles like `Editor`.
Q: How do you manage encryption in cloud environments?   
   A: Use KMS (AWS KMS, Azure Key Vault, GCP KMS) to manage encryption keys, ensure data-at-rest and in-transit encryption.
Q: How would you isolate workloads in the cloud?  
    A: Use separate VPCs, subnets, service accounts, and firewall rules; adopt microsegmentation for better isolation.
Q: What is IaaC and how does it help with security?  
    A: IaaC automates resource provisioning with version-controlled code, ensuring repeatability, compliance, and secure configurations.
Q: How do you secure Terraform code?  
    A: Use `terraform validate`, `tfsec`, `checkov`, and enable remote state with encryption and access controls.
Q: How do you handle secrets in IaC?  
    A: Avoid hardcoding secrets; use tools like Vault, SSM Parameter Store, or Secrets Manager and reference them securely.
Q: How would you enforce compliance in Terraform code?  
    A: Use Sentinel (for Terraform Enterprise), Open Policy Agent (OPA), or pre-commit hooks to enforce policies.

Q. What is the difference between Terraform and CloudFormation in terms of security?  
    A: Terraform is cloud-agnostic and supports third-party security tools; CloudFormation is AWS-native with tight IAM integration but less flexibility.
Q: What is the difference between SAST and DAST?  
    A: SAST scans static code before execution; DAST scans the application in a running state for runtime vulnerabilities.
Q: What is IAST and where is it used?  
    A: Interactive Application Security Testing combines SAST and DAST and is used during functional testing with real-time feedback.
Q: How do you secure Docker images?  
    A: Use minimal base images, multi-stage builds, scan for vulnerabilities, and sign images with Notary or Cosign.
Q: What is Software Composition Analysis (SCA)?  
    A: SCA identifies open-source libraries and checks them for known vulnerabilities using tools like Snyk, Black Duck, or OWASP Dependency-Check.
Q: How do you validate IaC security before deployment?  
    A: Use tools like Checkov, tfsec, or Conftest during the CI phase to scan infrastructure definitions for misconfigurations.
Q: How do you ensure compliance in a multi-cloud environment?  
    A: Use CSPM tools (like Prisma Cloud, Wiz), enforce policies through IaC, automate audits, and track drift from baselines.
Q: What is CIS Benchmark and how is it used?  
    A: It's a set of best practices for securely configuring systems and cloud platforms. Tools like AWS Config and Azure Security Center enforce these benchmarks.
Q: What is GDPR and how do you comply with it in the cloud?  
    A: GDPR ensures data privacy. Use encryption, ensure data residency, enforce access logging, and allow data subject requests.
Q: What tools automate compliance audits?  
    A: Tools like AWS Config, Azure Policy, GCP Forseti, and third-party platforms like Lacework or Fugue automate checks and reporting.
Q: What is SOC 2 and how do you prepare for it in cloud environments?  
    A: SOC 2 evaluates controls for data security, availability, and confidentiality. Automate evidence collection and maintain logs for audits.
Q: How do you detect threats in the cloud?  
    A: Use CSP-native tools like AWS GuardDuty, Azure Defender, GCP Security Command Center; integrate SIEM for aggregation and correlation.
Q: What is the first step in incident response?  
    A: Detection and identification of an incident followed by classification, containment, and notification.
Q: How do you contain a compromised EC2 instance?  
    A: Isolate it via security groups or quarantine subnet, take snapshots, and analyze logs for forensics.
Q: How do you ensure incident response readiness?  
    A: Have a playbook, automate detection, simulate attacks (tabletop exercises), and define roles/responsibilities.
Q: What logging tools are recommended for cloud security?  
    A: AWS CloudTrail, Azure Monitor, GCP Cloud Audit Logs, and integration with tools like Splunk or ELK.
Q: How do you manage vulnerabilities in cloud workloads?  
    A: Perform regular scans, automate patching, prioritize CVEs, and use tools like Qualys, Nessus, or AWS Inspector.
Q: How do you prioritize vulnerabilities?  
    A: Based on CVSS score, exploitability, asset criticality, and business impact.
Q: What is Patch Management and how is it automated?  
    A: It's the process of applying security patches regularly. Use tools like AWS Systems Manager, Azure Automation, or GCP OS Patch Management.
Q: How do you ensure vulnerability mitigation in containers?  
    A: Scan base images, fix CVEs, use read-only file systems, and apply runtime security with tools like Falco.
Q: What is a zero-day vulnerability?  
    A: A security flaw unknown to vendors; it’s critical because no patch exists. Continuous monitoring and behavior-based detection are key.
Q: What is the principle of least privilege?  
    A: Grant users the minimum permissions necessary to perform their tasks.
Q: How do you manage secrets securely in the cloud?  
    A: Use secrets managers like AWS Secrets Manager, Azure Key Vault, or HashiCorp Vault with tight access policies.
Q: What’s the difference between roles and policies in IAM?   
    A: Roles define what actions can be performed, policies attach permissions to roles or users.
Q: How do you audit IAM usage?  
    A: Use cloud logs (CloudTrail, Azure AD logs), analyze permission usage, and remove unused entitlements.
Q: How do you enforce MFA in a cloud environment?   
    A: Use IAM policies and identity providers to require MFA for all users and sensitive operations.
Q: How do you secure Kubernetes clusters?   
    A: Enable RBAC, use NetworkPolicies, limit access via API server, scan images, and implement pod security policies.
Q: How do you secure serverless functions?   
    A: Restrict IAM roles, validate input, monitor logs, and minimize external dependencies.
Q: What is a Cloud Security Posture Management (CSPM) tool?  
    A: A tool that continuously evaluates and enforces cloud configuration security—examples include Prisma Cloud, Wiz, and Orca.
Q: How do you secure inter-service communication in microservices?  
    A: Use mutual TLS (mTLS), API gateways, service mesh (Istio), and zero-trust principles.
Q: How do you handle logging in multi-cloud security architectures?  
    A: Centralize logs with ELK, Splunk, or cloud-native SIEMs and ensure consistent log formats and retention policies.
Q: How do you promote a security-first culture in DevOps teams?  
    A: Embed security champions, conduct regular trainings, enforce secure coding standards, and integrate tools into developer workflows.
Q: How do you handle security-related incidents with Dev and Ops teams?  
    A: Use an incident playbook, communicate clearly, assign roles, and perform root cause analysis post-resolution.
Q: How do you stay updated with new security threats?  
    A: Follow CVE databases, threat intel feeds, participate in communities (OWASP, CloudSec), and subscribe to vendor alerts.
Q: What is your approach to evaluating new security tools?  
    A: Analyze based on need, ease of integration, cost, coverage, and community/vulnerability database support.
Q: How do you measure the effectiveness of DevSecOps implementation?  
    A: Track metrics like time-to-remediate, vulnerabilities per release, compliance scores, and feedback from developers/security teams.
