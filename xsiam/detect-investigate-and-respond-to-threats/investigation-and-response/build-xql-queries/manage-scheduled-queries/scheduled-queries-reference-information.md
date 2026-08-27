---
description: Review scheduled query settings, statuses, and run details in Cortex XSIAM .
---

# Scheduled Queries reference information

The table below lists the common fields in the **Scheduled Queries** page in Cortex XSIAM.

{% hint style="info" %}
### Note

Certain fields are exposed and hidden by default. An asterisk (\*) is beside every field that is exposed by default.
{% endhint %}

<details>

<summary>Scheduled Queries table</summary>

<table><thead><tr><th width="191">Field</th><th>Description</th></tr></thead><tbody><tr><td><strong>BQL</strong></td><td><p>Whether the query was created by the native search.</p><p>Native search has been deprecated, this field allows you to view data for queries performed before deprecation.</p></td></tr><tr><td><strong>ISSUED BY</strong></td><td>User who ran or scheduled the query.</td></tr><tr><td><strong>MITRE ATT&#x26;CK TACTIC</strong></td><td>MITRE ATT&#x26;CK tactics tagged in the scheduled query.</td></tr><tr><td><strong>MITRE ATT&#x26;CK TECHNIQUE</strong></td><td>MITRE ATT&#x26;CK techniques tagged in the scheduled query.</td></tr><tr><td><strong>NEXT EXECUTION</strong></td><td><ul><li><p>For queries that are scheduled to run at a specific frequency, this displays the next execution time.</p><p>For queries that were scheduled to run at a specific time and date, this field will show <code>None</code>.</p></li></ul></td></tr><tr><td><strong>PUBLIC API</strong></td><td>Whether the source executing the query was an XQL query API.</td></tr><tr><td><strong>QUERY DESCRIPTION</strong></td><td>Query parameters used to run the query.</td></tr><tr><td><strong>QUERY ID</strong></td><td>Unique identifier of the query.</td></tr><tr><td><strong>QUERY NAME</strong></td><td><ul><li>For saved queries, the <strong>Query Name</strong> identifies the query specified by the administrator.</li><li>For scheduled queries, the <strong>Query Name</strong> identifies the auto-generated name of the parent query. Scheduled queries also display an icon to the left of the name to indicate that the query is recurring.</li></ul><p><img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-cb59db61a6da9c065c6cfff3da30e8b457ea687c%2F945b06800080b0f23d1db8b6508b8c13212c7d35d2621d503499d3a563ea073c.png?alt=media" alt="query-scheduled.png" data-size="original"></p></td></tr><tr><td><strong>QUERY SYNTAX</strong></td><td>The exact syntax used to write the query.</td></tr><tr><td><strong>SCHEDULE TIME</strong></td><td>Frequency or time at which the query was scheduled to run.</td></tr><tr><td><strong>XQL</strong></td><td>Whether the query was created by XQL search.</td></tr></tbody></table>

</details>
