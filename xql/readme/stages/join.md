# join

Use the `join` stage to combine the results of two queries into a single result set based on a specified condition.

## Syntax

```sql
join conflict_strategy = both|left|right type = inner|left|right ((<xql query>) as <execution_name> <boolean_expr>)
```

## Parameters

| Name                | Type        | Required | Description                                                                                                                                                                                                                           |
| ------------------- | ----------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `conflict_strategy` | string      | No       | Identifies how column name conflicts are resolved if a field name exists in both the parent (left) query's result set and the joined (right) query's result set. Valid values are `both`, `left`, or `right`. The default is `right`. |
| `type`              | string      | No       | Defines the type of join, dictating which records are included in the final result set based on the join condition. Valid values are `inner`, `left`, or `right`. The default is `inner`.                                             |
| `xql query`         | query block | Yes      | The XQL query whose results you want to combine with the parent query. This sub-query must be enclosed in parentheses.                                                                                                                |
| `execution_name`    | string      | Yes      | Provides an alias for the joined query's result set using the `as` clause. This alias is used to refer to fields from the joined query (for example, `alias.field_name`).                                                             |
| `boolean_expr`      | expression  | Yes      | Identifies the conditions (join keys) that must be met to place a record in the join result set.                                                                                                                                      |

## Returns

The `join` stage returns a unified result set containing rows from the parent query combined with rows from the sub-query, based on the specified join type and condition.

## Usage notes

* The `join` stage can combine results, but it does not preserve sort order. If sorting is needed, specify the `sort` stage **after** the `join` stage.
* `join` operations, especially on large datasets like `xdr_data`, can be resource-intensive. It is a Best practice to pare down datasets before joining them.
* Always use the `fields` stage early in your queries, including within the sub-queries of a `join`, to select only necessary columns. This minimizes the data processed and improves performance.
* The `config case_sensitive` stage can be used at the beginning of the query or when adding a `join` stage to control case sensitivity for field value evaluation.
* By default, forensic datasets are not included in XQL query results unless explicitly defined. Queries for forensic data require specific enabling steps.

## Examples

### Example 1: Inner join

**Goal**: Perform an inner join to return only the records where there is a match in `event_id` from both the left and right datasets.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| filter event_id in (101, 102, 103, 104) // Simulates left side
| fields event_id, event_description
| join type = inner (
    dataset = sample_xql_raw
    | filter event_id in (103, 104, 105, 106) // Simulates right side
    | fields event_id as joined_event_id, is_successful as success_status
) as right_data right_data.joined_event_id = event_id // Join condition
```

**Explanation**: This query joins records from `sample_xql_raw` where `event_id` is 101, 102, 103, or 104, with records where `event_id` is 103, 104, 105, or 106. Only `event_id`s present in both sets will be returned. The `joined_event_id` from `right_data` is matched with `event_id` from the main query.

**Output**:

| event\_id | event\_description             | joined\_event\_id | success\_status |
| --------- | ------------------------------ | ----------------- | --------------- |
| 103       | Network connection established | 103               | true            |
| 104       | System heartbeat               | 104               | true            |

### Example 2: Left join

**Goal**: Perform a left join to return all records from the left dataset, and the matching records from the right.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| filter event_id in (101, 102, 103, 104) // Simulates left side
| fields event_id, event_description
| join type = left (
    dataset = sample_xql_raw
    | filter event_id in (103, 104, 105, 106) // Simulates right side
    | fields event_id as joined_event_id, is_successful as success_status
) as right_data right_data.joined_event_id = event_id // Join condition
```

**Explanation**: This query returns all `event_id`s 101, 102, 103, 104 from the left side. For `event_id`s 101 and 102, since there are no matching records on the right side, `NULL` is populated for `joined_event_id` and `success_status`.

**Output**:

| event\_id | event\_description             | joined\_event\_id | success\_status |
| --------- | ------------------------------ | ----------------- | --------------- |
| 101       | User login successful          | NULL              | NULL            |
| 102       | File access attempt            | NULL              | NULL            |
| 103       | Network connection established | 103               | true            |
| 104       | System heartbeat               | 104               | true            |

### Example 3: Right join

**Goal**: Perform a right join to return all records from the right dataset, and the matching records from the left.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| filter event_id in (101, 102, 103, 104) // Simulates left side
| fields event_id, event_description
| join type = right (
    dataset = sample_xql_raw
    | filter event_id in (103, 104, 105, 106) // Simulates right side
    | fields event_id as joined_event_id, is_successful as success_status
) as right_data right_data.joined_event_id = event_id // Join condition
```

**Explanation**: This query returns all `event_id`s 103, 104, 105, 106 from the right side. For `event_id`s 105 and 106, since there are no matching records on the left side, `NULL` is populated for `event_description`.

**Output**:

| event\_id | event\_description             | joined\_event\_id | success\_status |
| --------- | ------------------------------ | ----------------- | --------------- |
| 103       | Network connection established | 103               | true            |
| 104       | System heartbeat               | 104               | true            |
| NULL      | NULL                           | 105               | true            |
| NULL      | NULL                           | 106               | false           |

### Example 4: Conflict strategy left

**Goal**: Perform an inner join while prioritizing the column from the original (parent) query's result set when a conflict exists.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| filter event_id in (101, 102, 103, 104) // Simulates left side with original event_description
| fields event_id, event_description
| join conflict_strategy = left // Prioritize left side event_description
type = inner (
    dataset = sample_xql_raw
    | filter event_id in (103, 104, 105, 106) // Simulates right side data for join
    | fields event_id as joined_event_id, is_successful as event_description // This event_description will be discarded due to conflict_strategy = left
) as right_data right_data.joined_event_id = event_id // Join condition
| fields event_id, event_description, joined_event_id // Select fields to show output
```

**Explanation**: The sub-query renames `is_successful` to `event_description` to create a conflict. Since `conflict_strategy = left` is specified, the `event_description` from the primary (left) query, which contains string values (for example, "Network connection established"), is preserved.

**Output**:

| event\_id | event\_description             | joined\_event\_id |
| --------- | ------------------------------ | ----------------- |
| 103       | Network connection established | 103               |
| 104       | System heartbeat               | 104               |

### Example 5: Conflict strategy right

**Goal**: Perform an inner join while prioritizing the column from the inner (joined) query's result set when a conflict exists.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| filter event_id in (101, 102, 103, 104) // Simulates left side with original event_description
| fields event_id, event_description
| join conflict_strategy = right // Prioritize right side event_description
type = inner (
    dataset = sample_xql_raw
    | filter event_id in (103, 104, 105, 106) // Simulates right side data for join
    | fields event_id as joined_event_id, is_successful as event_description // This event_description will be kept
) as right_data right_data.joined_event_id = event_id // Join condition
| fields event_id, event_description, joined_event_id // Select fields to show output
```

**Explanation**: With `conflict_strategy = right`, the `event_description` column from the inner (right) query is kept. This results in the `event_description` column containing the boolean values from `is_successful` (for example, `true`), while the original string `event_description` from the left query is discarded for the joined records.

**Output**:

| event\_id | event\_description | joined\_event\_id |
| --------- | ------------------ | ----------------- |
| 103       | true               | 103               |
| 104       | true               | 104               |

## Related articles

* **Stages**: [`config`](config), [`dataset`](dataset), [`fields`](fields), [`filter`](filter), [`sort`](sort)
* **Datasets**: [`xdr_data`](https://www.google.com/search?q=%5Bhttps://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction%5D\(https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction\))
