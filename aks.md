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


### 💻 AKS Commands & Usage – Interview Reference Guide

This cheat sheet covers essential AKS commands and usage examples useful for interviews and day-to-day tasks.

---

## 🔧 Cluster Management

### Create an AKS Cluster
```bash
az aks create \
  --resource-group <resource-group> \
  --name <cluster-name> \
  --node-count 3 \
  --enable-addons monitoring \
  --enable-managed-identity \
  --generate-ssh-keys
```

### Get AKS Credentials (Kubeconfig)
```bash
az aks get-credentials \
  --resource-group <resource-group> \
  --name <cluster-name>
```

### View Cluster Details
```bash
az aks show \
  --resource-group <resource-group> \
  --name <cluster-name> \
  --output table
```

### Delete Cluster
```bash
az aks delete \
  --resource-group <resource-group> \
  --name <cluster-name> \
  --yes --no-wait
```

---

## 🔐 Identity & Access

### Enable Azure AD Integration (when creating cluster)
```bash
az aks create \
  --enable-aad \
  --aad-admin-group-object-ids <group-id>
```

### List Cluster Admin Credentials
```bash
az aks get-credentials \
  --admin \
  --resource-group <resource-group> \
  --name <cluster-name>
```

---

## 📦 Node Pool Operations

### Add a Node Pool
```bash
az aks nodepool add \
  --resource-group <resource-group> \
  --cluster-name <cluster-name> \
  --name <nodepool-name> \
  --node-count 2 \
  --node-vm-size Standard_DS2_v2
```

### Scale Node Pool
```bash
az aks nodepool scale \
  --resource-group <resource-group> \
  --cluster-name <cluster-name> \
  --name <nodepool-name> \
  --node-count 5
```

### Upgrade Node Pool
```bash
az aks nodepool upgrade \
  --resource-group <resource-group> \
  --cluster-name <cluster-name> \
  --name <nodepool-name> \
  --kubernetes-version <version>
```

---

## 📊 Monitoring & Logs

### Enable Monitoring Add-on
```bash
az aks enable-addons \
  --resource-group <resource-group> \
  --name <cluster-name> \
  --addons monitoring
```

### View Logs Using Azure Monitor
Navigate to Azure Portal → Monitor → Logs → Select AKS workspace.

---

## 🔄 Upgrades & Versions

### View Available Kubernetes Versions
```bash
az aks get-versions \
  --location <region> \
  --output table
```

### Upgrade Cluster Control Plane
```bash
az aks upgrade \
  --resource-group <resource-group> \
  --name <cluster-name> \
  --kubernetes-version <version> \
  --yes
```

---

## 🧪 Useful `kubectl` Commands with AKS

### List Nodes
```bash
kubectl get nodes
```

### Get Pods in All Namespaces
```bash
kubectl get pods -A
```

### Describe a Pod
```bash
kubectl describe pod <pod-name> -n <namespace>
```

### View Events
```bash
kubectl get events -A --sort-by='.metadata.creationTimestamp'
```

---

## ✅ Best Practices for Interview

- Always mention **`az aks get-credentials`** as the first step to interact with the cluster.
- Explain the difference between **admin** and **user** credentials.
- Know how to **scale**, **upgrade**, and **secure** the cluster.
- Highlight Azure-native integrations like **Azure Monitor**, **Azure Policy**, and **Azure AD**.

---

## 📎 References

- [AKS Documentation](https://learn.microsoft.com/en-us/azure/aks/)
- [Azure CLI AKS Commands](https://learn.microsoft.com/en-us/cli/azure/aks)

---
