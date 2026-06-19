---

## Deployment & GitOps Workflow

This configuration should be deployed via **Red Hat Advanced Cluster Management (RHACM)** or **ArgoCD (OpenShift GitOps)** to ensure continuous compliance.

### Manual Application (Break-Glass Scenario)
To apply this configuration directly to a specific MachineConfigPool (e.g., `worker`):

```bash
oc apply -f clusters/production/kubelet-custom-config.yaml


## When these thresholds are approached, the Kubelet flags the node with a PressureCondition (e.g., DiskPressure, MemoryPressure). Ensure your Prometheus rules alert on:

kube_node_status_condition{condition="MemoryPressure", status="true"}

kube_node_status_condition{condition="DiskPressure", status="true"}

