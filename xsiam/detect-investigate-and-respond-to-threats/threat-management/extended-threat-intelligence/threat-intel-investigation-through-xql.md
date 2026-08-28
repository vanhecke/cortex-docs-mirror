---
description: >-
  Use Cortex XSIAM XQL to query XTI indicators, threat objects, and
  relationships for threat intelligence investigations.
---

# Threat intel investigation through XQL

XTI is integrated into the Cortex Query Language (XQL) system, empowering you to create investigations and hunt queries using the full depth of the XTI intelligence library.

You can query threat intel indicators and threat objects through the XQL Search Portal by navigating to **Investigation & Response → Search → Query Builder**.

The following threat intel XQL datasets are available:

| **Dataset name**                | **Description**                                                                                 |
| ------------------------------- | ----------------------------------------------------------------------------------------------- |
| _threat\_intel\_indicators_     | Contains all active threat intel indicators with their attributes.                              |
| _threat\_intel\_threat\_actors_ | Contains all threat intel actors with their attributes.                                         |
| _threat\_intel\_malware_        | Contains all threat intel malware families with their attributes.                               |
| _threat\_intel\_relationships_  | Describes associations between threat objects (threat actors, malware families) and indicators. |
| _issue\_to\_indicator_          | Correlates threat intel data with issues data.                                                  |

Select the **Schema** tab to see all fields available for each dataset.

{% hint style="info" %}
Because XTI datasets are holistic, stateful representations rather than time-bound logs, the Time frame filter is disabled for these datasets.
{% endhint %}

**Related links**

For general information about XQL, see [Cortex XSIAM XQL](../../../reference-and-developer-docs/cortex-agentix-xql).

## Using XTI datasets in correlation rules

Using XTI datasets in correlation rules is not supported. Contact Palo Alto Networks if you have any questions.

<br>
