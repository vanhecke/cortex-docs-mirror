---
description: Manage access to Cortex XSIAM credentials and secure connection settings.
---

# Credentials permissions

Controls access to stored credential sets (reusable authentication objects that integrations and systems reference for connecting to external services). Credential sets centralize sensitive authentication data (such as, usernames, passwords, certificates, and API tokens) so they can be managed in one place rather than being embedded in each integration configuration.

Users can access Credentials on the **Credentials** page by going to **Settings** → **Configurations** → **Integrations** → **Credentials**.

To view the **Credentials** page, users require the following **View** permissions:

* Integrations
* Data Sources
* External Issue Mapping

Without these permissions, users can't view the Credentials page.

For more information, see [Manage credentials](../../../configure-cortex-xsiam/cortex-xsiam-data-sources/administration-and-troubleshooting/integrations/manage-credentials).

| Permission | Description                                                                                                                                                                                                                                                                         | Role Example                                                                                                                                                               |
| ---------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| None       | Completely revokes access to stored secrets. The **Credentials** page is hidden from the UI, all related Public API endpoints are blocked, and users cannot view or reference stored credentials in integrations, scripts, or playbooks.                                            | CLI Role, CLI Read Only Role                                                                                                                                               |
| View       | <p>Enables backend API read access to credential sets (e.g., for automation or API-based workflows).</p><p>If users have access to the Credentials page, they can view a list of stored credential sets and their names. Users can't create, modify, or delete credential sets.</p> | <ul><li>SOC Tier-1, 2, and 3 Analysts: May need to verify credential status/credential configurations.</li><li>Threat Hunter: Verify integration authentication.</li></ul> |
| View/Edit  | If users have access to the Credentials page, they can manage credential sets, including creating, deleting, and editing credentials.                                                                                                                                               | Security Engineer: Manage integration credentials.                                                                                                                         |

#### Required and recommended permissions

Credentials often serve as dependencies for other automation and integration tasks. Consider adding these permissions:

| Permission             | Permission Level  | Reason                                                                                                                                                                                                                                         |
| ---------------------- | ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Integrations           | View or View/Edit | <ul><li>View: Core permission to access the Credentials page. Required.</li><li>View/Edit: Highly Recommended. Users who manage credentials typically also need to configure integration instances that reference those credentials.</li></ul> |
| Data Sources           | View              | View: Core permission to access the Credentials page. Required.                                                                                                                                                                                |
| External Issue Mapping | View              | View: Core permission to access the Credentials page. Required.                                                                                                                                                                                |
| Playbooks              | Enabled           | Strongly recommended to view integrations that use the stored credentials.                                                                                                                                                                     |
| Scripts                | Enabled           | Strongly recommended to view scripts that may use credentials for external API calls.                                                                                                                                                          |
| Marketplace            | View              | Recommended. Allows browsing and installing integration content packs from the Marketplace, which may include integrations that use credential sets.                                                                                           |
| Audit                  | View              | Recommended to track credential creation, modification, and usage for security compliance.                                                                                                                                                     |
