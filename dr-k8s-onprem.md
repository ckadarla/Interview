Setting up **Disaster Recovery (DR)** for an **on-premises Kubernetes (K8s)** cluster involves planning for high availability, data protection, and rapid recovery in the event of failures — such as hardware issues, natural disasters, or accidental deletions.

Below is a **comprehensive DR setup guide** tailored for **on-prem Kubernetes clusters**:

---

## 🛡️ 1. **Disaster Recovery Objectives**

Before implementation, define:

* **RTO (Recovery Time Objective)**: How quickly you must recover.
* **RPO (Recovery Point Objective)**: How much data you can afford to lose.

---

## 🏗️ 2. **DR Strategy Components**

### A. **Kubernetes Cluster Backup**

1. **Etcd Backup**

   * Etcd holds cluster state (pods, deployments, secrets, etc.).
   * Backup etcd regularly.

   ```bash
   ETCDCTL_API=3 etcdctl snapshot save /backup/etcd-snapshot.db \
     --endpoints=https://127.0.0.1:2379 \
     --cacert=/etc/kubernetes/pki/etcd/ca.crt \
     --cert=/etc/kubernetes/pki/etcd/server.crt \
     --key=/etc/kubernetes/pki/etcd/server.key
   ```

2. **Cluster Manifests Backup**

   * Store all `YAML` manifests (Deployments, Services, ConfigMaps, etc.) in Git.
   * Use GitOps (ArgoCD or FluxCD) for managing cluster state.

3. **Cluster Configuration**

   * Backup kubeconfig, manifests, certificates, admission controllers, etc.

---

### B. **Persistent Volume (PV) Backup**

* Back up the actual application data stored in:

  * NFS, Ceph, GlusterFS, or local disks.
* Use tools like:

  * **Velero** with Restic or native snapshots
  * **Kasten K10**, **Trilio**, or **OpenEBS cStor backup**

---

### C. **Application-Level Backup**

For apps like PostgreSQL, MongoDB, Redis:

* Use app-native backup solutions:

  * pg\_dump / pg\_basebackup
  * mongodump
  * redis-cli --rdb

Automate backups and store them offsite.

---

## 🔁 3. **Cluster Replication or Cold Standby**

### Option 1: **Cold Standby Cluster (Most Common for On-Prem)**

* Setup a secondary cluster in a different physical location or DC.
* Backup etcd and persistent volumes regularly.
* Restore them to cold cluster when disaster occurs.

### Option 2: **Active-Passive**

* Primary runs workloads.
* Secondary kept in sync (e.g., rsync, DRBD, object replication).
* Only activated when primary fails.

### Option 3: **Active-Active** (complex for on-prem)

* Requires multi-master, cross-site clustering.
* Needs reliable low-latency connectivity.
* Possible with solutions like **Rancher**, **KubeFed**, **Kubemc**, or **Crossplane**.

---

## 🔁 4. **Automation & Tooling**

| Task                | Tool                                    |
| ------------------- | --------------------------------------- |
| Etcd Backup/Restore | `etcdctl`, K8s scripts                  |
| Resource Backup     | `Velero`, `Stash by AppsCode`           |
| GitOps Backup Infra | `FluxCD`, `ArgoCD`                      |
| Volume Backup       | `Velero`, `Kasten K10`, `Trilio`        |
| Monitoring & Alerts | `Prometheus`, `Grafana`, `Alertmanager` |
| Secret Management   | `Vault`, `Sealed Secrets`               |

---

## ☁️ 5. **Offsite Storage (Critical for DR)**

Ensure backups are sent to offsite/cloud storage:

* S3-compatible storage (MinIO, Ceph, AWS S3)
* Tape or disk backup systems
* Cloud archive (AWS Glacier, Azure Archive)

---

## 🧪 6. **Regular Testing**

* Simulate DR scenarios quarterly.
* Document restore procedures.
* Validate:

  * Etcd restore
  * PV restore
  * Full cluster recovery
  * Application availability

---

## 🔐 7. **Security Considerations**

* Encrypt all backups.
* Protect etcd snapshots (contain secrets).
* Secure transport (TLS) for offsite transfers.
* Use RBAC and audit logs to prevent unauthorized actions.

---

## 📋 Sample DR Runbook Steps

1. **Detect failure** – Alert via Prometheus/Alertmanager.
2. **Switch DNS / ingress to DR site**
3. **Provision new cluster from backup**
4. **Restore etcd snapshot or apply manifests from Git**
5. **Restore persistent volumes (Velero/Kasten)**
6. **Validate application health**
7. **Notify stakeholders**

---
Here's a **step-by-step procedure** to **restore etcd** in a Kubernetes cluster (typically used in on-prem DR scenarios):

---

# 🔁 **etcd Restore Procedure (Kubernetes DR)**

## 📌 Assumptions:

* You have a valid etcd snapshot file: `etcd-snapshot.db`
* You're restoring on a control plane node
* Etcd is running as a static pod (default for `kubeadm`-based setups)
* You are using etcd **v3**

---

## ✅ Step 1: Stop Existing etcd

> ⚠️ Required to prevent conflicts.

```bash
# If you're using systemd-managed kubelet
sudo systemctl stop kubelet

# Backup existing etcd data dir (important!)
sudo mv /var/lib/etcd /var/lib/etcd.bak
```

---

## ✅ Step 2: Restore the Snapshot

Run the following command **on the control plane node**:

```bash
ETCDCTL_API=3 etcdctl snapshot restore /path/to/etcd-snapshot.db \
  --data-dir=/var/lib/etcd \
  --name=<etcd-node-name> \
  --initial-cluster=<etcd-node-name>=https://127.0.0.1:2380 \
  --initial-cluster-token=etcd-cluster-1 \
  --initial-advertise-peer-urls=https://127.0.0.1:2380
```

> Replace `<etcd-node-name>` with the name from your original etcd static pod YAML (usually found in `/etc/kubernetes/manifests/etcd.yaml`)

---

## ✅ Step 3: Validate Restored Data Directory

Check that `/var/lib/etcd/member` exists and has files inside.

---

## ✅ Step 4: Restart Kubernetes Components

```bash
sudo systemctl start kubelet
```

This will re-run etcd as a static pod via the manifest `/etc/kubernetes/manifests/etcd.yaml`.

---

## ✅ Step 5: Validate etcd and Kubernetes Health

### Check etcd pod:

```bash
kubectl get pods -n kube-system -l component=etcd
```

### Check etcd health:

```bash
ETCDCTL_API=3 etcdctl endpoint health \
  --endpoints=https://127.0.0.1:2379 \
  --cacert=/etc/kubernetes/pki/etcd/ca.crt \
  --cert=/etc/kubernetes/pki/etcd/server.crt \
  --key=/etc/kubernetes/pki/etcd/server.key
```

### Check cluster:

```bash
kubectl get nodes
kubectl get pods -A
```

---

## 🧪 Optional: If the restore is to a different node or cluster

You may need to:

* Update the etcd static pod manifest (`/etc/kubernetes/manifests/etcd.yaml`)
* Adjust certs and IPs accordingly
* Reconfigure kube-apiserver to connect to new etcd

---

## 💡 Tips

* Always automate snapshot + copy to offsite using cron + `etcdctl snapshot save`.
* Store the etcd snapshot alongside cluster certificates and kubeconfig.
* Test restore quarterly!

---


Here's a comprehensive guide for setting up **Disaster Recovery (DR)** for **Kubernetes clusters on AWS and Azure**, covering strategies, tools, and key steps specific to each cloud platform.

---

# ☁️ **Kubernetes DR Strategy on AWS & Azure**

## 🔥 **Core DR Goals**

| Objective | Definition                                                                                          |
| --------- | --------------------------------------------------------------------------------------------------- |
| **RTO**   | Time to restore full functionality                                                                  |
| **RPO**   | Acceptable data loss (e.g., 15 mins)                                                                |
| **Goal**  | Quickly restore cluster + workloads + persistent data in a different region or account/subscription |

---

# 🧩 **Common DR Architecture Components**

| Component          | AWS                               | Azure                          |
| ------------------ | --------------------------------- | ------------------------------ |
| Managed Kubernetes | EKS                               | AKS                            |
| Object Storage     | S3                                | Azure Blob Storage             |
| Workload Backup    | Velero, Kasten K10, Trilio        | Velero, Azure Backup, Kasten   |
| GitOps Tool        | ArgoCD / FluxCD                   | ArgoCD / FluxCD                |
| PV Snapshots       | EBS Snapshots                     | Azure Disk Snapshots           |
| Disaster Site      | Another Region or Another Account | Another Region or Subscription |

---

## ✅ **1. DR Setup on AWS (EKS)**

### 🛠️ DR Strategy:

* **Primary EKS** in Region A
* **DR EKS cluster** in Region B (hot, warm, or cold)
* Use **Velero** for backup/restore of:

  * Kubernetes objects (Deployments, Services, etc.)
  * EBS volumes
* Use **S3** as the backup location (with cross-region replication)

### 📦 Tools:

* Velero with AWS plugin
* EBS Snapshots
* AWS S3 with cross-region replication
* KMS (for encryption)

### 🔁 Key Steps:

1. **Install Velero** with AWS plugin:

   ```bash
   velero install \
     --provider aws \
     --plugins velero/velero-plugin-for-aws \
     --bucket <s3-bucket-name> \
     --backup-location-config region=<region> \
     --snapshot-location-config region=<region> \
     --secret-file ./credentials-velero
   ```

2. **Enable cross-region S3 replication**:

   * Configure bucket policy and replication rules

3. **Schedule backups** (every X mins):

   ```bash
   velero create schedule daily-backup --schedule "0 2 * * *"
   ```

4. **Restore in DR region**:

   * Deploy DR EKS cluster via Terraform or EKS Blueprints
   * Install Velero pointing to replicated S3 bucket
   * Run:

     ```bash
     velero restore create --from-backup <backup-name>
     ```

5. **Restore stateful apps** with volume snapshots:

   * EBS volumes are snapshot-backed
   * Velero restores PVC + associated volume from snapshot

---

## ✅ **2. DR Setup on Azure (AKS)**

### 🛠️ DR Strategy:

* **Primary AKS** in Region A
* **DR AKS** in Region B
* Use **Velero** with Azure plugin + Azure Blob storage
* Replicate backups via **Azure Blob geo-redundancy**
* Restore PVs from **Azure Managed Disk snapshots**

### 📦 Tools:

* Velero with Azure plugin
* Azure Blob Storage (RA-GRS)
* Azure Disk Snapshots
* Azure Key Vault (secrets)
* Azure Resource Manager (ARM) or Bicep (infra restore)

### 🔁 Key Steps:

1. **Create Blob Storage for backup**

   ```bash
   az storage account create --name velero<suffix> --resource-group <rg> \
     --sku Standard_GRS --encryption-services blob
   ```

2. **Install Velero** with Azure plugin:

   ```bash
   velero install \
     --provider azure \
     --plugins velero/velero-plugin-for-microsoft-azure \
     --bucket <container-name> \
     --secret-file ./credentials-velero \
     --backup-location-config resourceGroup=<rg>,storageAccount=<account>,subscriptionId=<sub-id>
   ```

3. **Enable Azure Disk snapshot backup** (Velero uses CRDs to back up PVs)

4. **Automate AKS cluster restore**

   * Use ARM or Bicep to recreate AKS cluster + infra
   * Re-deploy Velero, point to storage
   * Restore backup:

     ```bash
     velero restore create --from-backup <backup-name>
     ```

---

## 🧠 Design Options (for Both AWS & Azure)

| Strategy                        | Description                                                              |
| ------------------------------- | ------------------------------------------------------------------------ |
| **Hot DR**                      | Secondary cluster always running, data replicated                        |
| **Warm DR**                     | Cluster infra pre-created, workloads restored during failover            |
| **Cold DR**                     | Infra provisioned only during a disaster                                 |
| **Multi-region active-passive** | Traffic routed via DNS/GSLB (e.g., AWS Route 53 / Azure Traffic Manager) |

---

## 🚨 Key Considerations

| Area                      | What to Think About                                   |
| ------------------------- | ----------------------------------------------------- |
| **Secrets**               | Back up Vault / Azure Key Vault / Kubernetes Secrets  |
| **DNS Failover**          | Use Route 53 (AWS) or Azure Traffic Manager           |
| **Ingress/Load Balancer** | Recreate external LB or use static IP with Front Door |
| **Cluster Identity**      | Match service principal / IAM roles                   |
| **Compliance**            | Secure snapshots and backups (KMS/Key Vault)          |
| **Test DR**               | Simulate restore every 3-6 months                     |

---

## 🧪 DR Runbook (Generic Cloud-based)

1. **Declare Disaster**
2. **Provision AKS/EKS in DR region (Terraform/ARM)**
3. **Restore K8s resources using Velero**
4. **Restore persistent volumes (snapshots or external DB)**
5. **Recreate Ingress, DNS, Certificates**
6. **Validate application health**
7. **Notify stakeholders & switch traffic**

---


