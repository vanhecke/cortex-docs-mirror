---
description: >-
  Manage endpoint application groups for Data Loss Prevention policies in Cortex
  XSIAM.
---

# Endpoint Applications Groups

Endpoint Applications Groups allow organizing endpoint applications into logical groups for use in Data-in-motion Rules. Instead of selecting individual applications in a rule, administrators can reference an application group, making rule management more scalable. Groups can contain custom application groups (user-defined collections of applications) and catalog web application groups (predefined web application categories).

Users access Endpoint Applications by going to **Modules** → **Data Security** → **Endpoint Data-in-Motion Rules** → **Endpoint Applications Groups**.

| Permission | Description                                                                                                                                                                                                                                                                                                                 | Recommended Roles                                                                                                                                                                                                                  |
| ---------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| None       | Users cannot access the **Endpoint Applications Groups** page. These users cannot see any application groups, their members, or their usage in rules.                                                                                                                                                                       | <ul><li>SOC Tier-1 Analyst: Application group management is outside Tier-1 scope.</li><li>Application group management is outside the IT infrastructure administration scope.</li></ul>                                            |
| View       | Users can navigate to the **Endpoint Applications Groups** page and see all application groups in the grid view. They can view group names, types (Custom Application Group, Catalog Web Applications Group), member applications, and group descriptions. They cannot create groups, edit existing ones, or delete groups. | <ul><li>SOC Tier-2 and 3 Analysts: May need to review group definitions when investigating DLP issues/advanced analysis.</li><li>Threat Hunter: May need to understand application groupings for threat hunting context.</li></ul> |
| View/Edit  | Users have full control over Endpoint Applications Groups. They can create new custom application groups and catalog web application groups, edit group membership and properties, and delete groups. All context menu actions are fully accessible.                                                                        | <ul><li>Security Engineer: Responsible for organizing applications into groups for DLP rule management.</li><li>Security Admin: Full administrative access to all DLP configurations.</li></ul>                                    |

**Required and recommended permissions**

Consider adding the following permissions:

| Permission            | Permission Level | Reason                                                                                                                                                         |
| --------------------- | ---------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Endpoint Applications | View             | Strongly recommended. Applications are organized into groups; viewing groups is essential to understanding how applications are categorized and used in rules. |
