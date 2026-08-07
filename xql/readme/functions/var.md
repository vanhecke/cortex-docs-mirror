# var

Use the `var()` function to compute the variance of a specified numeric field across all rows in each group within the `comp` stage. Variance measures how far values are spread out from the mean. By default, `var()` computes the population variance. This is equivalent to `VAR_POP` in SQL.

## Syntax

```sql
| comp var(<field>) [by <group_field1>, <group_field2>, ...] [as <alias>]
```

## Parameters

| Name          | Type    | Required | Description                                                                                       |
| ------------- | ------- | -------- | ------------------------------------------------------------------------------------------------- |
| `field`       | numeric | Yes      | The numeric field from which to compute the variance.                                             |
| `group_field` | any     | No       | One or more fields to group the results by. If omitted, all rows are treated as a single group.   |
| `alias`       | string  | No       | An alias for the output field. If not specified, the output field name defaults to `var_<field>`. |

## Returns

**Type**: numeric (float)

**Description**: The `var()` function returns the population variance of the specified field within each group. Returns NULL if all values in the group are NULL. Returns 0 if there is only one non-NULL value.

## Usage notes

* **Variance definition**: Variance is the average of the squared differences from the mean: `sum((x - mean)^2) / N`.
* **Relationship to standard deviation**: Variance is the square of the standard deviation. `var(x) = stddev_population(x)^2`.
* **Null handling**: NULL values are ignored in the computation.
* **Data types**: Only works with numeric fields.
* **Single value**: If there is only one non-NULL value, the variance is 0.
* **Use case**: Variance is useful for statistical analysis, anomaly detection, and understanding data distribution.

## Examples

### Example 1: Variance of response times per host

**Goal**: Compute the variance of response times for each host.

**XQL code**:

```sql
dataset = xdr_data
| comp var(action_total_time) by agent_hostname as response_variance
```

**Explanation**: The `var()` function computes the population variance of `action_total_time` for each unique `agent_hostname`, measuring how spread out the response times are from the mean.

**Output**:

| AGENT\_HOSTNAME | RESPONSE\_VARIANCE |
| --------------- | ------------------ |
| workstation-1   | 155.00             |
| workstation-2   | 69.22              |

### Example 2: Overall variance of bytes transferred

**Goal**: Compute the variance of bytes transferred across all events.

**XQL code**:

```sql
dataset = xdr_data
| comp var(action_network_bytes_received) as bytes_variance
```

**Explanation**: Without a `by` clause, the `var()` function computes the population variance across all rows.

**Output**:

| BYTES\_VARIANCE |
| --------------- |
| 6035782.45      |

### Example 3: Variance with mean and standard deviation

**Goal**: Compute variance alongside mean and standard deviation for comprehensive statistical analysis.

**XQL code**:

```sql
dataset = xdr_data
| comp var(action_total_time) as variance, avg(action_total_time) as mean, stddev_population(action_total_time) as stddev by agent_hostname
```

**Explanation**: This query combines `var()`, `avg()`, and `stddev_population()` to provide a complete statistical summary per host. Note that the variance equals the square of the standard deviation.

**Output**:

| AGENT\_HOSTNAME | VARIANCE | MEAN  | STDDEV |
| --------------- | -------- | ----- | ------ |
| workstation-1   | 155.00   | 45.30 | 12.45  |
| workstation-2   | 69.22    | 32.10 | 8.32   |

## Related articles

* **Stages**: [`comp`](../stages/comp), [`fields`](../stages/fields), [`limit`](../stages/limit)
* **Functions**: [`stddev_population()`](stddev_population_with_comp_stage), [`stddev_sample()`](stddev_sample_with_comp_stage), [`avg()`](avg_with_comp_stage)
* **Datasets**: [`xdr_data`](https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction)
