---
description: >-
  Monitor data ingestion health using metrics, custom rules, and built-in issue
  detection in Cortex XSIAM
---

# Monitor data ingestion health (BETA)

Cortex XSIAM collects granular data ingestion metrics that provide an insight into the data ingestion pipeline, and identify disruptions in data collection. With these metrics you can trace data collection from a specific source, and see a breakdown by data source attributes such as Collector Name and Final Reporting Device.

You can use these metrics in Cortex Query Language (XQL) queries to investigate disruption and degradation in log collection. You can also create correlation rules that use your own data ingestion logic to trigger issues when disruption occurs for a specific data source within a specific timeframe.

In addition, Cortex XSIAM has a built-in data ingestion monitoring and issues mechanism that monitors the availability and overall health of data ingestion in your environment, and triggers ingestion health issues if disruptions occur.

#### BETA feature limitations in Cortex XSIAM

The data ingestion monitoring and issue mechanism is currently a **BETA** feature. Note the following known issues and limitations:

* **Lag vs. data loss**: The mechanism currently does not differentiate between data ingestion lag (delays) and actual data loss.
* **Alert dispatching and case grouping**: Auto-generated health issues (including but not limited to ingestion) are not currently dispatched. This means they are not automatically grouped into cases. For example, if a Broker VM disconnects, separate alerts may be triggered for each affected data source rather than being consolidated into a single case.
* **Playbook automation**: Because auto-generated health issues are not grouped into cases (orphan issues), they cannot automatically trigger playbook automation. In Cortex XSIAM, playbooks require a case context to run.

Related topics

* [Overview of data ingestion metrics](../overview-of-data-ingestion-metrics)
* [Creating correlation rules to monitor data ingestion health](../overview-of-data-ingestion-metrics/creating-correlation-rules-to-monitor-data-ingestion-health)
* [Measuring data freshness](../overview-of-data-ingestion-metrics/measuring-data-freshness)
* [About health issues]()
