# top

Use the `top` stage to identify and return the most frequently occurring (or highest-sum) elements for a given field. The stage provides approximate counts and percentages, making it scalable for large datasets.

## Syntax

```sql
top <integer> <field> [by <field1> ,<field2>...] [top_count as <column name>, top_percent as <column name>]
```

## Parameters

| Name                 | Type    | Required | Description                                                                                                   |
| -------------------- | ------- | -------- | ------------------------------------------------------------------------------------------------------------- |
| `integer`            | integer | No       | Represents the number of top elements to return. If omitted, it defaults to up to 10 elements.                |
| `field`              | string  | Yes      | The field for which to find the top elements.                                                                 |
| `by field1, ...`     | string  | No       | An optional clause to group rows based on specified fields before identifying top elements within each group. |
| `top_count as ...`   | string  | No       | Optional alias to rename the default `TOP_COUNT` result column.                                               |
| `top_percent as ...` | string  | No       | Optional alias to rename the default `TOP_PERCENT` result column.                                             |

## Returns

The `top` stage returns a result set containing the specified fields, along with `TOP_COUNT` (the approximate count of the value) and `TOP_PERCENT` (the percentage of the value relative to the total).

## Usage notes

* The `top` stage produces approximate results, which are optimized for memory usage and time, particularly beneficial when dealing with vast amounts of data.
* **Early Filtering**: Apply `filter` stages as early as possible in your query to reduce the dataset size before the `top` stage processes the records.
* **Precise Field Selection**: Utilize the `fields` stage immediately after initial filtering to select only the necessary columns. This minimizes the data footprint passed to `top` and subsequent stages, improving overall query performance.
* **Timeframe Management**: Always use the smallest practical `timeframe` to limit data scanning.

## Examples

### Example 1: Basic top stage example

**Goal**: Identifies the top 3 most frequent event descriptions by count.

**XQL code**:

```sql
config timeframe = 1d // Use a practical timeframe
| dataset = sample_xql_raw // Specify the dataset
| fields event_id, event_description // Select relevant fields
| top 3 event_description // Find the top 3 event descriptions by frequency
| limit 5 // Limit results for brevity
```

**Explanation**: The query calculates the approximate frequency of each unique `event_description` and returns the top 3 based on that frequency. The query also provides the percentage of each in the total.

**Output**:

| event\_description               | TOP\_COUNT | TOP\_PERCENT |
| -------------------------------- | ---------- | ------------ |
| "User login successful"          | 1          | \~10.0%      |
| "File access attempt"            | 1          | \~10.0%      |
| "Network connection established" | 1          | \~10.0%      |

### Example 2: Top stage with `by` clause

**Goal**: Finds the top 1 event description for each 'is\_successful' status.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| fields is_successful, event_description // Select relevant fields
| top 1 event_description by is_successful // Find the top 1 event description within each 'is_successful' group
| limit 5
```

**Explanation**: The `by is_successful` clause groups the records first by their `is_successful` status, and then `top 1 event_description` is applied independently to each of these groups.

**Output**:

| is\_successful | event\_description      | TOP\_COUNT | TOP\_PERCENT |
| -------------- | ----------------------- | ---------- | ------------ |
| true           | "User login successful" | 1          | \~16.7%      |
| false          | "File access attempt"   | 1          | \~33.3%      |

### Example 3: Top stage with custom column names

**Goal**: Shows the top successful/unsuccessful statuses with custom count/percentage names.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| fields is_successful // Focus on the boolean field for clear counting
| top is_successful top_count as StatusCount, top_percent as StatusPercentage // Use custom column names
| limit 5
```

**Explanation**: The query identifies the frequencies of `true` and `false` in the `is_successful` field. The `top_count as StatusCount` and `top_percent as StatusPercentage` clauses rename the output columns as specified, enhancing readability.

**Output**:

| is\_successful | StatusCount | StatusPercentage |
| -------------- | ----------- | ---------------- |
| true           | 7           | 70.0%            |
| false          | 3           | 30.0%            |

## Related articles

* **Stages**: [`filter`](filter), [`fields`](fields), [`limit`](limit)
* **Functions**: [`approx_top`](../functions/approx_top)
* **Datasets**: [`xdr_data`](https://www.google.com/search?q=%5Bhttps://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction%5D\(https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction\))
