# row\_number (windowcomp)

Use the `row_number()` function within the `windowcomp` stage to assign a unique sequential integer to each row within a partition, based on the specified sort order. The numbering starts at 1 for the first row in each partition. This is equivalent to `ROW_NUMBER() OVER(...)` in SQL.

## Syntax

```sql
| windowcomp row_number() [by <partition_field1>, <partition_field2>, ...] sort [asc|desc] <sort_field1> [, [asc|desc] <sort_field2>, ...] [as <alias>]
```

## Parameters

| Name              | Type   | Required | Description                                                                                                                                           |
| ----------------- | ------ | -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| `partition_field` | any    | No       | One or more fields to partition the data by (equivalent to SQL `PARTITION BY`).                                                                       |
| `sort_field`      | any    | Yes      | One or more fields to define the order within each partition (equivalent to SQL `ORDER BY`). Required for numbering functions. Defaults to ascending. |
| `alias`           | string | No       | An alias for the output field.                                                                                                                        |

## Returns

**Type**: integer

**Description**: The `row_number()` function returns a unique sequential integer (starting at 1) for each row within its partition, based on the sort order. Unlike `rank()`, every row receives a distinct number even when sort values are tied.

## Usage notes

* **Sort required**: The `sort` clause is mandatory for the `row_number()` function.
* **Numbering function**: `row_number()` is a numbering function and cannot be used with window frames (`between` clause).
* **Unique values**: Unlike `rank()`, `row_number()` always assigns unique sequential numbers. When rows have identical sort values, the assignment among tied rows is non-deterministic.
* **Deduplication**: `row_number()` is commonly used for deduplication by assigning row numbers within groups and then filtering for `row_number = 1`.
* **1-based indexing**: Row numbering starts at 1, not 0.

## Examples

### Example 1: Number events chronologically per host

**Goal**: Assign a sequential number to each event per host, ordered by time.

**XQL code**:

```sql
dataset = xdr_data
| windowcomp row_number() by agent_hostname sort asc _time as event_seq
```

**Explanation**: The `row_number()` function assigns a sequential number to each row within each `agent_hostname` partition, ordered by `_time` in ascending order.

**Output**:

| \_TIME              | AGENT\_HOSTNAME | ALERT\_SEVERITY | EVENT\_SEQ |
| ------------------- | --------------- | --------------- | ---------- |
| 2024-01-15 08:00:00 | workstation-1   | 3               | 1          |
| 2024-01-15 09:00:00 | workstation-1   | 7               | 2          |
| 2024-01-15 10:00:00 | workstation-1   | 5               | 3          |
| 2024-01-15 08:30:00 | workstation-2   | 2               | 1          |
| 2024-01-15 09:30:00 | workstation-2   | 4               | 2          |

### Example 2: Deduplication — keep latest event per host

**Goal**: Keep only the most recent event for each host by using `row_number()` and filtering.

**XQL code**:

```sql
dataset = xdr_data
| windowcomp row_number() by agent_hostname sort desc _time as rn
| filter rn = 1
| fields - rn
```

**Explanation**: The `row_number()` function assigns `1` to the most recent event (sorted descending by `_time`) within each `agent_hostname` partition. The `filter` stage keeps only the first row per host, and `fields - rn` removes the helper column.

**Output**:

| \_TIME              | AGENT\_HOSTNAME | ALERT\_SEVERITY |
| ------------------- | --------------- | --------------- |
| 2024-01-15 10:00:00 | workstation-1   | 5               |
| 2024-01-15 09:30:00 | workstation-2   | 4               |

### Example 3: Global row numbering

**Goal**: Assign a global sequential number to all events ordered by time.

**XQL code**:

```sql
dataset = xdr_data
| windowcomp row_number() sort asc _time as global_row_num
```

**Explanation**: Without a `by` clause, the `row_number()` function assigns a unique sequential number to every row across the entire result set, ordered by `_time`.

**Output**:

| \_TIME              | AGENT\_HOSTNAME | GLOBAL\_ROW\_NUM |
| ------------------- | --------------- | ---------------- |
| 2024-01-15 08:00:00 | workstation-1   | 1                |
| 2024-01-15 08:30:00 | workstation-2   | 2                |
| 2024-01-15 09:00:00 | workstation-1   | 3                |
| 2024-01-15 09:30:00 | workstation-2   | 4                |
| 2024-01-15 10:00:00 | workstation-1   | 5                |

## Related articles

* **Stages**: [`windowcomp`](../stages/windowcomp), [`dedup`](../stages/dedup), [`sort`](../stages/sort)
* **Functions**: [`rank()`](rank_with_windowcomp_stage)
* **Datasets**: [`xdr_data`](https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction)
