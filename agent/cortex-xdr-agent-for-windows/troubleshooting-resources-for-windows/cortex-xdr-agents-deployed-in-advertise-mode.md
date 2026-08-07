---
description: >-
  Depending on your Cortex XDR agent release, you can install or upgrade the
  agent in Advertise mode.
---

# Cortex XDR Agents Deployed in Advertise Mode

Advertise mode is an **`msi`** property you can set manually through the **`msi`** execution command line or through a deployment profile in a third-party deployment tool such as Microsoft System Center Configuration Manager (SCCM), allowing the Windows Installer to advertise the availability of an application to users or other applications without actually installing the application. For more information on advertise mode, refer to the Microsoft Windows official documentation.

{% hint style="warning" %}
### Caution

When you want to install or upgrade a Cortex XDR agent on an endpoint where a Cortex XDR agent release prior to 7.0.3 was installed in Advertise mode, whether the agent is still running or was removed from the endpoint, you must first clean the endpoint from the remains of the previous installation in Advertise mode. Otherwise, if you don’t clean the endpoint, the installation/upgrade of the Cortex XDR agent will fail.
{% endhint %}

The following table summarizes the different scenarios of upgrade paths and the recommended workaround according to the different Cortex XDR agent releases:

|                                                                   | Upgrade to Agent Release 5.0.0 or Later                                                                                                         | Upgrade to Agent Release 7.0.3 or Later                                                                                                                                     | Upgrade to Agent Release 7.1.1 or Later                                                                                                                                                                        |
| ----------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Agent release 5.0.0 or later that was installed in Advertise mode | <p>Not supported, leads to undefined behavior.</p><p>Contact Palo Alto Networks Support for assistance before you can re-install the agent.</p> | <p>Not supported, you will receive an error in the agent installation log.</p><p>Contact Palo Alto Networks Support for assistance before you can re-install the agent.</p> | <p>You will receive an error in the agent installation log.</p><p>Add the <strong><code>CLEAN_AGGRESIVLY=1</code></strong> <code>msi</code> property to you command line and proceed to install the agent.</p> |
| Agent release 7.0.3 or later that was installed in Advertise mode | N/A                                                                                                                                             | Seamless                                                                                                                                                                    | Seamless                                                                                                                                                                                                       |

{% hint style="info" %}
### Note

Palo Alto Networks recommends that you always upgrade to the latest agent release of the latest major version and use the `CLEAN_AGGRESIVLY=1` `msi` property to mitigate any Advertised mode related issues.
{% endhint %}
