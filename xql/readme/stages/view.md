# view

Use the `view` stage to customize how your query results are displayed, enabling highlighting, graphing, and column reordering.

## Syntax

```sql
view highlight fields = <field1>[,<field2>,...] values = <value1>[,<value2>,...]
view graph type = <graph_type> xaxis = <field1> yaxis = <field2> [<optional parameters>] [series = <field3>]
view column order = default | populated
```

## Parameters

| Name           | Type    | Required            | Description                                                                                                                  |
| -------------- | ------- | ------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| `highlight`    | keyword | No                  | Indicates the view operation is to highlight specific text.                                                                  |
| `fields`       | string  | Yes (for highlight) | A comma-separated list of fields in which to search for the value to highlight.                                              |
| `values`       | string  | Yes (for highlight) | A comma-separated list of string values to highlight within the specified fields.                                            |
| `graph`        | keyword | No                  | Indicates the view operation is to generate a graph.                                                                         |
| `type`         | string  | Yes (for graph)     | Specifies the type of graph (for example, `pie`, `column`, `area`, `bubble`, `line`, `map`, `scatter`).                      |
| `xaxis`        | string  | Yes (for graph)     | The field to be used for the X-axis. Must be collatable.                                                                     |
| `yaxis`        | string  | Yes (for graph)     | The field to be used for the Y-axis. Must be collatable.                                                                     |
| `series`       | string  | No                  | Used for certain graph types (area, bubble, column, line, map, scatter) to group chart results based on this field's values. |
| `column order` | keyword | No                  | Indicates the view operation is to reorder columns.                                                                          |
| `default`      | keyword | No                  | Displays columns in their original order.                                                                                    |
| `populated`    | keyword | No                  | Displays columns with the most non-null values first.                                                                        |

## Returns

The `view` stage returns the query results formatted according to the specified visualization or ordering rules.

## Usage notes

* For graph types, the fields specified for `xaxis` and `yaxis` must be collatable.
* The `series` parameter is available for specific graph types (`area`, `bubble`, `column`, `line`, `map`, `scatter`) to group chart results based on `yaxis` values.
* The `view column order` option applies only to the Query Builder's display and is disregarded in widgets, Correlation Rules, public APIs, reports, and dashboards.

## Examples

### Example 1: Highlighting specific values

**Goal**: Highlight the text "successful" wherever it appears within the `event_description` field.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| view highlight fields = event_description values = "successful"
```

**Explanation**: This query will display the records and visually highlight the text "successful" in the `event_description` column (for example, in "User login successful").

**Output**:

| event\_id | event\_description               |
| --------- | -------------------------------- |
| 101       | "User login **successful**"      |
| 102       | "File access attempt"            |
| 103       | "Network connection established" |

### Example 2: Visualizing categorical data (Pie chart)

**Goal**: Create a pie chart showing the count of events grouped by their `is_successful` status.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| comp count() by is_successful as event_count
| view graph type = pie xaxis = is_successful yaxis = event_count
```

**Explanation**: This query counts the total number of events for each `is_successful` status (true or false). The query then displays these counts as a pie chart, where `is_successful` defines the slices (xaxis) and `event_count` defines their size (yaxis).

**Output**:

| is\_successful | event\_count |
| -------------- | ------------ |
| true           | 7            |
| false          | 3            |

### Example 3: Trend analysis (column graph)

**Goal**: Display a column graph showing the count of events per hour.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| bin _time span = 1h
| comp count() as hourly_events by _time
| view graph type = column xaxis = _time yaxis = hourly_events
```

**Explanation**: This query groups events into one-hour bins based on `_time`, counts the `hourly_events` for each bin, and presents the data as a column graph showing the hourly distribution.

**Output**:

| \_time                  | hourly\_events |
| ----------------------- | -------------- |
| 2023-10-26 10:00:00 UTC | 9              |
| 2023-10-26 11:00:00 UTC | 1              |

### Example 4: Adding granularity to graphs (series)

**Goal**: Show the sum of `duration_seconds` over time, segmented by `is_successful` status using a series.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| bin _time span = 1h
| comp sum(duration_seconds) as total_duration by _time, is_successful
| view graph type = column xaxis = _time yaxis = total_duration series = is_successful
```

**Explanation**: This query aggregates `duration_seconds` by hourly `_time` buckets and `is_successful` status. The view stage creates a column graph where each hour is represented, segmented by the success status.

**Output**:

| \_time                  | is\_successful | total\_duration |
| ----------------------- | -------------- | --------------- |
| 2023-10-26 10:00:00 UTC | true           | 39.9            |
| 2023-10-26 10:00:00 UTC | false          | 2.95            |
| 2023-10-26 11:00:00 UTC | true           | 60.0            |

### Example 5: Prioritizing display (column order)

**Goal**: Reorder the columns in the results table to display columns with the most non-null values first.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| comp count() as event_count by is_successful
| view column order = populated
```

**Explanation**: This query counts events by `is_successful` and then reorders the resulting columns. Columns that are consistently populated appear earlier in the table view.

**Output**:

| is\_successful | event\_count |
| -------------- | ------------ |
| true           | 7            |
| false          | 3            |

## Related articles

* **Stages**: [`bin`](bin), [`comp`](comp), [`config`](config)
* **Functions**: [`count`](../functions/count_with_windowcomp_stage), [`sum`](../functions/sum_with_comp_stage)
* **Datasets**: [`xdr_data`](https://www.google.com/search?q=%5Bhttps://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction%5D\(https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction\))
