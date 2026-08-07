# Manage access to saved queries

Review the following:

* [Manage access to objects]()

The Query Library serves as the central repository for your team's investigation logic. By using object-level access, you can ensure that specific Cortex Query Language (XQL) queries, such as those used for sensitive internal investigations or executive reporting, are only accessible to authorized users, user groups, and API keys.

{% hint style="warning" %}
### Prerequisite

**Configure tenant-level settings**: An administrator must first establish the sharing framework under **Settings** → **Configurations** → **Access Management** → **Objects**.

The configuration of these settings defines the authorized sharing workflows for saved queries in the Query Library, including the options that appear to users when clicking the three dot, vertical ellipsis (⋮) for a query in the Query Library:

* **Enable "Owners can Share objects they created"**: Grants owners the ability to share saved queries with specific users, user groups, and API keys to the query's access list. In the Query Library, this enables the **Share** option.
* **Disable "Owners can Share objects they created"**: Restricts owners to managing only **General access** (**Public** vs. **Restricted**). In the Query Library, this replaces the **Share** option with the **Manage Access** option.

For more information on these tenant-level configurations, see [Manage access to objects](#UUID-ff05f1c8-e516-ea74-9dff-ea8b26692754).
{% endhint %}

<details>

<summary>How access impacts the Query Builder</summary>

The permissions assigned to your role, combined with the ownership of specific objects, directly change the tools available to you while working in the Query Builder:

* **Restricted versus Public visibility**: Your Query Library view is personalized. You will only see queries where you are the Owner, queries that have been explicitly shared with you (or your user group or API key), or queries marked as **Public**.
* **Context-sensitive functionality**: The permissions assigned to your role, combined with the ownership of specific objects, directly change the tools available to you while working in the Query Builder and the Query Library. UI elements like the **Save as** menu or the **Share** action only appear if you have the required functional capabilities.

</details>

<details>

<summary>How to configure access to saved queries</summary>

Setting up access involves a two-part process: enabling the user interface (UI) elements in the role settings, and then defining the audience for individual saved query objects.

**Step 1: Define role capabilities**

Role-level permissions act as the "master switch" for Query Builder functionality and determine what actions a user can take.

1. Select **Settings** → **Configurations** → **Access Management** → **Roles**.
2. Right-click the relevant user role, and select **Edit Role**.
3. Under **Components**, expand **Investigation & Response**.
4. Ensure **Query Library** is set to **Enabled**.
5.  Define functional capabilities to control the UI:

    * **Create Queries**: Selecting this enables the **Save as** drop-down menu in the Query Builder. This allows users to select **Save as** → **Query to Library** or **Save as** → **Widget to Library**. The user who performs this action becomes the Owner of the object and is granted the inherent right to edit, delete, and manage sharing for that specific object..
    *   **Edit Public Queries**: This allows a user to modify queries marked as **Public** by others.

        <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>If the role of a user is set to <strong>Edit Public Queries</strong> but not <strong>Create Queries</strong>, they can update existing public queries, but the <strong>Save as</strong> drop-down menu will be hidden, preventing them from creating new Query Library entries.</p></div>

    Keep in mind the following:

    * If a custom query does not have an assigned **Owner**, an Administrator can use the **Change Owner** action to assign one.

**Step 2: Manage sharing for a specific query**

Once a query exists in the Query Library, the Owner (or an authorized Editor) can define who has permission to view (and run) or edit it.

1. Select **Investigation & Response** → **Search** → **Query Builder** → **XQL**.
2. Under the **Query Library** tab, locate the query that you want to share in the table.
3. Click the three dot, vertical ellipsis (⋮) and select the available action:
   * **Share**: This option appears when **Owners can Share objects they created** is enabled in tenant-level settings. It allows you to manage both **General access** and specific principals (users, user groups, and API keys).
   * **Manage Access**: This option appears when **Owners can Share objects they created** is disabled. It only allows you to change the **General access** state.
4. (If sharing is enabled) To share with specific entities (for **Restricted** queries):
   * Search for the User, User Group, or API Key.
   * Assign the access level: **Viewer** (can run/view) or **Editor** (can modify and, if permitted by tenant-level settings, share).
5.  Set the **General access** drop-down menu (if authorized by tenant-level settings):

    * **Restricted**: The query is private. It is only visible to the Owner and the specific principals added to the list.
    * **Public**: The query is visible to every user who has the Query Library enabled in their role.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>When the tenant-level setting <strong>Owners and editors can change the general access</strong> is unselected, the drop-down is disabled and only an administrator can configure this option.</p></div>
6. Click **Save**.

</details>

<details>

<summary>Sharing icons in the Query Library</summary>

The following icons in the Query Library table help you identify the security access of your queries:

* ![unshared-query-icon.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-6359b4205fea8606544d7b4c7c5687156ace7e55%2F3bcfc5837fbfdc660f71afb2044f1a9863658c916bb5e51a44a0360bb8a1f58f.png?alt=media): A **Restricted** query you created that is not shared with anyone else.
* ![query-created-by-me-shared-icon.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-4c2484efc33cdb3c32f1c42d33c301ce206a1e9e%2F9a5baddd6cb6e2f25bea9d1a3316e5d0a2feaecbbb032f0a38bb8812eb225b90.png?alt=media): A query you created that is currently shared with other users, user groups, or API keys.
* ![query-created-by-someone-else-shared.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-211db7c1c72ee56b7a8668d8d4bfcc9d4cad3075%2F40a7a4506d71374ee5a2c460682f0a337be1215996c770332177b219bb5d6f84.png?alt=media): A query created by another user that has been shared with you.
* ![PANW\_Query.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-ab9cbf4664bc7ca78d8ad14b6930c1971098f501%2F166b1287c043c7d155758b65cc6295d55aab36df8c01e9f42ae5ea8f06bce5ab.png?alt=media): A standard system query provided by Palo Alto Networks. These are always **Public** and can't be deleted, or have their ownership transferred.

</details>
