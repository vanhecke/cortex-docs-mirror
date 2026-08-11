# Zscaler

{% hint style="warning" %}
**Important**

This connector is only available for tenants that onboarded after July 26, 2026. For tenants that onboarded before this date, use Marketplace to access the standalone integration. For more information, see [Marketplace](../../../marketplace).
{% endhint %}

Zscaler is a cloud security solution built for performance and flexible scalability. This connector manages URL and IP address allow lists and block lists, categories, IP destination groups, and Sandbox reports, and it can also collect Zscaler Internet Access (ZIA) logs. It includes Red Canary, which collects and standardizes endpoint data to help teams detect, analyze, and respond to security issues.

This connector includes the following sub-capabilities (Marketplace integrations link to PAN DEV for more information):

* [RedCanary](https://xsoar.pan.dev/docs/reference/integrations/red-canary): Red Canary collects endpoint data using Carbon Black Response and CrowdStrike Falcon. The collected data is standardized into a common schema which allows teams to detect, analyze and respond to security incidents. This sub-capability is available with any active Cortex XSIAM or Cortex AgentiX license.
* [Zscaler](https://xsoar.pan.dev/docs/reference/integrations/zscaler): Zscaler is a cloud security solution built for performance and flexible scalability. This integration enables you to manage URL and IP address allow lists and block lists, manage and update categories, get Sandbox reports, create, manage, and update IP destination groups and manually log in, log out, and activate changes in a Zscaler session. This sub-capability is available with any active Cortex XSIAM or Cortex AgentiX license.
* [ZscalerZIdentity](https://xsoar.pan.dev/docs/reference/integrations/zscaler-z-identity): Zscaler Internet Access via ZIdentity OAuth 2.0. Provides URL/IP/domain classification, denylist and allowlist management, URL category management, sandbox reporting, user and group management, and IP destination group management using OAuth 2.0 client credentials authentication through ZIdentity. This sub-capability is available with any active Cortex XSIAM, Cortex Cloud, Cortex Cloud Runtime Security, Cortex XDR, or Cortex AgentiX license.

To configure this connector, follow the steps outlined in the configuration wizard.
