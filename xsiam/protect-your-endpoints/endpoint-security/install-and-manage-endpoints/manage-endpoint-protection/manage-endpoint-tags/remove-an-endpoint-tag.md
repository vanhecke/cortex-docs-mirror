---
description: Remove endpoint tags that are no longer needed in Cortex XSIAM.
---

# Remove an endpoint tag

Depending on where you created your tag - Server or Agent, you can choose to edit or remove the tag.

{% hint style="warning" %}
**Note:**

If you remove the tag and there are assigned users or user groups with scope settings, this can impact user permissions in the system.
{% endhint %}

### Remove an Endpoint tag from the Cortex XDR agent

1. Navigate to the Cytool folder location and open the CLI as an administrator.
2. Cytool Argument: `cytool endpoint_tags remove "tag1 [,tag2,...,tagN]"`.

### Remove an Endpoint tag from Cortex XSIAM

1. Navigate to **Inventory → Endpoints → All Endpoints → Tags field**.
2. Select one or more endpoints, right-click, and select **Endpoint Control → Remove Endpoint Tags**.
3. Click **Save**.
