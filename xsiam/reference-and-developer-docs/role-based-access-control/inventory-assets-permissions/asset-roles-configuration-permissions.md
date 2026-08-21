---
description: Configure functional asset roles and endpoint assignments in Cortex XSIAM.
---

# Asset Roles configuration permissions

Asset Roles Configuration allows organizations to define and manage specific functional roles for assets across their environment (such as Admin, User, or Server). By associating specific users and endpoints with these roles, security teams can enrich security events with role context and support role-based analytics and alerting. Users access these features by going to **Inventory** → **Assets** → **Asset Roles Configuration**.

{% hint style="info" %}
### Notice

Requires the Identity Threat Detection and Response add-on.
{% endhint %}

For more information, see [Asset Roles](../../../detect-investigate-and-respond-to-threats/asset-management/asset-configurations/asset-roles).

The Asset Roles configuration permissions control the ability to view, create, edit, and assign endpoints to functional asset roles.

| Permissions | Description                                                                                                                                                        | Roles Example                                                                                                                                                                                                        |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| None        | No access to the **Assets Roles Configuration** page.                                                                                                              | SOC Tier-1 Analyst: The role configuration is not part of daily operations                                                                                                                                           |
| View        | Read-only access to the **Assets Role Configuration** page, including viewing the roles list, details, members, and searching/filtering roles.                     | <ul><li>SOC Tier-2 Analyst: Reference role context during investigations.</li><li>SOC Tier-3 Analyst: Understand role assignments for analysis,</li><li>Threat Hunter: Reference role context for hunting.</li></ul> |
| View/Edit   | All view capabilities, plus all view/edit actions, such as add, edit, delete, and add endpoints to a role, as well as manually assign endpoints to specific roles. | Security Engineer: Configure and maintain asset roles.                                                                                                                                                               |

**Required and recommended permissions**

To effectively assign roles and investigate threats targeting specific functional users or servers, administrators and analysts require visibility into the underlying identity analytics and the overarching asset inventory. Consider adding the following permissions:

| Permission        | Permission Level | Reason                                                     |
| ----------------- | ---------------- | ---------------------------------------------------------- |
| Asset Inventory   | View             | Required to view assets associated with roles.             |
| Identity Security | View             | Strongly recommended to view identity analytics data.      |
| Host Insights     | View             | Recommended to view endpoint details for the role context. |
| Query Center      | View             | Recommended to run XQL queries on role data.               |
