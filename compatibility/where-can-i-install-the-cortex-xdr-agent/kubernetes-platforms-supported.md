# Kubernetes platforms supported

View the Kubernetes platforms that are supported with Cortex XDR agents.

### Supported Kubernetes platforms

This table shows the Kubernetes platform versions that have been compatibility tested. The table shows the latest version that has been tested. All versions that are not EOL, up to the latest version tested for compatibility in the table below are supported.

For installation instructions refer to Cortex XDR Agent for Linux → Install the Cortex XDR Agent for Kubernetes Hosts in the latest [Cortex XDR agent admin guide](broken-reference).

| Linux Kubernetes Platform                                                                     | Version                                                                                               |
| --------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| Unmanaged Kubernetes (k8s)                                                                    | 1.30                                                                                                  |
| Amazon Elastic Kubernetes Service (EKS)                                                       | 1.35                                                                                                  |
| <p> ↳ BottleRocket OS x86_64</p><p>  User mode agent only</p>                                 |                                                                                                       |
| <p> ↳ BottleRocket OS aarch64</p><p>  User mode agent only</p>                                |                                                                                                       |
| Microsoft Azure Kubernetes Service (AKS)                                                      | 1.35                                                                                                  |
|  ↳ CBL-mariner 2 x86\_64                                                                      |                                                                                                       |
| Google Kubernetes Engine (GKE)                                                                | 1.35                                                                                                  |
| <p> ↳ Google Container-Optimized OS (COS)<sup>*</sup> x86_64</p><p>  User mode agent only</p> |                                                                                                       |
|  ↳ Google Kubernetes Engine (GKE) Autopilot                                                   |                                                                                                       |
| Oracle Kubernetes Engine (OKE)                                                                | 1.33                                                                                                  |
| Red Hat Openshift Container Platform (OCP)                                                    | <p>4.18</p><p>4.19 in agent versions 9.1.1 and later</p><p>4.20 in agent versions 9.1.1 and later</p> |
| <p> ↳ RHCOS<sup>*</sup> x86_64</p><p>  User mode agent only</p>                               |                                                                                                       |
| SUSE Rancher Kubernetes Engine 2 (RKE2)                                                       | 1.28                                                                                                  |
| Talos                                                                                         | 1.8.3                                                                                                 |

{% hint style="info" %}
### Note

In Google Container-Optimized OS release 100 and earlier, where the FANOTIFY EXEC flag is not supported, the Kernel configuration may be partial for the user mode agent to properly function. In such cases, the agent will fallback to asynchronous mode.

In RHCOS version 4.12 and earlier, the Kernel configuration may be partial for the user mode agent to properly function. In such cases, the agent will fallback to asynchronous mode.
{% endhint %}
