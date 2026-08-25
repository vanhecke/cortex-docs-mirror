---
description: >-
  Learn how to create custom case and issue statuses and resolution reasons in
  Cortex XSIAM.
---

# Create custom case statuses and resolution reasons

### Before you begin

{% hint style="info" %}
Before you create a custom status, review the built-in options. For more information, see [Resolution reasons for cases and issues](../../detect-investigate-and-respond-to-threats/investigation-and-response/analyze-and-resolve-cases/resolve-the-case/resolution-reasons-for-cases-and-issues).

We recommend using the built-in statuses and resolution reasons where possible. Custom statuses and resolution reasons might not be supported by all content, and status syncing can take time.

In addition, custom statuses affect Cortex XSIAM’s ability to learn, correctly identify, and score future cases.
{% endhint %}

Create custom case statuses and resolution reasons that match your workflow. These settings apply to cases and issues. You can also use them in playbooks.

Creating custom case statuses and resolution reasons requires the **View/Edit** RBAC permission for **Case Properties** under **Configurations** → **Object Setup**.

{% hint style="info" %}
After creation, custom statuses and resolution reasons cannot be deleted or modified.
{% endhint %}

### Create custom case statuses

1.  Go to **Configurations** → **Object Setup** → **Cases** → **Properties**.

    The existing statuses and resolution types are listed.
2. In the **Add another status** field, type a new status and click **Save**.
3. Click **Edit** to rearrange the order of the statuses. This order is presented when you set a status or select a resolution type.
