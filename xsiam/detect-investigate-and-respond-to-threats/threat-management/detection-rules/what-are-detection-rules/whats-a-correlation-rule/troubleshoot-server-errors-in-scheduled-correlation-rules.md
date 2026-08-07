# Troubleshoot server errors in scheduled correlation rules

When you encounter any server errors in scheduled correlation rules, there are some steps you can perform to address the issues depending on the type of error. Follow the steps below to help troubleshoot the issue.

<details>

<summary>Errors related to the query</summary>

Error messages

```
 A server error occurred while running the query.
```

```
 This rule did not run because resources were exceeded during query execution.
```

Steps to perform

These errors indicate that the Cortex Query Language (XQL) query for the scheduled correlations rule is complex, broad, or exceeding resource limits. To fix the query, perform the following:

1. Run the query for the scheduled correlation rule in the Query Builder to identify syntax issues or logic errors introduced by any recent changes.
2. Review your query and decide which actions you can perform to fix the query:
   * Simplify the query by removing any fields that are not essential for the required results.
   * If the query covers an extended period, reduce the time frame.
   * If real-time correlation rules are supported and being used, consider converting your query to this mode.
   * When queries involve complex operations, such as `comp`, precede these with a `fields` stage to set only the necessary fields required to include in the query results.
   * Divide overly complex or data-heavy queries into multiple, simpler correlation rules.

</details>

<details>

<summary>Error related to the alert</summary>

Error message

```
A server error occurred while generating the alert.
```

Steps to perform

This error typically points to issues with the output alert configuration's complexity or content. Consider taking the following actions:

* Simplify the query output by excluding non-essential fields and any fields that may contain excessively large data.
* In some cases, the size of the query output can include fields that are too large to allow alerts to be generated successfully. To avoid this, we recommend setting boundaries that improve the chances of the correlation rule running successfully over time by performing the following:
  *   Limit the length of the calculated array fields by using the `arrayrange()` function. For more information, see [arrayrange](https://app.gitbook.com/s/fUtoMSNyY2P8jbK3cQsM/readme/functions/arrayrange).

      Example:Limits the length of the calculated `array_field` field to return only the first 1000 elements:

      ```
      arrayrange(array_field, 0, 1000)
      ```
  *   Limit the length of string fields set to an unlimited length using the `trim` function. For more information, see [ltrim](https://app.gitbook.com/s/fUtoMSNyY2P8jbK3cQsM/readme/functions/ltrim), [rtrim](https://app.gitbook.com/s/fUtoMSNyY2P8jbK3cQsM/readme/functions/rtrim), and [trim](https://app.gitbook.com/s/fUtoMSNyY2P8jbK3cQsM/readme/functions/trim).

      Example: Limits the length of the `string_field` field, which is set to an unlimited length, to return the first 1000 characters:

      ```
      rtrim(string_field, len(string_field) - 1000)
      ```
* Reduce the length and complexity of the **Alert Name**, **Description**, and any associated **Drill-Down Query**.
* Temporarily remove any mapped fields from the alert configuration.
* If present, verify the existence of the fields within the table. Temporarily remove suppression fields from the alert configuration.
* Use Static Severity: If dynamic severity is in use, switch to static.

</details>

<details>

<summary>When to contact support team</summary>

If the steps explained above don't resolve the issue, contact our support team and provide the following details:

* The exact error message received.
* The actions which led to the error.
* A list of the troubleshooting steps you've already attempted from the list provided above.

</details>
