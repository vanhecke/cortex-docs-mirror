---
description: Define rules in Cortex XSIAM Data Model Rules.
---

# RULE

Rules are very similar to functions in modern programming languages. They are essentially named pieces of Cortex Query Language (XQL) syntax, and can be reused in the code in the `MODEL` sections, or in other `RULE` sections (recursively), by using `[rule:ruleName]`. A `RULE` is an optional data model syntax.

`RULE` syntax is derived from XQL with a few modifications, as explained in the [Data Model Rules file structure and syntax]().

{% hint style="info" %}
### Note

For more information on the XQL syntax, see the XQL Language Reference Guide.
{% endhint %}

<details>

<summary>Points to keep in mind when writing RULE sections</summary>

*   Rules are defined by `[rule:ruleName]` as shown in the following example:

    ```programlisting
    [RULE: common_ngfw_modeling]
    alter xdm.source.ipv4 = json_extract_scalar(actor, "$.client_ip")
    | alter xdm.network.ip_protocol = if(
        proto = 6, XDM_CONST.IP_PROTOCOL_TCP,
        proto = 11, XDM_CONST.IP_PROTOCOL_UDP,
        proto
    );
    ```
* Rules are invoked by using a `call` stage.
* Rule names are not case-sensitive.
* Rule names must be unique across the entire file.
* As section order is not significant, you do not have to declare a `rule` before using it. You can have the `rule` definition section written below other sections that use that specific rule.
* Each field used in the `MODEL` and `RULE` sections is constructed using dot notation with a specific format. However, temporary variables, which will not affect the modeling, can be used. For more information, see [Field structure](field-structure).

</details>
