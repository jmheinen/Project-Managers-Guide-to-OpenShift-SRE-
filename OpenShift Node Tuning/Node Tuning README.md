# OpenShift Node Tuning Configuration

This directory contains the configurations for tuning node-level behavior on OpenShift Container Platform (OCP) using the `KubeletConfig` Custom Resource. 

In high-density enterprise environments, default node behaviors can easily lead to cascading failures. If a single node experiences sudden memory or disk saturation, the Linux kernel's Out-Of-Memory (OOM) killer or raw disk starvation can freeze the node entirely, causing ungraceful workloads drops and stalling the control plane. This profile establishes a proactive, multi-layered defense to keep worker nodes healthy and responsive.

---

## 🏗️ Operational Strategy

Instead of letting a node run completely out of resources and crash, this configuration programs the `kubelet` process to actively manage resource scarcity using a two-tiered threshold system:

1. **Soft Evictions:** Act as a warning phase. When a node starts running tight on resources, it enters a soft threshold. Pods are given a grace period to gracefully drain connections, save state, and schedule onto alternative nodes.
2. **Hard Evictions:** Act as an immediate circuit breaker. If resources drop past critical limits, the Kubelet immediately terminates pods without a grace period to safeguard the host operating system (Red Hat Enterprise Linux CoreOS).