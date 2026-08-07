---
description: Install, configure, and troubleshoot Podman for Cortex XSIAM engines.
---

# Podman

[Podman](https://podman.io/) is a daemonless container engine for developing, managing, and running [OCI containers](https://opencontainers.org/) on Linux. Containers can run as root or in rootless mode.

The Shell installer detects the operating system’s container management type. On RHEL 8 and later, it installs and configures Podman for rootless mode.

{% hint style="info" %}
Engine upgrades retain the existing container management type.
{% endhint %}

PowerShell integrations might require default SELinux policy configuration. Podman can affect processes that `mmap` to `/dev/zero`.

#### Docker hardening guidelines

Docker hardening guidelines can be applied to Podman, except Limit Available Memory, Limit Available CPU, and Limit PIDS.
