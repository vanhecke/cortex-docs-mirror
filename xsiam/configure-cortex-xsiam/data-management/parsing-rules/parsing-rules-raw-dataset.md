---
description: Work with the raw dataset used by Cortex XSIAM Parsing Rules.
---

# Parsing Rules Raw Dataset

{% hint style="warning" %}
### Prerequisite

Parsing Rules requires **View/Edit** RBAC permissions for **Data Management** (under **Configurations** → **Data Management**), which are the same permissions required for Dataset Management, Data Model Rules, and Event Forwarding.
{% endhint %}

Each vendor and product has its own raw dataset that uses the format `<vendor>_<product>_raw`. For example, for Palo Alto Networks Next-Generation Firewall, the dataset is called `panw_ngfw_raw`. This raw dataset by default keeps all raw logs, whether ingested or dropped for other datasets.

You can override the default raw dataset, by creating an `INGEST` section referring to that dataset.

The following syntax overrides the `panw_ngfw_raw` automatic Parsing Rule:

```programlisting
[ingest:vendor=panw, product=ngfw, target_dataset=panw_ngfw_raw]
filter ... | alter ...;
```
