# NIST

{% hint style="warning" %}
**Important**

This connector is only available for tenants that onboarded after July 26, 2026. For tenants that onboarded before this date, use Marketplace to access the standalone integration. For more information, see [Marketplace](../../../marketplace).
{% endhint %}

This sub-capability is available with any active Cortex XSIAM or Cortex AgentiX license.

CVE feed from the NIST National Vulnerability Database (NVD). Use this feed to create a feed of CVEs from NIST, using v2 of the NVD API and supporting the latest CVSS - Common Vulnerability Scoring System standard.

This connector includes the following sub-capabilities (Marketplace integrations link to PAN DEV for more information):

*   [FeedNVDv2](https://xsoar.pan.dev/docs/reference/integrations/feed-nv-dv2): This feed pulls CVE information from the NIST National Vulnerability Database using v2.0 of the API.

    By default, CVEs with a REJECTED status are excluded. Enable 'Include Rejected CVEs' to ingest them.

    This integration/feed deprecates the original National Vulnerability Database Feed integraiton as v1.0 of the API is being sunsetted in 2023.

To configure this connector, follow the steps outlined in the configuration wizard.
