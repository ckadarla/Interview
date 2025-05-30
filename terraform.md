```markdown
# 🧰 Terraform Commands – Explained with Usage and Examples

This markdown provides a concise overview of **commonly used Terraform CLI commands**, their purpose, and real-world examples – ideal for interviews and practical use.

---

## 📦 1. `terraform init`

### 🔹 Description:
Initializes a new or existing Terraform configuration directory by downloading the provider plugins and setting up the backend.

### ✅ Usage:
```bash
terraform init
```

### 🧪 Example:
```bash
terraform init -backend-config="storage_account_name=mytfstate" -upgrade
```

---

## 📄 2. `terraform validate`

### 🔹 Description:
Validates the syntax and structure of Terraform files (.tf), ensuring they’re well-formed.

### ✅ Usage:
```bash
terraform validate
```

---

## 🧾 3. `terraform fmt`

### 🔹 Description:
Automatically formats Terraform code to canonical HCL style.

### ✅ Usage:
```bash
terraform fmt
```

### 🧪 Example:
```bash
terraform fmt -recursive
```

---

## 🔍 4. `terraform plan`

### 🔹 Description:
Shows the execution plan – what Terraform will create, update, or destroy without applying it.

### ✅ Usage:
```bash
terraform plan
```

### 🧪 Example:
```bash
terraform plan -out=tfplan.out
```

---

## ⚙️ 5. `terraform apply`

### 🔹 Description:
Applies the changes required to reach the desired state of the configuration.

### ✅ Usage:
```bash
terraform apply
```

### 🧪 Example:
```bash
terraform apply tfplan.out
```

---

## 💣 6. `terraform destroy`

### 🔹 Description:
Destroys all infrastructure managed by Terraform.

### ✅ Usage:
```bash
terraform destroy
```

### 🧪 Example:
```bash
terraform destroy -auto-approve
```

---

## 🔙 7. `terraform output`

### 🔹 Description:
Displays the values of output variables from your Terraform state.

### ✅ Usage:
```bash
terraform output
```

### 🧪 Example:
```bash
terraform output resource_group_name
```

---

## 📥 8. `terraform import`

### 🔹 Description:
Brings an existing resource under Terraform management by writing it into the state file.

### ✅ Usage:
```bash
terraform import <resource_type>.<resource_name> <resource_id>
```

### 🧪 Example:
```bash
terraform import azurerm_resource_group.rg1 /subscriptions/<id>/resourceGroups/my-rg
```

---

## 🧱 9. `terraform taint`

### 🔹 Description:
Marks a resource for recreation during the next apply.

### ✅ Usage:
```bash
terraform taint <resource_type>.<resource_name>
```

### 🧪 Example:
```bash
terraform taint azurerm_virtual_machine.vm1
```

---

## 🚫 10. `terraform untaint`

### 🔹 Description:
Removes the "tainted" state from a resource.

### ✅ Usage:
```bash
terraform untaint <resource_type>.<resource_name>
```

---

## 🧪 11. `terraform state`

### 🔹 Description:
Advanced command to inspect or modify the Terraform state file.

### ✅ Usage:
```bash
terraform state list
terraform state show <resource_name>
```

### 🧪 Example:
```bash
terraform state list
terraform state show azurerm_storage_account.mystorage
```

---

## 📌 12. `terraform graph`

### 🔹 Description:
Generates a visual graph of Terraform resources and their dependencies.

### ✅ Usage:
```bash
terraform graph | dot -Tpng > graph.png
```

---

## 🔐 13. `terraform login`

### 🔹 Description:
Authenticates Terraform CLI with Terraform Cloud/Enterprise.

### ✅ Usage:
```bash
terraform login
```

---

## ☁️ 14. `terraform workspace`

### 🔹 Description:
Manages multiple workspaces (useful for dev, test, prod environments).

### ✅ Usage:
```bash
terraform workspace new dev
terraform workspace select dev
terraform workspace list
```

---

## 📚 Summary Table

| Command | Purpose |
|--------|---------|
| `terraform init` | Initialize Terraform working directory |
| `terraform validate` | Validate configuration syntax |
| `terraform fmt` | Format Terraform code |
| `terraform plan` | Show changes without applying |
| `terraform apply` | Apply infrastructure changes |
| `terraform destroy` | Destroy all managed infrastructure |
| `terraform output` | Display output values |
| `terraform import` | Import existing resources |
| `terraform taint` | Force resource recreation |
| `terraform state` | Manage and inspect state file |
| `terraform workspace` | Manage separate workspaces |
| `terraform graph` | Visualize resource dependency |
| `terraform login` | Authenticate to Terraform Cloud |

---

## ✅ Interview Tips

- Emphasize Terraform lifecycle (`init → plan → apply → destroy`)
- Discuss **idempotency**, **state management**, and **modularity**
- Be ready to explain **how to manage secrets** (e.g., using `Key Vault`)
- Mention **remote backend** and **locking** for team usage

---

## 📎 References

- [Terraform CLI Docs](https://developer.hashicorp.com/terraform/cli)
- [Terraform Azure Provider](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs)

---
Here are several **Terraform troubleshooting scenarios** commonly asked in interviews, along with explanations and visual diagram ideas that can be generated on request:

---

### **1. Terraform Plan Fails with Provider Initialization Error**

**Problem:**
`Error: Failed to instantiate provider`

**Causes & Fix:**

* Incorrect provider block or version mismatch.
* Fix by verifying `required_providers` and running:

  ```bash
  terraform init -upgrade
  ```

---

### **2. Terraform Apply Hangs or Fails due to State Lock**

**Problem:**
`Error: Error acquiring the state lock`

**Causes & Fix:**

* Another user/process is modifying the same state.
* Use:

  ```bash
  terraform force-unlock <LOCK_ID>
  ```

**Interview Tip:** Mention implications of manual unlocks and consistency.

---

### **3. Terraform Destroy Deletes Shared Resources**

**Problem:**
Unexpected deletion of shared infrastructure.

**Causes & Fix:**

* Lack of proper dependency segregation.
* Use separate workspaces or modules.
* Mark shared resources with `lifecycle.prevent_destroy = true`.

---

### **4. Terraform Fails Due to "Object has no attribute"**

**Problem:**
`Error: Unsupported attribute`

**Causes & Fix:**

* Trying to access an attribute that doesn't exist yet (like a list item not created).
* Use `terraform console` to inspect objects, and conditional checks.

---

### **5. Terraform Apply Succeeds but No Changes Occur**

**Problem:**
Terraform says "0 to add, 0 to change, 0 to destroy"

**Causes & Fix:**

* Resource drift not detected because Terraform thinks the state is current.
* Use `terraform refresh` or `terraform import`.

---

### **6. Terraform Plan Shows Re-Creation of Resources**

**Problem:**
Terraform wants to destroy and recreate resources on every plan.

**Causes & Fix:**

* Immutable resource fields changed (like name or subnet).
* Use `lifecycle.ignore_changes`.

---

### **7. Terraform Plan Applies Out-of-Order**

**Problem:**
Terraform fails due to dependency order issue.

**Causes & Fix:**

* Missing explicit dependencies.
* Use `depends_on` to enforce ordering.

---

### **8. Remote State Backend Errors (e.g., GCS, S3, Azure Blob)**

**Problem:**
Authentication or access denied.

**Causes & Fix:**

* Service account permission issues.
* Use correct `credentials` file or `az login/gcloud auth login`.

---

### **9. Terraform Init Fails with Backend Configuration Errors**

**Problem:**
`Backend initialization required, please run terraform init`

**Fix:**
Check backend block:

```hcl
terraform {
  backend "gcs" {
    bucket = "my-bucket"
    prefix = "terraform/state"
  }
}
```

Validate credentials and bucket accessibility.

---

### **10. Terraform Shows Output As Empty or Null**

**Problem:**
Outputs are not being returned or shown as `null`.

**Fix:**

* Ensure the output block references a valid resource attribute.
* Use `depends_on` if resource dependency is not implicit.

---
Great! Below is a **focused list of advanced Terraform troubleshooting scenarios** specifically related to **GCP (Google Cloud Platform)**. These examples cover common issues with GCP services, IAM, GCS backends, APIs, and state handling.

---

## 🔧 **Advanced GCP + Terraform Troubleshooting Scenarios**

---

### **11. GCP Resource Creation Fails with “permission denied”**

**Problem:**

```bash
Error creating <resource>: googleapi: Error 403: Permission denied
```

**Cause & Fix:**

* The service account used by Terraform lacks necessary IAM roles.
* Ensure roles like `roles/editor`, `roles/compute.admin`, or service-specific roles are attached.
* Use:

  ```bash
  gcloud projects get-iam-policy <project-id>
  gcloud auth list
  ```

📌 **Diagram Suggestion**: GCP IAM permission flow (Terraform ➝ Service Account ➝ API ➝ GCP Resource).

---

### **12. Terraform Fails to Create GCS Bucket Due to API Disabled**

**Problem:**

```bash
Error: Error creating bucket: googleapi: Error 403: Cloud Storage API has not been used
```

**Fix:**

* Enable required APIs:

  ```bash
  gcloud services enable storage.googleapis.com
  ```

🔧 Tip: Use a `null_resource` with a `local-exec` to check for enabled APIs.

---

### **13. State File Corruption in GCS Backend**

**Problem:**
Terraform cannot read/write to remote GCS backend.

**Cause & Fix:**

* Concurrent operations without locking.
* Corrupted JSON state file or metadata issues.

**Fix:**

* Use:

  ```bash
  gsutil ls gs://<bucket>/terraform/
  gsutil cp <backup>.tfstate <path>.tfstate
  terraform init
  ```

📌 **Diagram Suggestion**: Terraform Remote State in GCS + State Locking.

---

### **14. Terraform Creates Resources in the Wrong Region/Zone**

**Cause:**

* Variables not properly defined or overridden.
* Missing default values or wrong interpolation.

**Fix:**

* Validate:

  ```hcl
  variable "region" {
    default = "us-central1"
  }
  provider "google" {
    region = var.region
  }
  ```

🔍 Use `terraform plan -var region=us-central1` explicitly if needed.

---

### **15. GCP IAM Role Bindings in Terraform Cause Drift**

**Problem:**
IAM bindings always appear in plan as changes.

**Cause:**
Using `google_project_iam_binding` causes replacement of all bindings, not incremental.

**Fix:**

* Prefer `google_project_iam_member` for additive updates.
* Or manage all bindings in a single `google_project_iam_policy` block.

📌 **Diagram Suggestion**: IAM Role Binding vs Member in Terraform and effect on drift.

---

### **16. Error: "Quota exceeded" When Provisioning Resources**

**Cause:**
Terraform requests exceed project/region quotas (e.g., CPUs, IPs).

**Fix:**

* Check quotas:

  ```bash
  gcloud compute regions describe <region>
  ```
* Request quota increase from GCP Console.

---

### **17. Terraform Fails to Create Service Account Key**

**Problem:**

```bash
Error creating service account key: disabled service
```

**Fix:**

* Enable IAM API:

  ```bash
  gcloud services enable iam.googleapis.com
  ```

* Check org policies blocking service account key creation.

---

### **18. GKE Cluster Creation Fails Mid-Way**

**Problem:**
Terraform fails on GKE node pool creation with timeout or quota error.

**Fix:**

* Check for:

  * Unavailable subnet IPs.
  * Insufficient regional resources.
* Review logs in GCP Console ➝ GKE ➝ Operations.

📌 **Diagram Suggestion**: GKE provisioning flow (Terraform ➝ GKE API ➝ VPC/Subnet/IPs ➝ Cluster/Nodes).

---

### **19. Terraform Apply Times Out on Load Balancer Creation**

**Cause:**
GCP Load Balancers require health checks and backends to stabilize before Terraform finishes.

**Fix:**

* Add explicit `depends_on` for resources like `google_compute_backend_service`.

---

### **20. GCP Project Creation via Terraform Results in API Errors**

**Problem:**
Error: `Project creation failed: Request contains an invalid argument.`

**Fix:**

* Make sure `org_id` or `folder_id` is specified.
* Billing must be associated after project creation via `google_project_billing_info`.

---
Absolutely! Here are **more advanced and often overlooked Terraform + GCP troubleshooting scenarios**, especially useful for interviews and real-world experience showcasing.

---

## 🔧 **More GCP + Terraform Troubleshooting Scenarios**

---

### **21. Terraform Fails with `400: Requested entity already exists`**

**Problem:**

```bash
googleapi: Error 409: Requested entity already exists
```

**Cause:**

* Trying to recreate a deleted resource too soon (e.g., Pub/Sub topic, GCS bucket).
* GCP takes time to release some resource names globally.

**Fix:**

* Use unique suffixes (`random_id` or timestamp).
* Or delay and retry apply after cleanup propagation.

---

### **22. Terraform Plan Always Wants to Change GCP Subnet**

**Cause:**

* GCP sometimes represents secondary IP ranges in a different internal order.
* Terraform sees this as a change even if logically identical.

**Fix:**

* Use `lifecycle { ignore_changes = [secondary_ip_range] }`.

---

### **23. Terraform GKE Module Fails with “default node pool cannot be deleted”**

**Problem:**
GKE clusters provisioned via console have default node pools.

**Fix:**
If using Terraform to manage custom node pools:

```hcl
remove_default_node_pool = true
initial_node_count = 1
```

Then delete the default node pool in Terraform.

---

### **24. Terraform Apply Fails on Project IAM Binding Removal**

**Problem:**
Cannot remove bindings added by GCP or other tools.

**Cause:**
Bindings applied outside Terraform (console, CLI) cause drift.

**Fix:**

* Use `google_project_iam_member` or import current policy:

  ```bash
  terraform import google_project_iam_policy.my_policy <project_id>
  ```

---

### **25. Cloud Function Fails to Deploy via Terraform**

**Problem:**

```bash
Error creating function: Source code not uploaded
```

**Cause:**

* `source_archive_bucket` or `source_archive_object` not properly uploaded.

**Fix:**
Ensure archive is uploaded **before** function is created:

```hcl
depends_on = [google_storage_bucket_object.archive]
```

📌 **Tip:** Automate upload via `null_resource` and `local-exec`.

---

### **26. Terraform Apply Fails with "provider not supported" in Module**

**Cause:**
Provider not passed explicitly to module.

**Fix:**

```hcl
module "my_module" {
  source = "./modules/something"
  providers = {
    google = google
  }
}
```

---

### **27. Terraform Import Errors for GCP Resources**

**Problem:**
Resource exists, but import fails or partial state imported.

**Fix:**

* Use exact GCP format:

  ```bash
  terraform import google_compute_instance.myvm projects/<project>/zones/<zone>/instances/<name>
  ```

* Use `terraform show` to inspect imported attributes and manually adjust.

---

### **28. Terraform Creates Extra GCP Firewall Rules**

**Cause:**
Default rules are created by GCP console or Deployment Manager.

**Fix:**

* Clean up manually created rules.
* Manage all firewall rules via Terraform.
* Use naming standards and filters to prevent duplicates.

---

### **29. GCP VPC Peering Module Keeps Showing Changes**

**Cause:**
Peering configuration is eventually consistent and takes time.

**Fix:**

* Add `create_timeouts`, and reduce polling:

  ```hcl
  timeouts {
    create = "10m"
    delete = "10m"
  }
  ```

* Accept delay or add `lifecycle.ignore_changes`.

---

### **30. GCP DNS Resource Update Always Forces Replacement**

**Problem:**
Updating records in `google_dns_record_set` destroys old record.

**Fix:**

* Use `ttl` carefully (changing TTL replaces record).
* Avoid toggling between record types.

---
Here are **10 more advanced Terraform + GCP troubleshooting scenarios**, especially useful for **senior-level DevOps/Platform Engineer interviews** and **real-world diagnostics**.

---

## 🔧 **More Deep-Dive Terraform + GCP Troubleshooting Scenarios**

---

### **31. `google_project_service` repeatedly tries to enable already enabled API**

**Problem:**
Terraform keeps showing the same `google_project_service` resource in the plan.

**Cause:**
Terraform's state does not always match the actual enabled API state due to async delays.

**Fix:**

* Add `disable_on_destroy = false` to avoid re-enabling.
* Use a delay or retry logic if using `depends_on` for services.
* Use `terraform import` to correct state if needed.

---

### **32. GCP Secret Manager Resource Appears Recreated Every Plan**

**Problem:**
`google_secret_manager_secret_version` seems to recreate every time.

**Cause:**

* Resource content is considered "changed" due to lack of hashing or randomness.

**Fix:**
Use:

```hcl
lifecycle {
  ignore_changes = [secret_data]
}
```

Or hash content with checksum in the filename.

---

### **33. Terraform Fails to Destroy GCP Resources Due to Dependencies**

**Problem:**
Firewall rules, instance templates, or GKE clusters won’t destroy due to dependencies.

**Fix:**
Use `terraform graph` and `terraform state list` to identify dependencies. Then:

* Destroy manually with CLI
* Or use `terraform destroy -target` to handle in correct order.

---

### **34. Terraform Apply Fails With `resource_in_use_by_another_resource`**

**Cause:**
Trying to delete/update VPC or subnet still used by:

* Load balancer
* GKE cluster
* Static IP

**Fix:**

* Use GCP Console or `gcloud` to find dependencies:

  ```bash
  gcloud compute addresses list
  gcloud compute forwarding-rules list
  ```

* Remove or move those dependencies first.

---

### **35. GCS Remote State Backend Errors on Lock Acquisition**

**Problem:**

```bash
Error locking state: Error acquiring the state lock
```

**Fix:**

* Use `terraform force-unlock <lock-id>` cautiously.
* Avoid multiple `terraform apply` or `plan` processes at once.
* Consider switching to **Terraform Cloud** or **Consul** for robust locking.

---

### **36. Output From Module or Resource Not Found**

**Problem:**

```bash
Error: Reference to undeclared resource or module output
```

**Cause:**

* Incorrect naming or module output not exposed.

**Fix:**
Ensure:

```hcl
output "cluster_endpoint" {
  value = google_container_cluster.primary.endpoint
}
```

And call it as:

```hcl
module.gke_cluster.cluster_endpoint
```

---

### **37. Terraform Plan Fails With Unknown Variable or Null**

**Problem:**
Plan fails if a variable isn’t passed and doesn’t have a default.

**Fix:**

* Ensure required vars are passed:

  ```bash
  terraform plan -var="env=prod"
  ```

* Or mark variable optional:

  ```hcl
  variable "env" {
    type    = string
    default = "dev"
  }
  ```

---

### **38. GCP Load Balancer Forwarding Rule Conflicts With Existing IP**

**Problem:**

```bash
Error: IP address already in use
```

**Cause:**
Trying to reassign a static IP that’s already bound.

**Fix:**

* Use `google_compute_global_address` or `google_compute_address` and reference dynamically.

---

### **39. Terraform Tries to Replace Unchanged GCS Bucket**

**Cause:**

* Metadata like labels or storage class defaults in GCP cause drift.

**Fix:**
Use:

```hcl
lifecycle {
  ignore_changes = [labels, storage_class]
}
```

---

### **40. Terraform Workspace State Not Isolated in GCS Backend**

**Problem:**
Different Terraform workspaces overwrite each other’s state in same GCS bucket.

**Fix:**
Use `prefix` in backend config:

```hcl
backend "gcs" {
  bucket  = "tf-state-bucket"
  prefix  = "prod/"
}
```

---

