---
description: Hardware, OS, and required URLs for engines.
---

# Engine requirements

You can install engines on all Linux environments. Docker/Podman needs to be installed before installing an engine. If you are using the shell installer for an engine, Docker/Podman is installed automatically.

{% hint style="info" %}
The Cron package is required to install engines on a Linux machine.
{% endhint %}

**Engine hardware requirements**

If your hard drive is partitioned, we recommend a minimum of 50 GB for the `/var` partition.

| Component        | Dev Environment Minimum | Production Minimum |
| ---------------- | ----------------------- | ------------------ |
| CPU              | 8 CPU cores             | 16 CPU cores       |
| CPU architecture | x86\_64 only            | x86\_64 only       |
| Memory           | 16 GB RAM               | 32 GB RAM          |
| Storage          | 100 GB                  | 100 GB             |

**Operating system requirements**

You can deploy a Cortex XSIAM engine on the following operating systems:

| Operating System | Supported Versions                                       |
| ---------------- | -------------------------------------------------------- |
| Ubuntu           | 18.04, 20.04, 22.04, 24.04                               |
| RHEL             | <p>8.x, 9.x, 10.x</p><p>Includes all minor versions.</p> |
| Oracle Linux     | 7.x, 8.9, 9.3, 9.4, 10.1                                 |
| Amazon Linux     | 2, Amazon Linux 2023                                     |
| Rocky Linux      | 9.5, 9.6                                                 |

{% hint style="info" %}
CentOS 8.x reached End of Life (EOL) on December 31, 2021, and is no longer supported as an operating system.

CentOS 7.x reached End of Life (EOL) on June 30, 2024, and is no longer supported as an operating system.
{% endhint %}

**Engine required URLs**

You need to allow the following in the URLs for Cortex XSIAM engines to operate properly. The URLs are needed to pull container images from public Docker registries.

The endpoint URL is: `wss://api-<tenant domain>.xdr.<region>.paloaltonetworks.com/xsoar/d1ws`. For example, `wss://api-my-tenant.xdr.us.paloaltonetworks.com/xsoar/d1ws`

{% hint style="info" %}
If you have configured a range of **Approved IP Ranges** under **Allowed Sessions** on the **Security Settings** page, the engine must communicate through one of the approved IPs.
{% endhint %}

| FUNCTION            | SERVICE                                                                                                                                                                                                                                                                                                                                                                                             | PORT                       | DIRECTION |
| ------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------- | --------- |
| Integrations        |                                                                                                                                                                                                                                                                                                                                                                                                     | Integration-specific ports | Outbound  |
| Engine connectivity | HTTPS                                                                                                                                                                                                                                                                                                                                                                                               | 443 (configurable)         | Outbound  |
| Docker              | <ul><li>https://registry-1.docker.io</li><li>https://registry.fedoraproject.org</li><li>https://registry.access.redhat.com</li><li>https://docker.io</li><li>https://registry.docker.io</li><li><p>https://auth.docker.io</p><p>This URL may change at Docker’s discretion.</p></li><li><p>https://production.cloudflare.docker.com</p><p>This URL may change at Docker’s discretion.</p></li></ul> | 443                        | Outbound  |
