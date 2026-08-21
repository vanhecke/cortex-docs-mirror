---
description: >-
  Manage access to Cortex XSIAM forensic investigations, collections, and threat
  hunts.
---

# Forensics permissions

Controls access to Forensics (**Investigation & Response** → **Forensics**). Forensic investigations streamline your case response, data collection, threat hunting, and analysis of your endpoints.

{% hint style="info" %}
### Notice

You need the Forensics add-on to view Forensic investigations.
{% endhint %}

For more information, see [Forensic investigations](../../../../../detect-investigate-and-respond-to-threats/investigation-and-response/forensics#UUID-16d994cf-2c97-52ad-feb2-8752a758dc16).

| Permission | Description                                                                                                           | Roles Example                                                                                                                                                                                                                                                                                 |
| ---------- | --------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| None       | Users cannot see forensic artifacts or trigger new collections.                                                       |                                                                                                                                                                                                                                                                                               |
| View       | Read-only access to forensics investigations                                                                          | <ul><li>SOC Tier-1 Analyst: View forensics data for context, but cannot initiate collections.</li><li>SOC Tier-2 Analyst: View forensics data and escalate to Tier-3 for collections.</li><li>Security Engineer: View forensics for understanding data as not the primary function.</li></ul> |
| View/Edit  | Full read and write access, including create, edit, and delete investigations, start, pause, and delete threat hunts. | <ul><li>SOC Tier-3 Analyst: Full forensics capabilities, including triage and hunt.</li><li>Threat Hunter: Full forensics for deep-dive investigations.</li></ul>                                                                                                                             |

**Required and recommended Permissions**

Consider adding the following permissions:

| Permission            | Permission Level | Reason                                                                                                                                                       |
| --------------------- | ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Agent Administrations | View             | Forensics displays endpoint data extensively. Without this, endpoint information within forensics investigations will fail to load or show errors. Required. |
| Query Center          | View             | Strongly recommended to run queries on the host data.                                                                                                        |
| Cases & Issues        | View             | Strongly recommended to view issues associated with forensic investigations.                                                                                 |
