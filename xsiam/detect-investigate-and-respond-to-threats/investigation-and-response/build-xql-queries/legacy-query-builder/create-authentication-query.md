# Create authentication query

From the Query Builder, you can investigate authentication activity across all ingested authentication logs and data.

Some examples of authentication queries you can run include:

* Authentication logs by severity
* Authentication logs by the event message
* Authentication logs for a specific source IP address

### How to build an authentication query

1. From Cortex XSIAM, select **Investigation & Response** → **Search** → **Query Builder**.
2. Select **AUTHENTICATION**.
3.  Enter the search criteria for the authentication query.

    By default, Cortex XSIAM will return the activity that matches all the criteria you specify. To exclude a value, toggle the **`=`** option to **`=!`**.
4.  Choose when to run the query.

    Select the calendar icon to schedule a query to run on or before a specific date or Run to run the query immediately and view the results in the Query Center.

    While the query is running, you can always navigate away from the page and a notification is sent when the query completes. You can also **Cancel** the query or run a new query, where you have the option to **Run only new query (cancel previous)** or **Run both queries**.
5. When you are ready, view the results of the query. For more information, see [Review XQL query results](../how-to-build-xql-queries/review-xql-query-results).
