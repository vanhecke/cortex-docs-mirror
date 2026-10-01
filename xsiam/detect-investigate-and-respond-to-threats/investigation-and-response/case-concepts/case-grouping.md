---
description: >-
  Learn how Cortex XSIAM automatically groups related issues and artifacts into
  unified cases.
---

# Case grouping

Case grouping is a Precision AI™-powered capability that eliminates alert fatigue by automatically consolidating related issues and artifacts into a single unified case. Case grouping links issues that originate from the same attack flow or involve the same entity to reveal the full scope of a case. This approach replaces manual correlation with automated context, allowing you to focus on resolving complete problems rather than triaging isolated events.

{% hint style="warning" %}
Case grouping is supported for Security and Posture domains only.
{% endhint %}

### **Grouping methodologies**

The key grouping methodologies of case grouping in Cortex XSIAM are:

* **Artifact association:** Groups issues that share core artifacts (for example, SHA256, HostName, UserName).
* **Exact match detection:** Groups similar detections for the same entities.
* **Related entities:** Groups detections involving related assets within a close timeframe to highlight possible connections.

### **Case grouping qualification**

When a new issue is triggered, it is evaluated to determine if it meets the criteria for case promotion. If the issue qualifies, the system uses case grouping logic to correlate the issue with an existing case; if no match is found, a new case is generated.&#x20;

{% hint style="info" %}
The case grouping logic is dynamic and may be updated to reflect ongoing research and threat relevance.
{% endhint %}

Issues with the following conditions automatically qualify for case grouping:

* Assigned to the **Security** domain with **Medium** severity or higher.
* Assigned to the **Posture** domain with **Medium** severity or higher.

While case grouping is active, Cortex XSIAM can continue to link new issues to a case, however, to keep cases manageable, specific grouping thresholds are enforced. For more information see [Case thresholds](../overview-of-cases/case-thresholds).

In cases with multiple linked issues, you can see the connection between the issues and the case grouping status (active/inactive) in the [Grouping Graph](../analyze-and-resolve-cases/analyze-case-details/grouping-graph).&#x20;

### **Grouping artifacts**

The grouping algorithm evaluates extracted artifacts to determine whether an issue should join an existing case or initiate a new one. Each artifact type is governed by specific logic that accounts for its unique lifecycle and reliability. For example, grouping by Username may be subject to temporal constraints, while IP address logic varies based on whether the address is public, private, or dynamically allocated (DHCP).

These proprietary grouping logics are continuously tuned and updated. As a result, artifact behavior and correlation may change over time.

If you set up custom detections with correlation rules that trigger issues, you can influence the grouping of the triggered issues by mapping specific fields in your configuration. For more information, see [Optimize case grouping in correlations](../../../configure-cortex-xsiam/customize-cases-and-issues/optimize-case-grouping-in-correlations).

### **Integration with SmartScore**

Case grouping and SmartScore work together to improve triage efficiency. While case grouping provides the full context of an attack, **SmartScore** assigns a numerical value to that context, indicating the urgency and impact of the case. This allows you to prioritize the most critical cases first.
