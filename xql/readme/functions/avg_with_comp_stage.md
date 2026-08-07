# avg (comp)

Use the avg() function to calculate the average value of a numerical field within a group of rows. When used with the comp stage, it computes a single statistical average for the specified field across all records sharing matching values defined in a grouping clause.

## Syntax

```sql
comp avg(<field>) [as <alias>] [by <field1>[,<field2>...]] [addrawdata = true|false [as <target field>]]
```

## Parameters

| Name              | Type           | Required | Description                                                                                         |
| ----------------- | -------------- | -------- | --------------------------------------------------------------------------------------------------- |
| field             | integer, float | Yes      | The numerical field for which to calculate the average.                                             |
| alias             | string         | No       | An optional name for the resulting average field.                                                   |
| field1, field2... | any            | No       | Optional fields used to group rows for independent average calculations.                            |
| addrawdata        | boolean        | No       | If true, includes a column listing the raw events contributing to the aggregate. Defaults to false. |
| target field      | string         | No       | An optional alias for the raw data column if addrawdata is true.                                    |

## Returns

The avg() function returns a single numerical value representing the average of the input field for the specified group.

## Usage Notes

* The avg() function operates exclusively on numerical fields, including both integers and floating-point numbers.
* The comp stage must always precede the avg() function.
* When the comp stage is used, the system field \_time is removed from the result set unless explicitly included in a by clause.
* Calculated columns created by the comp stage are typically appended as the last columns in the result set.
* If addrawdata is set to true, the query supports up to 50 defined fields and displays up to 100 raw events.

## Examples

### Example 1: Average a field across the entire dataset

**Goal**: Calculate the average value of the duration\_seconds field for all records in the dataset without grouping.

**XQL Code**:

```sql
config timeframe = 1d  
| dataset = sample_xql_raw  
| comp avg(duration_seconds) as overall_avg_duration
```

**Explanation**: The avg() function computes the mean of all duration\_seconds values present in the sample\_xql\_raw dataset and names the result overall\_avg\_duration.

**Output**:

| overall\_avg\_duration |
| ---------------------- |
| 10.285                 |

### Example 2: Average a field grouped by another field

**Goal**: Calculate the average duration\_seconds separately for successful and unsuccessful events.

**XQL Code**:

```sql
config timeframe = 1d  
| dataset = sample_xql_raw  
| comp avg(duration_seconds) as avg_duration_by_status by is_successful
```

**Explanation**: This code groups records by their is\_successful status and then calculates the average duration\_seconds for each distinct group.

**Output**:

| is\_successful | avg\_duration\_by\_status |
| -------------- | ------------------------- |
| true           | 14.271428571428571        |
| false          | 0.9833333333333333        |

### Example 3: Average with raw data inclusion

**Goal**: Calculate average duration and include the JSON representation of raw events that contributed to each group.

**XQL Code**:

```sql
config timeframe = 1d  
| dataset = sample_xql_raw  
| fields is_successful, duration_seconds  
| comp avg(duration_seconds) by is_successful addrawdata = true as raw_events_for_avg
```

**Explanation**: This code calculates the average duration\_seconds grouped by is\_successful and uses the addrawdata = true option to generate a column containing the underlying raw data for each aggregate.

**Output**:

| is\_successful | avg\_duration\_by\_status | raw\_events\_for\_avg                                       |
| -------------- | ------------------------- | ----------------------------------------------------------- |
| true           | 14.271428571428571        | \[{"is\_successful": true, "duration\_seconds": 1.5}, ...]  |
| false          | 0.9833333333333333        | \[{"is\_successful": false, "duration\_seconds": 0.8}, ...] |

## Related Articles

* **Stages**: [comp](../stages/comp), [alter](../stages/alter),
