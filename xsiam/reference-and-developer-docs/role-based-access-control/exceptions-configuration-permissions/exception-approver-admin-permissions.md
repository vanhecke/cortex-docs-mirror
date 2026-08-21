---
description: Configure Exception Approver Admin permissions in Cortex XSIAM.
---

# Exception Approver Admin permissions

Controls access to the **Exception Management** section on the **Server Settings** page, located at **Settings** → **Configurations** → **General** → **Server Settings**.

This permission governs who can configure the exception approval workflow, specifically, whether exceptions require approval, and managing the list of designated approvers.

{% hint style="warning" %}
### Caution

Users also need **General Configuration** View permission to view or View/Edit **Exception Management** in **Server Settings**.
{% endhint %}

| Permission | Description                                                                                                                                                                       | Roles Example                                                                                                                                                                   |
| ---------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| None       | No access to the **Exception Management** section on the **Server Settings** page. Users cannot view or modify the approval workflow configuration and the list of approvers.     | SOC Tier 1 and Tier Analysts: No need for visibility into approval workflow configuration.                                                                                      |
| View       | The **Exception Management** section is visible on the **Server Settings** page. Users can view the approval configuration workflow and the list of approvers (names and emails). | SOC Tier 3 Analyst and Threat Hunter: Can view the approval workflow to understand the exception approval process and whether the exceptions they encounter have been approved. |
| View/Edit  | Read and write access to the **Exception Management** section on the **Server Settings** page. Users can configure the exception approval workflow and manage approvers.          | Security Engineer: Full access to toggle approval requirements and manage the approvers list.                                                                                   |

**Required and recommended permissions**

Consider adding the following permissions:

| Permissions                | Permission Level  | Reason                                                                                                                                                                                                                                                                                                                                                  |
| -------------------------- | ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| General Configuration      | View or View/Edit | <ul><li>View: The <strong>Exception Management</strong> section is on the <strong>Server Settings</strong> page. Without this permission, users cannot view the section. Required.</li><li>View/Edit: Users who configure exception approval workflows may also need to manage other server settings (email contacts, Google Maps key, etc.).</li></ul> |
| Issue Exclusion            | View              | Approver administrators should understand the exclusion/exception rules they are configuring for approval workflows. Without this, they are configuring approval settings without visibility into the rules being approved. Strongly recommended.                                                                                                       |
| Exception Management Admin | View              | Understanding the exception rules that will go through the approval workflow helps configure appropriate approvers and approval requirements. Strongly recommended.                                                                                                                                                                                     |
