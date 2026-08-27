---
description: Save and manage personal XQL queries in the Query Library in Cortex XSIAM.
---

# Manage your personal query library

Cortex XSIAM provides a Query Library for saving and managing your custom Cortex Query Language (XQL) queries. When creating a query in XQL or managing your queries from the Query Center, you can save them in the Query Library.

The Query Library contains a powerful search mechanism that enables you to search in any field related to the query, such as the query name, description, creator, query text, and labels. In addition, adding a label to your query enables you to search for these queries using these labels in the Query Library.

## How to add a query to your personal query library

1.  Save a query to your personal query library.

    You can do this in two ways:

    * **From the Query Builder**
      1. Select **Investigation & Response** → **Search** → **Query Builder** → **XQL**.
      2. In the XQL query field, define the parameters of your query.
      3. Select **Save as** → **Query to Library**.
    * **From the Query Center**
      1. Select **Investigation & Response** → **Search** → **Query Center**.
      2. Locate the query that you want to save to your personal query library.
      3. Right-click anywhere in the query row, and select **Save query to library**.
2. Set these parameters.
   * **Query Name**: Specify a unique name for the query. Query names must be unique in both private and shared lists, which includes other people’s queries.
   * **Query Description** (Optional): Specify a descriptive name for your query.
   * **Labels** (Optional): Specify a label that is associated with your query. You can select a label from the list of predefined labels or add your label and then select **Create Label**. Adding a label to your query enables you to search for queries using this label in the Query Library.
   * **Share with others**: You can either set the query to be private and only accessible by you (default) or move the toggle to **Share with others** the query, so that other users using the same tenant can access the query in their Query Library.
3.  Click **Save**.

    A notification appears confirming that the query was saved successfully to the library, and closes on its own after a few seconds.

    The query that you added is now listed as the first entry in the **Query Library**. The query editor is opened to the right of the query.
4.  Other available options.

    As needed, you can return to your queries in the **Query Library** to manage your queries. Here are the actions available to you.

    * Edit the name, description, labels, and parameters of your query by selecting the query from the **Query Library**, hovering over the line in the query editor that you want to edit, and selecting the edit icon to edit the text.
    * **Search query data and metadata**: Use the Query Library’s powerful search mechanism that enables you to search in any field related to the query, such as the query name, description, creator, query text, and label. The **Search query data and metadata** field is available at the top of your list of queries in the **Query Library**.
    * **Show**: Filter the list of queries from the **Show** menu. You can filter by the **Palo Alto Networks** queries provided with Cortex XSIAM , filter by the queries **Created by Me**, or filter by the queries **Created by Others**. To view the entire list, **Select all** (default).
    * **Save as new**: Duplicate the query and save it as a new query. This action is available from the query menu by selecting the 3 vertical dots.
    * **Share with others**: If your query is currently unshared, you can share with other users on the same tenant your query, which will be available in their Query Library. This action is only available from the query menu by selecting the 3 vertical dots when your query is unshared.
    * **Unshare**: If your query is currently shared with other users, you can **Unshare** the query and remove it from their Query Library. This action is only available from the query menu by selecting the 3 vertical dots when your query is shared with others. You can only **Unshare** a query that you created. If another user created the query, this option is disabled in the query menu.
    * **Delete** the query. You can only delete queries that you created. If another user created the query, this option is disabled in the query menu when selecting the 3 vertical dots.

## Managing your queries

{% hint style="info" %}
The ability to create, edit, or share queries is governed by access management. If certain options are unavailable, contact your administrator.
{% endhint %}

The visibility of saved queries in the Query Library is determined by access management. You can manage who can view (and run) or edit your queries by sharing them with specific users, user groups, or API keys. You can also view queries created and shared by others in your organization if they have granted you access or marked the query as Public.

The following icons in the Query Library table help you identify the sharing status of each query:

* [![unshared-query-icon.png](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABcAAAAXCAYAAADgKtSgAAAACXBIWXMAAA7EAAAOxAGVKw4bAAAAB3RJTUUH5QgDCzkZziIOJQAAAUBJREFUSInVlTGKg0AYhZ9LKtHOKl2aaXMCIYXtHEMPYJFWtPEOHkAPEHIAexWxywUCYiCFEpgQne0W3MRxdiVFHoj4j+/j583PjMI553iTvt4Ffjt8JfPT5XLB8XhEWZa43W4ghIBSCkKI0KfIZB6GIU6n06imqiqCIIBhGJO+2ViapkFVVWCMjZ7r9Yo0TYXe2Vjqusb9fgfnHIqijN6Px2MZnHMOxtjLtb7vl8GHYZiEL+58u91OwjebjdArNef7/f5pQy3LgmmaQp/UKAKA4zgoiuLnO8uyWY9U523bouu6Ue18Ps/6hJ23bYskSRBF0ct1Sils28Z6vf4bPM9z+L4/26Gu63BdF5RSOfjhcIDv+0Lob1FK4XnePHy32z1lLKM4jkeH2csNncpQJE3ToGnaqCY9iv/R595Enwv/BlOuqr+6JOVrAAAAAElFTkSuQmCC)](https://docs-cortex.paloaltonetworks.com/viewer/attachment/5CAbsl8idaK8R43ZLhoTOw/f7a4Lzck6Z9zARbRGMcZhg-5CAbsl8idaK8R43ZLhoTOw): Identifies Restricted queries you created that have not been shared.
* [![query-created-by-me-shared-icon.png](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABYAAAAaCAYAAACzdqxAAAAACXBIWXMAAA7EAAAOxAGVKw4bAAAAB3RJTUUH5QgDDAAXIlG4HQAAAZdJREFUSIntlDGu2kAURc+PItEYFsACDDVjCYkCuUYjFjANnenZAILaBS2mBi8AL8ANosFUNNAz9JiGAk2KKET+DuaL6CtRlFtZV/OOnt+7M2/GGMMn6MtnQP+DM/r67IDWmtlsRhzHpGmKEALP8xBCFNa9PUuF53lst9uMVy6Xmc/nVKvVh3WFo9Ba56AAaZoSRVFhx4Xg0+lUWPwy+Hf0Z8BFm7dt+3UwwHA4zHlSSlzXBSAIAhzHIQiCzJmncYPvkatUKgwGg1zEHMcBwLIs4jj+eMdpmlKv1/F9PwNNkoRut4tt21iWhVIqW2ge6Hw+m+l0aoQQZr/fG2OM6fV6RghhWq2WabfbZr1ePyo3v7zSSZIwGo3QWgM/F7Xb7QC4Xq+sVqvCP82NYrlc0u/371CAw+EAQK1WA6BUKtFsNgnDEIDj8ZgD55bnui6Xy4X3nu/7GS8MQyaTCQC3241Op8N4PH4MVkrdO3wPV0rRaDQy/o9UAGw2m/t3bsaLxSIHLZKUkiiKkFJm/A/l+BX9Y4/QXwn+BnCE1HNKdF0yAAAAAElFTkSuQmCC)](https://docs-cortex.paloaltonetworks.com/viewer/attachment/5CAbsl8idaK8R43ZLhoTOw/4qElFF4j3NLHQpO7JrH8Ew-5CAbsl8idaK8R43ZLhoTOw): Identifies queries you created that are currently shared with others.
* [![query-created-by-someone-else-shared.png](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABYAAAAZCAYAAAA14t7uAAAACXBIWXMAAA7EAAAOxAGVKw4bAAAAB3RJTUUH5QgDDAIR+QR/qgAAAYlJREFUSIntlbGK6kAUhj8v06RIYxGwFoKNjaVNAhY2voC+hg8gvoC906sPkFpIZSMyRZqg1gopUjhCmgFvdYNhs4kuu8XC/bt/OHz8czhzpvF4PB78gP78BPQ/+JeDxauFSZIQxzFZltFsNul0Oti2/Wn9S4mzLEMpRZZlAKRpShzHX0scBAHX6xWA0WhEv9/nfD6TJEkOr1Kj7OVJKZFS5t62bVarFY7jsNvt8uTD4fBTcGkrgiAoeK01YRgihMCyrMqkleB/LXjW/X4veMdx3gfXybIsut3u++BWq/XhzHVdjDHcbjeEEAhRPaml4Ol0WvCe5+H7PlEUYYxBa812u+VyubwH9n2fXq+X+8lkAhRHzBhDFEXs93uMMfVgrTVSSk6nU34mpeRwOOB5Hu12u9CGNE1RSn0AF+Y4DEPm8zla69Lr+b7PbDZDCIFSKq8TQjAYDMrB6/WaxWJRCnyW67osl8vKPQFPrXgFCnA8HtlsNrV1eeLn3VCn8Xhcm7h0V3yHft8P8hcQorCDKWfaqAAAAABJRU5ErkJggg==)](https://docs-cortex.paloaltonetworks.com/viewer/attachment/5CAbsl8idaK8R43ZLhoTOw/PNLef2oK69hU97ui74E~Tw-5CAbsl8idaK8R43ZLhoTOw): Identifies queries created by another user that have been shared with you.
* [![PANW\_Query.png](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABMAAAATCAYAAAByUDbMAAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAAAJcEhZcwAADsMAAA7DAcdvqGQAAAINSURBVDhP5ZS/a1pRFMe/sf6YBHVxdFADPhUVUWgG/wQXF4OB2MEODukg6WA6dEghFWwMzVTzByQOjRAFB4dGmrROQjo4KCmkUH9kEjcVb9850UdNpVAIWfqByzv3vHu+95x7D3fFYrEIPBCq2fdBeBwxrVaL3MEBnE7nzAO43W7kj46g1+tnnkWWntlcKBAIYDgc4lk8DpPJhPeHh9DpdPh+fY1EIoHBYDCLuOOJwWB4PbMZFsrlEAgGeU7BkpydfXUVVquVfUajEa1WC+12m+dzFsokoXf7+4oQ8ePmBi+3t/FmdxeTyYR9b/f2UKlU4PV6oVar2cdQmTTsdrsolcui1++L/u0tj3q9Lnw+n5AkSXw6P+d/yWSS10fX10Wn2xVnpZKQM2afInZSKPDiudjniwshHzgPsn8Xim1siJ+djrJpQY4lv1LmyfExRqMR281mE8/lAybo9mw2G17t7KBcLuPp2hoymYxS3ng8xsfTU7aVzGhEIhFRLBaFw+EQHo9HfJXL7PZ6YjMev8soFlvIiGwqdx6/tDWoDT7k87QRptMpXmxtYUWlQjabhUaj4TWUUSqVwpfLS54TS5s2KN8mCREqWSQcDiMajSpCdKv3hYg/+oyg/ul1uwiFQqjVakin06hWq3C5XDCbzUuFiL++Gn6/H41Gg0sl6NAdkoRvV1c8v8///gT9O8AvPKILVGBwO6gAAAAASUVORK5CYII=)](https://docs-cortex.paloaltonetworks.com/viewer/attachment/5CAbsl8idaK8R43ZLhoTOw/TsBEI51xraLpM_J8Yn0ExQ-5CAbsl8idaK8R43ZLhoTOw): Identifies out-of-the-box (OOTB) system queries provided by Palo Alto Networks.

Use the following tools and the vertical ellipsis (⋮) menu to manage your saved queries:

* **Search and filter**: Use the search field to find queries by metadata or content. Use the Show menu to filter by Owned by Me, Owned by Others, or Palo Alto Networks.
* Save as new: Duplicate a query using the vertical ellipsis (⋮) menu.
* Share/Manage Access: Once a query is saved to the library, the Owner (or an authorized Editor) can manage who else can interact with it using the vertical ellipsis (⋮) menu. The specific option available (Share or Manage Access) is determined by tenant-level settings.
* Change owner: Administrators can use the vertical ellipsis (⋮) menu to change the query owner to a different user.
* Delete: You can only delete queries that you own. Palo Alto Networks system queries cannot be deleted.

## Manage access to saved queries

Once a query is saved to the library, the Owner (or an authorized Editor) can manage who else can interact with it. The options available depend on the tenant-level settings configured by your administrator.

1. In the Query Library tab, locate the query you want to share in the table.
2. Click the three-dot vertical ellipsis (⋮) and select the available action:
   * Share: This option appears when Owners can Share objects they created is enabled in tenant-level settings. It allows you to manage both General access and specific principals (users, user groups, and API keys).
   * Manage Access: This option appears when Owners can Share objects they created is disabled in tenant-level settings. It only allows you to change the General access state.
3. (If sharing is enabled) To share with specific entities:
   * Search for the User, User Group, or API Key.
   * Assign the access level: Viewer (can run/view) or Editor (can modify and, if permitted by tenant-level settings, share).
4.  Set the General access drop-down menu (if authorized by tenant-level settings):

    * Restricted: The query is private. It is only visible to the Owner and the specific principals added to the list.
    * Public: The query is visible to every user who has the Query Library enabled in their role.

    When the tenant-level setting Owners and editors can change the general access is unselected, the drop-down is disabled, and only an administrator can configure this option.
5. Click Save.
