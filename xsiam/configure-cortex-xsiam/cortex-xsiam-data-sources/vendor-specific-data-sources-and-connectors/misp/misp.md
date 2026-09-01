---
description: Use MISP data with Cortex XSIAM.
---

# MISP

{% hint style="warning" %}
**Important**

This connector is only available for tenants that onboarded after July 26, 2026. For tenants that onboarded before this date, use Marketplace to access the standalone integration. For more information, see [Marketplace](../../../marketplace).
{% endhint %}

This connector is available with any active Cortex XSIAM or Cortex AgentiX license.

MISP (Malware Information Sharing Platform) is an open-source threat intelligence and threat sharing platform. This connector retrieves and ingests threat actor information from the MISP threat actor galaxy, ingests feeds into Cortex Threat Intel Management (TIM) via an MISP instance, and enriches indicators using data from an MISP instance.

This connector includes the following sub-capabilities (Marketplace integrations link to PAN DEV for more information):

* [FeedMISPThreatActors](https://xsoar.pan.dev/docs/reference/integrations/feed-misp-threat-actors): Fetches the MISP threat actor galaxy and builds it into Threat Actor indicators in Cortex Threat Intel Management (TIM).
* [MISP Feed](https://xsoar.pan.dev/docs/reference/integrations/misp-feed):
* [MISP V3](https://xsoar.pan.dev/docs/reference/integrations/misp-v3): Malware information sharing platform and threat sharing.

To configure this connector, follow the steps outlined in the configuration wizard.
