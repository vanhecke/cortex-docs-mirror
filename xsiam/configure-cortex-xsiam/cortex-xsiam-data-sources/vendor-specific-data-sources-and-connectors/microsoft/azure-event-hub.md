---
description: Use Azure Event Hub data with Cortex XSIAM.
---

# Azure Event Hub

You can configure collecting Azure Event Hub logs using a standard data source or content pack (onboarded prior to July 26, 2026):

| Collection Method                                               | Description                                                                                                                                                                                                                                                                                                                                                                                                  |
| --------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Standard data source overview                                   | Forward different types of logs to Cortex XSIAM from Azure Event Hub using the Microsoft Azure Event Hub data source.                                                                                                                                                                                                                                                                                        |
| Link to standard data source instructions                       | <p>The following types of logs can be ingested from Azure Event Hub:</p><ul><li>Activity logs</li><li>Microsoft Entra ID Activity logs and Microsoft Entra ID Sign-in logs</li><li>Resource logs, including AKS audit logs</li></ul><p>For more information, see <a href="azure-event-hub/ingest-logs-from-microsoft-azure-event-hub">Ingest logs from Microsoft Azure Event Hub</a>.</p>                    |
| Link to content pack details (onboarded prior to July 26, 2026) | [Azure Logs](https://cortex.marketplace.pan.dev/marketplace/details/MicrosoftEntraID): Use this content pack to ingest and normalize various Azure logs to the Cortex Data Model (XDM) schema, including Azure Entra ID events ingested via the Office 365 data source, and Azure Logs ingested via the Microsoft Azure Event Hub data source. It includes modeling and parsing rules for log normalization. |
