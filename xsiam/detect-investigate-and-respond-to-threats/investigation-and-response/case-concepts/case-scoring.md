# Case scoring

A case score is a numeric value that indicates the urgency of a case. Scoring can help you to streamline the process of prioritizing and investigating your cases, and help you to identify the cases that require immediate attention.

### **Types of scoring**

Cortex XSIAM uses the following scoring methods:

*   **Rule-based scoring:** The score is determined by user-defined scoring rules that match the issues linked to the case.

    You create scoring rules that define scores for issues with specific attributes or assets. You can base scoring rules on:

    * Hostnames
    * Asset objects, such as asset names, classes, categories, groups, providers, and business application names.
    * IP addresses
    * Users
    *   Active Directory, or Azure groups and organization units

        (Requires the Cloud Identity Engine to be configured).

    When an issue is created, Cortex XSIAM searches for scoring rules that match the issue. An issue can match multiple rules or sub-rules. If a match is found, Cortex XSIAM assigns the scores of the matching rules to the issue. If multiple rules match the issue, the issue score is an aggregation of the rule scores. By default, a score is applied only to the first issue in the case that matches the defined rule and sub-rule.

    You can create a rule hierarchy by setting up sub-rules. If an issue matches one or more sub-rules, the sub-rule scores are also aggregated in the issue score. However, a sub-rule score is only applied to an issue if the top-level rule was a match.

    To determine the case score, Cortex XSIAM calculates the combined issue score total for all issues in the case. You can see a breakdown of the score by clicking on the score in the details pane.
*   **SmartScore:** The score is automatically calculated, based on machine learning.

    SmartScore relies on machine learning, statistical analysis, case attributes, and cross-customer insights to identify high-risk cases. When an issue is created, Cortex XSIAM calculates the SmartScore according to the compiled data.
* **Manual scoring:** The score is defined by the user.

### **How Cortex XSIAM assigns the score**

For Cortex XSIAM to provide effective rule-based scores, you must define accurate scoring rules that are suitable for your environment and workflows.

When a case is created, Cortex XSIAM searches for a match between your scoring rules and the issues linked to a case. If a match is found, a rule-based score is assigned.

{% hint style="info" %}
### Note

* SmartScore requires sufficient data to calculate and display the score. On first activation, this can take up to 48 hours. If sufficient data is not available, no score is assigned.
* If no match is found and there is sufficient data available, Cortex XSIAM assigns a SmartScore. If Cortex XSIAM doesn't have sufficient data to assign a score, you can manually assign a score.
* To enable Cortex XSIAM to automatically assign a score to a case, you must enable SmartScore and define scoring rules. For more information, see [Set up case scoring](../../../configure-cortex-xsiam/customize-cases-and-issues/set-up-case-scoring).
{% endhint %}

You can view the assigned score on the **Cases** page.
