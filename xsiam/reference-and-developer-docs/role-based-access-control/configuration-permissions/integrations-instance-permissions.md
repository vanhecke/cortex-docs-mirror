# Integrations - instance permissions

Controls access to data collection integration instances, such as automation and feed integrations that collect and process data on the **Data Sources & Integrations** page (**Settings** → **Data Sources & Integrations**). It also controls access to classifiers and mappers **Settings** → **Configurations** → **Object Setup** → **Issues** → **Classification & Mapping**.

**Data Sources & Integrations page**

The Data Sources & Integrations page is a unified interface. Access levels are determined as follows:

* Data Sources permission only: Users can view the page and manage cloud accounts (CSP), Cloud Workload Protection (CWP) instances, and Cloud Access Security (CAS) connectors.
* Integrations permission only: Users can view the page and manage data collection integration instances, specifically automation and feed integrations.
* Both permissions: Users have full visibility and can manage both data sources and integrations on the same page.

There are two integration permissions:

* Integrations (under Data Collection): Configure data collection integrations
* Integration Permissions (under Integrations): Configure command permission for integrations.

| Permission | Description                                                                                                                                                                                                                                                                                                | Roles Example                                                                                                                                                                                            |
| ---------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| None       | Users cannot view or configure any data collection integrations, including feed and automation integrations, on the Data Sources & Integrations page.                                                                                                                                                      | SOC Tier-1 Analyst: Integration configuration is outside Tier-1 responsibilities.                                                                                                                        |
| View       | Read-only access to the Data Sources & Integrations page. Users can see integration instances, their status, configuration details, and associated classifiers/mappers.                                                                                                                                    | <ul><li>SOC Tier 2 and 3 Analysts: Verify integration status during case response/advanced analysis.</li><li>Threat Hunter: May need to understand data collection sources for threat hunting.</li></ul> |
| View/Edit  | <p>Full control over integration configurations. Users can create, modify, and delete integration instances, manage credentials, and configure classifiers and mappers for data ingestion.</p><p>Users can view the Credentials page, but cannot edit it without the Credentials View/Edit permission.</p> | Security Engineer: Primary responsibility for configuring integrations.                                                                                                                                  |

**Required and recommended permissions**

Managing integrations effectively often requires visibility into overlapping functional areas. Consider adding the following permissions:

| Permission      | Permission Level | Reason                                                                                                                                                      |
| --------------- | ---------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Data Sources    | View/Edit        | These are often used together on the Data Sources & Integrations page. Strongly recommended.                                                                |
| Marketplace     | View/Edit        | Strongly recommended. Necessary to install new integration content packs. Strongly recommended.                                                             |
| Log Collections | View/Edit        | Strongly recommended. Log collection integrations that may be configured alongside data collection integrations. Strongly recommended.                      |
| Credentials     | View/Edit        | Strongly recommended for users who need full integration management capabilities, including credential lifecycle management (creation, rotation, deletion). |
