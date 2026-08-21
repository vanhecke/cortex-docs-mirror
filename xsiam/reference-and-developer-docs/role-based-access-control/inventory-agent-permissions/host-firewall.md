---
description: Configure host firewall rules and review firewall events in Cortex XSIAM.
---

# Host Firewall

Provides endpoint-level network protection, such as defining inbound and outbound firewall rules and creating application-based rules in the Host Firewall page (**Inventory** → **Endpoints** → **Host Firewall)**. Users can also **Collect Detailed Host Firewall Logs** from **Inventory** → **Endpoints** → **Endpoint Control**.

{% hint style="warning" %}
### Caution

Misconfigured firewall rules can block legitimate traffic or allow malicious connections. Implement change management processes and test rules before deployment.
{% endhint %}

| Permissions | Description                                                                                                                                                                            | Roles Example                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| ----------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| None        | Cannot view the Host Firewall page, which includes firewall pages, firewall rules, and events, or Collect Detailed Host Firewall Logs.                                                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| View        | View the Host Firewall menu, which includes read-only access for Rule Groups and Host Firewall Events.                                                                                 | <ul><li>SOC Tier-1 Analyst: Firewall rules may provide context for network-related alerts. Helpful when triaging blocked connection issues.</li><li>SOC Tier-2 Analyst: Understanding firewall rules is important for investigating network-based threats. Critical for lateral movement investigations</li><li>Threat Hunter: Firewall rules help understand network protection posture for hunting. Hunters need to know what network traffic is allowed/blocked.</li></ul> |
| View/Edit   | All view capabilities, plus creating, editing, deleting, and enabling Host Firewall Rules Groups, and managing Host Firewall Events. Also can **Collect Detailed Host Firewall Logs**. | <ul><li>SOC Tier-3 Analyst: May need for emergency containment (blocking malicious IPs), but should require approval and documentation.</li><li>Security Engineer: Responsible for firewall rule development and maintenance. Creates and optimizes firewall policies.</li></ul>                                                                                                                                                                                              |

**Required and recommended permissions**

Consider adding the following permissions:

| Permission               | Permission Level | Reason                                                                                                                                                                  |
| ------------------------ | ---------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Agent Groups             | View             | Required. Must understand group structure to target firewall rules correctly. Incorrect targeting can block legitimate traffic or allow malicious connections.          |
| Agent Extension Policies | View             | Required. Host Firewall profiles are managed through extension policies. Without extension policy visibility, firewall rule changes may conflict with profile settings. |
| Agent Administrations    | View             | Strongly Recommended. View endpoints to understand firewall rule deployment and correlate firewall events with endpoint data.                                           |
| Network Configuration    | View             | Strongly Recommended. Network topology context is essential for designing effective firewall rules. Understanding network zones prevents blocking legitimate traffic.   |
| Cases & Issues           | View             | Strongly Recommended. Review security events to inform firewall rule decisions. Understanding attack patterns helps create effective rules.                             |
