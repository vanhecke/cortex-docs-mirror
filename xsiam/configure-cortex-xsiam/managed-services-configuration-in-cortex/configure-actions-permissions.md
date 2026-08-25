---
description: >-
  Configure Unit 42 Managed Services response permissions in Cortex XSIAM for
  server and workstation endpoint actions.
---

# Configure actions permissions

Configure how Unit 42 Managed Services performs Cortex XSIAM endpoint response actions. Set a permission level for each action and asset type.

The response permissions matrix on the **General** tab governs eight endpoint response actions. Configure each action separately for **Server** and **Workstation** assets. This enables stricter control for higher-criticality assets.

### Cortex XSIAM response permission levels

There are three permission levels to choose from:

| Permission level | Description                                                                                                                                    |
| ---------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| **Inform**       | Requires approval from your designated escalation contacts before any action is taken. No action will be performed until approval is received. |
| **No**           | Does not authorize our team to perform the specified action in your environment.                                                               |
| **Yes**          | Authorizes our team to act without prior approval.                                                                                             |

{% hint style="info" %}
### Note

When a permission level is set to **Inform**, configure at least one entry on the Escalation contacts tab so the Unit 42 Managed Services team can request approval before performing the action.
{% endhint %}

### Managed Services endpoint response actions

Set the permission level for each of the response actions for **Server** and **Workstation**.

| Action                           | Description                                                                  |
| -------------------------------- | ---------------------------------------------------------------------------- |
| Retrieve endpoint files          | Extract files from a managed asset for forensic analysis.                    |
| Initiate live terminal           | Open an interactive terminal session on a managed asset for investigation.   |
| Isolate endpoint                 | Disconnect a managed asset from the network to contain a threat.             |
| Run endpoint script              | Execute a script on a managed asset for remediation or data collection.      |
| Destroy file                     | Permanently delete a file from a managed asset. This action is irreversible. |
| Retrieve technical support files | Collect system logs and diagnostic data from a managed asset.                |
| Terminate process                | Stop a running process on a managed asset.                                   |
| Quarantine files                 | Isolate a file to prevent execution while preserving the file for analysis.  |

The Unit 42 Managed Services team operates in accordance with the configured permission level for each response action on each asset type. Actions set to Inform trigger an approval request to the escalation contacts before execution. Actions set to **No** are not performed.
