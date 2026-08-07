---
description: >-
  To enable full endpoint protection features on Linux endpoints, you must use a
  supported Linux Kernel version.
---

# Cortex XDR supported Kernel Module versions by distribution

On Linux endpoints, to perform malware analysis of Executable and Linkable Format (ELF) files and collect data for endpoint detection and response (EDR) and behavioral threat analysis, the Cortex XDR agent requires a Linux Kernel module.

{% hint style="warning" %}
### Caution

To deploy on a supported Kernel version, you must ensure it is possible to load third party Kernel modules. To do so, you can either:

* Disable UEFI SecureBoot.
* If UEFI SecureBoot is enabled, you must load the Cortex XDR certificate.

To load the certificate, follow the instructions detailed in Cortex XDR Agent Administrator Guide → Cortex XDR Agent for Linux → Install the Cortex XDR Agent for Linux → **Load SecureBoot Certificates**.
{% endhint %}

Changes to the Kernel module versions are distributed with content updates. For earlier Cortex XDR agent releases, changes to the kernel module versions are distributed with the agent releases.

#### Latest Kernel Module versions supported

See the [latest Kernel Module versions](https://app.gitbook.com/s/y29o8lwSBpbfPbvztsyt/) that are supported.
