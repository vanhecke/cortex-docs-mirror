# approx\_top

Use the `approx_top()` function to return the most frequently occurring elements or highest-sum elements for a specified field. This approximate aggregate function produces results that are highly scalable in terms of memory usage and time compared to exact results from regular aggregate functions.

## Syntax

```sql
comp approx_top(<string field>, <number>) [as <alias>[] [by <field1>[,<field2>...[][] [addrawdata = true|false [as <target field>[][]
```

```sql
comp approx_top(<string field>, <number>, <weight string field>) [as <alias>[] [by <field1>[,<field2>...[][][addrawdata = true|false [as <target field>[][]
```

## Parameters

| Name                | Type    | Required | Description                                                                                                                                                      |
| ------------------- | ------- | -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| string field        | string  | Yes      | The field for which to find the top elements.                                                                                                                    |
| number              | integer | No       | An integer specifying the number of top elements to return. If omitted, it defaults to up to 10 elements.                                                        |
| weight string field | numeric | No       | A numeric field used to calculate the sum for each unique value in the first specified field, causing the function to return approximate sums instead of counts. |

## Returns

The approx\_top() function returns a single array containing up to the specified number of JSON objects (structs). For the count variant, each struct will have "value" (the unique field value) and "count" (its approximate number of occurrences) keys. For the sum variant, each struct will have "value" and "sum" keys, representing the approximate sum calculated using the weight string field.

## Usage Notes

* The comp stage must always precede an approximate aggregate function like approx\_top().
* You can use the optional `by` clause to group rows based on one or more specified fields, which allows approx\_top() to compute the approximate top elements independently for each group.
* When you set the optional addrawdata parameter to true, the query processes up to 50 defined fields and includes a raw\_data column displaying up to 100 raw data events that contributed to the aggregate result.
* New columns created by the comp stage are typically added as the last columns in the result set, and any other fields not explicitly included in the `by` clause or as part of a calculated column is removed from the result set, including the \_time system field.

## Examples

### Example 1: Calculating approximate top counts (no weight field)

**Goal**: Calculate the top 2 approximate counts of is\_successful statuses across the entire dataset.

**XQL Code**:

```sql
config timeframe = 1d   
| dataset = sample_xql_raw   
| comp approx_top(is_successful, 2) as top_successful_statuses 
```

**Explanation**: The code identifies the top 2 most frequent values in the is\_successful field. The result is an array of JSON objects, each with a "value" and a "count".

**Output**:

| top\_successful\_statuses                                      |
| -------------------------------------------------------------- |
| \[{"value": true, "count": 7}, {"value": false, "count": 3}\[] |

### Example 2: Calculating approximate top sums (with weight field)

**Goal**: Calculate the top 2 dst\_domain values by the sum of their duration\_seconds across the entire dataset.

**XQL Code**:

```sql
config timeframe = 1d   
| dataset = sample_xql_raw   
| comp approx_top(dst_domain, 2, duration_seconds) as top_domains_by_duration_sum
```

**Explanation**: The code computes the sum of duration\_seconds for each unique dst\_domain and then returns the top 2 dst\_domain values based on these sums.

**Output**:

| top\_domains\_by\_duration\_sum                                                                    |
| -------------------------------------------------------------------------------------------------- |
| \[{"value": "www.mongodb.com", "sum": 60.0}, {"value": "downloads.teamviewer.com", "sum": 15.3}\[] |

### Example 3: Calculating approximate top sums grouped by another field

**Goal**: Calculate the top 1 dst\_domain by the sum of duration\_seconds separately for is\_successful = true and is\_successful = false events.

**XQL Code**:

```sql

config timeframe = 1d   
| dataset = sample_xql_raw   
| comp approx_top(dst_domain, 1, duration_seconds) as top_domain_durations_by_status by is_successful
```

**Explanation**: Groups records by their is\_successful status and calculates the single dst\_domain with the highest sum of duration\_seconds for each group.

**Output**:

| is\_successful | top\_domain\_durations\_by\_status                     |
| -------------- | ------------------------------------------------------ |
| true           | \[{"value": "www.mongodb.com", "sum": 60.0}\[]         |
| false          | \[{"value": "sharepoint.microsoft.com", "sum": 2.1}\[] |

### Example 4: Calculating approximate top counts with raw data inclusion

**Goal**: Include the raw events that contribute to the approximate top count calculation by using the addrawdata = true option.

**XQL Code**:

```sql
config timeframe = 1d   
| dataset = sample_xql_raw   
| comp approx_top(is_successful, 1) addrawdata = true as raw_data_for_top_is_successful
```

**Explanation**: The code computes the top 1 most frequent is\_successful value and automatically generates a new column named raw\_data\_for\_top\_is\_successful containing a JSON representation of the raw events that contributed to this result.

**Output**:

| top\_successful\_statuses        | raw\_data\_for\_top\_is\_successful                                                                                           |
| -------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| \[{"value": true, "count": 7}\[] | \[{"event\_id": 101, "is\_successful": true, ...}, {"event\_id": 103, "is\_successful": true, ...}, ...\[] (up to 100 events) |

## Related Articles\*\*

* **Stages**: [comp](../stages/comp), [alter](../stages/alter), [config](../stages/config), timeframe
* **Functions**: [approx\_count](approx_count), [approx\_quantiles](approx_quantiles)
