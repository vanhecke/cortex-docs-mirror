---
description: Define models in Cortex XSIAM Data Model Rules.
---

# MODEL

A **MODEL** section is used to define the mapping between a single dataset and the data model. The **MODEL** section is mandatory per dataset. A **RULE** section is optional, and is used to help organize the **MODEL** sections.

**MODEL** syntax is derived from Cortex Query Language (XQL), with a few modifications, as explained in [Data Model Rules file structure and syntax](). In addition, **MODEL** sections contain the following syntax add-ons:

* You can have multiple **MODEL** sections.
*   **MODEL** sections take parameters, and not names as **RULE** sections use, where some are mandatory and others are optional.

    ```programlisting
    [MODEL: dataset=<dataset>, content_id=<content_id>]
    <build the XQL logic>;
    ```

The parameter descriptions are explained in the following table:

| Parameter   | Description                                                                                                                                                                                |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| dataset     | The name of the dataset that contains the source data to apply the mapping on (mandatory).                                                                                                 |
| content\_id | Identifier of the content as defined in the content package from the Marketplace. This parameter is relevant only for Default Rules and is not available in User Defined Rules (optional). |

```programlisting
[MODEL: dataset=panw_ngfw_traffic]
filter appid = "dns"
| alter dns_helper = json_extract(event, "$.dns")
| alter xdm.network.dns.opcode = to_integer(json_extract_scalar(dns_helper, "$.opcode"),
        xdm.network.dns.is_truncated = to_boolean(json_extract_scalar(dns_helper, "$.is_truncated")
);
```

<details>

<summary>Points to keep in mind when writing MODEL sections</summary>

* **MODEL** parameter names are not case-sensitive.
* Cortex Data Model (XDM) System fields (`_time`, `_insert_time`, `_vendor`, `_product`) are mapped automatically from the dataset from the fields with the same names.
* As section order is not significant, you do not have to declare a `RULE` before using it in a `MODEL` section.
* Each field used in the `MODEL` and `RULE` sections is constructed using dot notation with a specific format. Each field must be part of the predefined field set of the data model's schema. However, temporary variables, which will not affect the modeling, may be used. For more information, see [Field structure](field-structure).
*   A `MODEL` section can invoke a rule using the `call` stage.

    Example 50.

    In this example, both the [RULE](rule) and `MODEL` sections are provided, so you can see how the `call` stage invokes the rule.

    ```programlisting
    [RULE: common_ngfw_modeling]
    alter xdm.source.ipv4 = json_extract_scalar(actor, "$.client_ip")
    | alter xdm.network.ip_protocol = if(
        proto = 6, XDM_CONST.IP_PROTOCOL_TCP,
        proto = 11, XDM_CONST.IP_PROTOCOL_UDP,
        proto
    );
    ```

    ```programlisting
    [MODEL: dataset=panw_ngfw_traffic]
    filter appid = "dns"
    | call common_ngfw_modeling
    | alter dns_helper = json_extract(event, "$.dns")
    | alter xdm.network.dns.opcode = to_integer(json_extract_scalar(dns_helper, "$.opcode"),
            xdm.network.dns.is_truncated = to_boolean(json_extract_scalar(dns_helper, "$.is_truncated")
    );
    ```
*   You can use the `config case_sensitive` stage in the `MODEL` section to configure whether field values in the XDM are evaluated as case-sensitive or case-insensitive. The `config case_sensitive` stage must be added at the beginning of the query. If you do not provide this stage in your query, the default behavior is `false`; case is not considered when evaluating field values.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>The <strong>Settings</strong> → <strong>Configurations</strong> → <strong>XQL Configuration</strong> → <strong>Case Sensitivity (case_sensitive)</strong> setting can overwrite this <code>case_sensitive</code> configuration for all fields in the application except for BIOCs, which will remain case insensitive no matter what this setting is set to. For more information on this setting, see <a href="https://app.gitbook.com/s/FOhYBYLdbwpnbJgr6uaX/cortex-xdr-3.x-documentation/cortex-xdr-xql/stages/config/case_sensitive">case_sensitive</a>.</p></div>
*   Cortex XSIAM enables analytics to run on the following data:

    * All mapped network data to the network 5 tuple (source IP, source port, target IP, target port, IP protocol), automatically creating network stories for XDM network data.
    * All mapped authentication data, automatically creating authentication stories for XDM identity data when certain mandatory fields are mapped. For more information, see [How to map authentication story events?](../how-to-map-authentication-story-events).

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>We recommend that you do not configure the same data source in both Marketplace and using a Cortex XSIAM data collector. Yet, if you do, the following will happen:</p><ul><li>For network data, all relevant logs from the different data sources are stitched to the same network story.</li><li>For authentication data, all relevant logs from the different data sources are stitched to the same authentication story as long as the logs contain the network 5 tuple (source IP, source port, target IP, target port, IP protocol). The rest of the logs, without the network 5 tuple, create duplicate authentication stories.</li></ul></div>

</details>
