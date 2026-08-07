# Graph Search permissions

Limits access to Graph Search **Investigation & Response** → **Search** → **Query Builder** → **Graph Search)**, which enables visual exploration of cloud asset relationships, configurations, and security findings through an interactive graph interface, such as discovering cloud asset relationships, investigating security findings, and analyzing effective permissions.

{% hint style="info" %}
### Notice

Graph Search requires a Cloud Posture Security, Cloud Runtime Security, or Cortex XSIAM Premium license.
{% endhint %}

For more information, see [Graph Search](../../../graph-search).

| Permission   | Description                                                                                                                              | Roles Example                                                                                                                                                                                                                                             |
| ------------ | ---------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Graph Search | Cannot view the **Graph Search** page, execute graph queries, or view saved queries.                                                     |                                                                                                                                                                                                                                                           |
| View         | Execute graph queries, export, and support all view capabilities, such as viewing recent queries, graph definitions, and runtime events. |                                                                                                                                                                                                                                                           |
| View/Edit    | Full access to use the graph and save specific graph views or templates for others to use.                                               | <ul><li>SOC Tier-1, 2, and 3 Analysts: Save graph queries for reuse in investigations.</li><li>Threat Hunter: Full graph search for cloud threat hunting.</li><li>Security Engineer: Full graph search for cloud security engineering/IT Admin.</li></ul> |

**Required and recommended Permissions**

Consider adding the following permissions:

| Permission            | Permission Level                 | Reason                                                                                                                                                           |
| --------------------- | -------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Query Center          | View                             | Graph Search translates XQL logic into visual nodes. Without search permissions, the graph cannot query the data lake. Required.                                 |
| Query Library         | Enabled with checkboxes selected | Strongly recommended to view and save graph queries in the library tab. Without this, the library tab in the Graph Search side panel may not function correctly. |
| Agent Administrations | View                             | Recommended to populate host-specific metadata (like OS version or isolation status) within the graph nodes.                                                     |
| Asset Inventory       | View                             | Graph Search visualizes cloud asset data. Required to view asset data in the graph search. Required.                                                             |
| Cases & Issues        | View                             | Strongly recommended to view cases and issues in graph search.                                                                                                   |
| Action Center         | View/Edit                        | Recommended so an analyst can right-click a node (process or file) in the graph and take immediate action, such as Terminate Process.                            |
