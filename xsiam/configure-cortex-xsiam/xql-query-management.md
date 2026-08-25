---
description: >-
  Configure Cortex XSIAM XQL query limits, timeouts, and visibility controls to
  protect tenant performance and query privacy.
---

# XQL query management

You can find **Query Management** options under **Settings** → **Configurations** → **General** → **Query Management**. These options enable administrators to set controls on running queries.

### Set query limits in Cortex XSIAM

{% hint style="warning" %}
Setting query limits requires **View/Edit** permissions for **Configurations** → **Query Management**.
{% endhint %}

Administrators can set query limits that control user-generated XQL queries within a tenant. Setting query limits helps to prevent resource strain and optimize tenant performance. You can control the following query settings:

*   **Concurrent queries per user**

    Prevent system overload by setting a maximum number of concurrent queries that a user can run.

    The concurrent query limit is applied per user.

    If a user is running a high number of queries and is approaching the concurrent query limit, a system message warns that a high query load is impacting their performance. If a user exceeds the defined limit of concurrent queries, new queries are blocked until the number of active queries drops below the limit.

    The user can view all of their In Progress queries from the Query Center, and cancel active queries to avoid being blocked and improve query performance. For more information, see [Overview of the Query Center](../detect-investigate-and-respond-to-threats/investigation-and-response/build-xql-queries/overview-of-the-query-center).

    If a user is blocked, other users of the tenant can continue to run queries. By default, query limits apply to all users of the tenant, but you can exclude specific roles and groups from these limits.

    Queries that are included in the concurrent queries calculation include:

    * Cortex Query Language (XQL) investigation queries, including cold and hot storage, XDM templates, XDR templates, free text search, and queries from the query library.
    *   Scheduled queries and scheduled reports.

        <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>A scheduled query or report is run on behalf of the user that created it, even if it is edited and run by another user.</p></div>
    * XQL widget queries in dashboards and reports
    * XQL public API queries (cold and hot storage)
    * BIOC test queries.
    * Correlation rule test queries.
    * XQL queries run from playbook tasks.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><ul><li>Queries run by correlation rules are not restricted by the query limit.</li><li>Very short queries do not count towards concurrent queries.</li></ul></div>
*   **Query duration timeout**

    Prevent long-running queries by setting a timeout duration for queries to automatically stop long-running queries and reserve tenant resources.

    Only integer values are supported for this field. In addition, the query timeout is an approximate value.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>To ensure optimal system performance, all queries (user-generated and otherwise) adhere to a default timeout limit of 60 minutes that is defined by Palo Alto and takes priority over the administrator-defined value. Therefore, regardless of the value specified in this field, queries will be stopped after 60 minutes.</p><p>You can override the default timeout limit by including the <code>config max_runtime_minutes</code> stage in your query to increase the query timeout value, up to the administrator-defined value.</p></div>

### Set a query limit

1. Go to **Settings** → **Configurations** → **General** → **Query Management**.
2. Under **Query Limits** select **Enabled**.
3.  Under **Concurrent Queries Per User**, specify the maximum number of queries a user is allowed to run concurrently. Queries exceeding this limit will be blocked.

    Important considerations:

    * A value of 0 will prevent all queries from running.
    * Setting a very low or very high limit could adversely affect overall query execution speed and system resources.
4.  Under **Query Timeout,** specify the maximum duration (in minutes) that any query can run.

    By default, the query duration timeout is set to 60 minutes for all queries regardless of the value specified in this field. For more information, see the explanation above regarding **Query timeout duration**.
5. Under **Excluded User Groups or Roles**, choose specific user groups or roles that should be excluded from the query limits.
6. Click **Save**.
7. Changes to the query limit settings are recorded in the **Management Audit Logs**.

### Restrict query visibility in Cortex XSIAM

Administrators can restrict non-admin users and API keys to viewing and managing only their own query history, which enhances tenant privacy and reduces operational noise. By limiting access to users' own search activities, you can secure sensitive investigations and ensure that API usage adheres to strict visibility controls.

The following areas in the **Query Builder** are affected when you restrict query visibility:

* **Query History** tab: Users and API keys see an access only the queries they initiated. Queries which are run implicitly on their behalf, such as background reports, BIOCs, or dashboards, are hidden from this view to reduce noise and maintain focus.
* **Active Queries** tab: Users and API keys view and manage any query they initiated, regardless of the source, including dashboards and widgets, allowing them to cancel operations they triggered.
* **Scheduled Queries** tab: Users see only the queries they personally scheduled.

#### **Query restriction use cases**

Restricting the access of users and APIs to only their own queries addresses specific operational and security needs:

* Reduce operational noise: Restricting visibility to only user-initiated **Investigation** or **Simple Search** sources in **Query History** makes the view more relevant to the analyst's immediate workflow.
* Prevent insider threat visibility: When investigating another user within the same tenant, restricting visibility prevents the individual being examined from seeing queries about themselves. Enabling this restriction protects the integrity of internal investigations.
* Secure API keys: Restricting API key access to their own queries prevents users from retrieving results using execution ID guessing. This aligns API privacy standards with the User Interface.

{% hint style="info" %}
Query visibility is subject to Role-Based Access Control (RBAC); users can't see queries for datasets they do not have permission to access.
{% endhint %}

### Enable query visibility restrictions in Cortex XSIAM

1. Go to **Settings** → **Configurations** → **General** → **Query Management**.
2. Under **Enforce query privacy for non-admins**,
   * Enable: Non-admin users can only see and manage their own query activity.
   * Disable: Non-admin users can view all queries in the tenant.
3. Click **Save**.

Changes to the query visibility settings are recorded in the **Management Audit Logs**.
