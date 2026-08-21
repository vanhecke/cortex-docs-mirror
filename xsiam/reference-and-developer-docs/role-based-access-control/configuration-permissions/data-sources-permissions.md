---
description: >-
  Manage access to Cortex XSIAM data source configuration and ingestion
  settings.
---

# Data Sources permissions

Enables the configuration and management of cloud and third-party data source integrations. This includes Cloud Service Provider (CSP) integrations (AWS, Azure, GCP), Cloud Workload Protection (CWP) instances, Cloud Access Security (CAS) connectors, and Outposts.

### Data Sources & Integrations page

Data Sources is managed under **Settings** → **Configurations** → **Data Collection** → **Data Sources & Integrations**. Access levels to the **Data Sources & Integrations** are determined with the Integrations permissions:

* Data Sources permission only: Users can view the page and manage cloud accounts (CSP), Cloud Workload Protection (CWP) instances, and Cloud Access Security (CAS) connectors.
* Integrations permission only: Users can view the page and manage data collection integration instances, specifically automation and feed integrations.
* Both permissions: Users have full visibility and can manage both data sources and integrations on the same page.

| Permission | Description                                                                                                                                                                                     | Roles Example                                                                                                                                                                                                         |
| ---------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| None       | Users cannot access the **Data Sources & Integrations** and **Outposts** pages.                                                                                                                 | SOC Tier-1 Analyst: Data source configuration is outside Tier-1 responsibilities.                                                                                                                                     |
| View       | Read-only access to view all configured instances, connection status, last sync times, and configuration details on the **Data Sources & Integrations** and **Outposts** pages.                 | <ul><li>SOC Tier-2 and 3 Analysts: May need to verify data source status/configurations during investigations.</li><li>Threat Hunter: May need to understand data sources for comprehensive threat hunting.</li></ul> |
| View/Edit  | Full control over data source management. Users can add new sources via the wizard, modify settings (credentials, sync intervals), enable/disable sources, and manage associated content items. | Security Engineer: Primary responsibility for configuring and maintaining data sources.                                                                                                                               |

### Required and recommended permissions

Consider adding the following permissions:

| Permission                        | Permission Level | Reason                                                                                                            |
| --------------------------------- | ---------------- | ----------------------------------------------------------------------------------------------------------------- |
| Integrations                      | View/Edit        | Data Sources & Integrations is a shared page; need to manage integrations on the same page. Strongly recommended. |
| Marketplace                       | View/Edit        | Browse and install new data source content packs from the Marketplace. Strongly recommended.                      |
| Log Collections                   | View             | Managing XDR Collectors that may feed into data sources. Recommended.                                             |
| Ingestion Monitoring (dashboards) | View             | Viewing data ingestion dashboards. Recommended.                                                                   |
