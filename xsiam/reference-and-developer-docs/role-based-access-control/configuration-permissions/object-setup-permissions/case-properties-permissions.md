---
description: >-
  Configure access to case domains, custom statuses, and resolution statuses in
  Cortex XSIAM.
---

# Case Properties permissions

Controls access to the following tabs from Cases (**Settings** → **Configurations** → **Object Setup** → **Cases**):

* Domains: These represent the primary classifications for cases, such as Malware, Phishing, or Network Intrusion. Each domain has a name, color, description, associated statuses, and resolution statuses.
* Properties: Manages custom case statuses and resolution statuses. For example, New, Under Investigation, Pending, Resolved.

{% hint style="warning" %}
### Caution

System-default statuses cannot be deleted, and domain names cannot be changed after creation.
{% endhint %}

| Permission | Description                                                                                                                                                                                    | Roles Example                                                                                                                                                                                                                                                                                                       |
| ---------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| None       | No access to the Domains or Properties tabs. The tabs are hidden from the Cases Object Setup navigation. The user cannot view or modify custom statuses, resolution statuses, or case domains. | SOC Tier-1 Analyst: Tier-1 analysts work within existing case structures; they do not need to see or modify case property definitions (statuses, domains).                                                                                                                                                          |
| View       | Read-only access. Users can browse the domains table and see existing custom and resolution statuses.                                                                                          | <ul><li>SOC Tier-2 and 3 Analysts: Need visibility into case structures (what statuses exist, what domains are configured) for investigation context and proper case categorization.</li><li>Threat Hunter: Needs context on case structures (statuses, domains) for hunting workflows and case creation.</li></ul> |
| View/Edit  | Full read/write access. Users can create up to 20 custom statuses, reorder them, and manage domain status assignments.                                                                         |                                                                                                                                                                                                                                                                                                                     |

### Required and recommended permissions

Consider adding the following permissions:

| Permission      | Permission Level  | Reasons                                                                                                                                                                       |
| --------------- | ----------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Cases & Issues  | View or View/Edit | <ul><li>View: Required to view cases that use these statuses and domains.</li><li>View/Edit: Strongly recommended to change the case status/domain on actual cases.</li></ul> |
| Fields and Type | View              | View the Fields tab alongside Domains/Properties in Cases Object Setup. Strongly recommended.                                                                                 |
| Layouts         | View              | View the Layouts and Layout Rules tabs in Cases Object Setup. Recommended.                                                                                                    |
| Audit           | View              | Track changes to statuses and domains. Strongly recommended.                                                                                                                  |
