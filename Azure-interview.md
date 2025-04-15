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
### Azure Virtual Machine Scale Sets (VMSS)

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

---
## Types of Azure Storage

Azure provides various storage options to meet different application needs. Below are the key types of storage services:

## 1. **Azure Blob Storage**
- **Description**: Object storage for unstructured data, such as text, images, videos, and backups.
- **Use Cases**: File storage, backups, data lakes, media storage.
- **Tiers**: Hot, Cool, Archive.

## 2. **Azure Disk Storage**
- **Description**: Persistent block storage for Azure Virtual Machines.
- **Use Cases**: OS disks, data disks, and high-performance workloads.
- **Types**: Managed Disks (Standard SSD, Premium SSD, Standard HDD).

## 3. **Azure File Storage**
- **Description**: Fully managed file shares in the cloud, accessible via SMB (Server Message Block) protocol.
- **Use Cases**: Lift-and-shift applications, shared storage for legacy apps.
- **Features**: Azure File Sync, SMB support, Azure Active Directory integration.

## 4. **Azure Queue Storage**
- **Description**: Simple message queuing for communication between applications or components.
- **Use Cases**: Decoupling workloads, async messaging, background task processing.
- **Features**: Simple REST-based API, maximum message size up to 64 KB.

## 5. **Azure Table Storage**
- **Description**: NoSQL key-value store for storing structured, non-relational data.
- **Use Cases**: Storing large amounts of structured data, application logs, metadata.
- **Features**: Scalable, low-latency, NoSQL capabilities.

## 6. **Azure Data Lake Storage**
- **Description**: A specialized form of Blob Storage optimized for big data analytics.
- **Use Cases**: Data lakes, analytics, and machine learning workloads.
- **Features**: Hierarchical namespace, security, analytics-friendly.

## 7. **Azure Blob Storage for Archive**
- **Description**: Long-term, low-cost storage for data that is rarely accessed.
- **Use Cases**: Archiving, compliance data storage, backups.
- **Tiers**: Archive (lowest cost, slow access).

## 8. **Azure NetApp Files**
- **Description**: High-performance file storage service that supports NFS and SMB protocols.
- **Use Cases**: Enterprise applications, SAP, databases requiring high throughput and low latency.
- **Features**: High IOPS, low latency, scalable storage.

## 9. **Azure Storage for Azure Kubernetes Service (AKS)**
- **Description**: Persistent storage for containers running on AKS.
- **Use Cases**: Containerized applications needing persistent storage.
- **Types**: Azure Disk, Azure File, Azure Blob.

## 10. **Azure Archive Storage**
- **Description**: Cost-effective solution for long-term data retention with infrequent access.
- **Use Cases**: Archiving, compliance requirements, backup data.
- **Features**: Low cost, slow retrieval times, designed for "cold" storage.

## Summary Table

| Storage Type              | Use Case                            | Access Mode    | Key Feature                           |
|---------------------------|-------------------------------------|----------------|---------------------------------------|
| **Blob Storage**           | Unstructured data, backups         | Object storage | Scalable, cost-effective              |
| **Disk Storage**           | Virtual Machine disks              | Block storage  | Managed disks, high-performance       |
| **File Storage**           | SMB file shares                    | File storage   | SMB support, Azure File Sync         |
| **Queue Storage**          | Message queuing                    | Queue storage  | Simple, REST-based API               |
| **Table Storage**          | NoSQL, key-value data storage      | NoSQL storage  | Scalable, low-latency                |
| **Data Lake Storage**      | Big data analytics                 | Object storage | Hierarchical namespace, analytics    |
| **Blob Archive Storage**   | Long-term, infrequent access       | Object storage | Low-cost, infrequent access          |
| **NetApp Files**           | Enterprise file storage            | File storage   | High IOPS, low latency               |
| **Storage for AKS**        | Persistent storage for containers  | Block & file   | Supports containers and Kubernetes    |
| **Archive Storage**        | Long-term, infrequent access       | Object storage | Low-cost, slow retrieval             |
---

