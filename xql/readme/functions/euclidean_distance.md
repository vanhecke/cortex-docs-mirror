# euclidean\_distance

Use the `euclidean_distance()` function to calculate the Euclidean distance between two numeric vectors (arrays). The Euclidean distance is the straight-line distance between two points in multi-dimensional space.

## Syntax

```sql
euclidean_distance(<vector1>, <vector2>)
```

## Parameters

| Name      | Type                        | Required | Description                                                                |
| --------- | --------------------------- | -------- | -------------------------------------------------------------------------- |
| `vector1` | array of integers or floats | Yes      | The first numeric vector (array). Must have the same length as `vector2`.  |
| `vector2` | array of integers or floats | Yes      | The second numeric vector (array). Must have the same length as `vector1`. |

## Returns

**Type**: float

**Description**: The `euclidean_distance()` function returns a non-negative float representing the straight-line distance between the two input vectors. A value of `0.0` indicates identical vectors. If either input is `null` or the vectors have different lengths, the function returns `null`.

## Usage notes

* **Input type**: XQL doesn't support NaN or infinite values as input and these value types also can not be returned.
* **Vector Length**: Both input vectors must have the same number of elements. If they differ in length, the function returns `null`.
* **Vector Type**: Only float values are supported for the input vectors.
* **Null Handling**: If either input expression is `null`, the function returns `null`.
* **Non-Negative Result**: The result is always ≥ 0. A result of `0.0` means the two vectors are identical.
* **Formula**: The Euclidean distance is calculated as `sqrt(sum((v1[i] - v2[i])^2))` for all elements `i`.
* **Common Use Cases**: This function is typically used within the `alter` stage for similarity analysis, anomaly detection, clustering, and comparing feature vectors in machine learning workflows.

## Examples

### Example 1: Calculate Euclidean distance between literal vectors

**Goal**: Calculate the Euclidean distance between specific vector pairs to verify known results.

**XQL code**:

```sql
dataset = xdr_data
| limit 1
| alter dist1 = euclidean_distance(arraycreate(0.0, 0.0), arraycreate(3.0, 4.0))
| alter dist2 = euclidean_distance(arraycreate(1.0, 2.0, 3.0), arraycreate(1.0, 2.0, 3.0))
| fields dist1, dist2
```

**Explanation**: The distance between `(0.0,0.0)` and `(3.0,4.0)` is `5.0` (a classic 3-4-5 right triangle). The distance between two identical vectors `(1.0,2.0,3.0)` is `0.0`.

**Output**:

| DIST1 | DIST2 |
| ----- | ----- |
| 5.0   | 0.0   |

### Example 2: Calculate Euclidean distance between field vectors

**Goal**: Compute the Euclidean distance between an array field and a reference vector.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| filter numeric_codes != null and array_length(numeric_codes) = 5
| alter reference_vector = arraycreate(10.0, 20.0, 30.0, 40.0, 50.0)
| alter euc_dist = euclidean_distance(numeric_codes, reference_vector)
| fields event_id, numeric_codes, euc_dist
| limit 3
```

**Explanation**: This query creates a reference vector and computes the Euclidean distance between each record's `numeric_codes` array and the reference vector. Lower values indicate the vectors are closer together in multi-dimensional space.

**Output**:

| EVENT\_ID | NUMERIC\_CODES          | EUC\_DIST |
| --------- | ----------------------- | --------- |
| 101       | \[13, -47, 29, 82, -15] | 107.35    |
| 102       | \[-21, 56, 13, -88, 42] | 148.92    |
| 105       | \[8, 15, 25, 35, 45]    | 9.95      |

### Example 3: Find most similar records using Euclidean distance

**Goal**: Sort records by their Euclidean distance to a reference vector to find the most similar ones.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| filter numeric_codes != null and array_length(numeric_codes) = 5
| alter ref = arraycreate(10.0, 20.0, 30.0, 40.0, 50.0)
| alter distance = euclidean_distance(numeric_codes, ref)
| fields event_id, numeric_codes, distance
| sort asc distance
| limit 3
```

**Explanation**: This query computes the Euclidean distance between each record's `numeric_codes` and a reference vector, then sorts by distance ascending to show the most similar records first.

**Output**:

| EVENT\_ID | NUMERIC\_CODES          | DISTANCE |
| --------- | ----------------------- | -------- |
| 105       | \[8, 15, 25, 35, 45]    | 9.95     |
| 101       | \[13, -47, 29, 82, -15] | 107.35   |
| 102       | \[-21, 56, 13, -88, 42] | 148.92   |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`filter`](../stages/filter), [`fields`](../stages/fields), [`sort`](../stages/sort), [`limit`](../stages/limit)
* **Functions**: [`cosine_distance()`](cosine_distance), [`arraycreate()`](arraycreate), [`array_length()`](array_length), [`sqrt()`](sqrt)
* **Datasets**: [`xdr_data`](https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction)
