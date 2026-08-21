---
description: >-
  Control access to sync profiles for mirroring cases with external platforms 
  in Cortex XSIAM.
---

# Sync Profile permissions

Controls access to case mirroring profiles configuration in **Settings** → **Configurations** → **Object Setup** → **Issues** → **Sync Profiles**.

Sync Profiles define the parameters for case mirroring with third-party platforms such as Jira and ServiceNow. When a profile is active, updates to cases in the tenant are automatically reflected in the external system, and depending on the profile type (inbound or bidirectional), changes in the external system can update XSIAM cases.

For more information, see [Create a sync profile](../../../../configure-cortex-xsiam/customize-cases-and-issues/create-a-sync-profile).

| Permission | Description                                                                                          | Roles Example                                                                                                                                                                           |
| ---------- | ---------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| None       | No access to Sync Profiles. Users cannot view, create, or select profiles for use in automation.     | <ul><li>SOC Tier 1 and 2 Analyst: Mirroring configuration is typically handled by engineers.</li><li>Threat Hunter: Layout configuration is outside the threat hunting scope.</li></ul> |
| View       | Read-only access. Users can view the Sync Profiles table and open profile details in read-only mode. | SOC Tier-3 Analyst: Should understand mirroring configurations for escalation workflows and cross-system case tracking.                                                                 |
| View/Edit  | Full read/write access to view, create, edit, and delete sync profiles.                              | Security Engineer: Configures and manages mirroring with external ticketing systems (Jira, ServiceNow).                                                                                 |

### Required and recommended permissions

Consider adding the following permissions:

| Permission       | Permission Level  | Reason                                                                                                                                                                                                          |
| ---------------- | ----------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Integrations     | View or View/Edit | <ul><li>View: Required to view the connector integrations (Jira, ServiceNow) used by sync profiles.</li><li>View/Edit: Strongly recommended to configure the connector instances needed for mirroring</li></ul> |
| Cases & Issues   | View              | Required to view cases that use sync profiles for mirroring.                                                                                                                                                    |
| Fields and Types | View              | Strongly recommended to understand field mappings in sync profiles (which XSIAM fields map to external fields).                                                                                                 |
| Case Properties  | View              | Strongly recommended to understand the custom statuses that are mapped in sync profiles.                                                                                                                        |
| Credentials      | View              | Strongly recommended to view credentials used by connector integrations.                                                                                                                                        |
| Playbooks        | Enabled           | Recommended to configure mirroring playbooks that use sync profiles.                                                                                                                                            |
| Audit            | View              | Recommended to track sync profile changes.                                                                                                                                                                      |
