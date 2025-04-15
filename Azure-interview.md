## 1. Rehost (Lift and Shift)

- **Definition**: Move applications to Azure without changes.
- **When to Use**:
  - Need a quick migration.
  - Compatible with Azure VMs.
- **Tools**:
  - Azure Migrate
  - Azure Site Recovery
- **Pros**:
  - Fastest migration path.
  - Minimal risk.
- **Cons**:
  - Doesn't leverage cloud-native features.
  - Higher long-term operational cost.

---

## 2. Refactor (Repackage / Lift, Tinker, and Shift)

- **Definition**: Minor changes to apps (e.g., config updates, containerization) to run on Azure.
- **When to Use**:
  - Want to migrate to PaaS or containers.
- **Tools**:
  - Azure App Service
  - Azure Kubernetes Service (AKS)
  - Azure Container Apps
- **Pros**:
  - Better use of cloud capabilities.
  - Easier to manage than VMs.
- **Cons**:
  - Some code/config changes required.
  - More complex than rehost.

---

## 3. Rearchitect

- **Definition**: Modify app architecture for scalability, resilience, and cloud-native design.
- **When to Use**:
  - Existing architecture isn’t scalable or modern.
- **Tools**:
  - Azure Functions
  - Azure Logic Apps
  - Azure Kubernetes Service (AKS)
  - Azure Event Grid / Service Bus
- **Pros**:
  - Cloud-native architecture benefits.
  - Supports microservices.
- **Cons**:
  - Time-consuming and costly.
  - Requires deeper expertise.

---

## 4. Rebuild (Redesign / Rewrite)

- **Definition**: Rebuild the app from scratch using cloud-native technologies.
- **When to Use**:
  - Legacy app is outdated or doesn’t meet needs.
- **Tools**:
  - Azure SQL
  - Cosmos DB
  - Azure Functions
- **Pros**:
  - Maximum cloud benefits.
  - Opportunity for modern business needs.
- **Cons**:
  - High cost and effort.
  - Potentially risky if mismanaged.

---

## 5. Replace (Drop and Shop)

- **Definition**: Replace app with SaaS solution.
- **When to Use**:
  - SaaS product satisfies the business requirement.
- **Examples**:
  - Dynamics 365 (ERP)
  - Microsoft 365 (Email, Collaboration)
- **Pros**:
  - Rapid deployment.
  - Low operational burden.
- **Cons**:
  - Limited customization.
  - Vendor lock-in possible.

---

## Summary Table

| Strategy    | Code Changes | Time to Migrate | Cloud-Native Benefits | Use Case                                |
|-------------|--------------|------------------|------------------------|-----------------------------------------|
| Rehost      | None         | Fast             | Low                    | Quick migration, legacy apps            |
| Refactor    | Minimal      | Moderate         | Moderate               | PaaS migration, minor tweaks            |
| Rearchitect | Moderate     | Longer           | High                   | Microservices, scalable design          |
| Rebuild     | Full rewrite | Longest          | Very High              | Legacy apps need modernization          |
| Replace     | None         | Varies           | Depends on SaaS        | When off-the-shelf SaaS is viable       |

# Azure Virtual Network (VNet)

**Azure Virtual Network (VNet)** is the fundamental building block for your private network in Azure. It enables secure communication between **Azure resources**, your **on-premises networks**, and the **internet**, similar to how traditional on-premises networks operate.

---

## 🔧 Key Features of Azure VNet

| Feature                      | Description |
|-----------------------------|-------------|
| **Isolation**               | Each VNet is isolated from other VNets and networks by default. |
| **Subnets**                 | VNets can be divided into subnets to organize and secure resources. |
| **Private IPs**             | Resources within a VNet communicate using private IP addresses. |
| **Routing**                 | Azure provides default routing and supports custom route tables. |
| **Network Security Groups** | NSGs allow or deny traffic to/from resources based on security rules. |
| **Service Endpoints**       | Securely connect to Azure services (e.g., Azure SQL, Storage) using the VNet. |
| **Private Link**            | Provides private access to PaaS services over your VNet. |
| **VNet Peering**            | Connect VNets across regions or subscriptions with high-speed links. |
| **VPN Gateway**             | Establish a secure connection between your on-premises network and Azure. |
| **ExpressRoute**            | Create a private, dedicated connection between your data center and Azure. |

---

## 🔄 Use Cases

- Deploy applications that require **secure internal communication**.
- Create **multi-tier application architectures** (e.g., web, app, and database tiers).
- Enable **hybrid connectivity** between on-prem and Azure environments.
- Provide **private access** to Azure services via Private Link.
- Isolate and **secure workloads** using NSGs and Azure Firewall.

---
