---
description: >-
  Manage Cortex XSIAM alert notification rules, templates, and forwarding
  settings.
---

# Alert Notifications permissions

Controls access to configure notification rules, templates, and external integration forwarding.:

* Configurations: Manage rules through **Settings** → **Configuration** → **General** → **Notifications**: Includes main notification rules and user notifications.
* External forwarding: Configure through **Settings** → **Configuration** → **Integrations** → **External Applications**.

{% hint style="warning" %}
### Caution

Configuring alert notifications requires underlying infrastructure. If forwarding notifications via Syslog, users need access to the Broker Service. For Slack or Email, users need access to the Integrations permissions.
{% endhint %}

| Permission | Description                                                        | Roles Example                                                                                                                                                                                                                                 |
| ---------- | ------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| None       | No access to notification configuration.                           | <ul><li>SOC Tier-1 or SOC Tier-2 Analyst: Typically don't need to configure notifications or check notification forwarding destinations.</li><li>Threat Hunter: Notification configuration is not typically part of threat hunting.</li></ul> |
| View       | Read-only access to notification settings.                         | <ul><li>SOC Tier-3 Analyst: May review notification forwarding.</li></ul>                                                                                                                                                                     |
| View/Edit  | Full access to create, modify, and delete notification forwarding. | Security Engineer: Often responsible for configuring notification integrations.                                                                                                                                                               |

### Required and recommended permissions

Consider adding the following permissions:

| Permission     | Permission Level  | Reason                                                                                                                                                              |
| -------------- | ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Cases & Issues | View              | Notifications can be configured for case-related events; understanding case workflow is essential. Strongly recommended.                                            |
| Broker Service | View or View/Edit | <ul><li>View: Required if using Broker VM for Syslog forwarding of notifications.</li><li>View/Edit: Configure Broker-based Syslog notification channels.</li></ul> |
| Integrations   | View              | Provides visibility into integration health. Consider View/Edit to configure new integration instances used by notification channels. Strongly recommended.         |
| Query Center   | View              | Query notification-related data and troubleshoot notification delivery. Recommended.                                                                                |
| Auditing       | View              | Track changes to notification configurations for compliance. Recommended.                                                                                           |
| Dashboards     | Enabled           | View notification-related dashboards and delivery metrics. Recommended.                                                                                             |
