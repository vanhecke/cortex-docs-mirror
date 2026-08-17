# Windows

### Supported Windows operating systems

The following Windows operating systems support the Cortex XDR agent.

{% hint style="info" %}
### Note

Due to a limitation on Windows Servers, Cortex XDR agent will not register with the Microsoft Security Center.
{% endhint %}

### Install the Cortex XDR agent on unsupported-ACS OS versions

Microsoft Trusted Signing (Azure Code Signing) Directive

Since March 2023, Microsoft request security vendors to sign binaries using [Trusted Signing (formerly Azure Code Signing)](https://techcommunity.microsoft.com/t5/security-compliance-and-identity/azure-code-signing-democratizing-trust-for-developers-and/ba-p/3604669). As a result, Cortex XDR agent versions require a specific Microsoft Windows patch. Note that any machines without this Windows patch are not able to install or upgrade to newer versions of Cortex XDR agent. This mainly impacted Windows machines running Windows 10 or below; Windows 11 machines have this patch pre-installed. Windows 7 machines must have an extended support license in order to install the patch. Additional information about the security patch and the specific patch numbers required per operating system build, KB5022661/KB4474419 . In cases where the Microsoft security patch has since expired, ACS support is achieved by installing cumulative updates after the release of the initial KB patch.

Cortex XDR agent versions later than 8.3-CE will automatically detect an ACS-unsupported OS and allow the installation to complete successfully.

In agent versions 7.9.103-CE and 8.3-CE, to override the default behavior, admin must provide an MSI flag, `NO_ACS_SUPPORT=1`, as a parameter to the installer. This flag indicates that the installation is to be made on an ACS-unsupported operating system. A fresh installation is needed for using this flag.

{% hint style="info" %}
### Note

The NO\_ACS\_SUPPORT flag cannot be provided as part of an existing Cortex XDR agent upgrade.
{% endhint %}

If upgrading from a 7.5-CE release line, even without explicitly providing the installer flag, the installer will detect that ACS is unsupported and will treat the installation as if the flag was given.

### Windows 7

{% hint style="info" %}
### Note

Cortex XDR agent 7.9 was the last version to support Windows 7. Release 7.9.103-CE gives extended support until December 31, 2026. No new capabilities will be developed for these OS versions.
{% endhint %}

| Windows 7 Operating System                                | 8.0 and later versions | 7.9.103‑CE |
| --------------------------------------------------------- | ---------------------- | ---------- |
| Windows 7 Operating System                                | 8.0 and later versions | 7.9.103‑CE |
| RTM                                                       | —                      | —          |
| <p>Windows 7 SP1</p><p>(All editions except Home)</p>     | —                      | ✓          |
| Embedded Standard 7 SP1                                   | —                      | ✓          |
| <p>Embedded POSReady 7</p><p>(Based on Windows 7 SP1)</p> | —                      | ✓          |

### Windows 8

All Windows 8 variants were supported until January 2023 (Microsoft EOL + 3 years). Release 7.9-CE, up to release 7.9.102-CE, offered support for Windows 8.1 until March 19, 2025. No new capabilities will be developed for these OS versions.

The extended-life agent 7.9.103-CE does not support Windows 8.1

### Windows 10

The Enterprise edition is tested for compatibility. Unless specifically stated otherwise, assume that all sub-editions are also compatible.

|                                                            | Cortex XDR agent |     |        |     |     |        |
| ---------------------------------------------------------- | ---------------- | --- | ------ | --- | --- | ------ |
|                                                            | 9.3              | 9.2 | 9.1-CE | 9.1 | 9.0 | 8.7-CE |
| 19H2, 20H1, 20H2, 21H1                                     | —                | —   | —      | —   | —   | ✓      |
| Threshold LTSB, Redstone LTSB, Redstone 5 LTSB, 21H2, 22H2 | ✓                | ✓   | ✓      | ✓   | ✓   | ✓      |
| <p>Windows 10 IoT Core<br>Windows 10 IoT Enterprise</p>    | ✓                | ✓   | ✓      | ✓   | ✓   | ✓      |

### Windows 11

The Enterprise edition is tested for compatibility. Unless specifically stated otherwise, assume that all sub-editions are also compatible.

|                               | Cortex XDR agent |     |        |     |     |        |
| ----------------------------- | ---------------- | --- | ------ | --- | --- | ------ |
|                               | 9.3              | 9.2 | 9.1-CE | 9.1 | 9.0 | 8.7-CE |
| <p>25H2<br>x86_64 and ARM</p> | ✓                | ✓   | ✓      | ✓   | ✓   | —      |
| <p>24H2<br>x86_64 and ARM</p> | ✓                | ✓   | ✓      | ✓   | ✓   | ✓      |
| <p>23H2<br>x86_64 and ARM</p> | ✓                | ✓   | ✓      | ✓   | ✓   | ✓      |
| <p>22H2<br>x86_64</p>         | ✓                | ✓   | ✓      | ✓   | ✓   | ✓      |

{% hint style="info" %}
### Note

Windows running on ARM is subject to certain limitations, see Known limitations in the latest Cortex XDR agent [release notes](https://cortex-docs.paloaltonetworks.com/agent-release-notes).
{% endhint %}

### Windows Server

The Datacenter edition is tested for compatibility. Unless specifically stated otherwise, assume that all sub-editions are also compatible.

{% hint style="info" %}
### Note

Release 7.9-CE, up to release 7.9.102-CE, was supported Windows Server until March 19, 2025.

The extended-life agent 7.9.103-CE supports Windows Server 2008 R2 SP1 until December 31, 2027.
{% endhint %}

<table data-search="false"><thead><tr><th></th><th width="138.5">Cortex XDR agent</th><th width="109.25"></th><th width="108"></th><th width="109.25"></th><th width="105.5"></th><th width="108"></th><th width="110"></th></tr></thead><tbody><tr><td></td><td>9.3</td><td>9.2</td><td>9.1-CE</td><td>9.1</td><td>9.0</td><td>8.7-CE</td><td>7.9.103-CE</td></tr><tr><td>2025</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>—</td></tr><tr><td>2022</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>—</td></tr><tr><td>2019 LTSC<br>2019 Core</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>—</td></tr><tr><td>2016</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>—</td></tr><tr><td>2012 (Support until Oct 2027)<br>2012 R2 (Support until Oct 2027)</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>—</td></tr><tr><td>2012 Core</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td><td>—</td></tr><tr><td>2008 R2 SP1</td><td>—</td><td>—</td><td>—</td><td>—</td><td>—</td><td>—</td><td>✓</td></tr></tbody></table>
