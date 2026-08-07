---
description: Working with datasets in Cortex Cloud AI Security.
---

# How to perform advanced AI Security investigations using XQL

{% hint style="info" %}
This feature is included with a Cortex XSIAM Premium license. It is also included with any other Cortex XSIAM license that has the Cloud Posture Security or Cloud Runtime Security add-on.
{% endhint %}

#### Overview

Cortex Cloud AI Security centralizes information about your AI ecosystem into a list of datasets, providing the foundation for comprehensive security investigations. Using Cortex Query Language (XQL) , security practitioners can create custom queries to extract valuable insights from these data sources within their appliance. For more information, see [Get started with XQL](../../reference-and-developer-docs/cortex-agentix-xql/get-started-with-xql).

You can use the following AI-related datasets:

| Dataset                             | Description                                                                                                                                                                                                                                                                                                                                                                |
| ----------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| asset\_inventory                    | Provides a normalized, structured inventory of all digital assets across your AI environment, including detailed metadata for each asset, such as type, cloud provider, region, and security configurations. The dataset also maps relationships between assets, enabling the identification of complex AI and cloud dependencies for a comprehensive AI security posture. |
| classification\_mgmt\_data\_profile | Provides administrative insights into the data classification policies and profiles configured within the Cortex Cloud Data Classification service.This dataset is primarily used for monitoring and managing the data classification rules in the Cortex Cloud environment.                                                                                               |
| findings                            | Contains the findings that are associated with the assets that are found in your environments. For more information, see [Findings and events](../../../detect-investigate-and-respond-to-threats/investigation-and-response/case-concepts/issues-findings-and-events#findings-and-events).                                                                                |
| issues                              | Consolidates all AI security vulnerabilities, misconfigurations, and threats detected by Cortex Cloud AI Security. Each entry includes detailed context, such as the affected asset ID, a risk score, a description of the issue, and suggested remediation steps. This dataset provides a unified, actionable view of all security risks for your organization.           |

#### Investigate Cortex Cloud AI Security

To run queries on your Cortex Cloud AI Security datasets:

1. In Cortex Cloud, in the navigation pane on the left, click **Investigation & Response**, then under **Search**, click **Query Builder**.
2. Click **XQL**.
3. You can start typing your query in the box at the top of the screen, or search for existing queries on the **Query Library** tab.
4. Click **Run**. The results of the query appear on the **Query Results** tab.

{% hint style="info" %}
### Note

For more information, see [Build XQL queries](../../detect-investigate-and-respond-to-threats/investigation-and-response/build-xql-queries).
{% endhint %}

#### Examples

Here are some examples of AI-related queries you can run in Cortex Cloud to investigate your AI Security posture:

<details>

<summary>1. AI assets that were first discovered in the last 7 days</summary>

```programlisting
dataset = asset_inventory
| filter xdm.asset.type.class = "AI"
| alter found = xdm.asset.first_observed
| filter timestamp_diff(found, current_time(), "DAY") >= 7
| fields
    xdm.asset.name as Asset_Name,
    xdm.asset.type.category as Asset_Type,
    xdm.asset.first_observed as First_Observed,
    xdm.asset.provider as Cloud,
    xdm.asset.cloud.region as Region
```

</details>

<details>

<summary>2. Sensitive AI assets, such as datasets containing sensitive data, models trained on sensitive data, or model endpoints using sensitive inference data</summary>

```programlisting
dataset = asset_inventory
| filter xdm.asset.type.class = "AI"
| join (
    dataset = findings
    | filter xdm.finding.type_id = 110000001
) as sensitive_AI sensitive_ai.xdm.finding.asset_id = xdm.asset.id
| fields
    xdm.asset.name as Asset_Name,
    xdm.asset.type.category as Asset_Type,
    xdm.asset.provider as Cloud,
    xdm.finding.normalized_fields as Sensitive_Data
```

</details>

<details>

<summary>3. Fine-tuned AI models</summary>

```programlisting
dataset = asset_inventory
| filter xdm.asset.type.category = "Model" and xdm.ai.model.kind = "FINE_TUNED"
| fields
    xdm.asset.name as Asset_Name,
    xdm.asset.type.category as Asset_Type,
    xdm.asset.provider as Cloud,
    xdm.ai.model.kind as model_kind
```

</details>

<details>

<summary>4. Public AI deployments that are accessible from the public internet</summary>

```programlisting
dataset = findings
| filter xdm.finding.type_id = 110000004
| join (dataset = asset_inventory | filter xdm.asset.type.category = "Model Endpoint") as public_endpoints public_endpoints.xdm.asset.id = xdm.finding.asset_id
| fields xdm.asset.name as Asset_Name, xdm.asset.type.category as Asset_Type, xdm.asset.provider as Cloud
```

</details>

<details>

<summary>5. AI datasets containing sensitive PII data</summary>

```programlisting
dataset = asset_inventory
| filter xdm.asset.type.class = "AI" and xdm.asset.type.category = "Dataset"
| join(
    dataset = findings
    | filter xdm.finding.type_id = 110000001
    | filter xdm.finding.is_active = TRUE
    | alter data_profile = json_extract_scalar_array(xdm.finding.normalized_fields, "$['xdm.data.data_profile']")
    | arrayexpand data_profile
) as sensitive_AI sensitive_ai.xdm.finding.asset_id = xdm.asset.id
| join(
    dataset = classification_mgmt_data_profile
    | filter name = "PII" and enabled = True
) as data_profile_def data_profile_def.id = to_integer(data_profile)
| fields name as data_type, xdm.asset.name as dataset_name, xdm.asset.strong_id as dataset_full_path, xdm.asset.provider as dataset_provider, xdm.asset.realm as dataset_realm, xdm.asset.type.name as dataset_type, xdm.finding.description as description
```

</details>

<details>

<summary>6. AI datasets containing sensitive PCI data</summary>

```programlisting
dataset = asset_inventory
| filter xdm.asset.type.class = "AI" and xdm.asset.type.category = "Dataset"
| join(
    dataset = findings
    | filter xdm.finding.type_id = 110000001
    | filter xdm.finding.is_active = TRUE
    | alter data_profile = json_extract_scalar_array(xdm.finding.normalized_fields, "$['xdm.data.data_profile']")
    | arrayexpand data_profile
) as sensitive_AI sensitive_ai.xdm.finding.asset_id = xdm.asset.id
| join(
    dataset = classification_mgmt_data_profile
    | filter name = "PCI" and enabled = True
) as data_profile_def data_profile_def.id = to_integer(data_profile)
| fields name as data_type, xdm.asset.name as dataset_name, xdm.asset.strong_id as dataset_full_path, xdm.asset.provider as dataset_provider, xdm.asset.realm as dataset_realm, xdm.asset.type.name as dataset_type, xdm.finding.description as description
```

</details>

<details>

<summary>7. AI assets with more than one issue</summary>

```programlisting
dataset = asset_inventory
| filter xdm.asset.type.class = "AI" and xdm.asset.type.category in ("Dataset", "Model", "Model Endpoint")
| join (
    dataset = issues_with_sbac
    | fields xdm.issue.id as issue_id, xdm.issue.domain, xdm.issue.status.progress as progress, xdm.issue.is_excluded as is_excluded
    | filter xdm.issue.domain = "POSTURE" and is_excluded != true and progress != "RESOLVED"
    | join type = inner (
        dataset = issue_to_asset
        | fields xdm.asset.id as ita_assetid, xdm.issue.id
    ) as its its.xdm.issue.id = issue_id
    | fields issue_id, ita_assetid
    | comp count(issue_id) as issues_count by ita_assetid
) as iss iss.ita_assetid = xdm.asset.id
```

</details>

<details>

<summary>8. VMs deploying self-managed AI models</summary>

```programlisting
dataset = asset_inventory
| filter xdm.asset.type.class = "AI" and xdm.asset.type.category in ("Model") and xdm.asset.type.id = "SELF_MANAGED_MODEL"
| alter relation = json_extract_array(xdm.asset.normalized_fields, "$['xdm.asset.relations']")
| arrayexpand relation
| alter relation_type = json_extract_scalar(relation, "$['xdm.asset.relation.type']")
| filter relation_type in("DEPLOYED_ON")
| alter relation_asset_id_to_find = json_extract_scalar(relation, "$['xdm.asset.relation.asset_id']")
| dedup relation_asset_id_to_find
| join(
    dataset = asset_inventory
) as vm_asset vm_asset.xdm.asset.id = relation_asset_id_to_find
| fields xdm.asset.name as compute_instance_name, xdm.asset.realm as compute_instance_realm, xdm.asset.provider as compute_instance_provider, xdm.asset.type.name as compute_instance_type
```

</details>

<details>

<summary>9. Disks storing self-managed AI models</summary>

```programlisting
dataset = asset_inventory
| filter xdm.asset.type.class = "AI" and xdm.asset.type.category in ("Model") and xdm.asset.type.id = "SELF_MANAGED_MODEL"
| alter relation = json_extract_array(xdm.asset.normalized_fields, "$['xdm.asset.relations']")
| arrayexpand relation
| alter relation_type = json_extract_scalar(relation, "$['xdm.asset.relation.type']")
| filter relation_type in("STORED_IN")
| alter relation_asset_id_to_find = json_extract_scalar(relation, "$['xdm.asset.relation.asset_id']")
| dedup relation_asset_id_to_find
| join(
    dataset = asset_inventory
) as vm_asset vm_asset.xdm.asset.id = relation_asset_id_to_find
| fields xdm.asset.name as disk_name, xdm.asset.realm as disk_realm, xdm.asset.provider as disk_provider, xdm.asset.type.name as disk_type, xdm.asset.strong_id as disk_id
```

</details>

<details>

<summary>10. Active AI models with the number of days since last used</summary>

```programlisting
dataset = asset_inventory
| filter xdm.asset.type.class = "AI"
| filter xdm.asset.type.category in ("Model")
| join (
    dataset = findings
    | filter xdm.finding.type_id = 110000007 and xdm.finding.is_active = TRUE
    | alter days_since_invoked = json_extract_scalar(xdm.finding.extended_fields, "$['days_since_invoked']")
) as model_activity model_activity.xdm.finding.asset_id = xdm.asset.id
| fields xdm.asset.name as Asset_Name, xdm.asset.type.category as Asset_Type, xdm.asset.first_observed as First_Observed, xdm.asset.provider as Cloud, xdm.asset.cloud.region as Region, days_since_invoked
```

</details>
