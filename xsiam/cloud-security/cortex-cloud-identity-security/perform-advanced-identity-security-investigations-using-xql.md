---
description: Working with datasets in Cloud Identity Security.
---

# Perform advanced Identity Security investigations using XQL

{% hint style="info" %}
This feature is included with a Cortex XSIAM Premium license. It is also included with any other Cortex XSIAM license that has the Cloud Posture Security or Cloud Runtime Security add-on.
{% endhint %}

#### Overview

Cloud Identity Security centralizes identity-related information into a list of datasets, providing the foundation for comprehensive security investigations. Using Cortex Query Language (XQL) , security practitioners can create custom queries to extract valuable insights from these data sources within your system. For more information, see [Get started with XQL](../../reference-and-developer-docs/cortex-agentix-xql/get-started-with-xql).

You can use the following identity-related datasets:

| Dataset                               | Description                                                                                                                                                                                                                                                                                 |
| ------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ciem\_permissions\_with\_last\_access | Contains the permissions of each identity that is discovered in your environments, including the time of their last access when applicable.                                                                                                                                                 |
| asset\_inventory                      | Contains an inventory of all the assets that are discovered in your environments. For more information, see [Asset management](../../detect-investigate-and-respond-to-threats/asset-management).                                                                                           |
| issues                                | Contains the issues that are related to the assets in your environments. For more information, see [Issues](../../../detect-investigate-and-respond-to-threats/investigation-and-response/case-concepts/issues-findings-and-events#issues).                                                 |
| findings                              | Contains the findings that are associated with the assets that are found in your environments. For more information, see [Findings and events](../../../detect-investigate-and-respond-to-threats/investigation-and-response/case-concepts/issues-findings-and-events#findings-and-events). |

#### Investigate Cloud Identity Security

To run queries on your Cloud Identity Security datasets:

1. In Cloud, in the navigation pane on the left, click **Investigation & Response**, then under **Search**, click **XQL Search**.
2. On the **XQL Search** screen, under **XQL Query**, in the text box, start typing your query. Alternatively, you can search for existing queries on the **Query Library** tab.
3. When you have finished entering your query, click **Run**. The results appear on the **Query Results** tab.

{% hint style="info" %}
### Note

For more information, see [Build XQL queries](../../detect-investigate-and-respond-to-threats/investigation-and-response/build-xql-queries).
{% endhint %}

#### Examples

Here are some examples of identity-related queries you can run in Cortex Cloud to investigate your identity posture:

<details>

<summary>1. Count the number of admin sources per account</summary>

```programlisting
dataset = ciem_permissions_with_last_access 
| filter action_access_isadministrative in(true, TRUE) 
| dedup source_cloud_resource_uai, source_cloud_account_id 
| comp count(source_cloud_resource_uai) as admins_count by source_cloud_account_id  
| sort desc admins_count
```

</details>

<details>

<summary>2. Azure service principals granting write permissions on the subscription level</summary>

```programlisting
dataset =  ciem_permissions_with_last_access
| filter dest_cloud_type = "AZURE" and action_access_level contains "Write" and grantedby_level_type = "AZURE_SUBSCRIPTION" and grantedby_cloud_entity_type = "service principal"
| fields source_cloud_resource_name, source_cloud_resource_type, grantedby_cloud_entity_name, grantedby_level_name, grantedby_level_type
```

</details>

<details>

<summary>3. Group permissions on production assets</summary>

```programlisting
dataset = ciem_permissions_with_last_access
| filter dest_cloud_type = "GCP" and action_access_level = "config" and source_cloud_resource_type = "user" and grantedby_cloud_entity_type = "group" and wildcard_match("prod.*", dest_cloud_resource_name)
| fields source_cloud_resource_name, grantedby_cloud_entity_name, dest_cloud_resource_name, dest_cloud_resource_type
```

</details>

<details>

<summary>4. Users without MFA and sensitive S3 and EC2 permissions</summary>

```programlisting
dataset =  ciem_permissions_with_last_access
| filter source_cloud_type = "aws" and source_cloud_resource_type = "user" and action_access_level contains "Config" and dest_cloud_service_name in ("s3", "ec2")
| join (dataset = asset_inventory) as assets source_cloud_resource_uai = assets.xdm.asset.id
| filter lowercase(json_extract_scalar(xdm.asset.normalized_fields, "$['xdm.identity.has_mfa']")) = "false"
```

</details>

<details>

<summary>5. Azure VM with data write permissions on the subscription levels</summary>

```programlisting
dataset = ciem_permissions_with_last_access
 | filter source_cloud_type = "azure" and source_cloud_resource_type = "virtualMachines" and (lowercase(action_access_level) contains "config" or lowercase(action_access_level) contains "write") and dest_cloud_resource_type ~= "^storageAccounts/blobServices" and grantedby_level_type = "AZURE_SUBSCRIPTION"
```

</details>

<details>

<summary>6. Policies granting wildcard permissions</summary>

```programlisting
dataset =  ciem_permissions_with_last_access 
| filter dest_cloud_resource_name ~= "^\*$" and grantedby_cloud_policy_type in ("AWS_CUSTOMER_MANAGED_POLICY", "AWS_MANAGED_POLICY")
| dedup grantedby_cloud_policy_id 
| fields grantedby_cloud_policy_id as policy_arn
```

</details>

<details>

<summary>7. Administrative roles open to third-party vendors and external unknown accounts</summary>

```programlisting
dataset =  ciem_permissions_with_last_access
| filter grantedby_cloud_entity_type = "role" and action_access_isadministrative = true and account_access in ("EXTERNAL_UNKNOWN", "THIRD_PARTY_VENDOR")
| fields grantedby_cloud_entity_name, grantedby_cloud_entity_account_name, source_cloud_account_name, account_access
```

</details>

<details>

<summary>8. Show identities with unused permissions</summary>

```programlisting
dataset = ciem_permissions_with_last_access 
| filter last_access_time != null and timestamp_diff(current_time(), last_access_time, "DAY") > 90 and source_cloud_resource_name !~= "^\*$"
| dedup source_cloud_resource_name, source_cloud_account_id, action_name, dest_cloud_resource_name, last_access_time
| fields  source_cloud_resource_name, source_cloud_account_id, action_name, dest_cloud_resource_name, last_access_time
```

</details>

<details>

<summary>9. Unused permissions by lambda functions</summary>

```programlisting
dataset = ciem_permissions_with_last_access 
| filter source_cloud_service_name= "lambda" and source_cloud_resource_type = "function" and source_cloud_region = "Virginia" and is_last_access_supported = true 
| alter days_since_used = timestamp_diff(current_time(), last_access_time, "DAY") 
| filter days_since_used > 90
| fields source_cloud_resource_uai, source_cloud_resource_name, days_since_used, action_name, action_access_level 
```

</details>

<details>

<summary>10. Get all the non-admin sources that can assume an admin role</summary>

```programlisting
dataset = ciem_permissions_with_last_access 
| filter action_name = "sts:AssumeRole"
| fields source_cloud_resource_uai, dest_cloud_resource_uai, dest_cloud_resource_id, dest_cloud_account_id 
| filter source_cloud_resource_uai not in(dataset = ciem_permissions_raw 
| filter action_access_isadministrative in(true, TRUE) 
| dedup source_cloud_resource_uai 
| fields source_cloud_resource_uai) 
| fields source_cloud_resource_uai as source, dest_cloud_resource_uai as dest_uai, dest_cloud_resource_id as dest_id, dest_cloud_account_id as dest_account_id 
| join(dataset = ciem_permissions_raw 
| filter grantedby_cloud_entity_type = "role" 
| filter action_access_isadministrative in(true, TRUE) 
| dedup grantedby_cloud_entity_id 
| fields grantedby_cloud_entity_account_id, grantedby_cloud_entity_id) as admin_roles (dest_id = admin_roles.grantedby_cloud_entity_id or (dest_id ~= "^\*$" and dest_account_id = admin_roles.grantedby_cloud_entity_account_id)) 
| fields source
```

</details>

<details>

<summary>11. Administrative permissions granted to EC2 instances that can access multiple services</summary>

```programlisting
dataset = ciem_permissions_with_last_access
| filter source_cloud_resource_type = "instance" and source_cloud_service_name = "EC2" and action_access_isadministrative = true
| comp values(action_name) as actions by source_cloud_resource_uai, source_cloud_resource_name, source_cloud_account_id, grantedby_cloud_entity_name
| join (dataset = asset_inventory) as assets source_cloud_resource_uai = assets.xdm.asset.id
| alter access_to_services = to_integer(json_extract_scalar(xdm.asset.normalized_fields, "$['xdm.identity.access_statistics.services']"))
| filter access_to_services >= 10
| fields source_cloud_resource_name, source_cloud_resource_uai, access_to_services, grantedby_cloud_entity_name
```

</details>
