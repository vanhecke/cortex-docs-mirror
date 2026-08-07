# Access management permissions

Set permissions for Users, Roles, User Groups, and Authentication Settings under Access Management (**Settings** → **Configurations** → **Access Management**).

{% hint style="warning" %}
### Caution

* SSO Configuration Risk: Granting View/Edit access allows users to modify the tenant's Single Sign-On (SSO) and authentication settings. Misconfigurations can cause tenant-wide lockouts. Ensure only authorized identity or infrastructure administrators hold this permission.
* Auditing is Mandatory: It is highly recommended that any user managing access also has visibility into the Auditing module to track changes.
* IT Admin: Unlike other modules, IT Admins require full View/Edit access here for user provisioning and SSO duties.
{% endhint %}

| Permission | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                   | Roles Example                                                                                                                                                 |
| ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| None       | No access to Access Management.                                                                                                                                                                                                                                                                                                                                                                                                                               | SOC Tier-1 and 2 Analysts and Threat Hunter: No need to manage users or roles.                                                                                |
| View       | Read-only access to users, roles, and groups.                                                                                                                                                                                                                                                                                                                                                                                                                 | <ul><li>SOC Tier-3 Analyst: May need to understand team structure.</li><li>Security Engineer: Should understand role structure but not manage users</li></ul> |
| View/Edit  | <p>Full access to create, modify, and delete users, roles, and groups, including configuring SSO settings.</p><div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong><br>Users with this permission are restricted from granting, modifying, or removing the <strong>Instance Administrator</strong> role for any user, user group, or API key, and cannot delete API keys that have this role.</p></div> |                                                                                                                                                               |

### Required and recommended permissions

Consider adding the following permissions:

| Permission            | Permission Level | Reason                                                                                                      |
| --------------------- | ---------------- | ----------------------------------------------------------------------------------------------------------- |
| Auditing              | View             | Track user and role changes for compliance; critical for access control audit trails. Strongly recommended. |
| Cases & Issues        | View             | Understand case workflows when configuring role permissions for case management. Recommended.               |
| General Configuration | View             | System settings context when managing platform access. Recommended.                                         |
| Dashboards            | Enabled          | View user activity dashboards and access patterns. Recommended.                                             |
| Query Center          | View             | Query user activity data for access reviews. Recommended.                                                   |
