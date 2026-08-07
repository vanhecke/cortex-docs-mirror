---
description: >-
  Create custom case and issue statuses and resolution reasons for your
  workflow.
---

# Create custom case statuses and resolution reasons

{% hint style="info" %}
Before you create a custom status, please review the built-in options. For more information, see [Resolution reasons for cases and issues](../../detect-investigate-and-respond-to-threats/investigation-and-response/analyze-and-resolve-cases/resolve-the-case/resolution-reasons-for-cases-and-issues).

We recommend using the built-in statuses and resolution reasons where possible. Custom statuses and resolution reasons might not be supported by all content, and status syncing can take time.

In addition, custom statuses affect Cortex XSIAM’s ability to learn, correctly identify, and score future cases.
{% endhint %}

You can create custom cases statuses and custom resolution reasons that are tailored to your workflow. Custom case statuses and resolution reasons apply to case and issue statuses, and can also be used in playbooks.

Adding custom ,case statuses and resolution reasons requires a **View/Edit** RBAC permission for **Case Properties** (under **Configurations** → **Object Setup**).

{% hint style="info" %}
After creation, custom statuses and resolution reasons cannot be deleted or modified.
{% endhint %}

How to create custom case statuses

1.  Go to **Configurations** → **Object Setup** → **Cases** → **Properties**.

    The existing statuses and resolution types are listed.
2. In the **Add another status** field, type a new status and click **Save**.
3. Click **Edit** to rearrange the order of the statuses. This order is presented when you set a status or select a resolution type.
