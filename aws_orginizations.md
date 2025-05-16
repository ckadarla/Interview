**AWS Organizations** is a service provided by Amazon Web Services (AWS) that allows you to centrally manage and govern multiple AWS accounts in a scalable and secure way.

### 🔹 **Key Features of AWS Organizations:**

1. **Multi-Account Management:**

   * Create and manage multiple AWS accounts under a single organization.
   * Useful for separating environments (e.g., dev, test, prod), business units, or projects.

2. **Consolidated Billing:**

   * All accounts under the organization can share a single payment method.
   * Take advantage of volume discounts and manage costs centrally.

3. **Organizational Units (OUs):**

   * Group accounts into OUs to apply policies and management controls at different levels (e.g., all production accounts in one OU).

4. **Service Control Policies (SCPs):**

   * Define guardrails by setting permission boundaries for accounts or OUs.
   * Prevent even account administrators from performing restricted actions.

5. **Centralized Governance:**

   * Manage access, compliance, and security policies across all accounts from the management account.

6. **Integration with AWS IAM:**

   * Works seamlessly with Identity and Access Management (IAM) to control what actions users and roles can perform.

---

### 🔹 **Common Use Cases:**

* **Enterprise account structure:** Isolate workloads, projects, or teams in separate AWS accounts for security and billing clarity.
* **Cost tracking and optimization:** Track usage and costs by account, business unit, or project.
* **Policy enforcement:** Enforce organization-wide restrictions (e.g., deny use of certain regions or services).

---

### 🔹 **Basic Terminology:**

| Term                             | Description                                                                     |
| -------------------------------- | ------------------------------------------------------------------------------- |
| **Management Account**           | The root account that creates the organization and manages other accounts.      |
| **Member Account**               | An AWS account that is part of the organization but not the management account. |
| **OU (Organizational Unit)**     | A container for grouping AWS accounts within the organization.                  |
| **SCP (Service Control Policy)** | A policy that defines allowable services and actions within accounts/OUs.       |

---

Here are some **common types of Service Control Policies (SCPs)** used under **AWS Organizations**, along with examples to help you understand how they’re used:

---

### 🔒 **1. Deny Use of Specific AWS Services**

Restrict the use of a service (e.g., EC2, S3) for compliance or cost control.

**Example: Deny EC2**

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Deny",
      "Action": "ec2:*",
      "Resource": "*"
    }
  ]
}
```

---

### 🌍 **2. Deny Use of AWS Regions**

Restrict access to AWS services in specific regions to meet compliance or data residency requirements.

**Example: Deny All Except us-east-1 and eu-west-1**

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Deny",
      "Action": "*",
      "Resource": "*",
      "Condition": {
        "StringNotEquals": {
          "aws:RequestedRegion": ["us-east-1", "eu-west-1"]
        }
      }
    }
  ]
}
```

---

### 🛑 **3. Prevent IAM Actions**

Control IAM privilege escalation or restrict creation/modification of IAM users, roles, or policies.

**Example: Deny IAM Role Creation**

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Deny",
      "Action": [
        "iam:CreateRole",
        "iam:PutRolePolicy",
        "iam:AttachRolePolicy"
      ],
      "Resource": "*"
    }
  ]
}
```

---

### 💳 **4. Deny Billing and Account Management**

Prevent access to account-level settings or billing information.

**Example: Deny Access to Billing Console**

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Deny",
      "Action": [
        "aws-portal:*",
        "budgets:*",
        "cur:*"
      ],
      "Resource": "*"
    }
  ]
}
```

---

### ✅ **5. Allow List (Whitelisting) Specific Services Only**

Allow access to only specific services; deny everything else.

**Example: Allow Only S3 and CloudWatch**

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "s3:*",
        "cloudwatch:*"
      ],
      "Resource": "*"
    }
  ]
}
```

> Note: You also need a **"Deny All"** SCP attached with this to make a true allowlist.

---

### 🛡️ **Best Practices for SCPs:**

* Always start with **monitor mode (FullAWSAccess + custom Deny policies)**.
* Test on **organizational units (OUs)** instead of directly on accounts.
* Use **naming conventions** for policies to manage them at scale.
* Use **tags** and **CloudTrail** to audit policy impact.

Would you like a table with use cases mapped to SCP examples or a visual policy inheritance diagram?
