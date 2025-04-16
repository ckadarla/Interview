# Azure Kubernetes Service (AKS) - Features and Add-on Differences

## Overview

Azure Kubernetes Service (AKS) is a managed Kubernetes offering from Microsoft Azure that simplifies Kubernetes deployment and management by handling much of the operational overhead.

---

## AKS Core Features

| Feature | Description |
|--------|-------------|
| **Managed Control Plane** | Azure manages the Kubernetes control plane components (API server, etcd, etc.), ensuring high availability and patching. |
| **Node Auto-Scaling** | Automatically scales the number of nodes based on the resource demand. |
| **Integrated Monitoring** | Native integration with Azure Monitor and Log Analytics for cluster and container insights. |
| **Azure AD Integration** | Enables Azure Active Directory-based authentication and RBAC for secure access control. |
| **Private Clusters** | Deploy private AKS clusters with no public IP exposure of the API server. |
| **Virtual Nodes (ACI Integration)** | Rapidly burst workloads to Azure Container Instances (ACI) without adding new nodes. |
| **Managed Identities** | Use Azure Managed Identities for accessing Azure resources from pods securely. |
| **Node Pool Management** | Support for multiple node pools with various VM sizes and OS types (Linux/Windows). |
| **Availability Zones** | Distribute nodes across zones for better resilience and fault tolerance. |
| **Secrets Integration** | Securely integrate with Azure Key Vault for managing application secrets. |

---

## Kubernetes-native Features vs AKS Add-on Features

| Category | Kubernetes-native Features | AKS Add-on Features |
|---------|-----------------------------|----------------------|
| **Scaling** | Horizontal Pod Autoscaler (HPA), Vertical Pod Autoscaler (VPA), Cluster Autoscaler (manual setup) | Node Auto-scaling managed by AKS |
| **Authentication** | Kubernetes RBAC, service accounts | Azure AD Integration with Kubernetes RBAC |
| **Monitoring** | Metrics Server, Prometheus, Grafana | Azure Monitor Container Insights (built-in add-on) |
| **Ingress** | NGINX, Traefik, Istio ingress controllers | Application Gateway Ingress Controller (AGIC) |
| **Networking** | Calico for NetworkPolicy, CNI plugins | Azure CNI (Advanced networking), Kubenet (Basic) |
| **Storage** | CSI drivers, Persistent Volumes, StorageClasses | Azure Disk & File CSI Drivers (managed add-ons) |
| **Security** | PodSecurityPolicy, NetworkPolicy, Secrets | Azure Policy Add-on, Azure Defender for Kubernetes |
| **Upgrades** | Manual via `kubectl` or CI/CD tools | One-click upgrade through Azure CLI/Portal |
| **GitOps** | Flux, ArgoCD (community managed) | Flux v2 GitOps Add-on (AKS-managed) |

---

## Summary

- **Kubernetes-native features** are part of the open-source Kubernetes project and can run on any conformant cluster.
- **AKS Add-ons** are tightly integrated with the Azure ecosystem, offering enhanced ease of use, scalability, and security with minimal configuration overhead.

Using AKS gives teams a balance between the power of Kubernetes and the productivity of a managed, cloud-native platform.

---
