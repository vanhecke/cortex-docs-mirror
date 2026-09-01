---
description: Use SANS DShield data in Cortex XSIAM to fetch attack subnet feeds.
---

# SANS DShield

{% hint style="warning" %}
**Important**

This connector is only available for tenants that onboarded after July 26, 2026. For tenants that onboarded before this date, use Marketplace to access the standalone integration. For more information, see [Marketplace](../../../marketplace).
{% endhint %}

This connector is available with any active Cortex XSIAM or Cortex AgentiX license.

Fetches a feed from DShield summarizing the top 20 attacking class C (/24) subnets over the last three days. The number of 'attacks' indicates the number of targets reporting scans from a subnet.

This connector includes the following sub-capabilities (Marketplace integrations link to PAN DEV for more information):

* [DShield Feed](https://xsoar.pan.dev/docs/reference/integrations/d-shield-feed)

To configure this connector, follow the steps outlined in the configuration wizard.
