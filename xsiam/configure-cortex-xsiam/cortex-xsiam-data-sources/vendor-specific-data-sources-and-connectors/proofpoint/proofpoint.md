# Proofpoint

{% hint style="warning" %}
**Important**

This connector is only available for tenants that onboarded after July 26, 2026. For tenants that onboarded before this date, use Marketplace to access the standalone integration. For more information, see Marketplace.
{% endhint %}

Proofpoint is an email security and threat protection platform that guards against phishing, malware, and advanced email attacks. It includes Targeted Attack Protection (TAP), Threat Response for automated issue response, Protection Server for email gateway management, Cloud Threat Response, Browser Isolation, and URL phishing validation via IsItPhishing.

This connector includes the following sub-capabilities (Marketplace integrations link to PAN DEV for more information):

* [IsItPhishing](https://xsoar.pan.dev/docs/reference/integrations/is-it-phishing): Collaborative web service that provides validation on whether a URL is a phishing page or not by analyzing the content of the webpage. This sub-capability is available with any active Cortex XSIAM or Cortex AgentiX license.
* Proofpoint Cloud Threat Response: Fetches Proofpoint Cloud Threat Response (CTR) incidents into Cortex XSIAM for case management, and exposes commands to list and retrieve incident details. This sub-capability is available with any active Cortex XSIAM or Cortex AgentiX license.
* [Proofpoint Email Security Event Collector](https://xsoar.pan.dev/docs/reference/integrations/proofpoint-email-security-event-collector): Collects events for Proofpoint Email Security using the streaming API. This sub-capability is available with any active Cortex XSIAM license.
* [Proofpoint Protection Server v2](https://xsoar.pan.dev/docs/reference/integrations/proofpoint-protection-server-v2): Proofpoint email security appliance. This sub-capability is available with any active Cortex XSIAM or Cortex AgentiX license.
* [Proofpoint TAP v2](https://xsoar.pan.dev/docs/reference/integrations/proofpoint-tap-v2): Use the Proofpoint Targeted Attack Protection (TAP) integration to protect against and provide additional visibility into phishing and other malicious email attacks. This sub-capability is available with any active Cortex XSIAM or Cortex AgentiX license.
* [Proofpoint Threat Protection](https://xsoar.pan.dev/docs/reference/integrations/proofpoint-threat-protection): Threat Protection APIs are REST APIs that allow Proofpoint On Demand customers to retrieve, add, update or delete certain PoD configurations. This sub-capability is available with any active Cortex XSIAM or Cortex AgentiX license.
* [Proofpoint Threat Response](https://xsoar.pan.dev/docs/reference/integrations/proofpoint-threat-response): Use the Proofpoint Threat Response integration to orchestrate and automate incident response. This sub-capability is available with any active Cortex XSIAM or Cortex AgentiX license.
* [ProofpointIsolationEventCollector](https://xsoar.pan.dev/docs/reference/integrations/proofpoint-isolation-event-collector): Proofpoint Isolation is an integration that supports fetching Browser and Email Isolation logs events. This sub-capability is available with any active Cortex XSIAM license.
* [ProofpointThreatResponseEventCollector](https://xsoar.pan.dev/docs/reference/integrations/proofpoint-threat-response-event-collector): Use the Proofpoint Threat Response integration to orchestrate and automate incident response. This sub-capability is available with any active Cortex XSIAM license.

To configure this connector, follow the steps outlined in the configuration wizard.
