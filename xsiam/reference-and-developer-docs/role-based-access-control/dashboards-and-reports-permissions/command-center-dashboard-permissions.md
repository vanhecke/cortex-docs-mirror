---
description: >-
  Manage access to Cortex XSIAM Command Center dashboards and their security
  metrics.
---

# Command Center Dashboard permissions

Controls access to XSIAM Command Center and Cortex Command Center.

For more information about these dashboards, see [Command Center reference](../../../detect-investigate-and-respond-to-threats/monitor-dashboards-and-reports/dashboard-reference/command-center-reference).

| Permission | Description                                                                 | Roles Example                           |
| ---------- | --------------------------------------------------------------------------- | --------------------------------------- |
| None       | No access to the XSIAM Command Center and Cortex Command Center Dashboards. |                                         |
| View       | View access to XSIAM Command Center and Cortex Center Dashboards.           | Most roles should have view permission. |

### Required and recommended permissions

As the Command Center is an aggregate view, it requires several other permissions to function correctly:

| Permission            | Permission Level | Reason                                                                                      |
| --------------------- | ---------------- | ------------------------------------------------------------------------------------------- |
| Dashboards            | Enabled          | Command Center requires Dashboards View as a prerequisite. Required                         |
| Cases & Issues        | View             | Case KPIs and click-through to cases require this permission. Strongly recommended.         |
| Agent Administrations | View             | Endpoint KPIs and click-through to endpoints require this permission. Strongly recommended. |
| Playbooks             | Enabled          | Playbook status widgets in the Command Center require this permission. Recommended.         |
| Ingestion Monitoring  | View             | Data ingestion KPIs in Command Center require this permission. Recommended.                 |
