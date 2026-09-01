---
description: Learn more about migrating to a new Microsoft 365 connector.
---

# Migrate to new Microsoft 365 connector

Migrate from the legacy **Microsoft365** connector to the new **Microsoft 365** connector to take advantage of improved performance, enhanced remediation capabilities, and unified Microsoft 365 configuration.

#### Why migrate? <a href="#why-migrate" id="why-migrate"></a>

By upgrading to the new connector, you benefit from:

* **Faster and more efficient scanning** with improved performance and reliability.
* **Enhanced remediation capabilities**, including:
  * Delete
  * Change public sharing
  * Quarantine
* **Microsoft Information Protection (MIP) label write support**, enabling automatic application of sensitivity labels directly from Cortex Cloud.
* **Unified Microsoft 365**, providing holistic security across identities, AI agents, security configurations, and Microsoft 365 applications such as Microsoft Teams, SharePoint, and OneDrive through a single configuration experience.

#### Migration steps <a href="#migration-steps" id="migration-steps"></a>

**Task 1. Remove the existing Microsoft365 Connector**

1. ​Remove your existing Microsoft 365 connector to prepare for the migration.
   * **Note:** Removing the connector clears the Microsoft 365 assets and objects previously discovered by the existing connector from the Data Security inventory. No data is deleted from your Microsoft 365 environment. The new connector automatically rediscovers and repopulates these assets during ingestion.
2. Wait approximately **24 hours** for the cleanup process to complete before proceeding to the next step.

**Task 2. Install the new Microsoft 365 Connector**

Install the new Microsoft 365 connector by following the configuration guide. For more information, see [Microsoft 365](../microsoft-365-new).

**Task 3. Monitor Data Ingestion**

The new connector begins ingesting existing and new Microsoft 365 data using Microsoft APIs. Depending on the size of your environment, the initial synchronization may take **a few days to several weeks**. We recommend monitoring the ingestion progress with the **Palo Alto Networks team** until your environment reaches full coverage.
