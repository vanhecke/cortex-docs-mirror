# ServiceNow Automation and Collection

{% hint style="warning" %}
**Important**

This connector is only available for tenants that onboarded after July 26, 2026. For tenants that onboarded before this date, use Marketplace to access the standalone integration. For more information, see [Marketplace](../../../marketplace).
{% endhint %}

ServiceNow is an IT service management platform that helps streamline security-related service management and IT operations. It provides a service-centric CMDB that proactively analyzes service-impacting changes, identifies issues, and eliminates outages. Cortex integrates with ServiceNow to create, update, query, and delete tickets and table records, perform Identity Lifecycle Management, collect audit and syslog events, and connect to ServiceNow MCP servers for agentic AI workflows.

This connector includes the following sub-capabilities (Marketplace integrations link to PAN DEV for more information):

* [ServiceNow CMDB](https://xsoar.pan.dev/docs/reference/integrations/service-now-cmdb): ServiceNow CMDB is a service-centric foundation that proactively analyzes service-impacting changes, identifies issues, and eliminates outages. This sub-capability is available with any active Cortex XSIAM, Cortex Cloud Posture Security, Cortex Cloud, Cortex Cloud Runtime Security, Cortex XDR, or Cortex AgentiX license.
* [ServiceNow Event Collector](https://xsoar.pan.dev/docs/reference/integrations/service-now-event-collector): Use this integration to fetch audits, syslog transactions, cases, and outbound HTTP logs from ServiceNow as Cortex XSIAM events. This sub-capability is available with any active Cortex XSIAM license.
* [ServiceNow IAM](https://xsoar.pan.dev/docs/reference/integrations/service-now-iam): Integrate with ServiceNow's services to execute CRUD operations for employee lifecycle processes. This sub-capability is available with any active Cortex XSIAM, Cortex Cloud Posture Security, Cortex Cloud, Cortex Cloud Runtime Security, Cortex XDR, or Cortex AgentiX license.
* ServiceNow MCP: Use this integration to connect securely with a ServiceNow Model Context Protocol (MCP) server and access its tools in real time. This sub-capability is available with any active Cortex XSIAM, Cortex Cloud Posture Security, Cortex Cloud, Cortex Cloud Runtime Security, Cortex XDR, or Cortex AgentiX license with the Attack Surface Management (ASM) or Exposure Management add-on.
* [ServiceNow v2](https://xsoar.pan.dev/docs/reference/integrations/service-now-v2): Use The ServiceNow IT Service Management (ITSM) solution to modernize the way you manage and deliver services to your users. This sub-capability is available with any active Cortex XSIAM, Cortex Cloud Posture Security, Cortex Cloud, Cortex Cloud Runtime Security, Cortex XDR, or Cortex AgentiX license.

To configure this connector, follow the steps outlined in the configuration wizard.
