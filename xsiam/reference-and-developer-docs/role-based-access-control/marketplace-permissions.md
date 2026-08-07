---
description: Configure Marketplace permissions for RBAC.
---

# Marketplace permissions

Configure access to manage content packs in Marketplace.

Marketplace is the central hub for discovering, installing, and managing content packs in Cortex XSIAM. Content packs include integrations, playbooks, scripts, dashboards, and other automation content that extend capabilities. Installing a content pack is typically the first step; further configuration of the included integrations or credentials must be completed in the Configurations section.

{% hint style="warning" %}
### Caution

Granting View/Edit access to the Marketplace allows users to install new content packs. As content packs often contain Python scripts and automated playbooks, this permission effectively allows users to introduce new executable code into the tenant. This should be restricted to Security Engineers and Administrators.
{% endhint %}

| Permissions | Description                                                                                                                                         | Roles Example                                                                                                                  |
| ----------- | --------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| None        | No access to the Marketplace, and users cannot view content packs.                                                                                  |                                                                                                                                |
| View        | Read-only access to browse, search, and view pack details and version history.                                                                      | SOC Tier 1, 2, and 3 Analysts, and Threat Hunters: Browse available content and reference content packs during investigations. |
| View/Edit   | Full access to install, uninstall, upload, and upgrade content packs. Users can also contribute content from other pages (e.g., scripts/playbooks). | Security Engineer: Full content management, including custom contributions.                                                    |

**Required and recommended permissions**

Consider adding the following permissions:

| Permission   | Permission Level | Reason                                                                      |
| ------------ | ---------------- | --------------------------------------------------------------------------- |
| Integrations | View             | Strongly recommended to view and configure installed integration instances. |
| Playbooks    | Enabled          | Recommended to view installed playbooks.                                    |
| Scripts      | Enabled          | Recommended to view installed scripts.                                      |
| Credentials  | View             | Strongly recommended to configure integration credentials.                  |
