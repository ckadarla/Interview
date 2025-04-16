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
