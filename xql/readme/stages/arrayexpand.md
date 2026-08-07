# arrayexpand

Use the `arrayexpand` stage to expand the values of a multi-value array field into separate events, creating a new record in the result set for each item present in the array.This is particularly useful when you need to analyze or filter individual elements within an array as if they were separate rows of data.

## Syntax

```sql
arrayexpand <array_field> [limit <limit_number>]

```

## Parameters

| Name           | Type    | Required | Description                                                                                                                                                                                                 |
| -------------- | ------- | -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `array_field`  | string  | Yes      | The name of the array field you wish to expand.                                                                                                                                                             |
| `limit_number` | integer | No       | Specifies the maximum number of records to create from the array expansion. If an array has more elements than this limit, only up to the specified number of records will be generated from its expansion. |

## Returns

The `arrayexpand` stage returns a dataset where, for each element in the specified array field, a new row is generated in the result set, duplicating all other fields from the original row.

## Usage notes

* The records created by `arrayexpand` are returned in no particular order.
* If a specific order is required, you must apply a `sort` stage after `arrayexpand`.
* The expansion duplicates all other fields from the original row for every new record created.

## Examples

### Example 1: Basic arrayexpand on a simple array

**Goal**: Expand the `string_tags` array into separate records. **XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| fields event_id, string_tags 
| arrayexpand string_tags
| limit 5 

```

**Explanation**: For each original row in `sample_xql_raw` that has values in `string_tags` (for example, event ID 101 has `["security", "login"]`), `arrayexpand` creates a separate row for each tag. Event ID 101 results in two rows: one for "security" and one for "login", each retaining the original `event_id`.

**Output:**

| event\_id | string\_tags |
| --------- | ------------ |
| 101       | security     |
| 101       | login        |
| 102       | filesystem   |
| 102       | critical     |
| 103       | network      |

### Example 2: arrayexpand with limit

**Goal**: Expand the `numeric_codes` array but restrict the number of expanded records for each original row to a specified limit.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| fields event_id, numeric_codes 
| arrayexpand numeric_codes limit 2 
| limit 5 

```

**Explanation**: For original rows like event ID 101, which has `numeric_codes` containing 5 elements, this query creates new records for only the first two elements. If the array has fewer than two elements, the query creates records for all existing elements.

**Output:**

| event\_id | numeric\_codes |
| --------- | -------------- |
| 101       | 13             |
| 101       | -47            |
| 102       | -21            |
| 102       | 56             |
| 103       | 90             |

### Example 3: arrayexpand followed by sort

**Goal**: Expand `string_tags` and then sort the resulting records by the expanded tag value.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| fields event_id, string_tags 
| arrayexpand string_tags
| sort asc string_tags 
| limit 5 

```

**Explanation**: This query first expands the `string_tags` array for each event. Then, it sorts all the generated records based on the `string_tags` field (which now holds individual tag values), ensuring the final output is ordered alphabetically by tag.

**Output:**

| event\_id | string\_tags |
| --------- | ------------ |
| 103       | cloud        |
| 102       | critical     |
| 105       | data\_ops    |
| 102       | filesystem   |
| 101       | login        |

### Example 4: arrayexpand on an array of JSON objects

**Goal**: Expand an array where each element is a JSON object, then extract a specific scalar value from those expanded objects.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| filter array_length(array_of_json_objects) > 0 
| fields event_id, array_of_json_objects 
| arrayexpand array_of_json_objects 
| alter action_type = json_extract_scalar(array_of_json_objects, "$.action") 
| fields event_id, action_type 
| limit 5
```

**Explanation**: For an event like ID 101, which has an array of JSON objects, this query first expands the array into separate records. Then, for each of these new records, it extracts the value associated with the "action" key using `json_extract_scalar()`, creating a new `action_type` field.

**Output:**

| event\_id | action\_type |
| --------- | ------------ |
| 101       | read         |
| 101       | write        |
| 106       | NULL         |
| 106       | NULL         |
| 105       | NULL         |

## Related articles

* **Stages**: [`sort`](sort), [`fields`](fields), [`limit`](limit), [`alter`](alter)
* **Functions**: [`json_extract_scalar`](../functions/json_extract_scalar), [`array_length`](../functions/array_length)
* **Datasets**: [`xdr_data`](https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction)
