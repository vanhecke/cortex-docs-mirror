# Overview of data ingestion metrics

{% hint style="warning" %}
### Prerequisite

For Cortex XSIAM to monitor data ingestion health and create health issues, you must enable **Cortex - Analytics.** Go to Configurations → **Cortex - Analytics**. For more information, see [Enable the Analytics Engine and Identity Analytics](../../../onboard-cortex-xsiam/deployment-steps/cortex-xsiam-analytics/enable-the-analytics-engine-and-identity-analytics).
{% endhint %}

The data ingestion metrics are calculated in 5-minute aggregation periods and saved to the `metrics_source` dataset and `metrics_view` preset. These metrics measure the amount, size, and rate at which logs are ingested by a data source:

| Metric              | Description                                                                             |
| ------------------- | --------------------------------------------------------------------------------------- |
| total\_size\_bytes  | Total size (in bytes) of the logs collected during the aggregation period.              |
| total\_size\_rate   | Average size (in bytes per second) of the logs collected during the aggregation period. |
| total\_event\_count | Total number of logs collected during the aggregation period                            |
| total\_event\_rate  | Average number (in count per second) of logs collected during the aggregation period.   |

In the `metrics_source` dataset, the data ingestion metrics are saved alongside additional fields that describe the data source associated with the metrics. Only entries with ingestion metric values greater than zero are saved in the dataset. Entries with zero values are not saved in this dataset.

`metrics_view` is a preset for data in the `metrics_source` dataset. The preset also simulates completion of entries with zero values in data ingestion metrics at runtime, which allows effective use of metrics. Therefore, when investigating disruptions in data collection, we recommend using the `metrics_view` preset in XQL queries and correlation rules.

Cortex XSIAM built-in data ingestion monitoring and issue mechanism uses the data ingestion metrics to identify disruptions in the data ingestion pipeline. Using analytical logic, Cortex XSIAM creates an ingestion baseline for each data source that reflects the routine pattern of log collection. If a data source isn't ingesting logs, or there is a significant deviation from the baseline, ingestion issues are triggered. You can see all ingestion issues on the **Health Issues** page. To troubleshoot or investigate an issue, right-click an issue and click **Investigate in XQL query**. For more information, see [Investigate and resolve health issues](about-health-issues/investigate-and-resolve-health-issues).

In addition, you can create your own custom logic for data ingestion health monitoring by setting up correlation rules that monitor the data ingestion metrics. For more information, see [Creating correlation rules to monitor data ingestion health](overview-of-data-ingestion-metrics/creating-correlation-rules-to-monitor-data-ingestion-health).

The following table describes all the fields in the `metrics_source` dataset and `metrics_view` preset:

<details>

<summary>Read more...</summary>

| Field                                  | Type     | Description                                                                                                                                            |
| -------------------------------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| total\_size\_bytes                     | Integer  | Total size (in bytes) of the logs collected during the aggregation period.                                                                             |
| total\_size\_rate                      | Integer  | Average size (in bytes per second) of the logs collected during the aggregation period.                                                                |
| total\_event\_count                    | Integer  | Total number of logs collected during the aggregation period                                                                                           |
| total\_event\_rate                     | Integer  | Average number (in count per second) of logs collected during the aggregation period.                                                                  |
| data\_freshness\_max\_delay            | Float    | Maximum delay value from all log entries in a record between log creation at the source and ingestion into Cortex XSIAM (in seconds).                  |
| data\_freshness\_median                | Float    | Median delay value from all log entries in a record between log creation at the source and ingestion into Cortex XSIAM (in seconds).                   |
| data\_freshness\_ninetieth\_percentile | Float    | Ninetieth percentile of delay values from all log entries in a record between log creation at the source and ingestion into Cortex XSIAM (in seconds). |
| last\_seen                             | Datetime | Time that the last logs were collected.                                                                                                                |
| \_vendor                               | String   | Vendor of the observing data source.                                                                                                                   |
| \_product                              | String   | Product name of the observing data source.                                                                                                             |
| \_device\_id                           | String   | (For firewall devices) Device ID                                                                                                                       |
| \_log\_type                            | String   | (For firewall devices) Log type                                                                                                                        |
| \_collector\_type                      | String   | (Event Metadata) Type of collector that provided the log.                                                                                              |
| \_collector\_name                      | String   | (Event Metadata) Name of the collector instance.                                                                                                       |
| \_collector\_id                        | String   | (Event Metadata) ID of the XDR Collector.                                                                                                              |
| \_collector\_ip                        | String   | (Event Metadata) IP address of the XDR Collector.                                                                                                      |
| \_reporting\_device\_name              | String   | (Event Metadata) Host name of the device where the log originated.                                                                                     |
| \_reporting\_device\_ip                | String   | (Event Metadata) IP Address of the device where the log originated.                                                                                    |
| \_final\_reporting\_device\_name       | String   | (Event Metadata) Hostname of the device that the log was extracted from.                                                                               |
| \_final\_reporting\_device\_ip         | String   | (Event Metadata) IP of the device that the log was extracted from.                                                                                     |
| \_broker\_device\_name                 | String   | (Event Metadata) Host name of the Broker VM.                                                                                                           |
| \_broker\_device\_ip                   | String   | (Event Metadata) IP address of the Broker VM.                                                                                                          |
| \_broker\_device\_id                   | String   | (Event Metadata) ID of the Broker VM.                                                                                                                  |
| \_time                                 | Datetime | Timestamp of the interval.                                                                                                                             |
| \_insert\_timestamp                    | Datetime | Recorded time of the entry.                                                                                                                            |

</details>
