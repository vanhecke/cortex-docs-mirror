---
description: Learn Cortex XSIAM Data Model Rules file structure and syntax.
---

# Data Model Rules file structure and syntax

{% hint style="warning" %}
### Prerequisite

Data Model Rules requires **View/Edit** RBAC permissions for **Data Management** (under **Configurations** → **Data Management**), which are the same permissions required for Dataset Management, Parsing Rules, and Event Forwarding.
{% endhint %}

<details>

<summary>File structure</summary>

The Data Model Rules file consists of multiple sections of the following two types, which also represent the custom syntax specific to Data Model Rules:

* [MODEL](data-model-rules-file-structure-and-syntax/model): This section is used to define the mapping between a single dataset and the data model.
* (OPTIONAL) [RULE](data-model-rules-file-structure-and-syntax/rule): Rules are part of the Cortex Query Language (XQL) syntax, which are tagged with a name, and can be reused in the code in the **MODEL** sections, or in other **RULE** sections (recursively), by using `[rule:ruleName]`.

The order of the sections is not significant.

</details>

<details>

<summary>Syntax</summary>

The syntax used in the Data Model Rules file is derived from XQL, with a few modifications. This subset of XQL is called _XQL for Data Modeling (XQLm)_.

{% hint style="info" %}
### Note

For more information on XQL syntax, see the XQL Language Reference Guide.
{% endhint %}

In the `MODEL` and `RULE` sections, the following modifications apply to the XQLm syntax:

*   Only the following XQL stages are permitted: [alter](https://app.gitbook.com/s/fUtoMSNyY2P8jbK3cQsM/readme/stages/alter) and [filter](https://app.gitbook.com/s/fUtoMSNyY2P8jbK3cQsM/readme/stages/filter). An additional `call` stage is supported, which is used to invoke another rule.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>You cannot <code>call</code> a <code>RULE</code> section that exists in Default Rules from the User Defined Rules section.</p></div>
* No output stages are supported.
* `XDM_ALIAS` cannot be used in rules. It is only supported in queries. For more information, see the [search](https://app.gitbook.com/s/fUtoMSNyY2P8jbK3cQsM/readme/stages/search) stage.
* Every model definition in the Data Model Rules file must end with a semicolon (`;`).
*   Each XDM field used in the `MODEL` and `RULE` sections is constructed using dot notation using the following format:

    ```programlisting
    xdm.[<context>].[<compound>].<field>
    ```

    For more information, see [Field structure](data-model-rules-file-structure-and-syntax/field-structure).

</details>
