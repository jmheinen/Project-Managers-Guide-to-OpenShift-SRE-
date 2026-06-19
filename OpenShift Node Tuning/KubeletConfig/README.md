# OpenShift Kubelet Configuration for SRE Resilience

This repository manages custom `KubeletConfig` Custom Resources (CRs) for OpenShift Container Platform (OCP). In a large-scale enterprise environment, default Kubelet settings can leave nodes vulnerable to resource exhaustion, disk-fill cascades, and cascading failures. 

As Site Reliability Engineers (SREs), our goal is to maximize **Cluster MTTD (Mean Time to Detection)** and **MTTR (Mean Time to Resolution)** while enforcing node stability. This configuration implements proactive eviction thresholds, aggressive log rotation, and strict garbage collection to safeguard node health.

---

When a node runs out of resources, Kubernetes attempts to reclaim them. If it fails, the kernel's Out-Of-Memory (OOM) killer steps in, which can unpredictably terminate critical system processes or infrastructure pods. 

By tuning the `KubeletConfig`, we establish a two-tiered defensive perimeter:

1. **Soft Evictions:** A warning phase that alerts SRE monitoring (Prometheus/Alertmanager) and gives workloads a grace period to terminate gracefully or scale down.
2. **Hard Evictions:** An immediate, non-negotiable pod termination strategy to preserve the OS and underlying crypto/control-plane functions of the node.



