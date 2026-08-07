# Asset Groups permissions

**Asset Groups permissions**

Asset Groups enable organizations to manage asset groups, such as creating logical groupings of assets, applying policies and rules to asset groups, scoping user access to specific asset groups (SBAC), and supporting automation exclusions by asset group.

{% hint style="warning" %}
### Caution

SBAC: Asset Groups form the foundation of Scope-Based Access Control (SBAC). Granting a user View/Edit access to Asset Groups allows them to modify the groups that dictate data access boundaries for other users in the tenant.
{% endhint %}

The following features are affected:

* Asset Groups: **Inventory** → **Assets** → **Groups**. For more information, see [Asset groups](../../../detect-investigate-and-respond-to-threats/asset-management/asset-groups).
* User Groups: When defining or editing a user group, you can scope an asset by defining the access group. For more information, see [Scope user access to applications (Application SBAC)](https://app.gitbook.com/s/8Z0RLJ1BFF5TQL8VtUeK/application-security-posture-management-aspm/applications/scope-user-access-to-applications-application-sbac).
* Automations Exclusion Center: When selecting Edit Policy, you can add an Asset Group to exclude the relevant asset class. For more information, see [Manage automation exclusion policies](../../../configure-cortex-xsiam/automations/automation-exclusion-center/manage-automation-exclusion-policies).

| Permissions | Description                                                                                                                | Roles Example                                                                                                                                                                                                             |
| ----------- | -------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| None        | No access to the Asset Group Menu, and limited ability to view groups in SBAC and Select groups in Automation Exclusion.   | SOC Tier 1 Analyst: Asset group management is not part of the daily operations.                                                                                                                                           |
| View        | Read-only access to the View Assets Group list, details, members, search and filter groups, and only view groups in SBAC.  | <ul><li>SOC Tier 2 Analyst: Reference asset groups during investigations</li><li>SOC Tier 3 Analyst: Understand asset groupings for analysis.</li><li>Threat Hunter: Reference asset groups for scoped hunting.</li></ul> |
| View/Edit   | All View capabilities, plus create, edit, delete, add assets to a group in SBAC, and select groups in automation exclusion | Security Engineer: Configure and maintain asset groups                                                                                                                                                                    |

**Recommended permissions**

Consider adding the following permissions:

| Permission      | Permission Level  | Reason                                                                                                                                |
| --------------- | ----------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| Asset Inventory | View or View/Edit | <ul><li>View: Required to view assets to add to groups.</li><li>View/Edit: Recommended to manage asset tags and properties.</li></ul> |
| Host Insights   | View              | Recommended to view endpoint details for group context                                                                                |
| Query Center    | View              | Recommended to run XQL queries on asset group data.                                                                                   |
