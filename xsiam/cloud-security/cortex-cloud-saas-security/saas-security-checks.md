---
description: >-
  Use SaaS Security Checks in Cortex XSIAM to identify at-risk assets and
  prioritize remediation.
---

# SaaS Security Checks

SaaS Security Checks provides security telemetry for posture misconfigurations, vulnerabilities, and compliance in one unified view. This consolidated dashboard provides a queryable, prioritized view of your attack surface, accelerating automated triage, incident response, and compliance auditing.

<img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2FsTN50fsPyBbITq1HaqvK%2Funknown.png?alt=media&#x26;token=d3ff0626-c7d7-4232-8aec-c948bb6f5f3c" alt="" height="429" width="624">

The dashboard captures the following key metrics to help you remediate assets at risk:

* SaaS Security Check Score: Renders the current, aggregate security posture score as a normalized percentage, while also tracking score volatility over a rolling 90-day window to monitor long-term posture drift.
* Overall Compliance: Monitors adherence to mapped compliance standards and frameworks.
* Provider Instances by Security Check Score: Categorizes individual SaaS tenant configurations (such as Salesforce, Mural, or Google Workspace) to identify low-performing integrations, based on their security scores.
* Issues to Address: Acts as a prioritized vulnerability backlog, organizing discovered misconfigurations by severity to guide triage queues.

Optionally, you can also navigate to **Module > SaaS > Security Checks > Posture** to view a tabular list of Posture Issues filtered by SaaS Issues. Select any Issue to view a full list of **Remediation Actions**. Here you can also view the **Evidence** section, that includes granular information about specific application settings that lead to misconfigurations.
