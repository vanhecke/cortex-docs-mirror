---
description: Use XQL macros to reuse query logic in Cortex XSIAM.
---

# XQL macros

XQL macros are reusable XQL code snippets stored in the Macro Library that enable modular query design. Unlike full saved queries which are complete and executable queries, macros are code fragments designed to be inserted into other queries at specific points in the pipeline. The macro pre-processor resolves all macro calls by performing text substitution before the query is compiled and executed.

A query is a complete piece of code that you wrote for a specific dataset which is kept in the library for future use. A macro is a series of functions or queries that are dataset-agnostic, and can be used instead of writing out a long query. Macros are used to simplify complex queries by breaking them down into smaller, reusable components.

## Syntax

```sql
call_macro "<macro_name>"
```

With parameters:

```sql
call_macro "<macro_name>" param1=value1, param2=value2
```

## Parameters

| Name         | Type      | Required | Description                                                                                                                                                                          |
| ------------ | --------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `macro_name` | string    | Yes      | The name of the macro as saved in the Macro Library. Must be enclosed in double quotes.                                                                                              |
| `param`      | key=value | No       | One or more parameters to pass to the macro. Parameters are substituted into the macro definition where `${param}` placeholders appear. Multiple parameters are separated by commas. |

## Returns

The `call_macro` statement is replaced by the macro's definition text after parameter substitution. The resulting expanded query is then compiled and executed as a single query.

## How macros work

The macro resolution process follows these steps:

1. The XQL pre-processor scans the query for `call_macro` statements.
2. For each `call_macro`, it retrieves the macro definition from the Macro Library.
3. Parameter values are substituted into `${param}` placeholders in the macro definition.
4. The macro call is replaced with the expanded text.
5. If the expanded text contains additional `call_macro` statements (nested macros), steps 2–4 repeat.
6. The fully expanded query is compiled and executed.

## Usage notes

* Macros support dynamic parameters using `${variable_name}` syntax in the macro definition.
* Macros can call other macros (nested macros). The pre-processor resolves all nested calls recursively. However, you can't create macros that reference each other in a circular chain. For example you can't have macro A that calls macro B, which in turn calls macro A.
* You can have 10 `call_macro` stages in a single query. Each query can have 3 nested macros. In total there can be 30 macros in a single query.
* A macro **cannot** call a full saved query. Use the `call` stage to execute full saved queries.
* A macro definition **cannot** begin with a `dataset` or `datamodel` statement. Macros are code fragments, not complete queries.
* There's no syntax validation for macros, so be careful when you build them.
* Macros are available in one-time queries, scheduled queries, widgets, dashboards, reports, and scheduled correlations.
* Macros are managed through the Macro Library with the same RBAC/SBAC access controls as saved queries.
* The Query History, Active Queries and Scheduled Queries views display the original query text with `call_macro` statements. The Query Builder displays the fully expanded (substituted) query.
* You can use macros across stages.
* You can use APIs to run a query that includes a macro, which will be expanded in runtime.

## Macros vs. saved queries

| Feature                           | Macros (`call_macro`)                    | Saved Queries (`call`)                |
| --------------------------------- | ---------------------------------------- | ------------------------------------- |
| Purpose                           | Reusable code snippets for modular logic | Complete, executable queries          |
| Position in pipeline              | Anywhere in the pipeline                 | Must be the starting point of a query |
| Execution                         | Text substitution before compilation     | Executes as a separate query call     |
| Can contain `dataset`/`datamodel` | No                                       | Yes                                   |
| Can call macros                   | Yes                                      | Yes                                   |
| Can call saved queries            | No                                       | Yes (via `call`)                      |
| Location in UI                    | Macro Library                            | Query Library                         |

## Macro display in different views

| View                 | Display behavior                                                                                                                                                         |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Query Builder Editor | Hover over a `call_macro` statement to see the macro definition in an inline overlay. Click to expand and replace the macro call with the literal code (undo supported). |
| Query History        | Shows the fully expanded query that was executed (all macros substituted).                                                                                               |
| Active Queries       | Shows the original query text with `call_macro` statements (pre-substitution).                                                                                           |
| Scheduled Queries    | Shows the original query text with `call_macro` statements (pre-substitution).                                                                                           |

## Examples

### Example 1: Basic macro usage

**Goal**: Use a macro to filter and select specific fields from network data.

Assume a macro named `network_filter` is saved in the Macro Library with the following definition:

```sql
filter action_country != "US" | fields agent_hostname, action_country, action_remote_ip
```

**XQL code**:

```sql
dataset = xdr_data
| call_macro "network_filter"
```

**Explanation**: The pre-processor replaces `call_macro "network_filter"` with the macro definition. The expanded query becomes:

```sql
dataset = xdr_data
| filter action_country != "US" | fields agent_hostname, action_country, action_remote_ip
```

**Output**:

| AGENT\_HOSTNAME | ACTION\_COUNTRY | ACTION\_REMOTE\_IP |
| --------------- | --------------- | ------------------ |
| server-01       | DE              | 203.0.113.5        |
| workstation-12  | JP              | 198.51.100.22      |

### Example 2: Macro with parameters

**Goal**: Use a macro with dynamic parameters to create a reusable field transformation.

Assume a macro named `classify_severity` is saved with the following definition:

```sql
alter severity_label = if(${field} < 3, "Low", if(${field} < 7, "Medium", "High"))
```

**XQL code**:

```sql
dataset = xdr_data
| call_macro "classify_severity" field=action_severity
| fields event_id, action_severity, severity_label
```

**Explanation**: The parameter `field` is substituted with `action_severity`. The expanded query becomes:

```sql
dataset = xdr_data
| alter severity_label = if(action_severity < 3, "Low", if(action_severity < 7, "Medium", "High"))
| fields event_id, action_severity, severity_label
```

**Output**:

| EVENT\_ID | ACTION\_SEVERITY | SEVERITY\_LABEL |
| --------- | ---------------- | --------------- |
| evt-001   | 2                | Low             |
| evt-002   | 5                | Medium          |
| evt-003   | 9                | High            |

### Example 3: Nested macros

**Goal**: Demonstrate a macro that calls another macro.

Assume two macros are saved:

Macro `extract_domain` definition:

```sql
alter domain = arrayindex(split(${field}, "@"), 1)
```

Macro `email_analysis` definition:

```sql
call_macro "extract_domain" field=${email_field}
| comp count() as email_count by domain
| sort desc email_count
```

**XQL code**:

```sql
dataset = xdr_data
| call_macro "email_analysis" email_field=sender_address
| limit 10
```

**Explanation**: The pre-processor first expands `email_analysis`, substituting `${email_field}` with `sender_address`. The intermediate result contains `call_macro "extract_domain" field=sender_address`, which is then expanded. The final query becomes:

```sql
dataset = xdr_data
| alter domain = arrayindex(split(sender_address, "@"), 1)
| comp count() as email_count by domain
| sort desc email_count
| limit 10
```

**Output**:

| DOMAIN       | EMAIL\_COUNT |
| ------------ | ------------ |
| example.com  | 1,245        |
| corp.net     | 892          |
| external.org | 456          |

### Example 4: Macro called from a saved query

**Goal**: Show how a saved full query can include macro calls.

Assume a saved query named `daily_threat_report` contains:

```sql
dataset = xdr_data
| filter event_type = ENUM.EVENT_TYPE.NETWORK
| call_macro "classify_severity" field=action_severity
| call_macro "network_filter"
| comp count() as threat_count by severity_label, action_country
| sort desc threat_count
```

**XQL code**:

```sql
call "daily_threat_report"
```

**Explanation**: The `call` stage executes the saved query. During execution, the pre-processor expands both `call_macro` statements within the saved query before compilation.

**Output**:

| SEVERITY\_LABEL | ACTION\_COUNTRY | THREAT\_COUNT |
| --------------- | --------------- | ------------- |
| High            | CN              | 342           |
| Medium          | RU              | 218           |
| Low             | DE              | 156           |

## Related articles

* **Stages**: The `call` stage, the `filter` stage, the `alter` stage, the `fields` stage
