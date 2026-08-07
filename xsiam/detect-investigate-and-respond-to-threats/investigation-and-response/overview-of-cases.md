---
description: Understand how cases work in Cortex XSIAM.
---

# Overview of cases

Understand how cases work in Cortex XSIAM.

{% hint style="warning" %}
### Prerequisite

To work with cases, an administrator must configure your user role with specific RBAC permissions. Permissions must be enabled in the following order:

1. **Playbooks**: This component (under **Investigation & Response** → **Automations**) must be set to **Enabled** first. Role-level permissions determine your ability to create new playbooks or edit those marked as **Public**. Specific access to individual custom playbooks and scripts is managed at the object level. For detailed information on the access model, see [Access to playbooks](../../configure-cortex-xsiam/automations/playbooks/access-to-playbooks).
2. **Cases and Issues**: Once **Playbooks** are enabled, you can set **Cases and Issues** (under **Cases & Issues**) to **View** or **View/Edit**. This is also required to view the results of playbooks executed within a case.

For more information on setting RBAC permissions, see [Role permissions by component](../../reference-and-developer-docs/role-based-access-control/role-permissions-by-component).
{% endhint %}
