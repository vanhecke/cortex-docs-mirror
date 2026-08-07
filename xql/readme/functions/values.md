# values

Use the `values()` function to collect all distinct (unique) values of a specified field across grouped rows within the `comp` stage and return them as an array. This is similar to `ARRAY_AGG(DISTINCT ...)` in SQL.

## Syntax

```sql
| comp values(<field>) [by <group_field1>, <group_field2>, ...] [as <alias>]
```

## Parameters

| Name          | Type   | Required | Description                                                                                          |
| ------------- | ------ | -------- | ---------------------------------------------------------------------------------------------------- |
| `field`       | any    | Yes      | The field whose distinct values will be collected into an array.                                     |
| `group_field` | any    | No       | One or more fields to group the results by. If omitted, all rows are treated as a single group.      |
| `alias`       | string | No       | An alias for the output field. If not specified, the output field name defaults to `values_<field>`. |

## Returns

**Type**: array

**Description**: The `values()` function returns an array containing all distinct (unique) values of the specified field within each group. NULL values may be excluded. The order of elements in the array is not guaranteed.

## Usage notes

* **Distinct values**: Unlike the `list()` function which collects all values including duplicates, `values()` returns only unique values.
* **Data types**: Works with any data type (string, numeric, datetime, etc.).
* **Null handling**: NULL values are typically excluded from the result array.
* **No ordering**: The order of elements in the resulting array is not guaranteed.
* **No grouping**: When used without a `by` clause, all rows are aggregated into a single group.
* **Use case**: Useful for finding all unique values of a field within groups, such as all unique users who accessed a resource.

## Examples

### Example 1: Distinct source IPs per destination

**Goal**: Find all unique source IP addresses that connected to each destination IP.

**XQL code**:

```sql
dataset = xdr_data
| comp values(action_local_ip) by action_remote_ip as unique_source_ips
```

**Explanation**: The `values()` function collects all distinct `action_local_ip` values for each unique `action_remote_ip`, eliminating duplicate IPs.

**Output**:

| ACTION\_REMOTE\_IP | UNIQUE\_SOURCE\_IPS           |
| ------------------ | ----------------------------- |
| 10.0.0.1           | \[192.168.1.10, 192.168.1.20] |
| 10.0.0.2           | \[192.168.1.30]               |

### Example 2: All unique usernames across events

**Goal**: Find all distinct usernames across all events.

**XQL code**:

```sql
dataset = xdr_data
| comp values(actor_effective_username) as unique_users
```

**Explanation**: Without a `by` clause, the `values()` function collects all distinct `actor_effective_username` values across the entire dataset.

**Output**:

| UNIQUE\_USERS                        |
| ------------------------------------ |
| \[admin, user1, user2, svc\_account] |

### Example 3: Distinct event types per host

**Goal**: Find all unique event types observed on each host.

**XQL code**:

```sql
dataset = xdr_data
| comp values(event_type) by agent_hostname as event_types, count(*) as total_events
```

**Explanation**: This query combines `values()` with `count()` to show both the distinct event types and the total event count per host.

**Output**:

| AGENT\_HOSTNAME | EVENT\_TYPES              | TOTAL\_EVENTS |
| --------------- | ------------------------- | ------------- |
| workstation-1   | \[NETWORK, PROCESS, FILE] | 150           |
| workstation-2   | \[NETWORK, REGISTRY]      | 85            |

## Related articles

* **Stages**: [`comp`](../stages/comp), [`fields`](../stages/fields), [`limit`](../stages/limit)
* **Functions**: [`list()`](list_with_comp_stage), [`count()`](count_with_comp_stage), [`count_distinct()`](count_distinct)
* **Datasets**: [`xdr_data`](https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction)
