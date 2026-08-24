---
description: Define field structures in Cortex XSIAM Data Model Rules.
---

# Field structure

{% hint style="warning" %}
### Prerequisite

Data Model Rules requires **View/Edit** RBAC permissions for **Data Management** (under **Configurations** → **Data Management**), which are the same permissions required for Dataset Management, Parsing Rules, and Event Forwarding.
{% endhint %}

When creating Data Model Rules, each field used in the `MODEL` and `RULE` sections is constructed using dot notation using the following format:

```programlisting
xdm.<context>.[<compound>].<field>
```

*   `xdm.<context>.[<compound>].<field>`

    Example 53.

    ```programlisting
    xdm.source.host.device_id
    ```
*   `xdm.<context>.<field>`

    Example 54.

    ```programlisting
    xdm.source.ipv4
    ```

| Part         | Description                                                                                                                                                                     |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `<context>`  | This is a composition of fields (`<field>`), either simple or `<compound>`, that are grouped together to form a logically coherent unit.                                        |
| `<compound>` | This is a set of simple fields that are grouped together to form a meaningful group. For example, `subject` and `recipients` are part of the `<compound>` field called `email`. |
| `<field>`    | This is a field that represents a primitive data type, such as a string or number or an array, or an IP address.                                                                |

{% hint style="info" %}
### Note

For more information on these data model fields, see [XSIAM Data Model Schema](https://app.gitbook.com/s/HVBaxKOW1b6qcIQ6iMBh/).
{% endhint %}

<details>

<summary>Using ENUM fields</summary>

For fields of the `ENUM` type, you can map values from a predefined list of ENUMs. For example, the field `xdm.network.ip_protocol` is defined as `Enum.IP_PROTOCOL`, so you can assign it values such as `XDM_CONST.IP_PROTOCOL_TCP`. The full list can be found in the automatically suggested values for the relevant fields.

This syntax is not mandatory, and you can map any `STRING` value, but we recommend its use for consistency across all model mapping.

```programlisting
[RULE: common_ngfw_modeling]
alter xdm.source.ipv4 = json_extract_scalar(actor, "$.client_ip")
| alter xdm.network.ip_protocol = if( 
    proto = 6, XDM_CONST.IP_PROTOCOL_TCP, 
    proto = 11, XDM_CONST.IP_PROTOCOL_UDP, 
    proto
);
```

</details>
