---
description: Manage access to Cortex XSIAM Threat Intelligence API configuration.
---

# Threat Intelligence permission - API configuration

Controls access to the configuration page for external threat intelligence API keys (Virus Total) on Settings → Configurations → Integrations → Threat Intelligence. This configuration enables the enrichment of indicators within the tenant using Virus Total.

| Permission | Description                                                                                | Role Example                                                                                                           |
| ---------- | ------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------- |
| None       | The user cannot access or view the Threat Intelligence configuration page.                 | SOC Tier-1 Analyst: Uses TI data but doesn't configure.                                                                |
| View       | Users can see if a VirusTotal API key is configured but cannot add, edit, or test the key. | SOC Tier-2 and 3 Analysts: May need to review TI configurations.                                                       |
| View/Edit  | Full access to add, edit, test, and save VirusTotal API key configurations.                | <ul><li>Threat Hunter: Configure and use TI feeds</li><li>Security Engineer: Configure TI feed integrations.</li></ul> |

#### Required and recommended permissions

Managing threat intelligence effectively requires access to the modules that consume this data. Consider adding the following permissions:

| Permission          | Permission Level | Reason                                                                                                     |
| ------------------- | ---------------- | ---------------------------------------------------------------------------------------------------------- |
| Threat Intelligence | View/Edit        | Strongly recommended to access the Threat Intel module to manage indicators and IOCs that consume TI data. |
| Detection Rules     | View/Edit        | Strongly recommended to manage IOC and BIOC detection rules that leverage threat intelligence feeds.       |
| Integrations        | View             | Recommended to view integration instances that ingest threat intelligence data.                            |
| Credentials         | View             | Recommended to view credentials used by TI feed integrations.                                              |
| Query Center        | View             | Recommended to query threat intelligence data via XQL for hunting and analysis.                            |
