# sla\_time\_remaining

Use the `sla_time_remaining()` function to return the duration left, in seconds, until an SLA breach occurs. The function abstracts the complex time-tracking logic for active, paused, and completed SLAs, including time spent paused, so that you can query, filter, and sort cases by real-time SLA status.

## Syntax

```sql
sla_time_remaining (<sla_timer_field>)
```

## Parameters

| Name              | Type | Required | Description                                                                                                         |
| ----------------- | ---- | -------- | ------------------------------------------------------------------------------------------------------------------- |
| `sla_timer_field` | JSON | Yes      | An SLA field exposed in the `cases` dataset, such as `resolution_sla`, or a user-defined SLA under `custom_fields`. |

## Returns

The `sla_time_remaining()` function returns an integer representing the number of seconds remaining until the SLA breaches:

* A **positive** value indicates the SLA is still within its goal (time remaining before breach).
* A **negative** value indicates the SLA has breached (time elapsed past the goal).
* **NULL** is returned when the SLA has no active or completed timing information.

The remaining time is the SLA goal minus the time the SLA has been active, and any time the SLA was paused is not counted against it.

## Usage notes

* Time spent paused does not count against the SLA, so a case that is paused does not continue to lose remaining time.
* For an SLA that is still running, the remaining time reflects the elapsed time up to now; for a completed SLA, it reflects the total time it took to resolve.
* The function can be used in the `filter` ,  `sort`,  and `comp` stages, and supports arithmetic and comparison operators (`<`, `>`, `<=`, `>=`, `=`) for building "at risk" and "breached" views.
* Because the return value is a numeric duration in seconds, it is compatible with statistical functions such as `percentile()`, `median()`, `avg()`, `min()`, and `max()`.
* The function is available to XQL widgets in dashboards and reports, and can be executed through PAPI (for example, `POST /public_api/v1/xql/get_query_results/`).

## Examples

### Example 1: Display remaining time for the resolution SLA

**Goal**: Show, for each case, how much time remains before the resolution SLA breaches.

**XQL code**:

```sql
dataset = cases // Query the cases dataset
| alter time_left = sla_time_remaining(resolution_sla) // Seconds until breach (negative if breached)
| fields case_id, status, resolution_sla, time_left
| limit 5
```

**Explanation**: For each case, `sla_time_remaining()` inspects the `resolution_sla` timer, computes the net elapsed time (excluding pauses), and subtracts it from the SLA goal. A running case with a 2-hour goal that has been active for 1.5 hours (with no pauses) returns `1800` seconds; a case that has already exceeded its goal returns a negative value.

**Output**:

| CASE\_ID | STATUS       | RESOLUTION\_SLA                                 | TIME\_LEFT |
| -------- | ------------ | ----------------------------------------------- | ---------- |
| 23339    | in\_progress | {"goal":"02:00:00","status":"within\_sla", ...} | 1800       |
| 23340    | in\_progress | {"goal":"01:00:00","status":"within\_sla", ...} | 600        |
| 23341    | in\_progress | {"goal":"01:00:00","status":"breached", ...}    | -1200      |
| 23342    | resolved     | {"goal":"02:00:00","status":"within\_sla", ...} | 3600       |
| 23343    | in\_progress | {"goal":"04:00:00","status":"within\_sla", ...} | 5400       |

### Example 2: Find cases breaching within the hour

**Goal**: Surface all cases whose resolution SLA will breach in less than one hour (3600 seconds) but has not yet breached.

**XQL code**:

```sql
dataset = cases
| alter time_left = sla_time_remaining(resolution_sla)
| filter time_left > 0 and time_left < 3600 // Positive but under one hour
| fields case_id, severity, time_left
| sort asc time_left // Most urgent first
```

**Explanation**: The `filter` stage keeps only cases with a positive remaining time (not yet breached) under 3600 seconds. Sorting ascending by `time_left` places the most at-risk cases at the top. This is the query behind a typical "Cases at Risk" widget.

**Output**:

| CASE\_ID | SEVERITY | TIME\_LEFT |
| -------- | -------- | ---------- |
| 23341    | critical | 300        |
| 23350    | high     | 900        |
| 23348    | medium   | 2400       |
| 23345    | low      | 3300       |

### Example 3: Rank cases by urgency using sort

**Goal**: Build a prioritized queue by sorting all open cases by the time remaining on their resolution SLA, with the most overdue cases first.

**XQL code**:

```sql
dataset = cases
| filter status = "in_progress"
| alter time_left = sla_time_remaining(resolution_sla)
| sort asc time_left // Most negative (most overdue) at the top
| fields case_id, assignee, time_left
| limit 5
```

**Explanation**: Because breached cases return negative values, sorting ascending brings the most overdue cases to the top of the list, followed by those closest to breaching. This lets analysts triage work directly from real-time SLA state.

**Output**:

| CASE\_ID | ASSIGNEE | TIME\_LEFT |
| -------- | -------- | ---------- |
| 23341    | alice    | -4200      |
| 23360    | bob      | -600       |
| 23350    | alice    | 900        |
| 23345    | carol    | 3300       |
| 23343    | bob      | 5400       |

### Example 4: Aggregate SLA headroom with statistical functions

**Goal**: Report the average and median remaining time across all in-progress cases, grouped by severity, to understand SLA pressure per tier.

**XQL code**:

```sql
dataset = cases
| filter status = "in_progress"
| alter time_left = sla_time_remaining(resolution_sla)
| comp avg(time_left) as avg_remaining, median(time_left) as median_remaining by severity
| sort asc median_remaining
```

**Explanation**: The `sla_time_remaining()` output is a numeric duration, so it flows directly into aggregation functions. Negative group averages indicate a severity tier that is, on average, past SLA and requires immediate attention.

**Output**:

| SEVERITY | AVG\_REMAINING | MEDIAN\_REMAINING |
| -------- | -------------- | ----------------- |
| critical | -1500          | -900              |
| high     | 1200           | 800               |
| medium   | 5400           | 4800              |
| low      | 12600          | 11000             |

## Related articles

* **Functions**: [`is_sla_breached`](is_sla_breached)
* **Stages**: [`alter`](file:///8951409/Cortex_XQL_Command_Reference/Stages/alter.md), [`filter`](file:///8951409/Cortex_XQL_Command_Reference/Stages/filter.md), [`sort`](file:///8951409/Cortex_XQL_Command_Reference/Stages/sort.md), [`comp`](file:///8951409/Cortex_XQL_Command_Reference/Stages/comp.md), [`config`](file:///8951409/Cortex_XQL_Command_Reference/Stages/config.md)

