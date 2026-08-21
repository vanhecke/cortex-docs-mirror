---
description: >-
  Manage access to Cortex XSIAM's endpoint inventory, host details, and hygiene
  data.
---

# Host Insights permissions

Limits access to Host Insights/Inventory (**Inventory** → **Endpoints** → **Host Insights)**), which enables you to gain visibility and inventory into the business and IT operational data on all your endpoints. For more information, see [Host Inventory](../../../../protect-your-endpoints/endpoint-security/install-and-manage-endpoints/harden-endpoint-security/host-inventory).

Unlike Forensics, which is a point-in-time snapshot, Host Insights is designed for broad fleet visibility and hygiene. It covers:

* Host Inventory: Operating system details, installed software, local user accounts, and listening ports.
* Searchability: The ability to hunt for "at-risk" systems across the environment (e.g., finding every server running an outdated version of Java).

{% hint style="info" %}
### Note

It is important to distinguish between Host Insights and Asset Inventory permissions. Host Insights is a deep insight into endpoints that have a Cortex XDR agent installed. Asset Inventory is a broad list of everything on your network (unmanaged devices, cloud buckets, etc.). For more information, see [Asset Inventory permissions](../../../inventory-assets-permissions#UUID-1f0e9b81-b0f0-25c9-443f-69d6c3fb64cf).

Accessing the **Host Inventory** menu (from **Host Insights**) provides different capabilities based on your license. If you have Cortex XSIAM Enterprise or Cortex XSIAM NG-SIEM with a Host Insights license, you have access to Vulnerability Assessment. For Cortex XSIAM Premium or Cloud Security (Posture/Runtime) licenses, you have access to Vulnerability Management. See [Vulnerability Management permissions](../../../exposure-and-vulnerability-management-permissions#UUID-aa0a32d6-5a36-4767-4f13-4808e4059a73).
{% endhint %}

| Permissions | Description                                                                                                                                       | Roles Example                                                                                                                                                                                                                                 |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| None        | Limits access to the **Host Inventory** menu.                                                                                                     |                                                                                                                                                                                                                                               |
| View        | Users can search the inventory, view host details, and browse software lists. They can open the Asset View but cannot trigger management actions. | <ul><li>SOC Tier-1 Analyst: View host inventory and vulnerability data for triage.</li><li>Security Engineer: View host data for detection development.</li></ul>                                                                             |
| View/Edit   | Full access to the inventory, including the ability to manage scan settings or trigger manual inventory refreshes.                                | <ul><li>SOC Tier-2 Analyst: View host data and escalate for file search/destroy.</li><li>SOC Tier-3 Analyst: Full host insights, including file search and destroy.</li><li>Threat Hunter: Full host insights for endpoint hunting.</li></ul> |

**Required and recommended Permissions**

Consider adding the following permissions:

| Permission            | Permission Level | Reason                                                                                                                                                                                         |
| --------------------- | ---------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Agent Administrations | View             | Host Insights displays endpoint/agent data. Without this, the host data will fail to load properly. Required.                                                                                  |
| Query Center          | View             | Strongly recommended to run queries on the host data.                                                                                                                                          |
| Asset Inventory       | View             | Strongly recommended for the user to view Host Insights data directly within the broader Asset View for a seamless experience.                                                                 |
| File Search           | Checked          | Dependency for file search action. Only needed if View/Edit permission is granted for Host Insights and the user needs to search for files across endpoints.                                   |
| Destroy Files         | Checked          | Dependency for the destroy files action. Only needed if View/Edit permission is granted and the user needs to delete files from endpoints. This is an irreversible action; grant with caution. |
