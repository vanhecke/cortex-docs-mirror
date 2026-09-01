---
description: Use Recorded Future threat intelligence data in Cortex XSIAM.
---

# Recorded Future

{% hint style="warning" %}
**Important**

This connector is only available for tenants that onboarded after July 26, 2026. For tenants that onboarded before this date, use Marketplace to access the standalone integration. For more information, see [Marketplace](../../../marketplace).
{% endhint %}

Ingest threat intelligence from Recorded Future. The RiskList Feed downloads lists of IP addresses, domains, URLs, CVEs, or file hashes with known risk associations, including risk scores and supporting evidence, while the Event Collector fetches alerts from Recorded Future.

This connector includes the following sub-capabilities (Marketplace integrations link to PAN DEV for more information):

* [Recorded Future Feed](https://xsoar.pan.dev/docs/reference/integrations/recorded-future-feed): This sub-capability is available with any active Cortex XSIAM or Cortex AgentiX license.
* [RecordedFutureEventCollector](https://xsoar.pan.dev/docs/reference/integrations/recorded-future-event-collector): This integration fetches alerts from Recorded Future. This sub-capability is available with any active Cortex XSIAM license.

To configure this connector, follow the steps outlined in the configuration wizard.
