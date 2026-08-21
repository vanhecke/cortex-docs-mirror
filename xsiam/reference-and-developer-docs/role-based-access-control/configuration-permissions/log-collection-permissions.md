---
description: Manage access to Cortex XSIAM log collection configuration and data sources.
---

# Log Collection permissions

Configure XDR Collectors, installers, and collection policies through **Settings** → **Configurations** → **XDR Collectors**.

| Permission | Description                                                                                                                  | Roles Example                                                                                                                                                                                          |
| ---------- | ---------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| None       | No access to the XDR Collectors configuration pages.                                                                         | SOC Tier-1 Analyst: Focus on issue triage; log collection configuration is not within their scope.                                                                                                     |
| View       | Read-only access to the XDR Collector menu, including configuration, administration, and groups.                             | <ul><li>SOC Tier 2 and 3 Analyst: May need to verify collection status when investigating cases.</li><li>Threat Hunter: May need to verify data collection during threat hunting activities.</li></ul> |
| View/Edit  | Full read and write access. The user can view, create, modify, and delete configurations, collection profiles, and policies. | Security Engineer: Responsible for configuring and maintaining log collection infrastructure.                                                                                                          |

### Required and recommended permissions

Consider adding the following permissions:

| Permission            | Permission Level | Reason                                                                                              |
| --------------------- | ---------------- | --------------------------------------------------------------------------------------------------- |
| Broker Service        | View/Edit        | Managing broker VMs that host collectors; collectors often run on Broker VMs. Strongly recommended. |
| Agent Profiles        | View/Edit        | Managing collection profiles referenced by policies. Strongly recommended.                          |
| Agent Administrations | View             | Viewing endpoint agents that may be related to collection. Recommended.                             |
| Data Sources          | View             | Viewing data source status related to collected logs. Recommended.                                  |
