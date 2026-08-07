# count (windowcomp)

Use the count() function within a windowcomp stage to calculate and return a single count value over a defined window or group of rows, presenting the result for each row within that window frame. The function can operate by counting non-null values for a specified field, or by counting the total number of rows within the window when no field is specified.

## Syntax

```sql
windowcomp count([<field>]) [by <field> [,<field>,...]] [sort [asc|desc] <field1> [, [asc|desc] <field2>,...]] [between 0|null|<number>|-<number> [and 0|null|<number>|-<number>] [frame_type=range]] [as <alias>] 
```

## Parameters

| Name               | Type                            | Required | Description                                                                                                                         |
| ------------------ | ------------------------------- | -------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| field              | string, integer, float, boolean | No       | The field to count non-null values for. If omitted, the function counts all rows including those with null values.                  |
| by field           | string, integer, float, boolean | No       | The field(s) used to partition the data into distinct groups, allowing the function to operate independently within each partition. |
| sort field         | string, integer, float, boolean | No       | Defines the order of rows within each partition, which is critical when defining a window using the between clause.                 |
| between boundaries | integer, null                   | No       | Defines the "window frame" (a specific range of rows) relative to the current row over which the count is calculated.               |
| frame\_type        | string                          | No       | Specifies whether the window is defined by rows (the default) or a value range.                                                     |
| alias              | string                          | No       | The alias name for the output column, assigned using the as clause.                                                                 |

## Returns

The count() function returns a single numerical value representing the count. This value is displayed in a new column for every row in the group of rows it applies to.

## Usage Notes

* Defining a field for count() is optional; providing a field counts non-null values, while omitting it counts total rows.
* The by clause partitions the data into distinct groups, and the count() function operates independently within each of these partitions, meaning a separate count is computed for each group.
* The sort clause is mandatory for many windowcomp functions as it defines the order of rows within each partition, which is critical when defining a window using the between clause.
* If the between clause is omitted, the default window used is typically the entire partition.
* The windowcomp stage must always precede analytic functions like count() that calculate statistics.
* Only one function can be defined per field within a single windowcomp stage.

## Examples

### Example 1: Over an entire partition (no field specified - counts all rows)

**Goal**: Calculate the total number of events (rows) for all events within each is\_successful group, replicating this total count value for every row in that group.

**XQL Code**:

```sql
config timeframe = 1d   
| dataset = sample_xql_raw   
| fields event_id, _time, is_successful, event_description   
| windowcomp count() by is_successful sort asc _time as count_in_partition   
| sort asc is_successful, asc _time, asc event_id   
| limit 10 
```

**Explanation**: For the false partition, there are 3 rows, so the count\_in\_partition is 3 for each row in this partition. For the true partition, there are 7 rows, so the count is 7 for each row in that partition.

**Output**:

| \_time                  | event\_id | is\_successful | event\_description               | count\_in\_partition |
| ----------------------- | --------- | -------------- | -------------------------------- | -------------------- |
| 2023-10-26 10:05:30 UTC | 102       | false          | "File access attempt"            | 3                    |
| 2023-10-26 10:40:10 UTC | 106       | false          | "Unauthorized access detected"   | 3                    |
| 2023-10-26 10:55:55 UTC | 109       | false          | "API request throttled"          | 3                    |
| 2023-10-26 10:00:00 UTC | 101       | true           | "User login successful"          | 7                    |
| 2023-10-26 10:15:15 UTC | 103       | true           | "Network connection established" | 7                    |
| 2023-10-26 10:20:00 UTC | 104       | true           | "System heartbeat"               | 7                    |
| 2023-10-26 10:30:45 UTC | 105       | true           | "Data transformation"            | 7                    |
| 2023-10-26 10:45:00 UTC | 107       | true           | "Cloud resource modification"    | 7                    |
| 2023-10-26 10:50:20 UTC | 108       | true           | "Software update initiated"      | 7                    |
| 2023-10-26 11:00:10 UTC | 110       | true           | "Database backup completed"      | 7                    |

### Example 2: Over an entire partition (field specified - counts non-null values)

**Goal**: Calculate the count of event\_description specifically to count non-null occurrences of that field for all events within each is\_successful group.

**XQL Code**:

```sql
config timeframe = 1d   
| dataset = sample_xql_raw   
| fields event_id, _time, is_successful, event_description   
| windowcomp count(event_description) by is_successful as non_null_count_in_partition   
| sort asc is_successful, asc _time, asc event_id   
| limit 10 
```

**Explanation**: Because all event\_description values in the dataset are non-null, the counts for each partition are identical to counting all rows (3 for false and 7 for true), explicitly demonstrating that count(field) only counts non-null instances.

**Output**:

| \_time                  | event\_id | is\_successful | event\_description               | non\_null\_count\_in\_partition |
| ----------------------- | --------- | -------------- | -------------------------------- | ------------------------------- |
| 2023-10-26 10:05:30 UTC | 102       | false          | "File access attempt"            | 3                               |
| 2023-10-26 10:40:10 UTC | 106       | false          | "Unauthorized access detected"   | 3                               |
| 2023-10-26 10:55:55 UTC | 109       | false          | "API request throttled"          | 3                               |
| 2023-10-26 10:00:00 UTC | 101       | true           | "User login successful"          | 7                               |
| 2023-10-26 10:15:15 UTC | 103       | true           | "Network connection established" | 7                               |
| 2023-10-26 10:20:00 UTC | 104       | true           | "System heartbeat"               | 7                               |
| 2023-10-26 10:30:45 UTC | 105       | true           | "Data transformation"            | 7                               |
| 2023-10-26 10:45:00 UTC | 107       | true           | "Cloud resource modification"    | 7                               |
| 2023-10-26 10:50:20 UTC | 108       | true           | "Software update initiated"      | 7                               |
| 2023-10-26 11:00:10 UTC | 110       | true           | "Database backup completed"      | 7                               |

### Example 3: Rolling window (preceding 2 rows and current row, no field)

**Goal**: Count the total number of rows within the current row and the two immediately preceding rows within its partition, operating on a sliding window ordered by \_time.

**XQL Code**:

```sql
config timeframe = 1d   
| dataset = sample_xql_raw   
| fields event_id, _time, is_successful, event_description   
| windowcomp count() by is_successful sort asc _time between -2 and 0 as rolling_count   
| sort asc is_successful, asc _time, asc event_id   
| limit 10 
```

**Explanation**: The between -2 and 0 clause defines a window including the current row and the two preceding rows. For each row, the count() calculates the number of rows within its specific rolling window, starting from the beginning of the partition if there are not enough preceding rows.

**Output**:

| \_time                  | event\_id | is\_successful | event\_description               | rolling\_count |
| ----------------------- | --------- | -------------- | -------------------------------- | -------------- |
| 2023-10-26 10:05:30 UTC | 102       | false          | "File access attempt"            | 1              |
| 2023-10-26 10:40:10 UTC | 106       | false          | "Unauthorized access detected"   | 2              |
| 2023-10-26 10:55:55 UTC | 109       | false          | "API request throttled"          | 3              |
| 2023-10-26 10:00:00 UTC | 101       | true           | "User login successful"          | 1              |
| 2023-10-26 10:15:15 UTC | 103       | true           | "Network connection established" | 2              |
| 2023-10-26 10:20:00 UTC | 104       | true           | "System heartbeat"               | 3              |
| 2023-10-26 10:30:45 UTC | 105       | true           | "Data transformation"            | 3              |
| 2023-10-26 10:45:00 UTC | 107       | true           | "Cloud resource modification"    | 3              |
| 2023-10-26 10:50:20 UTC | 108       | true           | "Software update initiated"      | 3              |
| 2023-10-26 11:00:10 UTC | 110       | true           | "Database backup completed"      | 3              |

### Example 4: Fixed window (current row to unbounded following, field specified)

**Goal**: Calculate the count of non-null event\_description values for each row over a fixed window that starts from the current row and extends to the end of its partition.

**XQL Code**:

```sql
config timeframe = 1d   
| dataset = sample_xql_raw   
| fields event_id, _time, is_successful, event_description   
| windowcomp count(event_description) by is_successful sort asc _time between 0 and null as count_from_current   
| sort asc is_successful, asc _time, asc event_id   
| limit 10 
```

**Explanation**: The between 0 and null clause defines a window starting from the current row to the very end of the partition. count(event\_description) dynamically updates for each row to represent the remaining number of non-null values.

**Output**:

| \_time                  | event\_id | is\_successful | event\_description               | count\_from\_current |
| ----------------------- | --------- | -------------- | -------------------------------- | -------------------- |
| 2023-10-26 10:05:30 UTC | 102       | false          | "File access attempt"            | 3                    |
| 2023-10-26 10:40:10 UTC | 106       | false          | "Unauthorized access detected"   | 2                    |
| 2023-10-26 10:55:55 UTC | 109       | false          | "API request throttled"          | 1                    |
| 2023-10-26 10:00:00 UTC | 101       | true           | "User login successful"          | 7                    |
| 2023-10-26 10:15:15 UTC | 103       | true           | "Network connection established" | 6                    |
| 2023-10-26 10:20:00 UTC | 104       | true           | "System heartbeat"               | 5                    |
| 2023-10-26 10:30:45 UTC | 105       | true           | "Data transformation"            | 4                    |
| 2023-10-26 10:45:00 UTC | 107       | true           | "Cloud resource modification"    | 3                    |
| 2023-10-26 10:50:20 UTC | 108       | true           | "Software update initiated"      | 2                    |
| 2023-10-26 11:00:10 UTC | 110       | true           | "Database backup completed"      | 1                    |

## Related Articles

* **Stages**: [windowcomp](../stages/windowcomp), [comp](../stages/comp), [alter](../stages/alter)
* **Functions**: [count()](count_with_windowcomp_stage)
