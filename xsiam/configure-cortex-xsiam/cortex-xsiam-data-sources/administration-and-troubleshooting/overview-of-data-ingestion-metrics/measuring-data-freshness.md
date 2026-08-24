---
description: >-
  Understand how Cortex XSIAM measures and reports delays between log creation
  and ingestion.
---

# Measuring data freshness

freshness delay value by measuring the difference between log creation at the source (`_TIME`) and ingestion into Cortex XSIAM (`_INSERT_TIME`).

Metrics are collected and calculated per data source during five-minute aggregation periods and allocated into the following buckets. The recorded freshness delay value is the top value in the range of the bucket:

* 0 to 30 seconds → 30 seconds
* 30 to 60 seconds → 60 seconds
* 60 seconds to 5 minutes → 300 seconds
* 5 minutes to 1 hour → 3,600 seconds
* 1 hour to 24 hours→ 86,400 seconds
* 24 hours to week→ 604,800 seconds

| Metric                                 | Description                                                                                                                                                                                                               |
| -------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| data\_freshness\_max\_delay            | <p>Maximum freshness delay value among all log entries in an aggregation period.</p><p>This reflects the worst case.</p>                                                                                                  |
| data\_freshness\_median                | <p>Median freshness delay value among all log entries in an aggregation period.</p><p>50% of values are smaller than the median, and 50% of values are higher or equal to the median.</p>                                 |
| data\_freshness\_ninetieth\_percentile | <p>Ninetieth percentile of delay values among all log entries in an aggregation period.</p><p>This delay value is 90% higher than other log entry differences. It reflects the worst case, but eliminates the spikes.</p> |

The metrics are saved to the `metrics_source` dataset and are also available in the `metrics_view` preset.

* The max\_delay metric is taken from the maximum bucket value with a restricted limit; therefore, metrics show whole numbers.
* The median and ninetieth\_percentile metrics are statistical calculations that give an approximation of the real value; therefore, metrics show decimal numbers.
* Time slots with a zero log count or zero byte count display records with zero values. Subsequently, the data freshness metrics will also have zero values.
* Timezone differences between `_TIME` and `_INSERT_TIME` might cause time skews with negative differences. Negative differences are rounded to zero values.

<br>

***
