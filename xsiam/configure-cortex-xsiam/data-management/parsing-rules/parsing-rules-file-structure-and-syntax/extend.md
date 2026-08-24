---
description: Extend default rule logic in Cortex XSIAM Parsing Rules.
---

# EXTEND

{% hint style="warning" %}
### Prerequisite

Parsing Rules requires **View/Edit** RBAC permissions for **Data Management** (under **Configurations** → **Data Management**), which are the same permissions required for Dataset Management, Data Model Rules, and Event Forwarding.
{% endhint %}

An `EXTEND` section is used to chain your Parsing Rules logic to extend your existing default `RULE` sections, which are added by a Content Package you installed from [Marketplace](../../../marketplace). While optional to configure, an `EXTEND` section runs immediately after the default `RULE` section that it extends, and enables data manipulation without overriding or interfering with the existing vendor Parsing Rules. For more information on the `RULE` section in Parsing Rules, see [RULE](rule).

`EXTEND` syntax is derived from Cortex Query Language (XQL) with a few modifications as explained in the [Parsing Rules file structure and syntax]() section. You can have multiple XQL statements, separated by a semicolon (;). Each statement creates a different extension.

{% hint style="info" %}
### Note

For more information on the XQL syntax, see [Get started with XQL](../../../../reference-and-developer-docs/cortex-agentix-xql/get-started-with-xql).
{% endhint %}

A few more points to keep in mind when writing `EXTEND` sections:

* You can only extend a default rule that is not overridden in the `RULE` sections.
* A rule can only be extended once.
* A `CONST` section that is defined in **Default Rules** cannot be used in the **User Defined Rules** when configuring an `EXTEND` section.
*   An `EXTEND` section must specify the full header of the rule it is extending. When you extend a rule that was added by a Content Package installed from Marketplace, the `EXTEND` section uses the format `[EXTEND:<rule name> content_id = "<pack id>"]`, where the `content_id` comes from the Content Package that the extended rule belongs to.

    Example 47.

    You can see here the `EXTEND` section in **User Defined Rules** uses the full header of the `RULE` it’s extending from **Default Rules**.

    Default Rules:

    ```programlisting
    [RULE:parse_ngfw_hipmatch content_id = "IronNet"]
    alter _time = time_generated
    | call extract_common_ngfw_fields
    | call extract_hipmatch_only_fields
    | call common_post_processing;
    ```

    User Defined Rules:

    ```programlisting
    [EXTEND:parse_ngfw_hipmatch content_id = "IronNet"]
    alter source = json_extract_scalar(source, "$.string")
    | filter __firewall_type = "firewall.hipmatch";
    ```

    When this rule is run, the default `RULE` section runs, and is immediately followed by the `EXTEND` section. This is equivalent to running one single `RULE` section as follows:

    ```programlisting
    [RULE:parse_ngfw_hipmatch content_id = "IronNet"]
    alter _time = time_generated
    | call extract_common_ngfw_fields
    | call extract_hipmatch_only_fields
    | call common_post_processing
    | alter source = json_extract_scalar(source, "$.string")
    | filter __firewall_type = "firewall.hipmatch";
    ```
