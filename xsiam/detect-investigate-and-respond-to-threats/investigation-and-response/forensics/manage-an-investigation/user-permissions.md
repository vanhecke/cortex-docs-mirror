# User permissions

By default, investigation permissions utilize the role-based access control (RBAC) settings configured in the system. Users must have a role with the Forensic permissions set to **View** in order to view forensic investigations. In order to create investigations or collections, a user must have a role where the Forensics permissions is set to **View/Edit**. Without either role, a user cannot interact with the forensics interface.

If Scope-Based Access Control (SBAC) is enabled on your system, from the **Permissions** table, you can select the users from which to assign permissions to the investigation.

Users with account administrator or instance administrator roles have access to investigations and can't be cleared from the **Permissions** table. They can view and edit all Investigations, including adding/removing users, creating/deleting collections, closing the Investigation. This prevents investigation lockout in the event of a user leaving before the Investigation is complete.

{% hint style="info" %}
Even if a user does not have access to view an investigation via the **Forensics Investigations** page, they can still query the results of the collections using an XQL query.
{% endhint %}

The **Permissions** fields describe the following information:

<table><thead><tr><th width="156">Field</th><th>Description</th></tr></thead><tbody><tr><td>User Name</td><td>Name of the user as logged in the <strong>Settings → Configurations</strong> → <strong>Access Management</strong> → <strong>Users</strong>.</td></tr><tr><td>Email</td><td>The user's email as logged in the <strong>Settings</strong> <strong>→ Configurations →</strong> <strong>Access Management</strong> → <strong>Users</strong>.</td></tr><tr><td>User Type</td><td>Indicates whether the user was defined in Cortex XSIAM using the CSP (Customer Support Portal), SSO (single sign-on) using your organization’s IdP, or both CSP/SSO.</td></tr><tr><td>Role</td><td>Name of the role assigned specifically to the user that is not inherited from somewhere else, such as a User Group. When the user does not have any Cortex XSIAM access permissions that are assigned specifically to them, the field displays No-Role.</td></tr><tr><td>Permissions</td><td>Options are None, View, View/Edit</td></tr></tbody></table>
