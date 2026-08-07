---
description: >-
  Learn more about the Cortex XSIAM Graph Search Query Library to manage your
  queries.
---

# Manage the Graph Search Query Library

{% hint style="info" %}
### Notice

This feature is included with a Cortex XSIAM Premium license. It is also included with any other Cortex XSIAM license that has the Cloud Posture Security or Cloud Runtime Security add-on.
{% endhint %}

{% hint style="warning" %}
### Prerequisite

Graph Search requires **View** or **View/Edit** RBAC permissions for **Graph Search** under **Investigation & Response** → **Search**.
{% endhint %}

Cortex XSIAM provides as part of Graph Search a Query Library for saving and managing your own queries, queries shared with you, and built-in Graph Search queries provided by Palo Alto Networks to help illustrate how to build meaningful Graph Search queries on your data. When creating a query in Graph Search or managing your Graph Search queries from the Query Center, you can save queries to your personal query library as part of the Query Library. You can also decide whether the Graph Search query is shared with others (on the same tenant) in their Query Library or unshare it, so it is only visible to you. You can also view the Graph Search queries that are shared by others (on the same tenant) in your Query Library.

<details>

<summary>How to access the Query Library?</summary>

The Query Library is accessible from the **Graph Search** page. By default, it's open as a separate pane at the bottom of the page. Whenever the Query Library is closed, you can always click **Query Library** at the top right corner of the page to reopen it.

</details>

<details>

<summary>What does the Query Library include?</summary>

The Query Library consists of two tables called **Query Library** (default) and **My Recents**, which you can toggle. The **Query Library** table lists all the Graph Search queries available in your Query Library, while the **My Recents** table only lists the Graph Search queries that you've run from the **Graph Search** page, **Query Library** table, **My Recents** table, and Query Center.

The queries listed in your **Query Library** table have different icons to help you identify the different states of the queries:

* ![unshared-query-icon.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-6359b4205fea8606544d7b4c7c5687156ace7e55%2F3bcfc5837fbfdc660f71afb2044f1a9863658c916bb5e51a44a0360bb8a1f58f.png?alt=media)Created by me and unshared.
* ![query-created-by-me-shared-icon.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-4c2484efc33cdb3c32f1c42d33c301ce206a1e9e%2F9a5baddd6cb6e2f25bea9d1a3316e5d0a2feaecbbb032f0a38bb8812eb225b90.png?alt=media)Created by me and shared.
* ![query-created-by-someone-else-shared.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-211db7c1c72ee56b7a8668d8d4bfcc9d4cad3075%2F40a7a4506d71374ee5a2c460682f0a337be1215996c770332177b219bb5d6f84.png?alt=media)Created by someone else and shared.
* ![PANW\_Query.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-ab9cbf4664bc7ca78d8ad14b6930c1971098f501%2F166b1287c043c7d155758b65cc6295d55aab36df8c01e9f42ae5ea8f06bce5ab.png?alt=media)Created by Palo Alto Networks.

</details>

<details>

<summary>Adding queries to the Query Library</summary>

Graph Search queries can be added to the Query Library in multiple ways.

1.  Save a query to your personal query library.

    You can do this in following ways:

    * **From Graph Search in the Query Builder**
      1. Select **Investigation & Response** → **Search** → **Query Builder** → **Graph Search**.
      2. From inside the Graph Search query interface at the top of the **Graph Search** page, click **Select** to open the entity picker dialog box, and define the parameters of your query.
      3. Click **Search** to run your query and view the query results.
      4. Click **Save Query**.
    * **From Graph Search in the My Recents table of the Query Library**
      1. Select **Investigation & Response** → **Search** → **Query Builder** → **Graph Search**.
      2. Click **Query Library**.
      3. Toggle to **My Recents** to open your recent queries.
      4. Right-click anywhere in the Graph Search query row, and select **Save query to library**.
    * **From the Query Center**
      1. Select **Investigation & Response** → **Search** → **Query Center**.
      2. Locate the Graph Search query that you want to save to the Query Library.
      3. Right-click anywhere in the Graph Search query row, and select **Save query to library**.
2. Set these parameters:
   * **Query Name**: Specify a unique name for the Graph Search query. Query names must be unique in both private and shared lists, which includes other people’s queries.
   * **Query Description** (Optional): Specify a descriptive name for your Graph Search query.
   * **Labels** (Optional): Specify a label that is associated with your Graph Search query. You can add a label and then select **Create Label**, or select a label from the list, if any exist from a previous query. Adding a label to your Graph Search query enables you to search for queries using this label in the Query Library.
   * **Share with others**: You can either set the Graph Search query to be private and only accessible by you (default) or move the toggle to **Share with others** the query, so that other users using the same tenant can access the query in their Query Library.
3.  Click **Save**.

    A notification appears confirming that the query was saved successfully to the library, and closes on its own after a few seconds.

    The Graph Search query that you added is now listed as the first entry in the **Query Library**.

</details>

<details>

<summary>Managing Graph Search queries in the Query Library</summary>

As needed, you can return to your queries in the Query Library to manage your queries in both the **Query Library** and **My Recents** tables. Here are the actions available to you, where the options differ depending on the table and states of the query:

* Filter the list of queries using the filters displayed on the column headings of the table.
* **Run**: Run the Graph Search query from either the **Query Library** and **My Recents** tables. This pivot (right-click) option will close the Query Library to display the query results.
* **Save as new**: Duplicate the query and save it as a new query. This pivot (right-click) option is only available from the **Query Library** table for all queries.
* **Save query to library**: This pivot (right-click) option is only available from the **My Recents** table.
* **Share with others**: If your query is currently unshared, you can share with other users on the same tenant your query, which will be available in their Query Library. This pivot (right-click) option is only available from the query menu of the **Query Library** table when your query is unshared.
* **Unshare**: If your query is currently shared with other users, you can **Unshare** the query and remove it from their Query Library. This pivot (right-click) option is only available from the query menu of the **Query Library** table when your query is shared with others. You can only **Unshare** a query that you created. If another user created the query, this option is disabled in the query menu.
* **Remove** the query. You can only remove queries that you created. If another user created the query or for Palo Alto Networks, this pivot (right-click) option is disabled in the query menu.

</details>
