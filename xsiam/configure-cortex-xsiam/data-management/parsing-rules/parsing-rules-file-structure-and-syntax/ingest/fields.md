---
description: Use 'fields' in Cortex XSIAM Parsing Rules.
---

# fields

### Syntax

```
[INGEST: vendor="<vendor>", product="<product>", target_dataset="<dataset_name>"]
fields <field_1>, <field_2>, ... ;
```

### Description

The `fields` stage in the `INGEST` section of a parsing rule allows you to explicitly define which fields from a raw log should be saved into a dataset.

This stage works identically to the [fields](https://cortex-docs.paloaltonetworks.com/xql-command-reference-guide/readme/stages/fields) stage in XQL, which defines the columns returned in a query result set. Yet, when used within the `INGEST` section of a parsing rule, it serves to control the schema of the stored data.

#### **Usage**

Use the `fields` stage to:

* **Resume data flow:** If a dataset has reached its 2,000-field limit, you can use the `fields` stage to explicitly select only the necessary fields, allowing automatic parsing to continue.
* **Manage large datasets:** If you know in advance that a data source will ingest more than 2,000 fields, you can use this stage to pre-filter and define the specific fields you wish to retain.

{% hint style="info" %}
**Note**

For more details on field selection, including how to use aliases and wildcards, see the Cortex Query Language (XQL) [fields](https://cortex-docs.paloaltonetworks.com/xql-command-reference-guide/readme/stages/fields) stage reference.
{% endhint %}
