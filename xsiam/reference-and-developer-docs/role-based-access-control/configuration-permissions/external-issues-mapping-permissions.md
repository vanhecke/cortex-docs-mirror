---
description: Manage access to Cortex XSIAM mappings for external issue integrations.
---

# External Issues Mapping permissions

Configure how alerts from third-party systems are translated into Cases through **Settings** → **Configurations** → **Data Collection** → **External Issues Mapping**.

For more information, see [External alerts using External Issue Mapping](../../../configure-cortex-xsiam/cortex-xsiam-data-sources/external-alerts-using-external-issue-mapping).

| Permission | Description                                                                                                                                                                                                                                                                                                                        | Roles Example                                                                                                                                                                   |
| ---------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| None       | Users cannot access the **External Issue Mapping** page.                                                                                                                                                                                                                                                                           | SOC Tier-1 Analyst: External mapping configuration is not within Tier-1 scope.                                                                                                  |
| View       | Users can access the **External Issue Mapping** page and view all configured issue mappings and parsers. They can review how external alerts from third-party systems (such as Splunk, QRadar, or other SIEMs) are being mapped to issue fields. They can examine parser configurations, field mappings, and transformation rules. | <ul><li>SOC Tier 2 and 3 Analysts: Can review mappings for investigation purposes.</li><li>Threat Hunter: Understanding issue sources is valuable for threat hunting.</li></ul> |
| View/Edit  | Users have full control over external issue mapping configurations. They can create new parsers and mapping rules, modify existing field mappings and transformation logic, enable or disable specific mappings, configure how external issue fields map to issue properties, and delete mapping configurations.                   | Security Engineer: Responsible for configuring alert mappings and parsers.                                                                                                      |

### Required and recommended permissions

Consider adding the following permissions:

| Permission      | Permission Level | Reason                                                                              |
| --------------- | ---------------- | ----------------------------------------------------------------------------------- |
| Cases & Issues  | View             | View the issues that result from external mappings. Required.                       |
| Detection Rules | View             | Understanding correlation rules that may use external issues. Strongly Recommended. |
| Data Sources    | View             | Understanding which data sources feed into external issue mappings. Recommended.    |
