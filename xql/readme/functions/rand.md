# rand

Use the `rand()` function to generate a pseudo-random floating-point number between 0 (inclusive) and 1 (exclusive).

## Syntax

```sql
rand()
```

## Parameters

This function takes no parameters.

## Returns

**Type**: float

**Description**: The `rand()` function returns a pseudo-random floating-point number in the range 0, 1). Each invocation produces a different random value.

## Usage notes

* **Input type**: XQL doesn't support NaN or infinite values as input and these value types also can not be returned.
* **No Arguments**: The `rand()` function takes no parameters and generates a new random value each time it is called.
* **Range**: The returned value is always ≥ 0.0 and < 1.0.
* **Non-Deterministic**: Each call to `rand()` produces a different value. Results are not reproducible across query executions.
* **Scaling**: To generate random numbers in a different range, multiply the result by the desired range and add an offset. For example, `add(multiply(rand(), 100), 1)` generates a random number between 1 and 101.
* **Common Use Cases**: This function is typically used within the `alter` stage for random sampling, generating test data, randomized ordering, and probabilistic analysis.

## Examples

### Example 1: Generate random values for each record

**Goal**: Add a random value to each record in the dataset.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter random_val = rand()
| fields event_id, random_val
| limit 3
```

**Explanation**: This query generates a random floating-point number between 0 and 1 for each record and stores it in `random_val`. Each record receives a different random value.

**Output**:

| EVENT\_ID | RANDOM\_VAL |
| --------- | ----------- |
| 101       | 0.73214     |
| 102       | 0.15892     |
| 103       | 0.94501     |

### Example 2: Random sampling of records

**Goal**: Randomly sample approximately 50% of records from the dataset.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter sample_flag = rand()
| filter sample_flag < 0.5
| fields event_id, source_name
| limit 5
```

**Explanation**: This query assigns a random value to each record, then filters to keep only records where the random value is less than 0.5, effectively sampling approximately 50% of the data.

**Output**:

| EVENT\_ID | SOURCE\_NAME |
| --------- | ------------ |
| 102       | server-01    |
| 104       | server-03    |
| 107       | server-02    |
| 109       | server-01    |
| 111       | server-03    |

### Example 3: Generate random integers in a specific range

**Goal**: Generate random integers between 1 and 100 for each record.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter random_int = to_integer(add(multiply(rand(), 100), 1))
| fields event_id, random_int
| limit 3
```

**Explanation**: This query scales the random value from \[0, 1) to \[1, 101) by multiplying by 100 and adding 1, then converts to an integer using `to_integer()` to produce whole numbers between 1 and 100.

**Output**:

| EVENT\_ID | RANDOM\_INT |
| --------- | ----------- |
| 101       | 47          |
| 102       | 83          |
| 103       | 12          |

## Related articles

* **Stages**: \[`alter`, [`filter`](../stages/filter), [`fields`](../stages/fields), [`limit`](../stages/limit)
* **Functions**: [`multiply()`](multiply), [`add()`](add), [`to_integer()`](to_integer), [`floor()`](floor)
