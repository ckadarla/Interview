Here’s a focused set of **Kubernetes (K8s), Google Kubernetes Engine (GKE), and Google Cloud Platform (GCP)** **troubleshooting interview questions and answers** tailored for mid to senior-level roles. These are practical, scenario-based, and designed to help you showcase your problem-solving skills during interviews.

---

### 🔧 **Kubernetes Troubleshooting Questions**

---

**1. Q: A pod is stuck in `Pending` state. How do you troubleshoot it?**

**A:**

* Run `kubectl describe pod <pod-name>` to check:

  * Events (e.g., `0/3 nodes available: insufficient memory`)
  * Scheduling issues (e.g., affinity, taints/tolerations)
* Check if there's a `ResourceQuota` or `LimitRange` blocking scheduling.
* Check if there are available nodes: `kubectl get nodes`.
* Inspect scheduler logs if needed.

---

**2. Q: How do you troubleshoot a `CrashLoopBackOff` error?**

**A:**

* Check logs: `kubectl logs <pod-name> --previous` for crash reasons.
* Validate container `command` or `entrypoint`.
* Check liveness/readiness probes – failing probes can restart containers.
* Ensure dependent services (e.g., DB) are up.
* Resource limits: OOMKilled events.

---

**3. Q: How do you debug failing DNS resolution inside a pod?**

**A:**

* Check CoreDNS status: `kubectl get pods -n kube-system -l k8s-app=kube-dns`.
* Use busybox or dnsutils to test DNS from within a pod:

  ```bash
  kubectl exec -it <pod> -- nslookup <service-name>
  ```
* Verify `resolv.conf` inside pod: `cat /etc/resolv.conf`.
* Validate CoreDNS config: `kubectl -n kube-system edit configmap coredns`.

---

**4. Q: You deployed a service but it’s not accessible via ClusterIP. What do you check?**

**A:**

* Verify endpoints: `kubectl get endpoints <svc-name>` – must not be empty.
* Check target pod labels match service `selector`.
* Use `kubectl exec` to curl service IP from another pod.
* Ensure network policies aren’t blocking traffic.

---

**5. Q: How do you investigate when pods can’t pull images?**

**A:**

* Look at event logs: `kubectl describe pod <pod-name>`.
* Check for:

  * Invalid image name
  * Missing `imagePullSecrets`
  * Permissions issue (e.g., private registry)
  * Network/DNS resolution issue to registry

---

### ☸️ **GKE-Specific Troubleshooting Questions**

---

**6. Q: Your GKE cluster nodes are not joining the cluster. What do you do?**

**A:**

* Use Cloud Console or `gcloud container clusters describe` to check cluster health.
* Check firewall rules (port 10250, 443) and routes.
* Check node service account IAM permissions (e.g., `roles/container.nodeServiceAgent`).
* Look at serial console logs of the VM.

---

**7. Q: How do you troubleshoot GKE node pool autoscaling issues?**

**A:**

* Check autoscaler events: `gcloud container clusters describe <cluster>`.
* Confirm pods are unschedulable: `kubectl describe pod <pod>`.
* Review CPU/memory requests – too large can block scheduling.
* Check if the node pool has reached max size.

---

**8. Q: You updated a deployment, but rollout is stuck. What do you check?**

**A:**

* Run `kubectl rollout status deployment/<name>`.
* Check pod health: liveness/readiness probes, logs.
* Look at `kubectl describe deployment` for conditions.
* Ensure there are enough resources for new pods to schedule.

---

**9. Q: How do you troubleshoot network connectivity issues between GKE pods in different namespaces?**

**A:**

* Ensure `NetworkPolicy` isn’t blocking traffic.
* Use `kubectl exec` to test connectivity with `ping` or `curl`.
* Validate correct service or DNS name.
* Check if GKE cluster has VPC-native (alias IPs) enabled or not.

---

**10. Q: How to debug persistent volume claim (PVC) mounting failure in GKE?**

**A:**

* Check PVC and PV status: `kubectl get pvc,pv`.
* Describe PVC for events: `kubectl describe pvc <name>`.
* Verify StorageClass and underlying disk availability.
* Check node IAM permissions for Compute Engine APIs.
* Ensure the disk is in the same zone as the node.

---

### ☁️ **GCP Infrastructure Troubleshooting Questions**

---

**11. Q: A GKE workload can't access a GCP service (e.g., Cloud Storage). What do you check?**

**A:**

* Ensure correct Workload Identity binding or node service account has necessary roles (e.g., `roles/storage.objectViewer`).
* Check `gcloud auth list` or service account token inside pod.
* Validate IAM policy bindings on the resource.
* Check for any VPC firewall rules blocking egress.

---

**12. Q: You can't SSH into a GKE node. What are your options?**

**A:**

* Use Cloud Console serial port logs to debug.
* Use "Connect to serial console" or reset the SSH keys.
* Check if the node is in a private GKE cluster – use a bastion host or IAP tunnel.
* Use `gcloud compute ssh --tunnel-through-iap`.

---

**13. Q: GKE ingress is not routing traffic. How do you troubleshoot?**

**A:**

* Check ingress status: `kubectl describe ingress`.
* Validate backend service and pod health.
* Ensure NodePorts are open in firewall rules.
* Check load balancer status in Cloud Console.
* Confirm DNS and certificate configurations.

---

**14. Q: How do you debug GCP firewall rules impacting GKE workloads?**

**A:**

* Use `gcloud compute firewall-rules list`.
* Ensure rules allow ingress to NodePort range (30000-32767).
* Validate source IP ranges, protocols, and tags.
* Use VPC flow logs to inspect blocked traffic.

---

**15. Q: GKE pod logs are missing in Cloud Logging. How do you troubleshoot?**

**A:**

* Confirm Logging is enabled in cluster.
* Check `fluentbit`/`logging-agent` DaemonSet status.
* Inspect logging agent logs in the node.
* Verify IAM permissions: service account needs `logging.logWriter`.
* Check for disk pressure or resource issues on nodes.

---

Great! Here’s **Part 2** with more **Kubernetes, GKE, and GCP troubleshooting interview Q\&A**, focusing on **advanced real-world issues**, perfect for **SRE/DevOps/Platform Engineer** roles.

---

## 🔧 **Advanced Kubernetes Troubleshooting Questions**

---

**16. Q: What steps do you follow if kubelet on a node is not registering with the API server?**

**A:**

* Check kubelet logs: `journalctl -u kubelet` or `/var/log/kubelet.log`.
* Verify node has correct cloud metadata and configuration.
* Validate the node certificate is valid and not expired.
* Ensure network/DNS reachability to the control plane.
* Restart kubelet and container runtime if needed.

---

**17. Q: A pod is in `Terminating` state for a long time. What could be wrong?**

**A:**

* Likely causes:

  * Finalizers not removed
  * Pod with long-running shutdown hook or hanging process
  * PV unmount stuck
* Check `kubectl describe pod` and look for finalizers.
* Use `kubectl patch pod <pod> -p '{"metadata":{"finalizers":[]}}' --type=merge` (last resort).
* Check node logs for unmounting issues.

---

**18. Q: How would you troubleshoot a Kubernetes Job that never completes?**

**A:**

* Check `kubectl get jobs` and describe the job.
* Inspect pod logs to identify logic or dependency issues.
* Ensure retries/backoff limits are set appropriately.
* Validate resources and network policies.
* Use `kubectl get events` to look for scheduling or crash errors.

---

**19. Q: You suspect a memory leak in one of your microservices. How do you approach it?**

**A:**

* Observe container memory usage via:

  * `kubectl top pod` or metrics from Prometheus/Grafana
* Check for `OOMKilled` status in pod events.
* Use `kubectl logs` and `heap profiler` if built in.
* Add resource limits and configure liveness probes to restart when leaking.

---

**20. Q: How do you debug if service discovery (ClusterIP, DNS) fails intermittently?**

**A:**

* Ensure CoreDNS has enough CPU/memory and isn't throttling.
* Check for high DNS QPS load or race conditions.
* Inspect `CoreDNS` logs: `kubectl logs <dns-pod> -n kube-system`.
* Use a sidecar like `dnsmasq` to offload frequent lookups.

---

## ☸️ **Advanced GKE Troubleshooting Questions**

---

**21. Q: How do you diagnose degraded GKE node performance?**

**A:**

* Check node logs and metrics (CPU throttling, disk IO wait, memory pressure).
* Run `kubectl describe node` and `kubectl top node`.
* Use GCP Monitoring (Ops Agent) for system-level metrics.
* Look for noisy neighbor pods or daemonsets consuming excess resources.

---

**22. Q: In a private GKE cluster, the control plane can't reach workloads. What do you check?**

**A:**

* Verify control plane authorized networks.
* Ensure GKE Master Authorized Networks and firewall rules are in place.
* Check if Cloud NAT is configured for outbound access.
* Use `gcloud container clusters describe` to verify IP blocks.

---

**23. Q: GKE workload identity is not attaching correctly. How do you debug it?**

**A:**

* Ensure GKE metadata server is accessible in pods.
* Check annotations on the service account:

  ```yaml
  iam.gke.io/gcp-service-account: <gcp-sa>@<project>.iam.gserviceaccount.com
  ```
* Validate IAM policy bindings: `gcloud projects get-iam-policy`.
* Ensure no conflicting Kubernetes secrets or legacy service accounts.

---

**24. Q: Ingress traffic is failing randomly. How do you approach it?**

**A:**

* Validate health checks: `gcloud compute health-checks list`.
* Check backend service logs.
* Confirm GKE nodes aren't overloaded.
* Check `kubectl describe ingress` and inspect backend pod readiness probes.

---

**25. Q: Pods across namespaces can’t communicate. There are no NetworkPolicies. What now?**

**A:**

* Confirm network plugin (CNI) is working (e.g., Calico, Cilium).
* Check for misconfigured custom routing tables or firewall rules.
* Validate that no node-specific kube-proxy or iptables rules are blocking.

---

## ☁️ **Advanced GCP Infrastructure Troubleshooting**

---

**26. Q: VPC peering is established, but traffic is not flowing. What do you check?**

**A:**

* Check that both sides have **export/import custom routes and subnetworks** enabled.
* Validate firewall rules allow necessary traffic.
* Ensure overlapping IP ranges are not configured.
* Use `traceroute` and VPC flow logs.

---

**27. Q: How do you troubleshoot intermittent Cloud NAT failures affecting GKE egress?**

**A:**

* Check NAT gateway logs for dropped connections or SNAT exhaustion.
* Validate NAT config and scaling rules (e.g., minimum ports per VM).
* Ensure all subnet routes are covered under NAT config.
* Monitor SNAT port usage with `Cloud Monitoring`.

---

**28. Q: GKE node pool creation is failing. How do you debug?**

**A:**

* Review error in `gcloud container node-pools create`.
* Check project-level quotas (CPU, IPs, disks).
* Validate IAM permissions for the cluster service account.
* Inspect the Compute Engine API logs for failures.

---

**29. Q: A GKE node is NotReady. What steps do you take?**

**A:**

* Describe node: `kubectl describe node <node-name>`.
* Common causes:

  * Disk pressure, memory pressure
  * kubelet or containerd/crio failure
  * Cloud API access failure
* Restart node agent or reimage if needed.

---

**30. Q: How do you trace slow application performance in GKE with Cloud tools?**

**A:**

* Use **Cloud Profiler** for CPU/memory bottlenecks.
* Use **Cloud Trace** to identify latency between services.
* Use **Cloud Logging** with filters for latency logs.
* Check Prometheus/Grafana or GKE Dashboard for pod metrics.

---

Absolutely! Here's **Part 3** of **Kubernetes, GKE, and GCP troubleshooting Q\&A**, featuring more **expert-level, real-world issues** for senior DevOps/SRE/Platform interviews:

---

## 🔍 **Kubernetes Troubleshooting – Continued**

---

**31. Q: You get an error: `FailedScheduling: 0/5 nodes are available: insufficient cpu`. But the nodes seem underutilized. What’s happening?**

**A:**

* Possible issues:

  * Pods have high CPU requests, not actual usage.
  * Resource fragmentation: requests don't fit due to node constraints.
  * DaemonSets, taints, or affinity rules restrict node selection.
* Use:

  ```bash
  kubectl describe pod <pod-name>
  kubectl get nodes -o custom-columns=NAME:.metadata.name,CPU:.status.allocatable.cpu
  ```

---

**32. Q: How do you investigate when `kubectl exec` fails with `error dialing backend`?**

**A:**

* Check if the `kube-apiserver` can reach the node (firewall issue?).
* Validate the API server’s `kubelet-client-certificate`.
* If using `konnectivity-agent` (GKE): ensure it's healthy.
* Logs:

  ```bash
  kubectl logs -n kube-system konnectivity-agent-*
  ```

---

**33. Q: A StatefulSet pod fails to attach to its PVC. What are your steps?**

**A:**

* Check `kubectl describe pvc` for `FailedAttachVolume`.
* Validate the PV is still bound and storage class is available.
* Inspect disk attachment in GCP (if using PD).
* Delete the pod to retry attachment.

---

**34. Q: Why might `kubectl get logs` not show logs for a running pod?**

**A:**

* Container restarted: check `kubectl logs -p`.
* Logging agent (e.g., Fluentbit) not forwarding logs.
* Pod uses sidecar container: specify `-c <container-name>`.
* Filesystem issues preventing log writing to `/var/log`.

---

**35. Q: Your K8s control plane is slow or unresponsive. What do you do?**

**A:**

* Check `etcd` health:

  ```bash
  ETCDCTL_API=3 etcdctl endpoint health
  ```
* Look for high API server load:

  ```bash
  kubectl get --raw /metrics | grep apiserver_request_duration_seconds
  ```
* Excessive watch clients or custom controllers can cause overload.
* Audit logs for spike in traffic from external systems.

---

## ☸️ **GKE-Specific Deep Troubleshooting**

---

**36. Q: You notice pods are stuck in `ContainerCreating`. What do you investigate?**

**A:**

* Volume attachment (PVC) issues.
* Image pull delays or errors:

  ```bash
  kubectl describe pod <pod-name> | grep -A 10 Events
  ```
* DNS resolution failure in node init.
* Container runtime issues on node (e.g., containerd crash).

---

**37. Q: GKE autoscaler isn't scaling up when pods are pending. Why?**

**A:**

* Pod resource requests too high for any node template.
* Taints or affinity rules prevent scheduling.
* Check cluster autoscaler logs:

  ```bash
  kubectl logs -n kube-system deployment/cluster-autoscaler
  ```
* Regional GKE clusters sometimes delay node provisioning.

---

**38. Q: How do you recover a GKE node that is unreachable but not deleted automatically?**

**A:**

* Use:

  ```bash
  gcloud compute instances reset <node-name>
  ```
* If stuck, cordon and drain:

  ```bash
  kubectl cordon <node>
  kubectl drain <node> --ignore-daemonsets --delete-emptydir-data
  ```
* Check if auto-repair is enabled: `gcloud container clusters describe`.

---

**39. Q: You need to force a pod restart in GKE without deleting the pod manually. How?**

**A:**

* Modify an annotation:

  ```bash
  kubectl patch deployment <dep> -p \
  "{\"spec\":{\"template\":{\"metadata\":{\"annotations\":{\"date\":\"$(date +%s)\"}}}}}"
  ```

---

**40. Q: How can you identify which GKE workloads are consuming the most egress traffic?**

**A:**

* Use **VPC flow logs** with filters for egress traffic.
* In GKE, use **Cloud Monitoring dashboards** or **Prometheus metrics**.
* Install `kubecost` or use GKE usage metering if enabled.
* Look at:

  ```bash
  iptables -L -v -n  # on node
  ```

---

## ☁️ **GCP Infrastructure Troubleshooting – Continued**

---

**41. Q: A Cloud Function triggered by Pub/Sub isn’t firing. How do you troubleshoot?**

**A:**

* Confirm Pub/Sub topic exists and has messages.
* Check Cloud Function logs.
* Inspect permissions: ensure Pub/Sub service account can invoke the function.
* Validate trigger binding in Cloud Console or `gcloud functions describe`.

---

**42. Q: You cannot SSH into a GCE VM. What are the typical root causes?**

**A:**

* SSH keys not propagated (check metadata).
* Firewall rule blocking port 22.
* OS Login is enabled but IAM permissions missing.
* Disk corruption or broken startup scripts.

---

**43. Q: Cloud Run is returning 503s intermittently. How do you debug it?**

**A:**

* Look for cold start latency (review logs).
* Ensure concurrency settings are optimal.
* Validate backend readiness probes.
* Look into Cloud Run metrics (request count, latency, container crash count).

---

**44. Q: How do you trace a failed `gcloud deploy` command?**

**A:**

* Add `--verbosity debug` to the command.
* Use `gcloud builds log <build-id>` to see Build step output.
* Validate service account permissions for Cloud Build.
* Inspect IAM roles and Artifact Registry bindings.

---

**45. Q: Cloud Storage bucket is returning 403 for a service account. How do you debug it?**

**A:**

* Ensure the correct IAM role (e.g., Storage Object Viewer) is bound.
* Check organization policies for bucket restrictions.
* Use:

  ```bash
  gcloud storage buckets get-iam-policy gs://<bucket-name>
  ```

---
Great! Here's **Part 4** of the **Kubernetes, GKE, and GCP troubleshooting interview Q\&A**, focusing on **real-world production issues**, **platform-level debugging**, and **deep dive concepts**.

---

## ☸️ **Kubernetes Advanced Troubleshooting**

---

**46. Q: How do you debug a crashlooping container when `kubectl logs` shows nothing?**

**A:**

* Check `kubectl describe pod` for events like `OOMKilled`, `CrashLoopBackOff`.
* Run `kubectl logs <pod> -p` for previous container logs.
* If container exits too fast, use an `initContainer` or modify entrypoint to `sleep`:

  ```yaml
  command: ["sleep"]
  args: ["3600"]
  ```

---

**47. Q: What causes `DNS resolution failed` errors inside Kubernetes pods?**

**A:**

* kube-dns/CoreDNS pods may be:

  * Crashlooping or under pressure.
  * Blocked by network policy.
* Check:

  ```bash
  kubectl get pods -n kube-system -l k8s-app=kube-dns
  kubectl exec <pod> -- nslookup kubernetes.default
  ```

---

**48. Q: Your services are intermittently failing inside the cluster. How do you verify if it's a network issue?**

**A:**

* Deploy a debug pod (`nicolaka/netshoot`) and run:

  ```bash
  dig <service>
  curl <pod-ip>:<port>
  traceroute, tcpdump
  ```
* Validate `kube-proxy` and CNI logs for dropped connections.

---

**49. Q: Why would a Kubernetes Job or CronJob never complete or repeat execution?**

**A:**

* Image pull error, wrong entrypoint/command.
* `backoffLimit` too low or not defined.
* Schedule conflict or overlap (for CronJobs).
* Use:

  ```bash
  kubectl get jobs
  kubectl describe cronjob <job-name>
  ```

---

**50. Q: A deployment is stuck in rollout. What steps do you follow?**

**A:**

* Use:

  ```bash
  kubectl rollout status deployment <name>
  kubectl describe deployment <name>
  ```
* Common causes:

  * Readiness probe failure.
  * Resource constraints.
  * Missing image tag/version or failed pull.
* Use `kubectl get rs` to see new ReplicaSet behavior.

---

## ☸️ **GKE Deep Dive Issues**

---

**51. Q: Your new GKE node pool isn’t registering with the cluster. What do you check?**

**A:**

* Check GKE node status:

  ```bash
  gcloud container clusters get-credentials <cluster>
  kubectl get nodes
  ```
* Look at instance logs (serial port logs via Cloud Console).
* Check service account roles: `roles/container.nodeServiceAccount`.
* Validate VPC firewall rules: allow port 10250.

---

**52. Q: GKE Workload Identity is enabled, but pods can’t access GCP resources. How do you fix it?**

**A:**

* Steps:

  * Check annotation:

    ```yaml
    iam.gke.io/gcp-service-account: "<gcp-sa>@<project>.iam.gserviceaccount.com"
    ```
  * Validate binding:

    ```bash
    gcloud iam service-accounts add-iam-policy-binding \
      --role roles/iam.workloadIdentityUser \
      --member "serviceAccount:<PROJECT>.svc.id.goog[<namespace>/<k8s-sa>]" \
      <gcp-sa>@<project>.iam.gserviceaccount.com
    ```
  * Confirm GKE metadata API access isn't blocked.

---

**53. Q: Horizontal Pod Autoscaler (HPA) isn’t scaling up. Where do you start?**

**A:**

* Check if metrics are available:

  ```bash
  kubectl get --raw /apis/custom.metrics.k8s.io
  ```
* Inspect pod CPU/memory usage.
* Look at HPA events:

  ```bash
  kubectl describe hpa
  ```
* Ensure `metrics-server` is deployed and healthy.

---

**54. Q: You upgraded GKE and now workloads are failing with Istio or Linkerd. What's likely?**

**A:**

* The control plane may be incompatible.
* Check if sidecar injection is failing:

  ```bash
  kubectl get pods -n istio-system
  ```
* Validate MutatingWebhookConfiguration rules.
* Recheck mTLS or `DestinationRule` configs.

---

**55. Q: How do you detect and fix a memory leak in a GKE application?**

**A:**

* Use `kubectl top pod` or Prometheus to monitor memory usage.
* Identify constant growth in memory over time.
* Add memory limits to prevent node exhaustion.
* Capture heap dumps and analyze in tooling like `VisualVM`, `heaptrack`.

---

## ☁️ **GCP Infrastructure Extended Issues**

---

**56. Q: Cloud NAT is enabled, but your private GKE cluster cannot access the internet. What do you check?**

**A:**

* Ensure route table includes default route (`0.0.0.0/0`) via Cloud NAT.
* Verify subnet region and NAT gateway region match.
* Check if firewall allows egress from source tags/ranges.
* Use:

  ```bash
  gcloud compute networks subnets describe <subnet-name>
  ```

---

**57. Q: BigQuery scheduled queries are failing silently. How do you debug them?**

**A:**

* Go to **BigQuery > Scheduled Queries**, check job history.
* Look at:

  * Dataset permissions.
  * Destination table quotas.
  * SQL errors or timeout issues.

---

**58. Q: Cloud Build pipeline fails with `permission denied` on Artifact Registry. What’s wrong?**

**A:**

* Confirm Cloud Build service account has:

  * `roles/artifactregistry.writer`
* Check if repo is regional and matches GKE/workload region.
* Validate Docker authentication:

  ```bash
  gcloud auth configure-docker <region>-docker.pkg.dev
  ```

---

**59. Q: IAM policy changes don’t reflect immediately. What’s the cause?**

**A:**

* IAM propagation delay (\~60 seconds in most cases).
* Inconsistent APIs or session caching.
* Use:

  ```bash
  gcloud projects get-iam-policy <project>
  ```

  and recheck credentials (use `gcloud auth list`).

---

**60. Q: VPC peering is set up but no traffic flows between two networks. How do you fix it?**

**A:**

* Ensure both peers have `export`/`import` custom routes enabled.
* Check firewall rules on both VPCs.
* Peering doesn’t support overlapping CIDR ranges.
* Confirm DNS resolution if `Private Google Access` is needed.

---

