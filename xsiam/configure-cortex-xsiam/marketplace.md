---
description: >-
  Explore Cortex XSIAM Marketplace to discover, install, and manage content
  packs.
---

# Marketplace

Marketplace is a centralized content portal that enables you to download and manage content in Cortex XSIAM. Content is organized into content packs created by different contributors, such as Palo Alto Networks, Partners, and MSSPs, to support specific security orchestration use cases. Each content pack can include a variety of components, such as integrations, playbooks, scripts, and correlation rules.

You can view and install Marketplace content packs directly from within Cortex XSIAM or browse the full catalog at the [Cortex Developer Docs for Marketplace (PAN DEV)](https://cortex.marketplace.pan.dev/marketplace/) site.

### Marketplace and connectors in Cortex XSIAM

Cortex XSIAM is introducing a unified approach to third-party integrations through connectors. This shift changes how some content is discovered and managed within Marketplace, depending on your tenant onboarding date.

{% hint style="warning" %}
If your Cortex XSIAM tenant was onboarded after July 26, 2026, you may notice that some integrations listed on the [Cortex Developer Docs for Marketplace (PAN DEV)](https://cortex.marketplace.pan.dev/marketplace/) site do not appear as standalone items in the Cortex XSIAM Marketplace catalog.

These integrations have been consolidated into uniquely named connectors. Instead of installing a standalone integration, you should add the vendor's connector from the **Data Sources & Integrations** page to access these capabilities. The connector wizard will guide you through the configuration of these services, which are now managed as sub-capabilities within the connector.
{% endhint %}

#### Technical documentation reference

While the new connector wizards handle all configuration steps, new tenants should still refer to the [Cortex Developer Docs for Marketplace (PAN DEV)](https://cortex.marketplace.pan.dev/marketplace/) site for critical technical information not provided in the wizard, such as:

* Available commands
* Required incident fields and data schemas
* Specific sub-capability technical metadata

#### Existing tenants

Tenants onboarded prior to July 26, 2026, will continue to see and use standalone Marketplace integrations for services that have not yet been migrated to the connector framework for their account. These can be installed from **Marketplace → Content Packs** and configured on the **Data Sources & Integrations** page.
