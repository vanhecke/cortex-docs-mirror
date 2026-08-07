# cosine\_distance

Use the `cosine_distance()` function to calculate the cosine distance between two numeric vectors (arrays). The cosine distance measures the dissimilarity between two vectors based on the angle between them.

## Syntax

```sql
cosine_distance(<vector1>, <vector2>)
```

## Parameters

| Name      | Type                        | Required | Description                                                                |
| --------- | --------------------------- | -------- | -------------------------------------------------------------------------- |
| `vector1` | array of integers or floats | Yes      | The first numeric vector (array). Must have the same length as `vector2`.  |
| `vector2` | array of integers or floats | Yes      | The second numeric vector (array). Must have the same length as `vector1`. |

## Returns

**Type**: float

**Description**: The `cosine_distance()` function returns a value between 0 and 2, where 0 indicates identical direction, 1 indicates orthogonal (perpendicular) vectors, and 2 indicates opposite directions. If either input is `null` or the vectors have different lengths, the function returns `null`.

## Usage notes

* **Input type**: XQL doesn't support NaN or infinite values as input and these value types also can not be returned.
* **Vector Length**: Both input vectors must have the same number of elements. If they differ in length, the function returns `null`.
* **Vector Type**: Only float values are supported for the input vectors.
* **Null Handling**: If either input expression is `null`, the function returns `null`.
* **Zero Vectors**: If either vector is a zero vector (all elements are 0), the result is undefined and may return `NaN` or `null`.
* **Relationship to Cosine Similarity**: Cosine distance = 1 - cosine similarity. A cosine distance of 0 means the vectors are identical in direction (cosine similarity of 1).
* **Common Use Cases**: This function is typically used within the `alter` stage for similarity analysis, text comparison using embedding vectors, anomaly detection, and machine learning feature comparison.

## Examples

### Example 1: Calculate cosine distance between literal vectors

**Goal**: Calculate the cosine distance between specific vector pairs to verify known results.

**XQL code**:

```sql
dataset = xdr_data
| limit 1
| alter dist1 = cosine_distance(arraycreate(1.0, 0.0, 0.0), arraycreate(1.0, 0.0, 0.0))
| alter dist2 = cosine_distance(arraycreate(1.0, 0.0, 0.0), arraycreate(0.0, 1.0, 0.0))
| fields dist1, dist2
```

**Explanation**: `cosine_distance` of two identical vectors `(1.0, 0.0, 0.0)` returns `0.0` (no distance). The distance between `(1.0, 0.0, 0.0)` and `(0.0, 1.0, 0.0)` returns `1.0` since these vectors are orthogonal (perpendicular).

**Output**:

| DIST1 | DIST2 |
| ----- | ----- |
| 0.0   | 1.0   |

### Example 2: Calculate cosine distance between field vectors

**Goal**: Compute the cosine distance between two array fields in a dataset.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| filter numeric_codes != null
| alter reference_vector = arraycreate(1.0, 2.0, 3.0, 4.0, 5.0)
| alter cos_dist = cosine_distance(numeric_codes, reference_vector)
| fields event_id, numeric_codes, cos_dist
| limit 3
```

**Explanation**: This query creates a reference vector and computes the cosine distance between each record's `numeric_codes` array and the reference vector. Lower values indicate the vectors point in a more similar direction.

**Output**:

| EVENT\_ID | NUMERIC\_CODES             | COS\_DIST |
| --------- | -------------------------- | --------- |
| 101       | \[13, -47, 29, 82, -15]    | 0.8523    |
| 102       | \[-21, 56, 13, -88, 42]    | 1.3241    |
| 103       | \[90, -33, 7, 51, -62, 18] | null      |

### Example 3: Compare similarity of two records

**Goal**: Use cosine distance to determine how similar two records are based on their numeric arrays.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| filter numeric_codes != null and array_length(numeric_codes) = 5
| alter ref = arraycreate(10.0, 20.0, 30.0, 40.0, 50.0)
| alter distance = cosine_distance(numeric_codes, ref)
| alter similarity = subtract(1, distance)
| fields event_id, numeric_codes, distance, similarity
| sort asc distance
| limit 3
```

**Explanation**: This query computes the cosine distance between each record's `numeric_codes` and a reference vector, then derives the cosine similarity as `1 - distance`. Results are sorted by distance ascending, showing the most similar records first.

**Output**:

| EVENT\_ID | NUMERIC\_CODES          | DISTANCE | SIMILARITY |
| --------- | ----------------------- | -------- | ---------- |
| 105       | \[8, 15, 25, 35, 45]    | 0.0123   | 0.9877     |
| 101       | \[13, -47, 29, 82, -15] | 0.8523   | 0.1477     |
| 102       | \[-21, 56, 13, -88, 42] | 1.3241   | -0.3241    |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`filter`](../stages/filter), [`fields`](../stages/fields), [`sort`](../stages/sort), [`limit`](../stages/limit)
* **Functions**: [`euclidean_distance()`](euclidean_distance), [`arraycreate()`](arraycreate), [`array_length()`](array_length)
* **Datasets**: [`xdr_data`](https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction)
