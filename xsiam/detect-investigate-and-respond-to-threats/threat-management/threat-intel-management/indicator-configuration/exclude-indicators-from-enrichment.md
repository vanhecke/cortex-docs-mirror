---
description: >-
  Exclude selected indicators from enrichment to control processing and data
  usage.
---

# Exclude indicators from enrichment

You can disable enrichment for individual indicators or disable enrichment for all indicators fetched by any of the following feeds:

* Azure Feed
* Office 365 Feed
* Cisco WebEx Feed
* Cloudflare Feed
* Fastly Feed
* AWS Feed
* Zoom Feed
* Public DNS Feed
* Google IP Ranges Feed

If you disable enrichment for an incoming feed, the indicators are extracted and saved but not enriched by Cortex XSIAM, enabling you to conserve system resources when dealing with known indicators.

When an indicator has enrichment excluded, the **Enrich Indicator** button is disabled. If you try to enrich an indicator that is enrichment excluded, an error will occur.

Indicators of the following indicator types can have enrichment excluded:

* IP
* Domain
* Email
* URL
* File

Exclude enrichment for a feed integration

To exclude enrichment for indicators fetched from a feed integration, when configuring an instance of the feed integration, select the **Enrichment Excluded** checkbox.

Exclude enrichment for individual indicators

When creating or editing an indicator of one of the following types: IP, Domain, Email, URL, or File, you have the option to set **Enrichment Excluded** to **Yes** or **No**. The default is **No**.

View list of enrichment excluded indicators

To view the enrichment excluded indicators in the **Indicators** table, add the **Enrichment Excluded** column to the table.
