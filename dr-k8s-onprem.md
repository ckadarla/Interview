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


