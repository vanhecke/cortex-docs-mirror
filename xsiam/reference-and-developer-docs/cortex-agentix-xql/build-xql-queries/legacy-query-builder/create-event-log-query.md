---
description: Create legacy event log queries in Cortex XSIAM.
---

# Create event log query

From the **Query Builder** you can search Windows and Linux event log attributes and investigate event logs across endpoints with a Cortex XDR agent installed.

Some examples of event log queries you can run include:

* Critical level messages on specific endpoints.
* Message descriptions with specific keywords on specific endpoints.

### How to build an event log query

1. From Cortex XSIAM , select **Investigation & Response** → **Search** → **Query Builder**.
2. Select **EVENT LOG**.
3.  Enter the search criteria for your Windows or Linux event log query.

    Define any event attributes for which you want to search. By default, Cortex XSIAM will return the events that match the attribute you specify. To exclude an attribute value, toggle the **`=`** option to **`=!`**. Attributes are:

    * **PROVIDER NAME**: The provider of the event log.
    * **USERNAME**: The username associated with the event.
    * **EVENT ID**: The unique ID of the event.
    * **LEVEL**: The event severity level.
    * **MESSAGE**: The description of the event.

    To specify an additional exception (match this value except), click the **+** to the right of the value and specify the exception value.
4.  (_Optional_) Limit the scope to an endpoint or endpoint attributes:

    Specify one or more of the following attributes: Use a pipe (**|**) to separate multiple values.

    Use an asterisk (**\***) to match any string of characters.

    * **HOST**: **HOST NAME**, **HOST IP** address, **HOST OS**, **HOST MAC ADDRESS**, or **INSTALLATION TYPE**.
    * **INSTALLATION TYPE** can be either Cortex XDR agent or Data Collector.
    * **PROCESS**: **NAME**, **PATH**, **CMD**, **MD5**, **SHA256**, **USER NAME**, **SIGNATURE**, or **PID**.
5.  Specify the time period for which you want to search for events.

    Options are **Last 24H** (hours), **Last 7D** (days), **Last 1M** (month), or select a **Custom** time period.
6.  Choose when to run the query.

    Select the calendar icon to schedule a query to run on or before a specific date or **Run** to run the query immediately and view the results in the **Query Center**.

    While the query is running, you can always navigate away from the page, and a notification is sent when the query completes. You can also **Cancel** the query or run a new query, where you have the option to **Run only new query (cancel previous)** or **Run both queries**.
7. When you are ready, view the results of the query. For more information, see [Review XQL query results](../how-to-build-xql-queries/review-xql-query-results).
