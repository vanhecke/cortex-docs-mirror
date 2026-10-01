---
description: >-
  Learn how Cortex XSIAM cases unify issues, assets, and artifacts for
  streamlined investigations.
---

# What are cases?

A case is a defined problem created by connecting related issues into a single story. It shows the impacted assets and key data in one place, helping you focus on the threats that matter most, reduce noise, and resolve the problem efficiently using automation. Each case is unique and requires its own investigation.

Cases comprise the following objects:

* **Issues:** Problems detected in your environment that exceed defined thresholds or surpass your organization's accepted level of risk and threat tolerance.
* **Assets:** Specific entities impacted in a case and how they fit into the case story.
* **Artifacts:** Objects to which behavior or influence can be attributed, such as filenames, processes, domains, and IP addresses.

To see a list of all cases, go to **Cases & Issues** → **Cases**.

While cases are configured to work OOTB, users with specific requirements can customize and tailor their cases.

### **Case creation and issue grouping**

Not all issues are promoted to cases. When a new issue is triggered, it is evaluated to determine if it meets the criteria for case promotion. If the issue qualifies, the system uses case grouping logic to correlate the issue with an existing case; if no match is found, a new case is generated.  For more information, see [Case grouping](../case-concepts/case-grouping).

{% hint style="warning" %}
Case grouping is supported for Security and Posture domains only.&#x20;
{% endhint %}

#### Automatic case creation

A case is automatically generated for any issue that falls into these categories:

* It is assigned to the **Security** or **Posture** domain with **Medium** severity or higher.
* It was generated from the **public API** and has **Medium** severity or higher.
* It was created from **correlations** and has **Medium** severity or higher.

While most low-severity issues do not create cases, specific analytic rules can trigger case creation for low-severity issues when action is deemed necessary. Low-severity issues created from correlation rules are not grouped into cases.

#### Manual case creation

You can also manually create cases from the **Cases** page and select issues to link to the case. For more information, see [Create a case.](https://app.gitbook.com/s/mxWuY3s7AUvWfzCV9p1A/cases-and-issues/analyze-and-resolve-cases/additional-case-actions/create-a-case)

At least one issue must be linked to a case. If all issues are unlinked from a case, the case is deleted.
