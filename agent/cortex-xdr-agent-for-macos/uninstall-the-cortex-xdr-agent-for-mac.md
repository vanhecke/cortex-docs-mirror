---
description: Learn how to uninstall the Cortex XDR agent from a Mac endpoint.
---

# Uninstall the Cortex XDR Agent for Mac

From the Cortex XDR management console, you can uninstall the Cortex XDR agent on an endpoint (refer to _Uninstall the Cortex XDR Agent_ in the Administrator's Guide for your Cortex XDR license type). You can also uninstall the agent from the endpoint directly by using the uninstaller that comes with the Cortex XDR agent installation package that you downloaded from the Cortex XDR management console to install the agent (Endpoints → Endpoint Management → **Agent Installations**).

After you uninstall the agent, the endpoint is no longer protected by Cortex XDR security policies and the license returns to the pool of available licenses.

{% hint style="warning" %}
### Danger

To uninstall the agent, you need the uninstall password or a temporary token. See [Manage Agent Tokens](https://github.com/iKettles/palo-alto-networks-gitbook/tree/iain/import/document/preview/403317/README.md#UUID-862fecd8-73ec-1856-c849-f5c37860aec3) to obtain a temporary token.

Ensure that you extract the uninstaller from the installer package which is the same version as the Cortex XDR agent for Mac currently installed on the endpoint.

Ensure that the installer file, called `Cortex XDR Uninstaller.app`, is saved in the following location: `/Library/Application\Support/PaloAltoNetworks/Traps/bin`
{% endhint %}

1. Run the Cortex XDR agent uninstaller `Cortex XDR Uninstaller.app` from: `/Library/Application\Support/PaloAltoNetworks/Traps/bin`.
2. When prompted, enter the Cortex XDR agent uninstall password or temporary token, and click **OK**.
3.  When prompted, enter the macOS credentials for a user that has permissions to uninstall apps and click **OK**.

    The uninstaller completes the uninstall process and removes the Cortex XDR agent and related files.
