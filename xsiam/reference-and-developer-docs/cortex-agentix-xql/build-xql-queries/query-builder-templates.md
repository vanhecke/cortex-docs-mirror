---
description: >-
  Use Query Builder templates to query your data sets without using the Cortex
  Query Language.
---

# Query Builder templates

You can use the Query Builder templates to create effective queries without using the Cortex Query Language (XQL).

From the Query Builder, you can select the following templates:

* **Basic**: Search by IP address, host name, user name, and domain.
* **Free text**: Search for a free text string.

The templates are set up with predefined filtering fields and fieldsets that are specific to the template type. You can specify values for the default fields and add any other required fields to refine and adapt your search. The Query Builder templates support any filtering fields from the Cortex Data Model (XDM) schema.

{% hint style="info" %}
### Tip

To get started with queries, you can run an empty template query with no values specified. The query results will include all of the fields in the template specific fieldset. Based on the query results, you can run subsequent queries to narrow down your search.
{% endhint %}
