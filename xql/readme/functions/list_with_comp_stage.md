# list (comp)

Use the `list()` function to collect all values of a specified field across grouped rows and return them as an array (list) within the `comp` stage. This is equivalent to `ARRAY_AGG` in SQL.

## Syntax

```sql
| comp list(<field>) [by <group_field1>, <group_field2>, ...] [as <alias>]
```

## Parameters

| Name          | Type   | Required | Description                                                                                        |
| ------------- | ------ | -------- | -------------------------------------------------------------------------------------------------- |
| `field`       | any    | Yes      | The field whose values will be collected into a list.                                              |
| `group_field` | any    | No       | One or more fields to group the results by. If omitted, all rows are treated as a single group.    |
| `alias`       | string | No       | An alias for the output field. If not specified, the output field name defaults to `list_<field>`. |

## Returns

**Type**: array

**Description**: The `list()` function returns an array containing all values of the specified field within each group. NULL values may be included.

## Usage notes

* **Duplicates**: The `list` function collects all values, including duplicates.
* **Order**: The order of elements in the resulting array is not guaranteed unless a `sort` stage is applied before the `comp` stage.
* **Distinct values**: If you need only distinct values, consider using the `values` function instead.
* **Data types**: The function can be used with any data type.
* **No grouping**: When used without a `by` clause, all rows are aggregated into a single group.

## Examples

### Example 1: Collect all source IPs by destination IP

**Goal**: Collect all local IP addresses grouped by remote IP address.

**XQL code**:

```sql
dataset = xdr_data
| comp list(action_local_ip) by action_remote_ip as source_ips
```

**Explanation**: The `list()` function collects all `action_local_ip` values for each unique `action_remote_ip` and returns them as an array named `source_ips`.

**Output**:

| ACTION\_REMOTE\_IP | SOURCE\_IPS                                 |
| ------------------ | ------------------------------------------- |
| 10.0.0.1           | \[192.168.1.10, 192.168.1.20, 192.168.1.10] |
| 10.0.0.2           | \[192.168.1.30]                             |

### Example 2: Collect all usernames across all events

**Goal**: Collect all effective usernames from all events into a single array.

**XQL code**:

```sql
dataset = xdr_data
| comp list(actor_effective_username) as all_users
```

**Explanation**: Without a `by` clause, the `list()` function aggregates all `actor_effective_username` values across all rows into a single array named `all_users`.

**Output**:

| ALL\_USERS                           |
| ------------------------------------ |
| \[admin, user1, admin, user2, user1] |

## Related articles

* **Stages**: [`comp`](../stages/comp), [`sort`](../stages/sort), [`fields`](../stages/fields)
* **Functions**: [`values()`](values), [`count()`](count_with_comp_stage)
* **Datasets**: [`xdr_data`](https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction)
