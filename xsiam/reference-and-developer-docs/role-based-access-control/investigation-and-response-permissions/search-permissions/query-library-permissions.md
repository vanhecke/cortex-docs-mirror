# Query Library permissions

Controls access to the Query Library, which is a repository of saved XQL queries within Cortex XSIAM. It allows users to save, organize, share, and reuse XQL queries across the team. Key capabilities include:

* Browse, search, and filter saved queries by name, labels, and type
* Save new queries from XQL Search results
* Share queries with specific users or make them public

Users can primarily access Query Library from **Investigation & Response** → **Search** → **XQL Search**, and select the **Query Library** tab.

{% hint style="info" %}
### Note

Users must have at least View permission in **Query Center** to access the **Query Library** from **Query Center**.

If you want to execute and schedule queries from the Query Library, you also need View/Edit permission in the **Query Center**.
{% endhint %}

Cortex XSIAM enforces least-privileged per-object access by allowing you to manage access for individual instances of Saved Queries. For more information, see [Manage access to objects.](../../../../../onboard-cortex-xsiam/post-deployment/manage-user-roles-and-access-management#UUID-ff05f1c8-e516-ea74-9dff-ea8b26692754)

| Permission | Description                                                                                                                                                                                                                                                                                                                                                                              | Roles Example                                       |
| ---------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------- |
| Enabled    | <p>Users can browse, search, filter, and view saved queries. Users can also save, edit, delete, and share their own queries. Users can also be granted:</p><ul><li><strong>Create Queries:</strong> Users can edit, delete, and share queries.</li><li><strong>Edit Public Queries</strong>: Adds the ability to edit and delete public/shared queries created by other users.</li></ul> | Most roles require creating/editing public queries. |
| Disabled   | No access to the **Query Library**.                                                                                                                                                                                                                                                                                                                                                      |                                                     |

**Required and recommended permissions**

| Permission     | Permission Level  | Reason                                                                                                                                                                                                                           |
| -------------- | ----------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Query Center   | View or View/Edit | <ul><li>View: The XQL Search page (where the Query Library lives) requires this permission. Without it, users cannot access the page. Required.</li><li>View/Edit. Required if users want to run and schedule queries.</li></ul> |
| Dataset Access | N/a               | Required. Queries reference specific datasets. Without dataset access, queries will return errors or empty results.                                                                                                              |
| Dashboards     | Enabled           | Strongly recommended for users to take a query from the Library and instantly turn it into a Dashboard widget for persistent monitoring.                                                                                         |
| Reports        | Enabled           | Recommended for users who need to link a Library query to a scheduled report (e.g., a weekly "Top 10 Blocked IPs" report).                                                                                                       |
