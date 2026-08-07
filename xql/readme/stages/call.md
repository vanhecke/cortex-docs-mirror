# call

Use the `call` stage to reference and execute a saved query from the Query Library as a sub-query within your current XQL query. This allows you to modularize complex logic, reuse common query patterns, and maintain cleaner query structures.

## Syntax

```sql
call <saved_query_name>
```

## Parameters

| Name               | Type   | Required | Description                                                                                                                                                                           |
| ------------------ | ------ | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `saved_query_name` | string | Yes      | The exact name of the saved query in the Query Library that you want to execute. If the name contains spaces, it must be enclosed in double quotes (for example, `"My Saved Query"`). |

## Returns

The `call` stage returns the dataset produced by the execution of the referenced saved query. The subsequent stages in your main query will process this returned dataset.

## Usage notes

* The `call` stage effectively replaces itself with the full XQL string of the saved query at execution time.
* It is best practice to use `call` at the beginning of your query pipeline to fetch a prepared dataset, though it can be used wherever a dataset transformation is valid, provided the saved query's output is compatible with the preceding stages.
* Recursive calls (a query calling itself) are not supported.
* Ensure the saved query you are calling exists in the Query Library and that you have permission to view it.
* If the saved query name changes, you must update the `call` statement in your queries to reflect the new name.

## Examples

### Example 1: Calling a saved query

**Goal**: Use a pre-defined saved query named "Failed Logins Last 24h" to start an investigation.

**XQL code**:

```sql
call "Failed Logins Last 24h"
| filter user_name != "admin"
| fields _time, user_name, src_ip
```

**Explanation**: The query first executes the saved query "Failed Logins Last 24h". The results of that query are then passed to the `filter` stage, which removes records where the user is "admin", and finally selects specific fields for display.

**Output**: The output depends entirely on the data returned by the saved query and the subsequent filter.

### Example 2: Reusing data preparation logic

**Goal**: Reuse a standardized data cleaning query named `clean_xdr_data` before performing a specific aggregation.

**XQL code**:

```sql
call clean_xdr_data
| comp count(event_id) by agent_os_type
```

**Explanation**: The `clean_xdr_data` saved query is executed first (likely filtering out noise and normalizing fields). The resulting "clean" dataset is then aggregated to count events by OS type.

**Output**:

| agent\_os\_type | count |
| --------------- | ----- |
| Windows         | 1500  |
| Linux           | 450   |
| macOS           | 200   |

## Related articles

* **Stages**: [`filter`](filter), [`fields`](fields), [`comp`](comp)
