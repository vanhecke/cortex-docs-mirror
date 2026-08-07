# Connectors

Connectors represent the new, strategic approach for integrating third-party services and data sources into Cortex XSIAM. A connector consolidates all of a vendor's security capabilities, such as log collection, automation and remediation, and posture management, into a single, uniquely named entry with a guided configuration wizard.

### Benefits of the unified connector experience

This unified approach provides several key benefits:

* **Security-capability-driven setup**: If a connector wizard is available for your tenant, you can disregard the manual configuration steps on the [Cortex Developer Docs for Marketplace (PAN DEV)](https://cortex.marketplace.pan.dev/marketplace/) site. Yet, you should still refer to [PAN DEV](https://cortex.marketplace.pan.dev/marketplace/) for specific information related to the integration (now referred to as a **sub-capability** in the new connector world), such as:
  * Fetched incidents data
  * Commands
  * Other specific technical details related to the integration
* **Selective capability onboarding**: For vendors with multiple services (such as Microsoft 365 or Google Workspace), you can choose to enable the full suite at once or select individual **sub-capabilities** (integrations) as needed. Additional capabilities can be enabled later without disrupting your existing configuration.
* **Wizard-driven setup**: The configuration wizard dynamically adjusts its steps based on the specific capabilities you choose to enable for that vendor.
* **Centralized vault credentials**: Authenticate your connectors directly with stored vault credentials instead of manually entering credentials, extending standard platform security across all capabilities.\
  You can configure and save vault credentials under **Settings** → **Configurations** → **Integrations** → **Credentials**.

### The connector configuration experience

The configuration workflow depends on your onboarding date and the specific connector you are enabling. The transition to the unified experience is designed to support both existing and new customers within a single guide. Each connector topic specifies the license supported and whether it is available to all customers or only to those who received Cortex XSIAM starting July 26, 2026.

* **New customers** (onboarded after July 26, 2026): You will see the updated connector experience across the entire catalog.
* **Existing customers** (onboarded before July 26, 2026): You have immediate access to a subset of the unified catalog. For other Marketplace integrations, you will continue to use the legacy implementation until those specific connectors are enabled for your tenant.

#### Connector wizard

When using a unified connector, you follow a guided wizard within Cortex XSIAM.

* **Security-capability-driven setup**: If a connector wizard is available for your tenant, you can disregard the manual configuration steps on the Palo Alto Networks Developer (PAN DEV) site.
* **PAN DEV technical reference**: While the wizard handles the setup process, you should still refer to the [Cortex Developer Docs for Marketplace (PAN DEV)](https://cortex.marketplace.pan.dev/marketplace/) for specific technical information related to the service (sub-capability), such as:
  * Fetched Incidents Data
  * Available Commands
  * Other integration-specific data schemas and required fields not provided in the wizard.

#### Legacy Marketplace implementation

For integrations not yet available as a unified connector for your tenant, you will continue to use the legacy implementation. These do not feature a configuration wizard and require following the setup instructions on the [Cortex Developer Docs for Marketplace (PAN DEV)](https://cortex.marketplace.pan.dev/marketplace/) site for all configuration steps. For more information, see [Marketplace](../marketplace).

### Connectivity and capabilities

Unified connectors group vendor functionality into specific security capabilities. Depending on the connector selected, the wizard will present options based on the following possible capabilities:

* **Automation and Remediation**: Run automated actions and remediation commands against the connected service.
* **Fetch Issues**: Fetch issues and incidents from the connected service for investigation and response.
* **Log Collection**: Collect and ingest logs and events from the connected service.
* **Threat Intelligence and Enrichment**: Ingest threat intelligence and enrich indicators using data from the connected service.
* **Fetch Assets and Vulnerabilities**: Fetch assets and vulnerabilities from the connected service into the Unified Asset Inventory.
* **Fetch Secrets**: Retrieve secrets and credentials from the connected service.
* **Security Posture**: Detect, monitor, and alert on the security settings and configurations of your SaaS applications.
* **Data Security**: Scan and protect sensitive data, including files, attachments, and records within the service.
* **Identity Posture**: Maintain visibility and control over SaaS-based identities, including users, groups, roles, and granular permissions.
* **Agent Security Scanning**: Monitor and assess the security posture and activity of agents within the service environment.

For connectors that support multiple services or complex configurations, these capabilities may be further divided into **sub-capabilities**. For example, a single connector might allow you to independently enable "Users" and "Groups" under the Identity Posture capability.

Access to specific connectors and their individual sub-capabilities is determined by your tenant license and onboarding date.

Connectors are configured by navigating to **Settings → Data Sources & Integrations → + Add New**.

### Marketplace integrations not supported via connectors

The following Marketplace integrations remain outside the unified connector framework and must be managed as standalone integrations via the Marketplace. For these integrations, use the existing Marketplace configuration and documentation:

| Integration Name                                                                                           | Category       |
| ---------------------------------------------------------------------------------------------------------- | -------------- |
| [AWS-SNS-Listener](https://xsoar.pan.dev/docs/reference/integrations/aws-sns-listener)                     | Infrastructure |
| [Core REST API](https://xsoar.pan.dev/docs/reference/integrations/core-rest-api)                           | System / API   |
| [Cortex Core - IOC](https://xsoar.pan.dev/docs/reference/integrations/cortex-core---ioc)                   | System         |
| [Cortex Core - IR](https://xsoar.pan.dev/docs/reference/integrations/cortex-core---ir)                     | System         |
| [Generic Export Indicators Service](https://xsoar.pan.dev/docs/reference/integrations/edl)                 | Networking     |
| [Generic Webhook](https://xsoar.pan.dev/docs/reference/integrations/generic-webhook)                       | Utility        |
| [Image OCR](https://xsoar.pan.dev/docs/reference/integrations/image-ocr)                                   | Utility        |
| [Microsoft Teams](https://xsoar.pan.dev/docs/reference/integrations/microsoft-teams)                       | Collaboration  |
| [Palo Alto Networks WildFire Reports](https://xsoar.pan.dev/docs/reference/integrations/wild-fire-reports) | Security       |
| [Rasterize](https://xsoar.pan.dev/docs/reference/integrations/rasterize)                                   | Utility        |
| [TAXII Feed](https://xsoar.pan.dev/docs/reference/integrations/taxii-feed)                                 | Threat Intel   |
| [TAXII2 Server](https://xsoar.pan.dev/docs/reference/integrations/taxii2-server)                           | Threat Intel   |
| [XQL Query Engine](https://xsoar.pan.dev/docs/reference/integrations/xql-query-engine)                     | Analytics      |
| [Zoom](https://xsoar.pan.dev/docs/reference/integrations/zoom)                                             | Collaboration  |
