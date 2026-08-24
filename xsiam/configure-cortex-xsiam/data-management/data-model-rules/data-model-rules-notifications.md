---
description: Configure notifications for Cortex XSIAM Data Model Rules.
---

# Data Model Rules notifications

{% hint style="warning" %}
### Prerequisite

Data Model Rules requires **View/Edit** RBAC permissions for **Data Management** (under **Configurations** → **Data Management**), which are the same permissions required for Dataset Management, Parsing Rules, and Event Forwarding.
{% endhint %}

To help you monitor effectively your Data Model Rules, Cortex XSIAM sends notifications to your Cortex XSIAM console Notification Center.

Cortex XSIAM sends the following notification:

* **Invalid Data Model Rules**: Notifies when a Data Model Rule is invalid and will be excluded from `datamodel` queries.

To ensure you and your colleagues stay informed about Data Model Rules activity, you can also [Configure notification forwarding](../../../onboard-cortex-xsiam/post-deployment/data-and-log-forwarding/forward-logs-and-data-from-cortex-xsiam-to-external-services/configure-notification-forwarding) to forward your Data Model Rules logs to an email distribution list or Syslog server. For more information about the Data Model Rules audit logs, see [Monitor Data Model Rules activity](monitor-data-model-rules-activity).
