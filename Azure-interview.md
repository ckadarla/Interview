# Azure 5 R's Migration Model

The Azure 5 R's model helps choose the right migration strategy for each application when moving to the cloud.

## 1. Rehost (Lift and Shift)
- **Description**: Move applications to Azure VMs without code changes.
- **Use Case**: Quick migration, minimal risk.
- **Pros**: Fast and simple.
- **Cons**: No cloud-native benefits.
- **Tools**: Azure Migrate, Azure Site Recovery.

## 2. Refactor (Repackage)
- **Description**: Minor code/config changes to run apps on Azure PaaS/containers.
- **Use Case**: Modernization without a full rewrite.
- **Pros**: Better scalability and manageability.
- **Cons**: Some development effort required.
- **Tools**: Azure App Service, Azure Container Apps, AKS.

## 3. Rearchitect
- **Description**: Modify application architecture for the cloud.
- **Use Case**: Need for scalability, high availability, modernization.
- **Pros**: Enables microservices, event-driven design.
- **Cons**: Higher complexity and cost.
- **Tools**: AKS, Azure Functions, Event Grid, Service Bus.

## 4. Rebuild (Rewrite)
- **Description**: Rebuild the app from scratch using cloud-native services.
- **Use Case**: Legacy or outdated apps.
- **Pros**: Fully optimized for the cloud.
- **Cons**: Time-consuming and expensive.
- **Tools**: Azure PaaS, Azure Functions, Cosmos DB.

## 5. Replace (Drop and Shop)
- **Description**: Replace the application with a SaaS solution.
- **Use Case**: When an off-the-shelf solution meets the need.
- **Pros**: Low management overhead, quick to deploy.
- **Cons**: Less control, vendor lock-in.
- **Examples**: Microsoft 365, Dynamics 365.

## Summary Table
-----------------------------------------------------------------------------------------------
| Strategy    | Code Changes | Migration Time | Cloud Benefits | Use Case                     |
|-------------|--------------|----------------|----------------|------------------------------|
| Rehost      | None         | Fast           | Low            | Legacy apps, quick move      |
| Refactor    | Minimal      | Moderate       | Medium         | PaaS-ready apps              |
| Rearchitect | Moderate     | Long           | High           | Apps needing modernization   |
| Rebuild     | High         | Longest        | Very High      | Legacy apps, full redesign   |
| Replace     | None         | Varies         | Depends on SaaS| SaaS-based replacements      |
-----------------------------------------------------------------------------------------------

---
# Azure Virtual Network (VNet)
**Azure Virtual Network (VNet)** is the fundamental building block for your private network in Azure. It enables secure communication between **Azure resources**, your **on-premises networks**, and the **internet**, similar to how traditional on-premises networks operate.

## 🔧 Key Features of Azure VNet
---
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
# Azure Virtual Machine Scale Sets (VMSS)

## Overview
Azure Virtual Machine Scale Sets (VMSS) allow you to deploy and manage a group of identical, load-balanced VMs. VMSS provides high availability, scalability, and automated VM management.

## Key Features
- **Auto-scaling**: Automatically increases or decreases VM instances based on demand or schedules.
- **Load Balancing**: Distributes traffic across multiple VM instances using Azure Load Balancer or Application Gateway.
- **Integrated with Azure Autoscale**: Scales based on CPU, memory, disk I/O, or custom metrics.
- **Uniform or Flexible Orchestration**:
  - **Uniform**: Identical VMs managed as a group (ideal for stateless workloads).
  - **Flexible**: Supports VM instance uniqueness and mixed VM types (better for stateful or complex workloads).
- **Support for Availability Zones**: Ensures high availability across zones.

## Use Cases
- Web server farms
- Microservices and container-based architectures
- Batch processing jobs
- High availability and disaster recovery environments

## Benefits
- Simplifies VM management at scale
- Cost-effective with auto-scale based on usage
- Improves app availability and performance

## Tools & Integrations
- Azure Portal
- Azure CLI / PowerShell
- ARM / Bicep / Terraform
- Integrated with Azure Monitor and Alerts

## Example
Deploy a VMSS with autoscale to handle fluctuating web traffic during peak hours and scale down during off-peak hours to save cost.
