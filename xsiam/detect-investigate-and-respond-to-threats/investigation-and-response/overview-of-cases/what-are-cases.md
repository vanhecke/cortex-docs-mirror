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

### **Case creation**

A case can be created automatically from an issue or manually by a user. When new issues are detected, Cortex XSIAM checks them against existing cases. If there is no matching case, a new case is created. When an issue is linked to a case, all associated assets and artifacts are also linked. After case creation, new issues can match the case until the grouping threshold is met.

A case is automatically generated for any issue with Medium severity or higher that falls into one of these categories:

* It is assigned to the Security domain.
* It is assigned to the Posture domain and has a High severity.
* It was generated from the public API or created from correlations.

While most low-severity issues do not create cases, specific analytic rules can trigger case creation for low-severity issues when action is deemed necessary. Low-severity issues created from correlation rules are not grouped into cases.

For more information about how cases are built, see [Case grouping](../case-concepts/case-grouping).
