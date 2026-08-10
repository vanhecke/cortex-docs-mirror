# Kubernetes platforms supported

View the Kubernetes platforms that are supported with Cortex XDR agents.

This table shows the Kubernetes platform versions that have been compatibility tested. The table shows the latest version that has been tested. All versions that are not EOL, up to the latest version tested for compatibility are supported.

For installation instructions refer to Cortex XDR Agent for Linux → Install the Cortex XDR Agent for Kubernetes Hosts in the latest [Cortex XDR agent admin guide](https://app.gitbook.com/o/r4DIGbR5VLvkZy3gAYsu/s/YhAQu4OiCd3X2NZv62G3/).

<table data-search="false"><thead><tr><th width="411.5">Linux Kubernetes Platform</th><th>Version</th></tr></thead><tbody><tr><td>Unmanaged Kubernetes (k8s)</td><td>1.30</td></tr><tr><td><p>Amazon Elastic Kubernetes Service (EKS)</p><ul><li>BottleRocket OS x86_64<br>User mode agent only</li><li>BottleRocket OS aarch64<br>User mode agent only</li></ul></td><td>1.35</td></tr><tr><td><p>Microsoft Azure Kubernetes Service (AKS)</p><ul><li>CBL-mariner 2 x86_64</li></ul></td><td>1.35</td></tr><tr><td><p>Google Kubernetes Engine (GKE)</p><ul><li>Google Container-Optimized OS (COS)<sup>*</sup> x86_64<br>User mode agent only</li><li>Google Kubernetes Engine (GKE) Autopilot</li></ul></td><td>1.35</td></tr><tr><td>Oracle Kubernetes Engine (OKE)</td><td>1.33</td></tr><tr><td><p>Red Hat Openshift Container Platform (OCP)</p><ul><li>RHCOS<sup>*</sup> x86_64<br>User mode agent only</li></ul></td><td><p>4.18</p><p>4.19 in agent versions 9.1.1 and later</p><p>4.20 in agent versions 9.1.1 and later</p></td></tr><tr><td>SUSE Rancher Kubernetes Engine 2 (RKE2)</td><td>1.28</td></tr><tr><td>Talos</td><td>1.8.3</td></tr></tbody></table>

{% hint style="info" %}
### Notes

In Google Container-Optimized OS release 100 and earlier, where the FANOTIFY EXEC flag is not supported, the Kernel configuration may be partial for the user mode agent to properly function. In such cases, the agent will fallback to asynchronous mode.

In RHCOS version 4.12 and earlier, the Kernel configuration may be partial for the user mode agent to properly function. In such cases, the agent will fallback to asynchronous mode.
{% endhint %}
