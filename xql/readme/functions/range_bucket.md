# range\_bucket

Use the `range_bucket()` function to determine which bucket a numeric value falls into, given an array of bucket boundaries. The function returns the index of the bucket (0-based) that contains the value.

## Syntax

```sql
range_bucket(<value>, <boundaries>)
```

## Parameters

| Name         | Type                        | Required | Description                                                                                 |
| ------------ | --------------------------- | -------- | ------------------------------------------------------------------------------------------- |
| `value`      | integer, float              | Yes      | The numeric value to classify into a bucket.                                                |
| `boundaries` | array of integers or floats | Yes      | A sorted array of boundary values that define the bucket edges. Must be in ascending order. |

## Returns

**Type**: integer

**Description**: The `range_bucket()` function returns a 0-based integer index indicating which bucket the value falls into. If the value is less than the first boundary, it returns `0`. If the value is greater than or equal to the last boundary, it returns the number of boundaries. If the input is `null`, the function returns `null`.

## Usage notes

* **Input type**: XQL doesn't support NaN or infinite values as input and these value types also can not be returned.
* **Sorted Boundaries**: The `boundaries` array must be sorted in ascending order. Unsorted boundaries produce undefined results.
* **Bucket Ranges**: For boundaries `[b1, b2, b3]`, the buckets are: bucket 0 = `(-∞, b1)`, bucket 1 = `[b1, b2)`, bucket 2 = `[b2, b3)`, bucket 3 = `[b3, +∞)`.
* **Null Handling**: If the `value` is `null`, the function returns `null`.
* **Common Use Cases**: This function is typically used within the `alter` stage for data binning, histogram creation, severity classification, and score grading.

## Examples

### Example 1: Classify values into predefined buckets

**Goal**: Classify numeric values into severity levels using predefined boundaries.

**XQL code**:

```sql
dataset = xdr_data
| limit 1
| alter bucket1 = range_bucket(5, arraycreate(0, 10, 50, 100))
| alter bucket2 = range_bucket(25, arraycreate(0, 10, 50, 100))
| alter bucket3 = range_bucket(75, arraycreate(0, 10, 50, 100))
| fields bucket1, bucket2, bucket3
```

**Explanation**: With boundaries `[0, 10, 50, 100]`, the value `5` falls in bucket 1 (between 0 and 10), `25` falls in bucket 2 (between 10 and 50), and `75` falls in bucket 3 (between 50 and 100).

**Output**:

| BUCKET1 | BUCKET2 | BUCKET3 |
| ------- | ------- | ------- |
| 1       | 2       | 3       |

### Example 2: Classify field values into risk levels

**Goal**: Assign risk levels to events based on their numeric value using bucket boundaries.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter risk_bucket = range_bucket(numeric_value, arraycreate(0, 25, 50, 75, 100))
| alter risk_level = if(risk_bucket = 0, "none", risk_bucket = 1, "low", risk_bucket = 2, "medium", risk_bucket = 3, "high", "critical")
| fields event_id, numeric_value, risk_bucket, risk_level
| limit 3
```

**Explanation**: This query classifies each `numeric_value` into a risk bucket using boundaries `[0, 25, 50, 75, 100]`, then maps each bucket to a human-readable risk level label.

**Output**:

| EVENT\_ID | NUMERIC\_VALUE | RISK\_BUCKET | RISK\_LEVEL |
| --------- | -------------- | ------------ | ----------- |
| 101       | 5.0            | 1            | low         |
| 102       | 60.0           | 3            | high        |
| 103       | 30.0           | 2            | medium      |

### Example 3: Create histogram buckets for duration values

**Goal**: Distribute duration values into histogram buckets for analysis.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter duration_bucket = range_bucket(duration_seconds, arraycreate(1, 5, 10, 30, 60))
| comp count(event_id) as event_count by duration_bucket
| fields duration_bucket, event_count
| sort asc duration_bucket
```

**Explanation**: This query assigns each event to a duration bucket based on `duration_seconds`, then counts the number of events in each bucket. This creates a histogram-like distribution of event durations.

**Output**:

| DURATION\_BUCKET | EVENT\_COUNT |
| ---------------- | ------------ |
| 0                | 3            |
| 1                | 5            |
| 2                | 4            |
| 3                | 2            |
| 4                | 1            |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`comp`](../stages/comp), [`fields`](../stages/fields), [`sort`](../stages/sort)
* **Functions**: [`arraycreate()`](arraycreate), [`if()`](if), [`floor()`](floor)
* **Datasets**: [`xdr_data`](https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction)
