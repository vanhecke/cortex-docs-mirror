---
description: >-
  Assign Cortex XSIAM roles and groups, configure RBAC permissions, and apply
  SBAC granular access.
---

# Assign user roles and groups

Assign roles directly to users or create user groups and assign roles to those groups. We recommend creating user groups (with a user role), and assigning users to those user groups rather than creating direct roles for each user.

{% hint style="info" %}
If an existing user in the Cortex Gateway no longer has a role or a user group assigned, the user is revoked. Any roles, user groups, or egress configurations created by that user are shown as created by **Revoked user** instead of the user’s email address.
{% endhint %}

## Assign a user/user group to a role

Cortex XSIAM provides predefined built-in user roles that provide specific access rights that cannot be modified. You can also create custom, editable user roles. If a user does not have any Cortex XSIAM access permissions that are assigned specifically to them, the field displays **No-Role**.

{% stepper %}
{% step %}
Select **Settings** → **Configurations** → **Access Management** → **Users**.
{% endstep %}

{% step %}
Right-click the relevant user and select **Edit User Permissions**.

{% hint style="info" %}
To apply the same settings to multiple users, select them, and then right-click and select **Edit Users Permissions**.
{% endhint %}
{% endstep %}

{% step %}
Ensure the **Role** tab is selected.
{% endstep %}

{% step %}
Under **Role**, select the default or custom role.
{% endstep %}

{% step %}
(Optional) Under **User Groups**, add the user to a group.
{% endstep %}

{% step %}
(Optional) Under **Show Accumulated Permissions**:

1. Do one of the following:
   * Select all to view the combined permissions for every role and user group assigned to the user.
   * Select a specific role assigned to the user to view the available permissions for that role.
2. Under **Components**, expand each list to view the permissions.

{% hint style="warning" %}
Setting Cortex Query Language (XQL) dataset access permissions for a user role can only be performed from **Cortex XSIAM Access Management**. For more information, see [Manage user roles](../../../post-deployment/manage-user-roles-and-access-management#UUID-751d26ed-9390-dddd-d4f6-bb1f20db3a1d).
{% endhint %}
{% endstep %}

{% step %}
(Optional) You can configure and manage granular scoping:

1. Click the **Scope** tab.
2. Under **Scope Definition**, expand the scoping areas that you want to grant the user role access to in the tenant by clicking the chevron icon (**>**) beside the scoping area title, and make any changes required. The following sections explain the options available to configure:

{% hint style="warning" %}
Before configuring, ensure you review **Understand scoping** in the [Manage user scope](../../../post-deployment/manage-user-roles-and-access-management#UUID-071cdbb6-6c6a-6afe-3a67-1fa79991a0a8) section.
{% endhint %}

<details>

<summary>Assets</summary>

Set the **Scope** by selecting one of the following:

* **No assets**: No asset is accessible.
* **All assets**: Defines access to all assets.
* **Select asset groups**: Defines access to the specific assets associated with the Asset Groups selected, and to view all their related cases, issues, and findings for these specific assets and Asset Groups. Under **Select asset groups**, define the specific asset groups that you want to grant access. Only Asset Groups relevant for scoping are listed, which are asset groups that are using only the asset attributes listed in [Manage user scope](../../../post-deployment/manage-user-roles-and-access-management/manage-user-scope#UUID-071cdbb6-6c6a-6afe-3a67-1fa79991a0a8_section-idm235041053079477) (under **Understand scoping** → **Scoping Areas** → **Assets**).

The scoping of assets also affects the scoping of cases, issues, and findings.

{% hint style="info" %}
Visibility of Security domain Issues that refer to assets with agents is controlled by the **Endpoints** scoping configuration.
{% endhint %}

</details>

<details>

<summary>Cases and Issues</summary>

Set the Scope by selecting one of the following:

* No cases and issues: Defines access to no cases and issues.
* All cases and issues: Defines access to all cases and issues. Users can view cases or issues referencing assets within their scope. Use the Assets section to define which assets are in scope.
*   Select domains: Defines access to the domains selected to view their related cases and issues. Under Select domains, define the specific domains that you want to grant access.

    Users can only view cases or issues referencing assets and endpoints within their scope. Use the Assets section to define which assets are in scope.

When selecting All cases and issues or Select domains, you can separately configure access to issues and cases that lack an asset reference or where the referenced asset is not in All Assets and All Endpoints inventories. To provide access, select the Allow access to cases and issues that are not referencing known assets or endpoints checkbox. Once selected, you can specifically control which users have access to issues and cases that lack Affected Assets (as seen in the issue’s panel) and Assets (as seen in the case's panel), or where the listed assets are not part of the Asset or Endpoint inventories. When the assets listed are not part of the inventories, the asset string is typically non-clickable. In some cases, such as for identity-related issues, assets may open a dedicated User Risk View, which differs from the standard inventories panels. In the Issues and Cases tables, such items can be identified by empty values in the following columns: Asset IDs, Target Agent Identifier, and Source Agent Identifier.

</details>

<details>

<summary>Endpoints</summary>

Set the Scope by selecting one of the following:

* No endpoints: Defines access to no endpoints, with no ability to view their related agent management and enterprise policies.
* All endpoints: Defines access to all endpoints with the ability to view their related agent management and enterprise policies. This configuration can impact the visibility of related Security domain Cases and Issues, but will not affect asset visibility.
* Select specific (at least one required): Defines specific access to all endpoint groups by selecting Endpoint Groups or all endpoint tags by selecting Endpoint Tags to view their related agent management and enterprise policies. This configuration can impact the visibility of related Security domain Cases and Issues, but will not affect asset visibility.

</details>

<details>

<summary>Datasets Rows</summary>

Configure a `filter` to define the specific subset of rows a user is allowed to access in each raw dataset. A raw dataset is every dataset where Palo Alto Networks data is ingested out-of-the-box or third-party data is ingested using a configured dedicated collector, also called a data source. This filter configuration does not impact the visibility of cases and issues.

Follow these steps to configure a `filter`.

1.  For datasets where no `filter` is defined, determine how to set the When no filter is defined option as either:

    * No rows are accessible (default): Without a configured `filter`, no rows are accessible. Users can query the datasets in Cortex Query Language (XQL) as they have access, but the results will be empty.
    * All rows are accessible: Without a configured `filter`, all rows are accessible. Users can query the datasets in Cortex Query Language (XQL) as they have access, and view all results.

    When defining a filter for row-level scoping on raw datasets, queries based on the Cortex Data Model (XDM) are not supported. XDM queries return specific rows only when All rows are accessible is selected and no filter is defined in the Datasets Rows scoping area. Otherwise, no rows are returned.
2. Define any filters for the applicable datasets listed in the table:
   1. Scroll down the list of datasets to the dataset you want to apply a `filter` on, and click the Edit Scope icon.
   2.  In the Define what rows are accessible window, continue to write the query for the `filter` in the query box (where the syntax is a limited subset of XQL) to limit the data rows for the selected dataset according to the access permissions you want the user to have. The beginning of the query is already defined before the query box, and there is no need to include this in your query.

       For optimal performance, we recommend using a single field in the `filter` definition and simple comparison operators.

       Supported syntax

       **Fields**

       You can define the rest of the `filter` in the query box, where only the following system fields are supported: `_broker_device_id`, `_broker_device_ip`, `_broker_device_name`, `_collector_id`, `_collector_ip`, `_collector_name`, `_collector_type`, `_device_id`, `_final_reporting_device_ip`, `_final_reporting_device_name`, `_log_type`, `_product`, `_scope`, `_reporting_device_ip`, `_reporting_device_name`, and `_vendor`.

       For more information on these fields, see the table that describes all the fields in the `metrics_source` dataset and `metrics_view` preset in [Overview of data ingestion metrics](../../../configure-cortex-xsiam/cortex-xsiam-data-sources/administration-and-troubleshooting/overview-of-data-ingestion-metrics). For more information on the `_scope` field (relevant when `_scope` is defined in the Parsing Rule), see \[Scenario 3: Supported fields don't provide the necessary segmentation] in Scenarios related to Datasets Rows scoping.

       **Comparison operators**

       The following comparison operators are supported:

       * Exact matches (`=`, `!=`)
       * Comparing numerical values (`>`, `<`, `>=`, `<=`)
       * Checking membership in lists (`in`)
       * Querying arrays (`array_contains`)
       * Partial matches (`contains`, `starts_with`): Using this operator has additional performance overhead, and we recommend avoiding its use.

       If you only want a user to be able to access rows in the `pan_dds_raw` dataset, when the `_collector_name` is `bu2_collector` , you'd have to define the `filter` in the query box as:

       ```
       _collector_name = “bu2_collector”
       ```
   3. (Optional) Set the Time frame for the query. The default is Last 1 day.
   4. (Optional) You can preview the query results displayed based on your defined query by clicking Preview. You can edit your query until you're satisfied with the output. By default, the query results are limited to 1000 records.
   5.  When you are finished, click Done.

       The Scope field for the dataset that you added the filter on is updated with the query.

       In the above example, the Scope field displays `_collector_name = “bu2_collector”`.

</details>

{% hint style="warning" %}
By default, **Enable Scope Based Access Control** is disabled in Settings → Configurations → General → **Server Settings**, and granular scoping is not enforced. Before enabling SBAC, we recommend that an administrator or a user with **Access Management** permissions first ensures that the users, user groups, and API Keys defined in Cortex XSIAM are granted the required access by assigning the relevant scopes. For more information, see [Manage user scope](../../post-deployment/manage-user-roles-and-access-management/manage-user-scope).
{% endhint %}
{% endstep %}

{% step %}
Save the user group.
{% endstep %}
{% endstepper %}

**Perform additional tasks**

For more information about additional tasks such as creating a custom role, modifying a user's role, or removing a user's role, see [Manage user access](../../../post-deployment/manage-user-roles-and-access-management#UUID-a112c99e-112f-ab8a-e5ed-e31445dee8fe).
