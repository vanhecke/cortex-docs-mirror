# abuse.ch

{% hint style="warning" %}
**Important**

This connector is only available for tenants that onboarded after July 26, 2026. For tenants that onboarded before this date, use Marketplace to access the standalone integration. For more information, see [Marketplace](../../../marketplace).
{% endhint %}

This sub-capability is available with any active Cortex XSIAM or Cortex AgentiX license.

abuse.ch is a set of community threat intelligence projects. Fetch and enrich indicators of compromise from URLhaus (malicious URLs used for malware distribution), Feodo Tracker (botnet C\&C IP blocklists), MalwareBazaar (malware samples and file-hash intel), ThreatFox (IOCs associated with malware), and the SSL Blacklist (malicious SSL certificates and associated IP addresses).

This connector includes the following sub-capabilities (Marketplace integrations link to PAN DEV for more information):

* [abuse.ch SSL Blacklist Feed](https://xsoar.pan.dev/docs/reference/integrations/abusech-ssl-blacklist-feed):
* [FeedURLhaus](https://xsoar.pan.dev/docs/reference/integrations/feed-ur-lhaus): Fetch url indicators for URLHaus.
* [Feodo Tracker IP Blocklist Feed](https://xsoar.pan.dev/docs/reference/integrations/feodo-tracker-ip-blocklist-feed):
* [MalwareBazaar](https://xsoar.pan.dev/docs/reference/integrations/malware-bazaar): MalwareBazaar is a project from abuse.ch with the goal of sharing malware samples with the Infosec community, AV vendors, and threat intelligence providers.
* [MalwareBazaar Feed](https://xsoar.pan.dev/docs/reference/integrations/malware-bazaar-feed): Use the MalwareBazaar Feed integration to get the list of malware samples added to MalwareBazaar within the last 60 minutes.
* [ThreatFox Feed](https://xsoar.pan.dev/docs/reference/integrations/threat-fox-feed):
* [URLhaus](https://xsoar.pan.dev/docs/reference/integrations/ur-lhaus): URLhaus has the goal of sharing malicious URLs that are being used for malware distribution.

To configure this connector, follow the steps outlined in the configuration wizard.
