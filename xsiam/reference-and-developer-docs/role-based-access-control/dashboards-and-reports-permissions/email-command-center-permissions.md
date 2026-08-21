---
description: >-
  Manage access to the Cortex XSIAM Email Command Center and email threat
  metrics.
---

# Email Command Center permissions

Controls access to the Email Command Center, which enables you to view high-level metrics on inbound email threats, phishing trends, and top targeted users.

For more information, see [Email Command Center](../../../detect-investigate-and-respond-to-threats/cortex-advanced-email-security/email-command-center).

{% hint style="info" %}
### Notice

Requires the Cortex Advanced Email Security add-on.
{% endhint %}

| Permission | Description                              | Roles Example                       |
| ---------- | ---------------------------------------- | ----------------------------------- |
| None       | No access to the Email Command Center.   |                                     |
| View       | View access to the Email Command Center. | Most roles should have view access. |

### Required and recommended permissions

Consider adding the following permissions:

| Permission                | Permission Level | Reason                                                                                                            |
| ------------------------- | ---------------- | ----------------------------------------------------------------------------------------------------------------- |
| Dashboards                | Enabled          | Required for the dashboard.                                                                                       |
| Command Center Dashboards | View             | Email Command Center is part of the Command Center framework. Required.                                           |
| Cases & Issues            | View             | Email-related cases and issues require this for click-through and context. Strongly recommended.                  |
| Query Center              | View             | Recommended for drilling down into raw email logs via XQL when a widget identifies a suspicious trend.            |
| Threat Intelligence       | View             | Recommended for the context of the malicious indicators (URLs, Attachments) displayed within the email dashboard. |
