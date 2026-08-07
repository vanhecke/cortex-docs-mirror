---
description: >-
  Cortex XSIAM generates issues to bring your attention to security risks in
  your framework.
---

# Investigate issues

{% hint style="warning" %}
### Prerequisite

To work with issues, an administrator must configure your user role with specific RBAC permissions. Permissions must be enabled in the following order:

1. **Playbooks**: This component (under **Investigation & Response** → **Automations**) must be set to **Enabled** first. Role-level permissions determine your ability to create new playbooks or edit those marked as **Public**. Specific access to individual custom playbooks and scripts is managed at the object level. For detailed information on the access model, see [Access to playbooks](../../configure-cortex-xsiam/automations/playbooks/access-to-playbooks).
2. **Cases and Issues**: Once **Playbooks** are enabled, you can set **Cases and Issues** (under **Cases & Issues**) to **View** or **View/Edit**.

For more information on setting RBAC permissions, see [Role permissions by component](../../reference-and-developer-docs/role-based-access-control/role-permissions-by-component).
{% endhint %}

Issues help you to monitor and control the security of your system framework by notifying you about risks to security in your framework. Cortex XSIAM generates issues from the following:

* Rules that you set up, such as BIOC, IOC, correlation rules, malware rules, automation rules, and vulnerability rules.
*   Findings

    Findings themselves are not issues, but findings that match a specific logic can generate issues.
* Agents
* Firewalls
* Analytics
*   Integrations

    Integrations enable you to ingest events, such as phishing emails, SIEM events, from third-party security and management vendors. You might need to configure the integrations to determine how events are classified as events. For example, for email integrations, you might want to classify items based on the subject field, but for SIEM events, you want to classify by event type.
