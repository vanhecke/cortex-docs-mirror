# Cloudflare

{% hint style="warning" %}
**Important**

This connector is only available for tenants that onboarded after July 26, 2026. For tenants that onboarded before this date, use Marketplace to access the standalone integration. For more information, see [Marketplace](../../../marketplace).
{% endhint %}

Cloudflare provides network and security products for consumers and businesses, using reverse proxies for web traffic, edge computing, and a content delivery network. This connector fetches indicators from the Cloudflare feed, connects to a Cloudflare Model Context Protocol (MCP) server to access Cloudflare tools in real time, collects Cloudflare Zero Trust audit and access authentication logs as events, and manages Cloudflare WAF firewall rules, filters, and IP-lists.

This connector includes the following sub-capabilities (Marketplace integrations link to PAN DEV for more information):

* [Cloudflare Feed](https://xsoar.pan.dev/docs/reference/integrations/cloudflare-feed): This sub-capability is available with any active Cortex XSIAM or Cortex AgentiX license.
* [Cloudflare MCP](https://xsoar.pan.dev/docs/reference/integrations/cloudflare-mcp): Use this integration to connect securely with a Cloudflare Model Context Protocol (MCP) server and access its tools in real time. This sub-capability is available with any active Cortex XSIAM or Cortex AgentiX license.
* [Cloudflare Zero Trust](https://xsoar.pan.dev/docs/reference/integrations/cloudflare-zero-trust): This sub-capability is available with any active Cortex XSIAM license.
* [CloudflareWAF](https://xsoar.pan.dev/docs/reference/integrations/cloudflare-waf): Cloudflare WAF integration allows customers to manage firewall rules, filters, and IP-lists. It also allows to retrieve zones list for each account. This sub-capability is available with any active Cortex XSIAM or Cortex AgentiX license.

To configure this connector, follow the steps outlined in the configuration wizard.
