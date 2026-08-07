---
description: >-
  Cortex XSIAM enables you to investigate any threat, also referred to as a
  lead, which has been detected.
---

# Research a known threat

This topic describes the steps you can take to investigate a lead. A lead can be:

* An issue from a non-Palo Alto Networks system with information relevant to endpoints or firewalls.
* Users or hosts that have been reported as acting abnormally.
* Information from online articles or other external threat intelligence that provides well-defined characteristics of the threat.

To research a known threat

1.  Use threat intelligence to build a Cortex Query Language (XQL) query using the Query Builder.

    For example, if external threat intelligence indicates a confirmed threat involving specific files or behaviors, search for those characteristics.
2. Review and refine the query results by using filters and running follow-up queries to find the information you are looking for.
3.  Select an event of interest, and open the **Causality view**.

    Review the chain of execution and data, navigate through the processes on the tree, and analyze the information.
4. Open the **Timeline** to view the sequence of events over time. If deemed malicious, take action using one or more of the response actions.
5.  Inspect the information again, and identify any characteristics you can use to create a BIOC or correlation rule.

    If you can create a BIOC or correlation rule, test and tune it as needed. For more information, see [Create a correlation rule](../threat-management/detection-rules/what-are-detection-rules/whats-a-correlation-rule/create-a-correlation-rule) and [Create a BIOC rule](../threat-management/detection-rules/what-are-detection-rules/whats-a-bioc/create-a-bioc-rule).
