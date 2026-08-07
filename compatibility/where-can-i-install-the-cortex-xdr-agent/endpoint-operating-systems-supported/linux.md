# Linux

### Supported Linux operating systems

The following Linux operating systems support the Cortex XDR agent.

The Cortex XDR agent protects Linux Servers by preventing known and unknown malware from running by halting any attempts to leverage software exploits and vulnerabilities to compromise the server. Cortex XDR offers two methods for agent protection on Linux endpoints; a Kernel module and a user-mode (eBPF-based) approach. To help you choose the best deployment for your environment, see the feature differences between these two modes in the latest Cortex XDR agent Admin guide.

See the [latest Kernel Module versions](https://docs-cortex.paloaltonetworks.com/r/Cortex-XDR/Linux-Kernel-Versions/Latest-Kernel-Module-Version-Support) supported.

{% hint style="info" %}
### Note

Cortex XDR agent 9.1 was the last agent release supporting Linux kernels below 3.10. To avoid service disruption, hosts running kernels below 3.10 must not be upgraded beyond the 9.1 agent line. Disable auto-upgrades for endpoint profiles managing those machines, and prevent manual upgrades of the hosts to agent versions later than 9.1
{% endhint %}

### Alibaba Cloud Linux

| Alibaba Cloud Linux Operating System | Agent version 9.3 | Agent version 9.2 | Agent version 9.1-CE | Agent version 9.1 | Agent version 9.0 |   |
| ------------------------------------ | ----------------- | ----------------- | -------------------- | ----------------- | ----------------- | - |
| Alibaba Cloud Linux 3                | ✓                 | ✓                 | ✓                    | ✓                 | —                 | — |

### AlmaLinux

| AlmaLinux Operating System | <p>Agent version<br>9.3</p> | <p>Agent version<br>9.2</p> | <p>Agent version<br>9.1-CE</p> | <p>Agent version<br>9.1</p> | <p>Agent version<br>9.0</p> | <p>Agent version<br>8.7-CE</p> |
| -------------------------- | --------------------------- | --------------------------- | ------------------------------ | --------------------------- | --------------------------- | ------------------------------ |
| AlmaLinux 8                | ✓                           | ✓                           | ✓                              | ✓                           | ✓                           | ✓                              |
| AlmaLinux 9                | ✓                           | ✓                           | ✓                              | ✓                           | ✓                           | ✓                              |
| AlmaLinux 10               | ✓                           | ✓                           | ✓                              | ✓                           | ✓                           | ✓                              |

### Amazon Linux/Amazon Linux 2/Amazon Linux 2023

<table data-header-hidden><thead><tr><th></th><th width="128"></th><th></th><th></th><th></th><th></th><th></th></tr></thead><tbody><tr><td>Amazon Linux Operating System</td><td>Agent version 9.3</td><td>Agent version<br>9.2</td><td>Agent version<br>9.1-CE</td><td>Agent version<br>9.1</td><td>Agent version<br>9.0</td><td>Agent version<br>8.7-CE</td></tr><tr><td>AMI 2018.03</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td></tr><tr><td>Amazon Linux 2 AMI</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td></tr><tr><td>Amazon Linux 2 AMI (aarch64)</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td></tr><tr><td>Amazon Linux 2023</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td></tr><tr><td>Amazon Linux 2023 (aarch64)</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>—</td></tr></tbody></table>

### Debian

| Debian Operating System    | <p>Agent version<br>9.3</p> | <p>Agent version<br>9.2</p> | <p>Agent version<br>9.1-CE</p> | <p>Agent version<br>9.1</p> | <p>Agent version<br>9.0</p> | <p>Agent version<br>8.7-CE</p> |
| -------------------------- | --------------------------- | --------------------------- | ------------------------------ | --------------------------- | --------------------------- | ------------------------------ |
| Debian 9 (Stretch)         | ✓                           | ✓                           | ✓                              | ✓                           | ✓                           | ✓                              |
| Debian 10 (Buster)         | ✓                           | ✓                           | ✓                              | ✓                           | ✓                           | ✓                              |
| Debian 10 (Buster) aarch64 | ✓                           | ✓                           | ✓                              | ✓                           | ✓                           | ✓                              |
| Debian 11 (Bullseye)       | ✓                           | ✓                           | ✓                              | ✓                           | ✓                           | ✓                              |
| Debian 12 (Bookworm)       | ✓                           | ✓                           | ✓                              | ✓                           | ✓                           | ✓                              |
| Debian 13 (Trixie)         | ✓                           | ✓                           | ✓                              | ✓                           | ✓                           | ✓                              |

### CentOS

| CentOS Operating System           | <p>Agent version<br>9.3</p>                  | <p>Agent version<br>9.2</p>                  | <p>Agent version<br>9.1-CE</p>               | <p>Agent version<br>9.1</p>                  | <p>Agent version<br>9.0</p>                  | <p>Agent version<br>8.7-CE</p>               |
| --------------------------------- | -------------------------------------------- | -------------------------------------------- | -------------------------------------------- | -------------------------------------------- | -------------------------------------------- | -------------------------------------------- |
| CentOS 6 (supports 6.7 and above) | Async mode only                              | Async mode only                              | ✓                                            | ✓                                            | ✓                                            | ✓                                            |
| CentOS 7                          | ✓                                            | ✓                                            | ✓                                            | ✓                                            | ✓                                            | ✓                                            |
| CentOS 7.9 aarch64                | <p>✓</p><p>User mode agent not supported</p> | <p>✓</p><p>User mode agent not supported</p> | <p>✓</p><p>User mode agent not supported</p> | <p>✓</p><p>User mode agent not supported</p> | <p>✓</p><p>User mode agent not supported</p> | <p>✓</p><p>User mode agent not supported</p> |
| CentOS 8                          | ✓                                            | ✓                                            | ✓                                            | ✓                                            | ✓                                            | ✓                                            |
| CentOS 8 aarch64                  | ✓                                            | ✓                                            | ✓                                            | ✓                                            | ✓                                            | ✓                                            |
| CentOS Stream 8                   | ✓                                            | ✓                                            | ✓                                            | ✓                                            | ✓                                            | ✓                                            |
| CentOS Stream 8 aarch64           | ✓                                            | ✓                                            | ✓                                            | ✓                                            | ✓                                            | ✓                                            |
| CentOS Stream 9                   | ✓                                            | ✓                                            | ✓                                            | ✓                                            | ✓                                            | ✓                                            |

### Fedora Server

| Fedora Operating System  | <p>Agent version<br>9.3</p> | <p>Agent version<br>9.2</p> | <p>Agent version<br>9.1-CE</p> | <p>Agent version<br>9.1</p> | <p>Agent version<br>9.0</p> | <p>Agent version<br>8.7-CE</p> |
| ------------------------ | --------------------------- | --------------------------- | ------------------------------ | --------------------------- | --------------------------- | ------------------------------ |
| Fedora Server (USM only) | ✓                           | ✓                           | ✓                              | ✓                           | ✓                           | ✓                              |

### openSUSE

| openSUSE Operating System    | <p>Agent version<br>9.3</p> | <p>Agent version<br>9.2</p> | <p>Agent version<br>9.1-CE</p>                 | <p>Agent version<br>9.1</p>                    | <p>Agent version<br>9.0</p>                    | <p>Agent version<br>8.7-CE</p>                 |
| ---------------------------- | --------------------------- | --------------------------- | ---------------------------------------------- | ---------------------------------------------- | ---------------------------------------------- | ---------------------------------------------- |
| openSUSE Leap 16.0 (UM only) | ✓                           | ✓                           | <p>✓</p><p>From content release 2280-36261</p> | <p>✓</p><p>From content release 2280-36261</p> | —                                              | —                                              |
| openSUSE Leap 15.6 (UM only) | ✓                           | ✓                           | <p>✓</p><p>From content release 2160-30885</p> | <p>✓</p><p>From content release 2160-30885</p> | <p>✓</p><p>From content release 2160-30885</p> | <p>✓</p><p>From content release 2160-30885</p> |
| openSUSE Leap 15.3           | ✓                           | ✓                           | ✓                                              | ✓                                              | ✓                                              | ✓                                              |
| openSUSE Leap 15.2           | ✓                           | ✓                           | ✓                                              | ✓                                              | ✓                                              | ✓                                              |
| openSUSE Leap 15.1           | ✓                           | ✓                           | ✓                                              | ✓                                              | ✓                                              | ✓                                              |

### Oracle Linux

| Oracle Linux Operating System                                                            | <p>Agent version<br>9.3</p> | <p>Agent version<br>9.2</p> | <p>Agent version<br>9.1-CE</p> | <p>Agent version<br>9.1</p> | <p>Agent version<br>9.0</p> | <p>Agent version<br>8.7-CE</p>                 |
| ---------------------------------------------------------------------------------------- | --------------------------- | --------------------------- | ------------------------------ | --------------------------- | --------------------------- | ---------------------------------------------- |
| <p>Oracle 6 (supports 6.7 and above)<br><br>Oracle Linux 6 with RHCK (kernel 2.6.32)</p> |                             |                             |                                |                             |                             |                                                |
| <p><br>Oracle Linux 6 with UEK Release 2 (kernel 2.6.39)</p>                             |                             |                             |                                |                             |                             |                                                |
| <p><br>Oracle Linux 6 with UEK Release 3 (kernel 3.8.13)</p>                             | Async mode only             | Async mode only             | ✓                              | ✓                           | ✓                           | ✓                                              |
| Oracle 7                                                                                 | ✓                           | ✓                           | ✓                              | ✓                           | ✓                           | ✓                                              |
| Oracle 8                                                                                 | ✓                           | ✓                           | ✓                              | ✓                           | ✓                           | ✓                                              |
| Oracle 8 aarch64                                                                         | ✓                           | ✓                           | ✓                              | ✓                           | ✓                           | ✓                                              |
| Oracle 9 x86\_64 — Release 9.3                                                           | ✓                           | ✓                           | ✓                              | ✓                           | ✓                           | ✓                                              |
| Oracle 9 x86\_64 — Release 9.4 and later                                                 | ✓                           | ✓                           | ✓                              | ✓                           | ✓                           | ✓                                              |
| Oracle 9 aarch64                                                                         | ✓                           | ✓                           | ✓                              | ✓                           | ✓                           | ✓                                              |
| Oracle 10 x86\_64                                                                        | ✓                           | ✓                           | ✓                              | ✓                           | ✓                           | <p>✓</p><p>From content release 1940-22526</p> |
| Oracle 10 aarch64                                                                        | ✓                           | ✓                           | ✓                              | ✓                           | ✓                           | <p>✓</p><p>From content release 1940-22526</p> |

#### Oracle Linux 9 x86\_64 release 9.3 requirements

| Kernel | Support        | Minimum agent version |
| ------ | -------------- | --------------------- |
| RHCK   | User mode only | 8.2                   |
| UEK    | Supported      | 7.9-CE                |

### Red Hat Enterprise Linux

| Red Hat Enterprise Linux Operating System | <p>Agent version<br>9.3</p>                  | <p>Agent version<br>9.2</p>                  | <p>Agent version<br>9.1-CE</p>               | <p>Agent version<br>9.1</p>                  | <p>Agent version<br>9.0</p>                  | <p>Agent version<br>8.7-CE</p>               |
| ----------------------------------------- | -------------------------------------------- | -------------------------------------------- | -------------------------------------------- | -------------------------------------------- | -------------------------------------------- | -------------------------------------------- |
| RHEL 6 (supports 6.7 and above)           | Async mode only                              | Async mode only                              | ✓                                            | ✓                                            | ✓                                            | ✓                                            |
| RHEL 7                                    | ✓                                            | ✓                                            | ✓                                            | ✓                                            | ✓                                            | ✓                                            |
| RHEL 8 x86\_64                            | ✓                                            | ✓                                            | ✓                                            | ✓                                            | ✓                                            | ✓                                            |
| RHEL 8 aarch64                            | <p>✓</p><p>User mode agent not supported</p> | <p>✓</p><p>User mode agent not supported</p> | <p>✓</p><p>User mode agent not supported</p> | <p>✓</p><p>User mode agent not supported</p> | <p>✓</p><p>User mode agent not supported</p> | <p>✓</p><p>User mode agent not supported</p> |
| RHEL 9 x86\_64                            | ✓                                            | ✓                                            | ✓                                            | ✓                                            | ✓                                            | ✓                                            |
| RHEL 9 aarch64                            | ✓                                            | ✓                                            | ✓                                            | ✓                                            | ✓                                            | ✓                                            |
| RHEL 10 x86\_64                           | ✓                                            | ✓                                            | ✓                                            | ✓                                            | ✓                                            | ✓                                            |
| RHEL 10 aarch64                           | ✓                                            | ✓                                            | ✓                                            | ✓                                            | ✓                                            | ✓                                            |

{% hint style="info" %}
### RHEL 9 requirement

RHEL 9.3 and later require agent version 8.2 or later.
{% endhint %}

### Rocky Linux

| Rocky Linux Operating System | <p>Agent version<br>9.3</p> | <p>Agent version<br>9.2</p> | <p>Agent version<br>9.1-CE</p> | <p>Agent version<br>9.1</p> | <p>Agent version<br>9.0</p> | <p>Agent version<br>8.7-CE</p> |
| ---------------------------- | --------------------------- | --------------------------- | ------------------------------ | --------------------------- | --------------------------- | ------------------------------ |
| Rocky Linux 10 x86\_64       | ✓                           | ✓                           | ✓                              | ✓                           | ✓                           | ✓                              |
| Rocky Linux 9 x86\_64        | ✓                           | ✓                           | ✓                              | ✓                           | ✓                           | ✓                              |
| Rocky Linux 9 aarch64        | ✓                           | ✓                           | ✓                              | ✓                           | ✓                           | ✓                              |
| Rocky Linux 8 x86\_64        | ✓                           | ✓                           | ✓                              | ✓                           | ✓                           | ✓                              |

### SUSE Linux Enterprise Server

| SUSE Linux Enterprise Server Operating System | <p>Agent version<br>9.3</p> | <p>Agent version<br>9.2</p> | <p>Agent version<br>9.1-CE</p>                 | <p>Agent version<br>9.1</p>                    | <p>Agent version<br>9.0</p> | <p>Agent version<br>8.7-CE</p>                 |
| --------------------------------------------- | --------------------------- | --------------------------- | ---------------------------------------------- | ---------------------------------------------- | --------------------------- | ---------------------------------------------- |
| Server 16.0                                   | ✓                           | ✓                           | <p>✓</p><p>From content release 2280-36261</p> | <p>✓</p><p>From content release 2280-36261</p> | —                           | —                                              |
| Server 15 SP7                                 | ✓                           | ✓                           | ✓                                              | ✓                                              | ✓                           | <p>✓</p><p>From content release 1940-22526</p> |
| Server 15 SP0-SP6                             | ✓                           | ✓                           | ✓                                              | ✓                                              | ✓                           | ✓                                              |
| Server 12 SP4-SP5                             | ✓                           | ✓                           | ✓                                              | ✓                                              | ✓                           | ✓                                              |
| Server 11 SP4                                 | Async mode only             | Async mode only             | ✓                                              | ✓                                              | ✓                           | ✓                                              |

### Ubuntu

| Ubuntu Operating System | <p>Agent version<br>9.3</p> | <p>Agent version<br>9.2</p> | <p>Agent version<br>9.1-CE</p> | <p>Agent version<br>9.1</p> | <p>Agent version<br>9.0</p> | <p>Agent version<br>8.7-CE</p> |
| ----------------------- | --------------------------- | --------------------------- | ------------------------------ | --------------------------- | --------------------------- | ------------------------------ |
| 12.04 LTS               | Async mode only             | Async mode only             | ✓                              | ✓                           | ✓                           | ✓                              |
| 14.04 LTS               | Async mode only             | Async mode only             | ✓                              | ✓                           | ✓                           | ✓                              |
| 16.04 LTS               | ✓                           | ✓                           | ✓                              | ✓                           | ✓                           | ✓                              |
| 18.04 LTS               | ✓                           | ✓                           | ✓                              | ✓                           | ✓                           | ✓                              |
| 18.04 LTS aarch64       | ✓                           | ✓                           | ✓                              | ✓                           | ✓                           | ✓                              |
| 20.04 LTS               | ✓                           | ✓                           | ✓                              | ✓                           | ✓                           | ✓                              |
| 20.04 LTS aarch64       | ✓                           | ✓                           | ✓                              | ✓                           | ✓                           | ✓                              |
| 22.04 LTS x86\_64       | ✓                           | ✓                           | ✓                              | ✓                           | ✓                           | ✓                              |
| 22.04 LTS aarch64       | ✓                           | ✓                           | ✓                              | ✓                           | ✓                           | ✓                              |
| 24.04 LTS x86\_64       | ✓                           | ✓                           | ✓                              | ✓                           | ✓                           | ✓                              |
| 24.04 LTS aarch64       | ✓                           | ✓                           | ✓                              | ✓                           | ✓                           | ✓                              |
