# Okta Automation and Collection

{% hint style="warning" %}
**Important**

This connector is only available for tenants that onboarded after July 26, 2026. For tenants that onboarded before this date, use Marketplace to access the standalone integration. For more information, see Marketplace.
{% endhint %}

Okta integrates with Cortex to help security teams understand and respond to identity threats as they emerge. It provides visibility into each user's groups, roles, and application access to streamline investigations, and enables identity-centric response actions such as suspending accounts, forcing password resets, and prompting step-up authentication. The connector also collects Okta authentication and audit logs, Okta Advanced Server Access (ASA) audit events, and Okta Auth0 logs, and supports Identity Access Management (IAM) CRUD operations for employee lifecycle processes.

This connector includes the following sub-capabilities (Marketplace integrations link to PAN DEV for more information):

* [Okta Event Collector](https://xsoar.pan.dev/docs/reference/integrations/okta-event-collector): Collects the events log for authentication and Audit provided by Okta admin API. This sub-capability is available with any active Cortex XSIAM license.
* [Okta IAM](https://xsoar.pan.dev/docs/reference/integrations/okta-iam): Integrate with Okta's Identity Access Management service to execute CRUD operations to employee lifecycle processes. This sub-capability is available with any active Cortex XSIAM, Cortex Cloud Posture Security, Cortex Cloud, Cortex Cloud Runtime Security, Cortex XDR, or Cortex AgentiX license.
* [Okta v2](https://xsoar.pan.dev/docs/reference/integrations/okta-v2): Integration with Okta's cloud-based identity management service. This sub-capability is available with any active Cortex XSIAM, Cortex Cloud Posture Security, Cortex Cloud, Cortex Cloud Runtime Security, Cortex XDR, or Cortex AgentiX license.
* [OktaASA](https://xsoar.pan.dev/docs/reference/integrations/okta-asa): Okta Advanced Server Access integration for Cortex XSIAM allows you to fetch logs of a wide range of configuration, enrollment, authentication, and authorization events that occur within the product and on your servers. This sub-capability is available with any active Cortex XSIAM license.
* [OktaAuth0EventCollector](https://xsoar.pan.dev/docs/reference/integrations/okta-auth0-event-collector): Okta Auth0 logs event collector integration for Cortex XSIAM. This sub-capability is available with any active Cortex XSIAM license.

To configure this connector, follow the steps outlined in the configuration wizard.
