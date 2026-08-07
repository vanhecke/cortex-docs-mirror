# Splunk Automation and Collection

{% hint style="warning" %}
**Important**

This connector is only available for tenants that onboarded after July 26, 2026. For tenants that onboarded before this date, use Marketplace to access the standalone integration. For more information, see Marketplace.
{% endhint %}

Run queries on Splunk servers and fetch events from both Splunk Enterprise Security (ES) and non-ES environments. SplunkPy fetches notable events (for Splunk ES up to 8.1) and SplunkPy v2 fetches Findings and Investigations (for Splunk ES 8.2 and higher), enriching them with Asset, Identity, and Drilldown data and supporting bi-directional mirroring between Splunk and Cortex.

This connector includes the following sub-capabilities (Marketplace integrations link to PAN DEV for more information):

* [SplunkPy](https://xsoar.pan.dev/docs/reference/integrations/splunk-py): Run queries on Splunk and fetch Notable Events (Splunk ES versions up to 8.2). This sub-capability is available with any active Cortex XSIAM, Cortex Cloud Posture Security, or Cortex AgentiX license.
* [SplunkPy v2](https://xsoar.pan.dev/docs/reference/integrations/splunk-py-v2): Run queries on Splunk and fetch Splunk ES Findings and Investigations (Splunk ES 8.2+). This sub-capability is available with any active Cortex XSIAM, Cortex Cloud Posture Security, or Cortex AgentiX license.
* SplunkPyPreRelease: Runs queries on Splunk servers. This sub-capability is available with any active Cortex XSIAM or Cortex AgentiX license.

To configure this connector, follow the steps outlined in the configuration wizard.
