---
description: >-
  Learn more about the complete data source and connector catalog available in
  Cortex XSIAM.
---

# Complete data source and connector catalog

The complete data source catalog is a conceptual grouping that is comprised of all configuration points available for data ingestion across Cortex XSIAM. It represents the aggregate of every integration method, from unified vendor connectors and cloud onboarding wizards to generic on-premise collectors and specialized Marketplace integrations.

The catalog is best understood by categorizing ingestion methods into the following core groups. By consulting the specific documentation sections dedicated to each category as detailed below, you gain a complete overview of all available ingestion options that collectively form the data source catalog.

### Vendor-specific data sources and connectors

This section includes integrations for specific third-party security and IT products, such as Okta, Box, and Salesforce. These include:

* **Connectors**: The strategic, unified experience that allows you to manage all of a vendor's capabilities, such as log collection, automation, and posture, through a single configuration wizard.
* **Standard data collectors**: Traditional built-in API and file-based collection functionalities.

Access to specific connectors depends on your license and tenant onboarding date. For more information, see [What are Cortex XSIAM Data Sources and Connectors?](what-are-cortex-xsiam-data-sources). Configured on the **Data Sources & Integrations** page.

### Cloud Service Provider (CSP) onboarding

Cortex XSIAM provides specialized onboarding wizards for integrating major cloud environments, such as AWS, Azure, GCP, and OCI. These wizards enable streamlined setup for asset discovery, cloud posture/runtime security, and log collection across your cloud infrastructure. Configured on the **Data Sources & Integrations** page.

### Generic on-premise data collectors

Flexible collectors for logs and data from local environments not tied to a specific vendor, including:

* **Broker VM applets**, such as Syslog Collector and Database Collector, configured using the **Broker VMs** page.
* **XDR Collectors (XDRC)** for on-host log collection, configured on the **XDR Collectors** page.

### Marketplace content packs (integrations)

Packages that offer rich security content, often including a collection integration for data ingestion alongside automation components.

* **New Tenants**: For tenants onboarded after July 26, 2026, standalone Marketplace integrations that have been consolidated into unified connectors are hidden from the catalog. Instead, these services are managed as sub-capabilities within the relevant vendor connector on the **Data Sources & Integrations** page to ensure a streamlined experience.
* **Existing Tenants**: Continue to use Marketplace integrations for services not yet migrated to the connector framework for your account. These are installed from **Settings → Configurations → Marketplace** and configured using the Data Source Onboarder on the **Data Sources & Integrations** page.

### Palo Alto Networks integrations

These integrations include both traditional data sources and new unified connectors to ensure deep telemetry ingestion and seamless cross-platform orchestration across the Palo Alto Networks security stack, such as Next-Generation Firewall and Prisma Access, configured on the **Data Sources & Integrations** page.

### Cloud Posture and Runtime Security data sources

These data sources provide agentless visibility and real-time control over cloud risks by using cloud-native APIs to monitor misconfigurations and secure container environments. These data sources are configured:

* Using Broker VM applets, such as AppSec Transporter, configured using the **Broker VMs** page.
* On the **Data Sources & Integrations** page.
