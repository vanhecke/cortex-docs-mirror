# Linux Kernel Versions

This reference documents the Linux kernel module versions supported by the Cortex XDR agent. It lists, for each supported Linux distribution, the kernel versions the agent can protect, along with the minimal agent version and minimal content version required for that support.

This reference is for administrators and security engineers who deploy the Cortex XDR agent on Linux hosts and need to confirm whether a given kernel is supported before rolling out or upgrading the agent.

## How this reference is organized

Support information is arranged in a three-level hierarchy:

* **Distribution** — A Linux distribution, such as Ubuntu or Red Hat Enterprise Linux (RHEL).
* **Architecture** — The CPU architecture, either x86\_64 or aarch64.
* **OS version** — A major version of the distribution, such as Ubuntu 22 or RHEL 9.

Each OS-version page lists a table of the supported kernel versions. For every kernel version, the table shows the minimal Cortex XDR agent version and the minimal content version required to support it.

## Covered distributions

This reference covers the following distributions:

* AlmaLinux
* Amazon Linux
* Amazon Linux 2
* Amazon Linux 2023
* CentOS
* CentOS Stream
* Debian
* OpenSUSE
* Oracle Linux
* Photon OS
* Red Hat Enterprise Linux (RHEL)
* Rocky Linux
* SUSE Linux Enterprise Server
* Ubuntu

## Find a supported kernel

To check whether a kernel is supported, navigate the table of contents in the left navigation:

1. Select your distribution to open its landing page.
2. Select the architecture that matches your host (x86\_64 or aarch64).
3. Open the page for your OS version and locate your kernel version in the table.

The minimal agent version and minimal content version shown next to a kernel version indicate the earliest Cortex XDR agent and content releases that support it.
