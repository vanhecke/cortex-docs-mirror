# Manage access to custom dashboards

Review the following:

* [Manage access to objects]()

The **Dashboard Manager** serves as the central repository for your visualizations. By using object-level access, you can ensure that custom (user-defined) dashboards, such as those used for sensitive executive reporting or specialized department views, are only accessible to authorized users and user groups. The permissions assigned to your role, combined with the ownership of specific objects, directly determine the content available to you; you can only access dashboards where you are the Owner, dashboards that have been explicitly shared with you (or your user group), or dashboards marked as **Public**.

{% hint style="warning" %}
### Prerequisite

*   **Configure tenant-level settings**: An administrator must first establish the sharing framework under **Settings** → **Configurations** → **Access Management** → **Objects**.

    The configuration of these settings defines the authorized sharing workflows for for all custom objects, including dashboards:

    * **Enable "Owners can Share objects they created"**: Grants owners the ability to share dashboards with specific users and user groups. In the **Dashboard Manager**, this enables the **Share** option.
    * **Disable "Owners can Share objects they created"**: Restricts owners to managing only **General access** (**Public** vs. **Restricted**). In the **Dashboard Manager**, this replaces the **Share** option with the **Manage Access** option.

    For more information on configuring tenant-level settings, see [Manage access to objects](#UUID-ff05f1c8-e516-ea74-9dff-ea8b26692754).
* **Define Scope-Based Access Control (SBAC)**: While object-level sharing grants access to the dashboard's layout and configuration, users must also have the appropriate SBAC permissions to view the actual data populated within the widgets. If a user has access to a shared dashboard but lacks the required data scope for the underlying datasets, the dashboard will load, but the widgets may appear empty or display an error. For more information on defining SBAC, see [Manage user scope](#UUID-071cdbb6-6c6a-6afe-3a67-1fa79991a0a8).
{% endhint %}

<details>

<summary>Understanding dashboard behavior</summary>

Because dashboards are composed of multiple visualization elements, it is important to understand how access is applied:

* **Dashboard vs. Widget access**: Access to a dashboard is managed through the **Dashboard Manager**. When you share a dashboard, you can also manage access for any **Custom Widgets** contained within it.
* **System Widgets**: Standard system widgets provided by Cortex XSIAM remain **Public** and accessible to all users by default; their access cannot be restricted.

</details>

<details>

<summary>Understanding widget behavior</summary>

Because dashboards are composed of multiple widgets, it is important to understand how access is applied to these individual components:

* **Widgets are not objects**: Unlike dashboards, individual widgets are not treated as independent objects. They do not have their own "Share" dialog and cannot be shared independently. Within the Widget Library, a widget is set to either **Restricted** (visible only to the creator) or **Public** (visible to all with Widget Library access).
* **Inherited access**: Any user who has been granted access to a custom dashboard (as a **Viewer** or **Editor**) can see all the widgets contained within that dashboard, including those marked as **Restricted**. This means you may see a widget on a shared dashboard that you cannot see in the Widget Library even if you have access to it.
  * **Dashboard Editors**: Can edit the dashboard layout, but the widget is only available in their Widget Library for editing when the widget is **Public**.
  * **Dashboard Viewers**: Can't make any changes to dashboards or widgets that are **Restricted**.

</details>

<details>

<summary>Change owner of a dashboard</summary>

To ensure continuity when personnel changes occur or to hand off management of a resource, only administrators can change the ownership of a custom dashboard.

{% hint style="info" %}
### Note

Only Account Admins and Instance Administrators have the authority to change the owner of an object.
{% endhint %}

1. Select **Dashboards & Reports** → **Dashboard Manager**.
2. Right-click the custom dashboard in the table and select **Change owner**.
3. Select the new owner from the list of users, and click **Change**.

</details>

<details>

<summary>How to configure access to custom dashboards</summary>

**Step 1: Set role-level permissions**

Role permissions define the functional capabilities for dashboards and the Widget Library, and determine what actions a user can take.

1. Select **Settings** → **Configurations** → **Access Management** → **Roles**.
2. Right-click the relevant user role, and select **Edit Role**.
3. Under **Components**, expand **Dashboards & Reports**, and locate **Dashboards**.
4. Configure access state:
   * **Disabled**: Users cannot navigate to **Dashboards & Reports** → **Dashboard Manager** or **Dashboards & Reports** → **Widget Library**. Dashboards cannot be shared with this role. If the user previously owned or had access to shared dashboards, they are no longer available.
   * **Enabled**: Allows dashboards to be accessed and managed according to defined sub-permissions. Grants access to the Widget Library as explained below in Manage the Widget Library.
5. If **Enabled**, assign specific capabilities to control the UI:
   * **Create Dashboards**: Enables the **New Dashboard** button on the **Dashboard Manager** page, allowing the user to create new custom dashboard objects. The user who performs this action becomes the **Owner** of the object and is granted the inherent right to edit, delete, and manage sharing for that specific object..
   * **Edit Public Dashboards**: Allows the user to modify custom dashboards set to **Public**, even if they are not the owner.
6. Click **Save**.

**Step 2: Manage the widget library**

The Widget Library is the central repository for predefined and custom widgets and is intended for browsing and selecting widgets to add to a dashboard. Access to and visibility within the Widget Library is determined by role-level permissions and your specific access level to the dashboards where those widgets reside:

* **Access to the Widget Library**: To access the Widget Library, your role must have the **Create Dashboards** or **Edit Public Dashboards** capability. Users who only have "View" permissions for dashboards cannot access the Widget Library.
*   **Widget Library visibility**: Visibility within the Widget library depends on ownership and inherited dashboard and widget permissions:

    * **Public and personal widgets**: You can always see widgets you created (**Restricted**) and widgets marked as **Public**.
    * **Inherited access via dashboards**: If a **Restricted** widget was created by another user but is part of a dashboard shared with you, you won't see it in the Widget Library and it can't be edited (unless you are an administrator).

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>If you're designated as an <strong>Editor</strong>, you can always duplicate the widget and make your changes on the copy.</p></div>

**Step 3: Manage sharing for a custom dashboard**

Once a custom dashboard exists in the Dashboard Manager, the Owner (or an authorized Editor) defines who can see or edit it.

1. Select **Dashboards & Reports** → **Dashboard Manager**.
2. Locate the custom dashboard that you want to share in the table.
3. Right-click the custom dashboard and select the available access option. The menu option you see depends on your tenant-level settings:
   * **Share**: Use this if your admin enabled sharing. It allows you to grant access to specific users/groups and change the **General access** (**Public**/**Restricted**).
   * **Manage Access**: Use this if sharing is disabled. It is a restricted view that only allows you to toggle the **General access** between **Public** and **Restricted**. You cannot grant access to specific individuals.
4. (If sharing is enabled) Search for the **User** or **User Group**, and assign the access level: **Viewer** (read-only) or **Editor** (can modify and share).
5. Set the **General access** state:
   * **Restricted**: Private to the Owner and the others granted access.
   * **Public**: Visible to all users with the **Dashboard** component enabled in their role.
6. Click **Save**.

</details>

<details>

<summary>Sharing icons in the Dashboard Manager</summary>

The following icons help you identify the security access of your custom dashboards:

* ![unshared-query-icon.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-6359b4205fea8606544d7b4c7c5687156ace7e55%2F3bcfc5837fbfdc660f71afb2044f1a9863658c916bb5e51a44a0360bb8a1f58f.png?alt=media): A **Restricted** custom dashboard you created that is not shared with anyone else.
* ![query-created-by-me-shared-icon.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-4c2484efc33cdb3c32f1c42d33c301ce206a1e9e%2F9a5baddd6cb6e2f25bea9d1a3316e5d0a2feaecbbb032f0a38bb8812eb225b90.png?alt=media): A custom dashboard you created that is currently shared with other users or user groups.
* ![query-created-by-someone-else-shared.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-211db7c1c72ee56b7a8668d8d4bfcc9d4cad3075%2F40a7a4506d71374ee5a2c460682f0a337be1215996c770332177b219bb5d6f84.png?alt=media): A custom dashboard created by another user that has been shared with you.
* ![PANW\_Query.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-ab9cbf4664bc7ca78d8ad14b6930c1971098f501%2F166b1287c043c7d155758b65cc6295d55aab36df8c01e9f42ae5ea8f06bce5ab.png?alt=media): A standard system dashboard provided by Palo Alto Networks. These are always **Public** and cannot be deleted or edited, and their ownership cannot be transferred. Yet, you can **Duplicate** a system dashboard to create a custom version that you can then modify and share.

</details>
