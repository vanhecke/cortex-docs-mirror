# stddev\_sample (comp)

Use the `stddev_sample()` function to compute the sample standard deviation of a specified numeric field across all rows in each group within the `comp` stage. Sample standard deviation uses Bessel's correction (dividing by N-1 instead of N) and is appropriate when the data represents a sample from a larger population. This is equivalent to `STDDEV_SAMP` in SQL.

## Syntax

```sql
| comp stddev_sample(<field>) [by <group_field1>, <group_field2>, ...] [as <alias>]
```

## Parameters

| Name          | Type    | Required | Description                                                                                                 |
| ------------- | ------- | -------- | ----------------------------------------------------------------------------------------------------------- |
| `field`       | numeric | Yes      | The numeric field from which to compute the sample standard deviation.                                      |
| `group_field` | any     | No       | One or more fields to group the results by. If omitted, all rows are treated as a single group.             |
| `alias`       | string  | No       | An alias for the output field. If not specified, the output field name defaults to `stddev_sample_<field>`. |

## Returns

**Type**: numeric (float)

**Description**: The `stddev_sample()` function returns the sample standard deviation of the specified field within each group. Returns NULL if there are fewer than two non-NULL values in the group.

## Usage notes

* **Sample vs. population**: Use `stddev_sample()` when the data is a sample from a larger population. Use `stddev_population()` when the data represents the entire population.
* **Formula**: Sample standard deviation is calculated as: `sqrt(sum((x - mean)^2) / (N - 1))`, where N is the number of non-NULL values (Bessel's correction).
* **Minimum values**: Requires at least two non-NULL values to produce a result. Returns NULL for groups with fewer than two values.
* **Null handling**: NULL values are ignored in the computation.
* **Data types**: Only works with numeric fields.

## Examples

### Example 1: Sample standard deviation of response times per host

**Goal**: Compute the sample standard deviation of response times for each host.

**XQL code**:

```sql
dataset = xdr_data
| comp stddev_sample(action_total_time) by agent_hostname as sample_stddev
```

**Explanation**: The `stddev_sample()` function computes the sample standard deviation of `action_total_time` for each unique `agent_hostname`, using Bessel's correction for unbiased estimation.

**Output**:

| AGENT\_HOSTNAME | SAMPLE\_STDDEV |
| --------------- | -------------- |
| workstation-1   | 14.42          |
| workstation-2   | 9.62           |

### Example 2: Overall sample standard deviation

**Goal**: Compute the sample standard deviation of bytes transferred across all events.

**XQL code**:

```sql
dataset = xdr_data
| comp stddev_sample(action_network_bytes_received) as bytes_sample_stddev
```

**Explanation**: Without a `by` clause, the `stddev_sample()` function computes the sample standard deviation across all rows.

**Output**:

| BYTES\_SAMPLE\_STDDEV |
| --------------------- |
| 2678.91               |

### Example 3: Compare population and sample standard deviations

**Goal**: Compare population and sample standard deviations to understand the effect of Bessel's correction.

**XQL code**:

```sql
dataset = xdr_data
| comp stddev_sample(action_total_time) as sample_std, stddev_population(action_total_time) as pop_std, count(action_total_time) as n by agent_hostname
```

**Explanation**: This query computes both `stddev_sample()` and `stddev_population()` alongside the count, showing how the sample standard deviation is slightly larger due to Bessel's correction (dividing by N-1 instead of N).

**Output**:

| AGENT\_HOSTNAME | SAMPLE\_STD | POP\_STD | N |
| --------------- | ----------- | -------- | - |
| workstation-1   | 14.42       | 12.45    | 5 |
| workstation-2   | 9.62        | 8.32     | 4 |

## Related articles

* **Stages**: [`comp`](../stages/comp), [`fields`](../stages/fields), [`limit`](../stages/limit)
* **Functions**: [`stddev_population()`](stddev_population_with_comp_stage), [`stddev_sample (windowcomp)`](stddev_sample_with_windowcomp_stage), [`avg()`](avg_with_comp_stage), [`var()`](var)
* **Datasets**: [`xdr_data`](https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction)
