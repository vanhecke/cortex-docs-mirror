---
description: >-
  Learn more about the supported Kubernetes platform versions for the Kubernetes
  connector.
---

# Supported Kubernetes distributions

The following are the supported Kubernetes platform versions for the Kubernetes connector (Posture Management). The table shows the latest version that is supported. We support n-3 versions of each supported Kubernetes environment.

| Kubernetes environment | Notes                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| ---------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Managed clusters       | <ul><li><p>Amazon Elastic Kubernetes Service (EKS)</p><div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>Does not include EKS AutoMode.</p></div></li><li>Microsoft Azure Kubernetes Service (AKS)</li><li><p>Google Kubernetes Engine (GKE)</p><div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>Does not include Autopilot.</p></div></li></ul> |
| Managed OpenShift      | <p>Managed OpenShift clusters are supported:</p><ul><li>Red Hat OpenShift Container Platform (OCP)- Self-hosted: 4.21.8 (Kubernetes 1.34.5)</li><li>Red Hat OpenShift Container Platform (OCP)- ROSA (AWS): 4.20.15 (Kubernetes 1.33.5)</li><li>Red Hat OpenShift Container Platform (OCP)- ARO (Azure): 4.20.15 (Kubernetes 1.33.6)</li></ul>                                                                                                                                   |
| Self-Managed           | <p>We support every CNCF-certified Kubernetes solution. We've tested our solution on:</p><ul><li>Self-managed vanilla/on-premise Kubernetes clusters.</li><li>Self-managed OpenShift Kubernetes clusters.</li><li>Rancher Distributions (RKE and RKE2).</li></ul>                                                                                                                                                                                                                |

Refer to the [Kubernetes platforms supported](https://app.gitbook.com/s/fZ8QSMnkjnXpuOeuRcam/where-can-i-install-the-cortex-xdr-agent/kubernetes-platforms-supported) page for the latest versions.
