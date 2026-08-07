# Query using Federated Search

To query using Federated search, navigate to **Incident Response → Investigation → Query Builder** and select **XQL**.

You can build queries across external datasets and ingested datasets, giving you a powerful tool.

In its current version, Federated Search enables only ad-hoc queries via the query builder. You can search, filter and use JOIN operations.

{% hint style="success" %}
**NOTE:**

The following aren't available in Federated Search and remain exclusive to fully ingested data.

* Complex, cross-source analytical functions, for example correlations, widgets, dashboards, and APIs
* `search`, `target` and `view` XQL stages


{% endhint %}

{% hint style="success" %}
**NOTE:**\
\
If there is a type mismatch between the schema and the data in the field, the query fails and Cortex XSIAM displays an error message. In this case, you must delete the external dataset, re-onboard it and make the required changes to the field type accordingly
{% endhint %}

