# Creating correlation rules to monitor data ingestion health

In addition to the OOTB Ingestion health issues, you can build your monitoring logic for ingestion by creating correlation rules that are specific to your requirements. You can create rules that monitor the data ingestion metrics for a specific source within a specific timeframe, and trigger ingestion health issues if there is a deviation from the regular pattern of log collection.

The following examples can help you set up your own correlation rules with the data ingestion metrics:

### Example 1: No logs collected from a data source for 1 hour

In this example, the correlation runs every hour and calculates the number of logs that are collected for each data source over the previous hour. If no logs are collected for a data source during an aggregation period, a security issue is triggered.

Example XQL:

```
preset = metrics_view  
| comp sum(total_event_count) as total_event_count_sum by _collector_id, _collector_ip, 
_collector_name, _collector_type, _final_reporting_device_ip, _final_reporting_device_name,
 _broker_device_id, _vendor, _product 
| filter total_event_count_sum = 0
```

Addition fields to specify in the correlation rule:

| Field                | Value                                                                                         |
| -------------------- | --------------------------------------------------------------------------------------------- |
| Time Schedule        | Hourly                                                                                        |
| Query time frame     | 1 Hour                                                                                        |
| Issue Suppression    | Select Enable issue suppression.                                                              |
| Fields               | Uncheck **`total_event_rate_sum`**, leave other fields checked.                               |
| Action               | Select Generate issue.                                                                        |
| Issue Domain         | Health                                                                                        |
| Severity             | High                                                                                          |
| Type                 | Ingestion                                                                                     |
| Issue Fields Mapping | Select Use preconfigured fields to map the fields that are relevant to data ingestion health. |

### Example 2: No logs received from a Firewall for 20 minutes

In this example, the correlation runs every 20 minutes and calculates the number of logs that are received for each firewall in a lookup dataset during the last 20 minutes. If no logs are received from a device during an aggregation period, a security issue is triggered.

Example XQL:

```
preset = metrics_view  
| join conflict_strategy = left  type = inner (dataset = ngfw_device_Id_keepalive 
| fields _device_id) as devices devices._device_id = _device_id  | comp sum(total_event_count)
 as total_event_count_sum by _device_id, _product,_vendor 
| filter total_event_count_sum = 0
```

Addition fields to specify in the correlation rule:

| Field                 | Value                                                                                         |
| --------------------- | --------------------------------------------------------------------------------------------- |
| Time Schedule         | Every 20 minutes                                                                              |
| Query time frame      | 20 minutes                                                                                    |
| Issue Suppression     | Select Enable issue suppression.                                                              |
| Fields                | Uncheck **`total_event_rate_sum`**, leave other fields checked.                               |
| Action                | Select Generate issue.                                                                        |
| Issue Domain          | Health                                                                                        |
| Severity              | High                                                                                          |
| Type                  | Collection                                                                                    |
| Issues Fields Mapping | Select Use preconfigured fields to map the fields that are relevant to data ingestion health. |

<br>
