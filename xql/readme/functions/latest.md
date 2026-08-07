# latest

Use the latest() function within a comp or windowcomp stage to retrieve the single chronologically latest value for a specified field within each group of rows.

## Syntax

```sql
comp latest(<field>) [as <alias>] [by <field1>[, <field2>...]] [addrawdata = true|false [as <target field>]]
```

## Parameters

| Name           | Type                       | Required | Description                                                                                      |
| -------------- | -------------------------- | -------- | ------------------------------------------------------------------------------------------------ |
| field          | string, numeric, timestamp | Yes      | The field from which you want to retrieve the chronologically latest value.                      |
| alias          | string                     | No       | An optional name for the output column.                                                          |
| field1, field2 | string, numeric, boolean   | No       | Optional fields used to group rows; the latest value is calculated independently for each group. |
| addrawdata     | boolean                    | No       | When set to true, includes a column listing the raw events contributing to the aggregate result. |

## Returns

The latest() function returns a single value representing the chronologically latest entry for the specified field within its window or partition.

## Usage Notes

* This function requires the dataset to contain a time-related field (such as \_time) to be considered valid for chronological evaluation.
* When used with the comp stage, system fields like \_time are removed from the result set unless explicitly included in the by clause.
* The order of selection depends entirely on the chronological order of events.
* If you utilize the addrawdata = true option, the query will process up to 50 defined fields and display up to 100 contributing events.

## Examples

### Example 1: Find the latest event ID across the entire dataset

**Goal**: Identify the ID of the most recent event recorded in the dataset.

**XQL Code**:

```sql
config timeframe = 1d  
| dataset = sample_xql_raw  
| comp latest(event_id) as latest_event_id
```

**Explanation**: This query scans the sample\_xql\_raw dataset for the last 24 hours and identifies the event\_id of the record with the most recent timestamp.

**Output**:

| LATEST\_EVENT\_ID |
| ----------------- |
| 110               |

### Example 2: Find the latest log entry grouped by success status

**Goal**: Retrieve the most recent raw log data separately for successful and unsuccessful events.

**XQL Code**:

```sql
config timeframe = 1d  
| dataset = sample_xql_raw  
| comp latest(raw_log_data) as latest_raw_log by is_successful
```

**Explanation**: The query partitions the data into groups based on the is\_successful status and retrieves the chronologically latest raw\_log\_data for each group.

**Output**:

| IS\_SUCCESSFUL | LATEST\_RAW\_LOG                              |
| -------------- | --------------------------------------------- |
| true           | "Full backup of prod\_db to S3 completed."    |
| false          | "Client C2 hit rate limit on /data endpoint." |

## Related Articles

* **Stages**: [comp](../stages/comp), [windowcomp](../stages/windowcomp), [config](../stages/config), [dataset](../stages/dataset)
* **Functions**: [earliest()](earliest), [first()](first), [last()](last)
