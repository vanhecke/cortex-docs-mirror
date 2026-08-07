---
description: >-
  Learn how to filter for empty values in the results table in Cortex Query
  Language.
---

# How to filter for empty values in the results table

When building a query, you can filter for empty values in the results table, which can include or exclude null or empty strings. In the query syntax, empty strings are represented as `""`, while null fields are represented as `null`.

*   Exclude null and empty strings using the following syntax:

    ```programlisting
    <name of field> != null and <field name> != ""
    ```
*   Include null or empty strings using the following syntax:

    ```programlisting
    <name of field> = null or <field name> = ""
    ```

**Example:**

Below is an example of filtering your endpoint data in the results table to exclude all null values and any empty strings for a user.

```programlisting
config timeframe = 90d
| dataset = endpoints
| filter endpoint_status in (CONNECTED, DISCONNECTED)
| filter user != null and user != ""
| fields user, group_names, endpoint_name
```
