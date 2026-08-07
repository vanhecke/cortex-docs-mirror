# stddev\_population (comp)

Use the `stddev_population()` function to compute the population standard deviation of a specified numeric field across all rows in each group within the `comp` stage. Population standard deviation measures the spread of values when the data represents the entire population. This is equivalent to `STDDEV_POP` in SQL.

## Syntax

```sql
| comp stddev_population(<field>) [by <group_field1>, <group_field2>, ...] [as <alias>]
```

## Parameters

| Name          | Type    | Required | Description                                                                                                     |
| ------------- | ------- | -------- | --------------------------------------------------------------------------------------------------------------- |
| `field`       | numeric | Yes      | The numeric field from which to compute the population standard deviation.                                      |
| `group_field` | any     | No       | One or more fields to group the results by. If omitted, all rows are treated as a single group.                 |
| `alias`       | string  | No       | An alias for the output field. If not specified, the output field name defaults to `stddev_population_<field>`. |

## Returns

**Type**: numeric (float)

**Description**: The `stddev_population()` function returns the population standard deviation of the specified field within each group. Returns NULL if all values in the group are NULL. Returns 0 if there is only one non-NULL value.

## Usage notes

* **Population vs. sample**: Use `stddev_population()` when the data represents the entire population. Use `stddev_sample()` when the data is a sample from a larger population.
* **Formula**: Population standard deviation is calculated as the square root of the population variance: `sqrt(sum((x - mean)^2) / N)`, where N is the number of non-NULL values.
* **Null handling**: NULL values are ignored in the computation.
* **Single value**: If there is only one non-NULL value, the population standard deviation is 0.
* **Data types**: Only works with numeric fields.

## Examples

### Example 1: Standard deviation of response times per host

**Goal**: Compute the population standard deviation of response times for each host.

**XQL code**:

```sql
dataset = xdr_data
| comp stddev_population(action_total_time) by agent_hostname as stddev_response
```

**Explanation**: The `stddev_population()` function computes the population standard deviation of `action_total_time` for each unique `agent_hostname`, measuring how spread out the response times are.

**Output**:

| AGENT\_HOSTNAME | STDDEV\_RESPONSE |
| --------------- | ---------------- |
| workstation-1   | 12.45            |
| workstation-2   | 8.32             |

### Example 2: Overall standard deviation of bytes transferred

**Goal**: Compute the population standard deviation of bytes transferred across all events.

**XQL code**:

```sql
dataset = xdr_data
| comp stddev_population(action_network_bytes_received) as bytes_stddev
```

**Explanation**: Without a `by` clause, the `stddev_population()` function computes the population standard deviation across all rows.

**Output**:

| BYTES\_STDDEV |
| ------------- |
| 2456.78       |

### Example 3: Compare standard deviation with mean

**Goal**: Compute both the mean and standard deviation to understand data distribution per host.

**XQL code**:

```sql
dataset = xdr_data
| comp stddev_population(action_total_time) as stddev_time, avg(action_total_time) as avg_time by agent_hostname
```

**Explanation**: This query combines `stddev_population()` with `avg()` to provide both the average and the spread of response times per host, enabling coefficient of variation analysis.

**Output**:

| AGENT\_HOSTNAME | STDDEV\_TIME | AVG\_TIME |
| --------------- | ------------ | --------- |
| workstation-1   | 12.45        | 45.30     |
| workstation-2   | 8.32         | 32.10     |

## Related articles

* **Stages**: [`comp`](../stages/comp), [`fields`](../stages/fields), [`limit`](../stages/limit)
* **Functions**: [`stddev_sample()`](stddev_sample_with_comp_stage), [`stddev_population (windowcomp)`](stddev_population_with_windowcomp_stage), [`avg()`](avg_with_comp_stage), [`var()`](var)
* **Datasets**: [`xdr_data`](https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction)
