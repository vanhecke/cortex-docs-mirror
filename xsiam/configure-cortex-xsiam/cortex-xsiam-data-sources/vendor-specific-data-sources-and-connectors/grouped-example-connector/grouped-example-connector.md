# Grouped Example Connector

{% hint style="warning" %}
**Important**

This connector is only available for tenants that onboarded after July 26, 2026. For tenants that onboarded before this date, use Marketplace to access the standalone integration. For more information, see [Marketplace](../../../marketplace).
{% endhint %}

POC of Grouped Connectors / view\_groups. Four mocked Microsoft-themed XSIAM sub-capabilities (EWS O365, EWS v2, Office 365 Feed, Microsoft Teams) wired to exercise: `settings.grouped`, split connection/configurations `view_groups` registries, per-handler `auth_options` `view_group` pinning, one profile shared across multiple capabilities, multiple profiles bound to one sub-capability, two integrations under the same capability with duplicated field names per `view_group`, integration-shared params across two sub-capabilities, per-integration `engine`/`proxy`/`trust-any-cert` in connection `general_configurations`, and per-integration `integrationLogLevel` with serializer rewrites. Appendix G + I carve-outs honored for Microsoft Teams. Every vendor / pack / capability mapping here is mocked.

This connector includes the following sub-capabilities (Marketplace integrations link to PAN DEV for more information):

* [EWS O365](https://xsoar.pan.dev/docs/reference/integrations/ewso365): The new EWS O365 integration uses OAuth 2.0 protocol and can be used with Exchange Online and Office 365 (mail).
* [EWS v2](https://xsoar.pan.dev/docs/reference/integrations/ews-v2): Exchange Web Services and Office 365 (mail).
* Fetch Issues:
* [Microsoft Teams](https://xsoar.pan.dev/docs/reference/integrations/microsoft-teams): Send messages and notifications to your team members.
* [Office 365 Feed](https://xsoar.pan.dev/docs/reference/integrations/office-365-feed):
* Threat Intelligence and Enrichment:

To configure this connector, follow the steps outlined in the configuration wizard.
