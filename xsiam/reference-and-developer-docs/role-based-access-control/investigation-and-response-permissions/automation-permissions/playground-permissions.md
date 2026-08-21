---
description: Manage access to the Cortex XSIAM playground for testing commands and scripts.
---

# Playground permissions

Controls Playground **Investigation & Response** → **Automation** → **Playground**, which is a testing environment for commands and scripts that is not connected to a live (active) investigation.

| Permission | Description                                                                                      | Roles Example                                                                                                                |
| ---------- | ------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------- |
| None       | Users cannot access the **Playground** page and cannot test commands, scripts, and integrations. | SOC Tier-1 analysts: Do not need Playground access for basic triage.                                                         |
| View/Edit  | Users can access the **Playground** page and can test commands, scripts, and integrations.       | SOC Tier 2 and 3 Analysts, Security Engineers, and Security Admins: Benefit from playground access for testing and learning. |

**Required and recommended permissions**

Consider adding the following permissions:

| Permission     | Permission Level | Reason                                                     |
| -------------- | ---------------- | ---------------------------------------------------------- |
| Scripts        | Enabled          | Strongly recommended to see the scripts being tested.      |
| Playbooks      | Enabled          | Strongly recommended to test playbook commands in context. |
| Cases & Issues | View             | Recommended, as commands reference case data.              |
| Query Center   | View             | Recommended for XQL query testing.                         |
