# EDL permissions

EDL (External Dynamic List) enables security teams to:

* Add IP Addresses and Domains to Dynamic Lists - Create lists of malicious or suspicious IPs/domains
* Integrate with Palo Alto Networks Firewalls - EDL lists are automatically synced and enforceable on PANW firewalls.
* Block Malicious Traffic - Firewalls can use EDL to block traffic to/from listed entities
* Centralized Threat Response - Manage blocklists from a single location across your security infrastructure

{% hint style="info" %}
### Note

This permission is for analysts to use as a response action during case investigation. The Long Running HTTP Integrations configuration (under **Configurations**) is for administrators to set up and manage the EDL service infrastructure. For more information, see [Forward Requests to Long-Running Integrations](../../../../configure-cortex-xsiam/cortex-xsiam-data-sources/administration-and-troubleshooting/integrations/forward-requests-to-long-running-integrations).
{% endhint %}

| Permission | Description                                                                                                                                                    | Roles Example                                            |
| :--------: | -------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------- |
|    None    | Nothing related to EDL, such as viewing EDL lists, adding entities to EDL, and accessing the EDL configuration.                                                |                                                          |
|  View/Edit | Add new IPs and domains to EDL entries in Action Center, Causality View, Issue View, XQL Queries, Threat Intel, and playbooks. Also removing entries from EDL. | All SOC Analysts, Threat Hunters, and Security Engineers |

**Required and recommended permissions**

Consider adding the following permissions:

| Permission     | Permission Level | Reason                                                                                                                                       |
| -------------- | ---------------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| Action Center  | View             | EDL is accessed through the Action Center. Required.                                                                                         |
| Cases & Issues | View             | Add to EDL/Remove from EDL appears in Case View and Causality View. Required.                                                                |
| Query Center   | View             | Add to the EDL context menu appears in the XQL Investigation results. Strongly recommended.                                                  |
| Threat Intel   | View             | Add to EDL appears in the IOC Rules context menu. Threat Intel view permission is needed to access the IOC Rules page. Strongly recommended. |
