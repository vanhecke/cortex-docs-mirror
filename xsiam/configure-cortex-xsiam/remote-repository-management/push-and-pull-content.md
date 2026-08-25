---
description: >-
  Push and pull Cortex XSIAM content through a remote repository to synchronize
  playbooks, scripts, and integrations between development and production
  tenants.
---

# Push and pull content

Use a Cortex XSIAM remote repository to push and pull content between development and production tenants. Synchronize playbooks, scripts, automation logic, and integrations after testing them in a development environment.

<details>

<summary>Push Cortex XSIAM content from a development tenant</summary>

When developed content is ready for production, push the content update from the development tenant to the remote repository.

### Cortex XSIAM content push considerations

* **Push**
  * **Role-level requirements**: The ability to push playbooks and scripts to a remote repository is governed by a specific set of RBAC permissions. Your role must have **Scripts** and **Playbooks** enabled (under **Investigation & Response** → **Automations** with **Edit Public** selected for both) and **Cases and Issues** (under **Cases & Issues**) set to **View/Edit**.
  * **Push scope**: When a push is initiated, the system synchronizes all custom content, such as all playbooks and scripts, within the tenant to the remote repository.

{% hint style="info" %}
For more information, see [Manage access to playbooks and scripts](../../onboard-cortex-xsiam/post-deployment/manage-user-roles-and-access-management/manage-access-to-objects/manage-access-to-playbooks-and-scripts), including the Remote Repositories (Push/Pull) section.
{% endhint %}

* **Manual export**: Do not manually export content from the development tenant to import to the production tenant. Use only the procedures outlined in the documentation to ensure that your content is properly updated in the production tenant.
* **Version compatibility**: We do not recommend pushing content from a development tenant to a production tenant if they have different versions. This helps avoid compatibility conflicts, versioning errors, and unintended behavior in the production environment.

### Deploy content across different Cortex XSIAM versions

Separating development and production environments into deployment phases lets you test an upgrade version before production deployment. New features might not work in a pre-upgrade environment. Cortex XSIAM displays warnings, visual indicators, and collapsible release notes for incompatible items.

### Push content from a Cortex XSIAM development tenant

On each page you can decide whether to include or exclude items, which prevents them from being pushed to production, on a temporary or permanent basis. You can only exclude individual content items, not content packs.

1. In the development tenant, select **Settings** → **Configurations** → **Remote Repository Content** → **User-Defined Content**.
2. Under the Included for **Prod** tab, search for the items you want to push. The results are displayed in a table according to:

* **NAME**: The name of the content item.
* **TYPE**: The content type, for example playbook, script, issue layout, and issue field.
* **STATUS**: The date the content item was created.
* **MESSAGE**: Additional details about the content item that were added by the content owner.
* **BY**: The content item of the person who performed the commit for the change or creation of the content.

3. Select the items you want to push to production, and click **Push to Prod**.
4. If the items have dependencies, review the contents and click **Push**.\
   Sometimes you may not want to push all content, content pack dependencies, etc. For example, when a user makes a change in a playbook that includes a script dependency to which another user is adding a feature, and the change does not require the new feature (version) of the script, you can push the playbook without the new script.
5. In the dialog box, add an optional message and click **Push**. You can now pull the content into the production tenant as explained below.

</details>

<details>

<summary>Pull Cortex XSIAM content into a production tenant</summary>

After you push content from the development tenant, the production tenant displays **Remote Repository Content Available**. For content conflicts, choose whether to keep local content or replace it.

### Cortex XSIAM content pull considerations

When pulling content from a remote repository, Cortex XSIAM handles ownership differently depending on whether the content is new or already exists in the environment:

* **Existing playbooks and scripts**: If the playbook or script already exists in the target environment, the content is updated while the current ownership and access configurations remain unchanged.
* **New playbooks and scripts (access and ownership)**: New playbooks and scripts always arrive in a **Restricted** state, regardless of the access or sharing permissions they had in the development tenant. Ownership assignment depends on your Remote Repository Settings for access to new content as explained in the task below.

{% hint style="info" %}
In a production (pull) tenant, manual editing of synchronized content is blocked:

* Users cannot be granted **Editor** permissions.
* Any existing **Editor** permissions (set before the tenant was configured for remote repository synchronization) are effectively treated as **Viewer** access. These capabilities are removed from Cortex XSIAM and blocked by the system regardless of role-level permissions.
{% endhint %}

{% hint style="warning" %}
## PREREQUISITE

When pulling playbooks or scripts from a remote repository into a production tenant, you must define how ownership and access are assigned for the incoming object's new content.

1. Select **Settings** → **Configurations** → **General** → **Remote Repository Settings**.
2. Under **Access to new content**, choose how to assign ownership for pulled content:

* **Keep the original owner**: Select this when the user managing access is the same in both tenants. This user is designated as the **Owner** in the production tenant. Recommended option when the same users exist in both the pushing tenant and the pulling one.
* **Owner is the user pulling content into the production tenant (default)**: Select this when users pulling content should also manage their access. The user who manually triggers the pull action is designated as the **Owner**.
* **Assign new content to this user**: Select this when a specific user is responsible for managing access to new content. An administrator specifies a specific user as the **Owner** of all playbooks and scripts included in the pull.

3. Set the **General access** state:

* **Restricted**: Private to the new **Owner**.
* **Public**: Visible to all authorized users.
{% endhint %}

### Pull content into a Cortex XSIAM production tenant

1. If you click **Remote Repository Content Available** in the navigation bar, the **Content update available** window opens with a list of content available for installation, including content packs and content items.
2. Click **Check for new content** or **Install content**.
3. If conflicts appear, click Resolve conflicts.
4. In the **Action** column, select one of the following:

* **Skip**: Keeps the local content in your production environment.
* **Replace**: Deletes the local content and installs the content from the content repository.

5. Click **Continue** to install the content.

</details>
