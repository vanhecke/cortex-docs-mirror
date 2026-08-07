# Data Management permissions

Controls access to dataset configuration, data transformation rules, and data lifecycle management in Cortex XSIAM through **Settings** → **Configurations** → **Data Management**.

This permission includes:

* Dataset Management: For viewing and managing datasets
* Parsing Rules: For data transformation during ingestion
* Data Model Rules: For data normalization
* Event Forwarding: For sending data to external systems

This permission only offers None or View/Edit access. While SOC Tier-2, Tier-3, and Threat Hunters may need to view data schemas for advanced investigations, granting them View/Edit access gives them full control to alter parsing rules, modify datasets, and change ingestion pipelines. Grant this permission with caution and ensure proper change management protocols are in place.

| Permission | Description                                                                                                          | Roles Example                                                                                                                                                                                                                                                                                                               |
| ---------- | -------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| None       | Users cannot access any Data Management configuration pages.                                                         | SOC Tier-1 Analyst: Data management configuration is outside Tier-1 responsibilities.                                                                                                                                                                                                                                       |
| View/Edit  | Full control over creating/managing datasets, modifying parsing rules, and configuring advanced ingestion pipelines. | <ul><li>SOC Tier-2 and 3 Analysts: May need to understand data schemas during investigations/advanced analysis.</li><li>Threat Hunter: May need to understand data schemas and transformations for hunting.</li><li>Security Engineer: Primary responsibility for configuring data pipelines and transformations.</li></ul> |

Required and recommended permissions

Consider adding the following permissions:

| Permission     | Permission Level | Permissions                                                                                          |
| -------------- | ---------------- | ---------------------------------------------------------------------------------------------------- |
| Public APIs    | View/Edit        | Compute Unit Usage page access; without this, the Compute Unit Usage page is inaccessible. Required. |
| Forensics      | View/Edit        | Data Export functionality; without this, the Data Export page is inaccessible. Required.             |
| Agent Profiles | View/Edit        | Some dataset operations reference profiles; needed for full context. Strongly recommended.           |
| Query Center   | View/Edit        | Running XQL queries against managed datasets. Strongly recommended.                                  |
| Data Sources   | View/Edit        | Understanding which data sources feed into managed datasets. Recommended.                            |
