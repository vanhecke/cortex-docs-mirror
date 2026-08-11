# CyberArk

{% hint style="warning" %}
**Important**

This connector is only available for tenants that onboarded after July 26, 2026. For tenants that onboarded before this date, use Marketplace to access the standalone integration. For more information, see [Marketplace](../../../marketplace).
{% endhint %}

CyberArk secures human and machine identities across hybrid and multi-cloud environments. This connector collects audit and authentication events from the CyberArk Identity Security Platform, CyberArk Identity, and CyberArk Endpoint Privilege Manager (EPM), activates and deactivates EPM risk plans for endpoints as a SOC response, and retrieves certificate information from CyberArk Certificate Manager.

This connector includes the following sub-capabilities (Marketplace integrations link to PAN DEV for more information):

* [CyberArk Identity Event Collector](https://xsoar.pan.dev/docs/reference/integrations/cyber-ark-identity-event-collector): This integration collects events from the Idaptive Next-Gen Access (INGA) using REST APIs. This sub-capability is available with any active Cortex XSIAM license.
* [CyberArkEPMEventCollector](https://xsoar.pan.dev/docs/reference/integrations/cyber-ark-epm-event-collector): CyberArk EPM Event Collector fetches events. This sub-capability is available with any active Cortex XSIAM, Cortex Cloud, Cortex Cloud Runtime Security, or Cortex XDR license.
* [CyberArkEPMSOCResponse](https://xsoar.pan.dev/docs/reference/integrations/cyber-ark-epmsoc-response): Use the CyberArk EPM integration to activate and deactivate CyberArk EPM risk plans for specific endpoints. This sub-capability is available with any active Cortex XSIAM, Cortex XDR, or Cortex AgentiX license.
* [CyberArkISP](https://xsoar.pan.dev/docs/reference/integrations/cyber-ark-isp): CyberArk Identity Security Platform secures human and machine identities across hybrid/multi-cloud environments with intelligent privilege controls, AI-driven threat detection, and Zero Trust enforcement. This sub-capability is available with any active Cortex XSIAM license.
* [VenafiTLSProtect](https://xsoar.pan.dev/docs/reference/integrations/venafi-tls-protect): This sub-capability is available with any active Cortex XSIAM or Cortex AgentiX license.

To configure this connector, follow the steps outlined in the configuration wizard.
