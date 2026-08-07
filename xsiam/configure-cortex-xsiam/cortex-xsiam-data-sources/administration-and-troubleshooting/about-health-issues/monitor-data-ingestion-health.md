# Monitor data ingestion health

Cortex XSIAM collects granular data ingestion metrics that provide an insight into the data ingestion pipeline, and identify disruptions in data collection. With these metrics you can trace data collection from a specific source, and see a breakdown by data source attributes such as Collector Name and Final Reporting Device.

You can use these metrics in Cortex Query Language (XQL) queries to investigate disruption and degradation in log collection. You can also create correlation rules that use your own data ingestion logic to trigger issues when disruption occurs for a specific data source within a specific timeframe.

In addition, Cortex XSIAM has a built-in data ingestion monitoring and issues mechanism that monitors the availability and overall health of data ingestion in your environment, and triggers ingestion health issues if disruptions occur.

Related topics

* [Overview of data ingestion metrics](../overview-of-data-ingestion-metrics)
* [Creating correlation rules to monitor data ingestion health](../overview-of-data-ingestion-metrics/creating-correlation-rules-to-monitor-data-ingestion-health)
* [Measuring data freshness](../overview-of-data-ingestion-metrics/measuring-data-freshness)
* [About health issues]()
