---
description: Query Cortex XSIAM case and issue data with Cortex Query Language.
---

# Query case and issue data

Cortex XSIAM uses Cortex Query Language (XQL) as the primary language for searching, analyzing, and transforming security data. XQL allows for highly efficient querying across vast amounts of security telemetry, such as:

* **Threat hunting:** Proactively search your entire environment for malicious activity, anomalies, and indicators of compromise (IOCs). Formulate queries to look for specific patterns of behavior that might indicate an ongoing attack, even if no alert has been triggered.
* **Investigation:** When a case or issue is generated, XQL allows security analysts to drill down into the underlying data, understand the full scope of an attack, identify affected assets, and trace the attacker's actions.
* **Forensics:** Extract detailed information about past events for post-incident analysis and compliance audits.
* **Reports and dashboards:** Create custom reports and dashboards to visualize security posture, track key metrics, and communicate insights to stakeholders.

To view and use sample investigative queries, such as the **Top Unresolved High Severity Cases** query, go to **Investigation & Response** → **Search** → **Query Builder** → **XQL** → **Query Library**. For more information about using XQL, see [Cortex XSIAM XQL](../../../../reference-and-developer-docs/cortex-agentix-xql).

You can query case and issue data in the `cases` and `issues` datasets. When using the `issues` dataset, keep in mind the following:

* Informational issues are not included in this dataset.
* Issue fields are limited to certain fields available in the API. For the full list, see [Create a new issue](https://app.gitbook.com/s/1ZrobAtcwfCDWAJAWeuj/issues-apis/issues-apis-overview).

The `issues` dataset is categorized by domain. To query only security issues, use the following XQL:

```
dataset = issues | filter issue_domain = "SECURITY"
```

To query only posture issues, use the following XQL:

```
dataset = issues | filter issue_domain = "POSTURE"
```
