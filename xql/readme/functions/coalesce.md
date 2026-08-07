# coalesce

Use the `coalesce()` function to return the first non-NULL value from a defined list of input fields or expressions.

## Syntax

```sql
coalesce (<field_1>, <field_2>, ...<field_n>)
```

## Parameters

| Name      | Type | Required | Description                                                                                   |
| --------- | ---- | -------- | --------------------------------------------------------------------------------------------- |
| `field_n` | Any  | Yes      | An arbitrary number of fields or expressions. The function evaluates them from left to right. |

## Returns

The `coalesce()` function returns a single value whose data type matches the first non-NULL argument it encounters. If all arguments are `NULL`, the function returns `NULL`.

## Usage notes

* Arguments are evaluated strictly from left to right. When a non-NULL value is found, the evaluation stops, and that value is returned.
* This function is valuable for ensuring data completeness and providing fall-back mechanisms, allowing you to define a prioritized list of data sources for a single field.

## Examples

### Example 1: Coalescing literal values of different types

**Goal**: Demonstrate the core "first non-NULL" behavior by providing various literal values, including NULLs, of different data types.

**XQL code**:

```sql
config timeframe = 1d // Sets the query timeframe 
| dataset = sample_xql_raw // Specifies the dataset to use 
| alter chosen_value_str = coalesce(NULL, "Fallback String", "Another Option") // First non-NULL string 
| alter chosen_value_int = coalesce(NULL, 123, NULL, 456) // First non-NULL integer 
| alter chosen_value_bool = coalesce(false, NULL, true) // First non-NULL boolean 
| fields event_id, chosen_value_str, chosen_value_int, chosen_value_bool 
| limit 3 
```

**Explanation**: For `chosen_value_str`, `coalesce()` skips `NULL` and returns "Fallback String". For `chosen_value_int`, it returns `123`. For `chosen_value_bool`, it returns `false`. This demonstrates the function's ability to handle various data types and select the first available non-NULL literal.

**Output**:

| EVENT\_ID | CHOSEN\_VALUE\_STR | CHOSEN\_VALUE\_INT | CHOSEN\_VALUE\_BOOL |
| --------- | ------------------ | ------------------ | ------------------- |
| 101       | Fallback String    | 123                | false               |
| 102       | Fallback String    | 123                | false               |
| 103       | Fallback String    | 123                | false               |

### Example 2: Coalescing existing fields

**Goal**: Use `coalesce()` with existing fields, specifically leveraging a field that can be NULL (`dst_domain`) and one that is always present (`event_description`) as a fallback.

**XQL code**:

```sql
config timeframe = 1d // Sets the query timeframe 
| dataset = sample_xql_raw // Specifies the dataset to use 
// dst_domain is NULL for event_id 105, event_description is always present 
| alter primary_or_fallback_description = coalesce(dst_domain, event_description) 
| fields event_id, dst_domain, event_description, primary_or_fallback_description 
| limit 5 
```

**Explanation**: For events where `dst_domain` is not `NULL` (for example, event 101-104), `coalesce()` returns the `dst_domain`. For event 105, where `dst_domain` is `NULL`, `coalesce()` falls back to `event_description`, providing "Data transformation".

**Output**:

| EVENT\_ID | DST\_DOMAIN       | EVENT\_DESCRIPTION             | PRIMARY\_OR\_FALLBACK\_DESCRIPTION |
| --------- | ----------------- | ------------------------------ | ---------------------------------- |
| 101       | ec2.amazonaws.com | User login successful          | ec2.amazonaws.com                  |
| 102       | sts.amazonaws.com | File access attempt            | sts.amazonaws.com                  |
| 103       | www.google.com    | Network connection established | www.google.com                     |
| 104       | dropbox.com       | System heartbeat               | dropbox.com                        |
| 105       | NULL              | Data transformation            | Data transformation                |

### Example 3: Coalescing multiple JSON paths for a single concept

**Goal**: Handle variations in JSON data where different keys might represent the same logical piece of information (for example, status code under `code` or `error`).

**XQL code**:

```sql
config timeframe = 1d // Sets the query timeframe 
| dataset = sample_xql_raw // Specifies the dataset to use 
// Extract 'code' or 'error' from JSON, using the first available 
| alter status_code = coalesce(simple_json_data -> code, simple_json_data -> error) 
| fields event_id, simple_json_data, status_code 
| limit 3 
```

**Explanation**: For event 101, `code` (200) is found first. For event 102, `code` is not present, so `error` ("access\_denied") is returned. For event 103, neither `code` nor `error_code` exists, resulting in `NULL`.

**Output**:

| EVENT\_ID | SIMPLE\_JSON\_DATA                                | STATUS\_CODE   |
| --------- | ------------------------------------------------- | -------------- |
| 101       | {"status": "ok", "code": 200}                     | 200            |
| 102       | {"status": "fail", "error": "access\_denied"}     | access\_denied |
| 103       | {"connection\_id": "CONN-001", "protocol": "TCP"} | NULL           |

### Example 4: Coalescing complex nested JSON paths for a unified identifier

**Goal**: Extract a "principal name" from multiple possible nested JSON paths within the `nested_json_data` field, such as `user.name`, `process.name`, `client.id`, or `db.name`.

**XQL code**:

```sql
config timeframe = 1d // Sets the query timeframe 
| dataset = sample_xql_raw // Specifies the dataset to use
| filter event_id in(101, 102, 108, 109, 110)
// Attempt to find a 'principal_name' from various nested JSON paths 
| alter principal_name = coalesce( 
    nested_json_data -> user.name, 
    nested_json_data -> process.name, 
    nested_json_data -> client.id, 
    nested_json_data -> db.name 
) 
| fields event_id, nested_json_data, principal_name 
| limit 5 
```

**Explanation**: For event 101, `user.name` ("Alice") is found first. For event 102, `user.name` is missing, but `process.name` ("cmd.exe") is present. For event 108, none of the specified paths exist, resulting in `NULL`. For event 109, `client.id` ("C2") is found. For event 110, `db.name` ("prod\_db") is found.

**Output**:

| EVENT\_ID | NESTED\_JSON\_DATA                                                                                  | PRINCIPAL\_NAME |
| --------- | --------------------------------------------------------------------------------------------------- | --------------- |
| 101       | {"user": {"id": "U1", "name": "Alice"}, "session": {"start": "10:00", "type": "web"\}}              | Alice           |
| 102       | {"process": {"name": "cmd.exe", "pid": 1234}, "target": {"path": "/var/log", "permission": "rwx"\}} | cmd.exe         |
| 108       | {"system":{"hostname":"webserver01","os":"Linux"},"patch":{"version":"1.2.3"\}}                     | NULL            |
| 109       | {"client":{"id":"C2","api\_key":"xyz"},"request":{"endpoint":"/data","rate":100\}}                  | C2              |
| 110       | {"db":{"name":"prod\_db","type":"SQL"},"storage":{"location":"S3","cost\_usd":15\}}                 | prod\_db        |

### Example 5: Selecting the first non-null username from multiple fields

**Goal**: Evaluate three different username fields (actor\_primary\_username, os\_actor\_primary\_username, and causality\_actor\_primary\_username) and return the first available (non-null) value to populate a single username column.

**XQL code**:

```sql
|dataset = sample_xql_raw
| fields actor_primary_username,
       os_actor_primary_username,
       causality_actor_primary_username 
| alter username = coalesce(actor_primary_username,
                          os_actor_primary_username,
                          causality_actor_primary_username) 
```

**Explanation**: The coalesce() function checks the provided arguments in order from left to right. The function returns the value of the first field that is not null. If actor\_primary\_username is null, it checks os\_actor\_primary\_username, and so on. This is a common technique for normalizing data when the same information might be stored in different fields depending on the event source.

**Output**:

| actor\_primary\_username | os\_actor\_primary\_username | causality\_actor\_primary\_username | username      |
| ------------------------ | ---------------------------- | ----------------------------------- | ------------- |
| null                     | "admin\_user"                | "system"                            | "admin\_user" |
| "jsmith"                 | "jsmith\_os"                 | null                                | "jsmith"      |
| null                     | null                         | "root"                              | "root"        |
| null                     | null                         | null                                | null          |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`config`](../stages/config), [`fields`](../stages/fields), [`limit`](../stages/limit), [`filter`](../stages/filter)
* **Functions**: [`if`](if)
* **Datasets**: [`xdr_data`](https://www.google.com/search?q=%5Bhttps://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction%5D\(https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction\))
