---
description: >-
  Configure URL and File log collection for Palo Alto Networks integrations in
  pre-3.x Cortex XSIAM to balance analytics visibility, correlation rules, and
  ingestion costs.
---

# Collecting URL and File log types

{% hint style="info" %}
**Note**

This topic is only relevant for customers who have not migrated to Cortex XSIAM 3.x. For customers who have migrated, see [Log type filtering](log-type-filtering).
{% endhint %}

For Palo Alto Networks integrations, you can choose whether to collect URL and File type logs. These logs enhance your cyber analytics, correlation rules and visibility for investigation. However, if you want to reduce ingestion charges, you can globally turn off collection of URL and File log types for all **Palo Alto Networks Integrations**.

When collection is turned off, some detectors won’t detect cyber attacks or provide full context, and correlation rules won’t be able to detect cyber events. For a full list of affected detectors, see [Detectors connected to URL and File log types](collecting-url-and-file-log-types/detectors-connected-to-url-and-file-log-types).

You can also calculate the amount of ingestion that URL and File log types are consuming by looking at the NGFW dashboard. This dashboard provides an overview of the PAN-NGFW ingestion status of all log types (including URL and File log types) and their daily consumption quota.

You can turn on or off **URL and File log types collection** on the **Data Sources & Integrations** page.
