# tag

Use the `tag` stage to augment your data by adding custom labels to records. These labels are appended to the `_tag` system field, making it easier to categorize and search for specific events later.

## Syntax

```sql
tag add <tag name>
tag add "<tag name1>", "<tag name2>", ...
```

## Parameters

| Name         | Type    | Required | Description                                                                                                    |
| ------------ | ------- | -------- | -------------------------------------------------------------------------------------------------------------- |
| `add`        | keyword | Yes      | The command operation to append a tag.                                                                         |
| `<tag name>` | string  | Yes      | The string value to be added as a tag. Must be enclosed in quotes if it contains spaces or special characters. |

## Returns

The `tag` stage returns the original records, enriched with the specified string values appended to the `_tag` system field.

## Usage notes

* The `tag` stage specifically modifies the `_tag` system field. Tags can only be applied to this field.
* While the `tag` stage itself is a straightforward operation, general XQL optimization principles should be applied to the query as a whole.
* Apply `filter` stages as early as possible in your query to reduce the dataset size before the `tag` stage processes the records.
* Utilize the `fields` stage immediately after initial filtering to select only the necessary columns. This minimizes the data footprint passed to `tag` and subsequent stages.
* Always use the smallest practical `timeframe` to limit data scanning.

## Examples

### Example 1: Adding a single tag to records

**Goal**: Adds "audit\_processed" to the `_tag` field for all records.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| fields event_id, event_description 
| tag add "audit_processed" 
| limit 3 
```

**Explanation**: The `tag add "audit_processed"` stage appends the string "audit\_processed" to the `_tag` system field for all records that pass through this stage.

**Output**:

| EVENT\_ID | EVENT\_DESCRIPTION               |
| --------- | -------------------------------- |
| 101       | "User login successful"          |
| 102       | "File access attempt"            |
| 103       | "Network connection established" |

### Example 2: Adding a list of tags to records

**Goal**: Adds "security\_incident" and "review\_needed" to `_tag` for unsuccessful events.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| filter is_successful = false 
| fields event_id, event_description, is_successful 
| tag add "security_incident", "review_needed" 
| limit 3
```

**Explanation**: The `filter is_successful = false` stage first narrows down the dataset to only unsuccessful events. The `tag add "security_incident", "review_needed"` stage then applies both specified tags to the `_tag` system field of these filtered records.

**Output**:

| EVENT\_ID | EVENT\_DESCRIPTION             | IS\_SUCCESSFUL |
| --------- | ------------------------------ | -------------- |
| 102       | "File access attempt"          | false          |
| 106       | "Unauthorized access detected" | false          |
| 109       | "API request throttled"        | false          |

## Related articles

* **Stages**: [`config`](config), [`filter`](filter), [`fields`](fields), [`limit`](limit)
