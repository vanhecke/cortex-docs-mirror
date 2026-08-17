# Linux

## Supported Linux operating systems

The following Linux operating systems support the Cortex XDR agent.



The Cortex XDR agent protects Linux servers, there are two methods for agent protection; a Kernel module and a user-mode (eBPF-based) approach. To help you choose the best deployment for your environment, see the feature differences between these two modes in the latest Cortex XDR agent Admin guide [Broken link](broken-reference "mention").

For the latest Kernel modules support see [here](https://cortex-docs.paloaltonetworks.com/linux-kernel-versions).

{% hint style="info" %}
### Note

Cortex XDR agent 9.1 was the last agent release supporting Linux kernels below 3.10. To avoid service disruption, hosts running kernels below 3.10 must not be upgraded beyond the 9.1 agent line. Disable auto-upgrades for endpoint profiles managing those machines, and prevent manual upgrades of the hosts to agent versions later than 9.1
{% endhint %}

### Alibaba Cloud Linux

|                       | Cortex XDR agent |     |        |     |     |        |
| --------------------- | ---------------- | --- | ------ | --- | --- | ------ |
|                       | 9.3              | 9.2 | 9.1-CE | 9.1 | 9.0 | 8.7-CE |
| Alibaba Cloud Linux 3 | ✓                | ✓   | ✓      | ✓   | —   | —      |

### AlmaLinux

|              | Cortex XDR agent |     |        |     |     |        |
| ------------ | ---------------- | --- | ------ | --- | --- | ------ |
|              | 9.3              | 9.2 | 9.1-CE | 9.1 | 9.0 | 8.7-CE |
| AlmaLinux 10 | ✓                | ✓   | ✓      | ✓   | ✓   | ✓      |
| AlmaLinux 9  | ✓                | ✓   | ✓      | ✓   | ✓   | ✓      |
| AlmaLinux 8  | ✓                | ✓   | ✓      | ✓   | ✓   | ✓      |

### Amazon Linux/Amazon Linux 2/Amazon Linux 2023

<table><thead><tr><th></th><th width="128">Cortex XDR agent</th><th></th><th></th><th></th><th></th><th></th></tr></thead><tbody><tr><td></td><td>9.3</td><td>9.2</td><td>9.1-CE</td><td>9.1</td><td>9.0</td><td>8.7-CE</td></tr><tr><td>AMI 2018.03</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td></tr><tr><td>Amazon Linux 2 AMI</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td></tr><tr><td>Amazon Linux 2 AMI (aarch64)</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td></tr><tr><td>Amazon Linux 2023</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td></tr><tr><td>Amazon Linux 2023 (aarch64)</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>—</td></tr></tbody></table>

### Debian

<table data-search="false"><thead><tr><th></th><th>Cortex XDR agent</th><th></th><th></th><th></th><th></th><th></th></tr></thead><tbody><tr><td></td><td>9.3</td><td>9.2</td><td>9.1-CE</td><td>9.1</td><td>9.0</td><td>8.7-CE</td></tr><tr><td>Debian 13 (Trixie)</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td></tr><tr><td>Debian 12 (Bookworm)</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td></tr><tr><td>Debian 11 (Bullseye)</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td></tr><tr><td>Debian 10 (Buster)</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td></tr><tr><td>Debian 10 (Buster) aarch64</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td></tr><tr><td>Debian 9 (Stretch)</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td></tr></tbody></table>

### CentOS

<table data-search="false"><thead><tr><th></th><th>Cortex XDR agent</th><th></th><th></th><th></th><th></th><th></th></tr></thead><tbody><tr><td></td><td>9.3</td><td>9.2</td><td>9.1-CE</td><td>9.1</td><td>9.0</td><td>8.7-CE</td></tr><tr><td>CentOS Stream 9</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td></tr><tr><td>CentOS Stream 8</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td></tr><tr><td>CentOS Stream 8 aarch64</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td></tr><tr><td>CentOS 8</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td></tr><tr><td>CentOS 8 aarch64</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td></tr><tr><td>CentOS 7.9 aarch64</td><td><p>✓</p><p>User mode agent not supported</p></td><td><p>✓</p><p>User mode agent not supported</p></td><td><p>✓</p><p>User mode agent not supported</p></td><td><p>✓</p><p>User mode agent not supported</p></td><td><p>✓</p><p>User mode agent not supported</p></td><td><p>✓</p><p>User mode agent not supported</p></td></tr><tr><td>CentOS 7</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td></tr><tr><td>CentOS 6<br>(6.7 and above)</td><td>Async mode only</td><td>Async mode only</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td></tr></tbody></table>

### Fedora Server

|                          | Cortex XDR agent |     |        |     |     |        |
| ------------------------ | ---------------- | --- | ------ | --- | --- | ------ |
|                          | 9.3              | 9.2 | 9.1-CE | 9.1 | 9.0 | 8.7-CE |
| Fedora Server (USM only) | ✓                | ✓   | ✓      | ✓   | ✓   | ✓      |

### openSUSE

|                              | Cortex XDR agent |     |                                                |                                                |                                                |                                                |
| ---------------------------- | ---------------- | --- | ---------------------------------------------- | ---------------------------------------------- | ---------------------------------------------- | ---------------------------------------------- |
|                              | 9.3              | 9.2 | 9.1-CE                                         | 9.1                                            | 9.0                                            | 8.7-CE                                         |
| openSUSE Leap 16.0 (UM only) | ✓                | ✓   | <p>✓</p><p>From content release 2280-36261</p> | <p>✓</p><p>From content release 2280-36261</p> | —                                              | —                                              |
| openSUSE Leap 15.6 (UM only) | ✓                | ✓   | <p>✓</p><p>From content release 2160-30885</p> | <p>✓</p><p>From content release 2160-30885</p> | <p>✓</p><p>From content release 2160-30885</p> | <p>✓</p><p>From content release 2160-30885</p> |
| openSUSE Leap 15.3           | ✓                | ✓   | ✓                                              | ✓                                              | ✓                                              | ✓                                              |
| openSUSE Leap 15.2           | ✓                | ✓   | ✓                                              | ✓                                              | ✓                                              | ✓                                              |
| openSUSE Leap 15.1           | ✓                | ✓   | ✓                                              | ✓                                              | ✓                                              | ✓                                              |

### Oracle Linux

<table data-search="false"><thead><tr><th></th><th>Cortex XDR agent</th><th></th><th></th><th></th><th></th><th></th></tr></thead><tbody><tr><td></td><td>9.3</td><td>9.2</td><td>9.1-CE</td><td>9.1</td><td>9.0</td><td>8.7-CE</td></tr><tr><td>Oracle 10 x86_64</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td><p>✓</p><p>From content release 1940-22526</p></td></tr><tr><td>Oracle 10 aarch64</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td><p>✓</p><p>From content release 1940-22526</p></td></tr><tr><td>Oracle 9 x86_64 — Release 9.4 and later</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td></tr><tr><td>Oracle 9 x86_64 — Release 9.3*</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td></tr><tr><td>Oracle 9 aarch64</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td></tr><tr><td>Oracle 8</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td></tr><tr><td>Oracle 8 aarch64</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td></tr><tr><td>Oracle 7</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td></tr><tr><td><p><br>Oracle Linux 6 (6.7 and above)</p><ul><li>RHCK (kernel 2.6.32)</li><li>UEK Release 2 (kernel 2.6.39)</li><li>UEK Release 3 (kernel 3.8.13)</li></ul></td><td>Async mode only</td><td>Async mode only</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td></tr></tbody></table>

\*Oracle Linux 9.3 x86\_64 notes:

| Kernel | Support        | Minimum agent version |
| ------ | -------------- | --------------------- |
| RHCK   | User mode only | 8.2                   |
| UEK    | Supported      | 7.9-CE                |

### Red Hat Enterprise Linux

<table data-search="false"><thead><tr><th></th><th>Cortex XDR agent</th><th></th><th></th><th></th><th></th><th></th></tr></thead><tbody><tr><td></td><td>9.3</td><td>9.2</td><td>9.1-CE</td><td>9.1</td><td>9.0</td><td>8.7-CE</td></tr><tr><td>RHEL 10 x86_64</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td></tr><tr><td>RHEL 10 aarch64</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td></tr><tr><td>RHEL 9* x86_64</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td></tr><tr><td>RHEL 9* aarch64</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td></tr><tr><td>RHEL 8 x86_64</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td></tr><tr><td>RHEL 8 aarch64</td><td><p>✓</p><p>User mode agent not supported</p></td><td><p>✓</p><p>User mode agent not supported</p></td><td><p>✓</p><p>User mode agent not supported</p></td><td><p>✓</p><p>User mode agent not supported</p></td><td><p>✓</p><p>User mode agent not supported</p></td><td><p>✓</p><p>User mode agent not supported</p></td></tr><tr><td>RHEL 7</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td></tr><tr><td>RHEL 6 (supports 6.7 and above)</td><td>Async mode only</td><td>Async mode only</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td></tr></tbody></table>

{% hint style="info" %}
### \*RHEL 9 requirement

RHEL 9.3 and later requires Cortex XDR agent version 8.2 or later.
{% endhint %}

### Rocky Linux

|                        | Cortex XDR agent |     |        |     |     |        |
| ---------------------- | ---------------- | --- | ------ | --- | --- | ------ |
|                        | 9.3              | 9.2 | 9.1-CE | 9.1 | 9.0 | 8.7-CE |
| Rocky Linux 10 x86\_64 | ✓                | ✓   | ✓      | ✓   | ✓   | ✓      |
| Rocky Linux 9 x86\_64  | ✓                | ✓   | ✓      | ✓   | ✓   | ✓      |
| Rocky Linux 9 aarch64  | ✓                | ✓   | ✓      | ✓   | ✓   | ✓      |
| Rocky Linux 8 x86\_64  | ✓                | ✓   | ✓      | ✓   | ✓   | ✓      |

### SUSE Linux Enterprise Server

|                   | Cortex XDR agent |                 |                                                |                                                |     |                                                |
| ----------------- | ---------------- | --------------- | ---------------------------------------------- | ---------------------------------------------- | --- | ---------------------------------------------- |
|                   | 9.3              | 9.2             | 9.1-CE                                         | 9.1                                            | 9.0 | 8.7-CE                                         |
| Server 16.0       | ✓                | ✓               | <p>✓</p><p>From content release 2280-36261</p> | <p>✓</p><p>From content release 2280-36261</p> | —   | —                                              |
| Server 15 SP7     | ✓                | ✓               | ✓                                              | ✓                                              | ✓   | <p>✓</p><p>From content release 1940-22526</p> |
| Server 15 SP0-SP6 | ✓                | ✓               | ✓                                              | ✓                                              | ✓   | ✓                                              |
| Server 12 SP4-SP5 | ✓                | ✓               | ✓                                              | ✓                                              | ✓   | ✓                                              |
| Server 11 SP4     | Async mode only  | Async mode only | ✓                                              | ✓                                              | ✓   | ✓                                              |

### Ubuntu

<table data-search="false"><thead><tr><th></th><th>Cortex XDR agent</th><th></th><th></th><th></th><th></th><th></th></tr></thead><tbody><tr><td></td><td>9.3</td><td>9.2</td><td>9.1-CE</td><td>9.1</td><td>9.0</td><td>8.7-CE</td></tr><tr><td>24.04 LTS x86_64</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td></tr><tr><td>24.04 LTS aarch64</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td></tr><tr><td>22.04 LTS x86_64</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td></tr><tr><td>22.04 LTS aarch64</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td></tr><tr><td>20.04 LTS</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td></tr><tr><td>20.04 LTS aarch64</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td></tr><tr><td>18.04 LTS</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td></tr><tr><td>18.04 LTS aarch64</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td></tr><tr><td>16.04 LTS</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td></tr><tr><td>14.04 LTS</td><td>Async mode only</td><td>Async mode only</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td></tr><tr><td>12.04 LTS</td><td>Async mode only</td><td>Async mode only</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td></tr></tbody></table>
