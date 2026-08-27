---
description: Explore Cortex XSIAM Query Builder template examples for common data queries.
---

# Query Builder template examples

The following examples can help familiarize you with running queries.

<details>

<summary>Use the Identity template to search for information about a specific user</summary>

**Goal**: Search for information about users working on the system.

This example uses the Identity template, but you can apply it to any of the templates. In the example, we run multiple queries that narrow down our search results and find the required information we require.

**Query 1: Search for information about all users**

1. Select Investigation & Response → Search → Query Builder.
2. Select the Identity template.
3.  Specify USER = \* and do not select Empty values.

    This searches for all users, and excludes empty values or strings from the results. The `USER` field is an alias so all associated fields are also searched.
4. Specify TIME → Last 7D.
5. Click Run.

In the Results page, scroll through the table to find a value or string that you want to investigate further. If you are not receiving results, you can broaden the TIME to Last 30D.

In this example, the results returned information about USER66 in the XDM.SOURCE.USER.USERNAME column. To refine the search for information about this user, run another query.

**Query 2: Search for information about a specific user**

1. Copy the term that you want to search, in this case USER66.
2.  Click Back to edit.

    The Identity template opens with the original search options.
3. Click Add field and select SOURCE.USER.USERNAME.
4. Specify SOURCE.USER.USERNAME = USER66 and do not select Empty values.
5. Click Run.

The Results page provides more information about USER66.

Look through the results for anything you would like to investigate further. In this example, there is information about the operations performed by this user in the XDM.EVENT.OPERATION column. We can refine the search to see all FILE\_REMOVE operations for USER66.

**Query 3: Search for FILE\_REMOVE operations for a specific user**

1. Click Back to edit.
2. Click Add field and select EVENT.OPERATION.
3. Specify EVENT.OPERATION = and select XDM\_CONST.OPERATION\_TYPE\_FILE\_REMOVE from the list.
4. Click Run.

Review the Results page and continue to refine your search by using this method.

</details>

<details>

<summary>Use the Network template to search for hosts triggering threat events in the United States</summary>

**Goal**: Search for information about source hosts in the United States that caused threat events over the last 7 days.

**Query 1: Search for network information in the United States**

1. Select Investigation & Response → Search → Query Builder.
2. Select the Network template.
3.  Specify COUNTRY = United States and do not select Empty values.

    This searches for network activity in the United States, and excludes empty values or strings from the results.
4. Specify TIME → Last 7D.
5. Click Run.

In the Results page, scroll through the table to find a value or string for which you would like to find more information.

In this example, the results returned information about XDM.EVENT.TYPE = threat for host DC3ENX4FGC07 in the XDM.SOURCE.HOST.HOSTNAME column. To refine the search, run another query.

**Query 2: Search for information about a specific host and event type**

1. Copy the term that you want to search, in this case DC3ENX4FGC07.
2.  Click Back to edit.

    The Network template opens with the original search options.
3. Click Add field and select EVENT.TYPE.
4. Specify EVENT.TYPE = threat and do not select Empty values.
5. Click Add field and select SOURCE.HOST.HOSTNAME.
6. Specify SOURCE.HOST.HOSTNAME = DC3ENX4FGC07 and do not select Empty values.
7. Click Run.

The Results page provides more information about EVENT.TYPE = threat actions from host DC3ENX4FGC07.

To investigate further, we could run another query, or in this case, investigate the causality chain of the event. In the search results, right-click and select Investigate Causality Chain.

</details>

<details>

<summary>Use the Free text template to search for an IP address</summary>

**Goal**: Search for information about IP address 175.18.7.29 in the last 24 hours.

1. Select Investigation & Response → Search → Query Builder.
2. Select the Free text template.
3. Specify Text Contains = 175.18.7.29.
4. Specify TIME → Last 24H.
5. Click Run.

In the Results page the searched string is highlighted. In the Fields column, you can see all of the fields in which the string was discovered. In the RAW\_DATA column, click Show more to see the specific row in the dataset in which the string was discovered.

If you want to deepen your search you can Continue in XQL, which opens an XQL search with the fields you defined in the template. You can add stages and functions to the XQL that narrow down your search.

</details>
