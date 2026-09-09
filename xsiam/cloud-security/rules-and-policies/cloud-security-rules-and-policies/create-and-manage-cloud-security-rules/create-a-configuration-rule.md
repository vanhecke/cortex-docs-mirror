---
description: >-
  Create Cortex XSIAM configuration rules that identify cloud resource
  misconfigurations and policy violations.
---

# Create a configuration rule

Configuration (config) rules monitor your resource configurations for potential policy violations or misconfigurations. Perform this task to create a custom configuration rule that you can use in a cloud security policy.

1. Navigate to **Posture Management** → **Rules & Policies** → **Rules** → **Cloud Security**.
2. Select **Create Rule > Config.**
3. Complete the **Overview** step:
   1. Enter a **Rule Name** and **Description**.
   2. Select a **Severity**. This will be the severity of any issues created with this rule.
   3. (Optional) Add **Labels**. These rules can be used to find rules when creating custom policies.
   4. (Optional) Enable Remediation using the toggle. In a later step, you'll enter the remediation instructions.
   5. (Optional) Associate this rule with a **Compliance Control**. Click **Add**, select one or more custom compliance controls from the list, and then click **Assign**.Custom configuration rules can only be associated with custom compliance controls.
   6. Click **Next**.
4. In the **Rule Logic** step, use the query builder to define the detection criteria. Select one of the following modes:
   1. **Simple Mode**: Presents a guided interface in which you can define basic conditions and address most common rule use cases.
   2. **Advanced Mode**: Presents a free-form XQL editor that allows you to build complex and flexible queries across unrestricted datasets. Supports advanced and custom use cases.
5. If you selected **Simple Mode**, complete the following steps:
   1. Select options from the dropdown menus to define the logic for your config rule, such as “Find EC2 instances where accessKeys are allowed”, and then click **Search** to view all matching results.
   2. Click **Next** to define Remediation instructions (if you had turned on Enable Remediation in the Overview step) or click **Done**.
6. If you selected **Advanced Mode**, complete the following steps:
   1. Define an XQL query for the rule, following the guidelines in [Guidelines for creating cloud security rules](#guidelines-for-creating-cloud-security-rules). For detailed XQL query instructions, see [XQL Language Structure](https://app.gitbook.com/s/mxWuY3s7AUvWfzCV9p1A/cortex-cloud-xql/get-started-with-xql/xql-language-structure).
   2. Click **Test** to determine if the query is valid.
   3. Select the **Affected Asset Type**. Generated issues will be linked to assets identified by the selected field.
   4. Check the list of query results to verify that the query is working as intended.
   5. Click **Next** to define Remediation instructions (if you had turned on Enable Remediation in the Overview step) or click **Done**.
7. (Optional) In the text field, define remediation actions or provide other information that will be included on issues created by this rule.
8. Click **Done** to save your config rule.

## **Guidelines for creating cloud security rules** <a href="#guidelines-for-creating-cloud-security-rules" id="guidelines-for-creating-cloud-security-rules"></a>

Follow these guidelines when creating an XQL query in a cloud security configuration rule. These are the requirements for creating a valid XQL query.XQL queries are supported for cloud security configuration rules only. XQL queries are not yet supported for other types of cloud security rules.

1. Use the `asset_inventory` dataset in config rules. No other datasets are supported.
2. Construct query conditions using the configuration JSON located in xdm.asset.raw\_fields. Example:`json_extract_scalar(`**`xdm.asset.raw_fields`**`, "$.Platform Discovery.metadataOptions.httpEndpoint")`
3. The evaluated asset type must be explicitly specified in the **filters** stage. Example:` dataset = asset_inventory | filter xdm.asset.provider = "aws" and`` `` `**`xdm.asset.type.id`**` `` ``= "LAMBDA_FUNCTION"| alter authType = json_extract_scalar(xdm.asset.raw_fields, "$.Platform Discovery.AuthType") | fields xdm.asset.id as asset_id, xdm.asset.type.class as class_name, xdm.asset.type.id as asset_type_id `
4. The query output must contain the `asset_id` (representing the asset) and `asset_type_id`. (representing the asset type).` dataset = asset_inventory | filter xdm.asset.provider = "aws" and xdm.asset.type.id = "LAMBDA_FUNCTION"| alter authType = json_extract_scalar(xdm.asset.raw_fields, "$.Platform Discovery.AuthType") | fields xdm.asset.id as`` `` `**`asset_id`**` , xdm.asset.type.class as class_name, xdm.asset.type.id as`` `` `**`asset_type_id`**
5. The query results must contain a maximum of 10 fields, including `asset_id` and `asset_type_id`.
6. The **fields** stage of the query must be positioned as the final step in the query pipeline.` dataset = asset_inventory | filter xdm.asset.provider = "aws" and xdm.asset.type.id = "LAMBDA_FUNCTION"| alter authType = json_extract_scalar(xdm.asset.raw_fields, "$.Platform Discovery.AuthType") |`` `` `**`fields xdm.asset.id as asset_id, xdm.asset.type.class as class_name, xdm.asset.type.id as asset_type_id`**

## **Example: XQL queries for cloud security rules**

Example XQL query for AWS EC2 in which IMDSv2 is not configured:

```programlisting
dataset = asset_inventory 
| filter xdm.asset.provider = "aws" and xdm.asset.type.id = "EC2_INSTANCE"
| alter state = json_extract_scalar(xdm.asset.raw_fields, "$.Platform 
Discovery.state.name")
| alter httpEndpoint = json_extract_scalar(xdm.asset.raw_fields, 
"$.Platform Discovery.metadataOptions.httpEndpoint")
| alter httpTokens = json_extract_scalar(xdm.asset.raw_fields, 
"$.Platform Discovery.metadataOptions.httpTokens")
| filter state contains "running" and httpEndpoint = "enabled" and 
httpTokens not contains "required"
| fields xdm.asset.id as asset_id, xdm.asset.type.id  as asset_type_id
```

## **Cloud security rule status for custom configuration rules** <a href="#cloud-security-rule-status-for-custom-configuration-rules" id="cloud-security-rule-status-for-custom-configuration-rules"></a>

Out-of-the-box and custom cloud security configuration rules are enabled by default, and can be manually disabled and reenabled as needed. Additionally, the system may change the status of custom configuration rules based on resource consumption.The statuses of cloud security configuration rules are described in the table below.

| **Status**    | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| ------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Enabled**   | Indicates that the rule is working normally.                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| **Moderated** | Indicates that the rule is consuming higher than expected resources, so the system is executing the rule less frequently.You will receive an in-product notification if the status of a rule is changed to Moderated.                                                                                                                                                                                                                                                                         |
| **Suspended** | Indicates that the rule has been suspended for exceeding the maximum allowed resource consumption.You will receive an in-product notification if the status of a rule is changed to Suspended.To reenable a suspended rule, you must update the query in the rule. After saving the updated rule, the status will automatically change to **Enabled**. If the updated rule continues to use excessive resources, the system will move it back into the **Moderated** or **Suspended** status. |
| **Disabled**  | Indicates that the rule has been manually disabled.                                                                                                                                                                                                                                                                                                                                                                                                                                           |
