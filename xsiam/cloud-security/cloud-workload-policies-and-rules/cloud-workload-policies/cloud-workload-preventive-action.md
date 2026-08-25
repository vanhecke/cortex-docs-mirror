---
description: >-
  Learn how Cortex XSIAM cloud workload preventive actions block Kubernetes
  deployments and fail CI pipelines.
---

# Cloud workload preventive action

Some Cloud Workload policies provide a **Prevent and Create an Issue** action that enforces compliance during deployments.

### **Prevention action for runtime stage policies**

The Prevent action at Runtime applies only to Kubernetes Workload Images assets.

When a Kubernetes Workload image violates a policy, the Kubernetes Admission Controller (on clusters where the KSPM Connector is deployed and Admission Control is enabled) can block it from being admitted to the cluster.

For all other asset types within the policy scope, no runtime prevention will occur. Instead, the violation will result in an Issue being created.

### **Prerequisites**

Ensure that your cluster has the Posture Management (KSPM) Connector deployed with the Admission Controller functionality enabled.

You can manage these deployments from the Kubernetes Connectivity Management page.

To access the [Kubernetes Connectivity Management](../../../configure-cortex-xsiam/cortex-xsiam-data-sources/administration-and-troubleshooting), navigate to the following URL in your tenant environment: https://\[TENANT-ADDRESS]/cwp/k8s-management.

### **Important considerations**

* **Recommended Approach**: Begin with the **Create an Issue** action to validate results before selecting **Prevent and Create an Issue**. This helps prevent potential disruptions to your applications or development workflows.
* **Impact on New Deployments**: The **Prevent and Create an Issue** action affects only new or future deployments that meet the prevention criteria. It does not impact cloud workload assets that are already deployed.

### **Prevention action for CI stage Policies**

Prevention actions in the CI stage triggers a pipeline failure by returning an exit code of 2 in the CI tool.
