---
description: Reuse existing Cortex XSIAM playbooks or create playbooks for new workflows.
---

# Choose from existing playbooks or create your own

Open the Investigation & Response → **Automation** → **Playbooks** page to find an existing playbook, customize it, or create a playbook.

### Find an existing playbook in Cortex XSIAM

Playbooks in your Org Repository have already been adopted by your organization and are available to run. The Playbook Catalog contains all available playbooks in the Marketplace that you can adopt into your Org Repository. You can preview before adopting.

1.  View the list of playbooks on the main **Playbooks** page in the Org Repository table. You can also search for a playbook that exists in the Org Repository by clicking **Add Filter**.

    Use free text in the search box, entering part or all of the playbooks' names or descriptions. You can also search for an exact match of the playbook name by putting quotation marks around the search text. For example, searching for **`"Block Account - Generic",`** returns the playbook with that name.

    Search for more than one exact match by including the logical operator "or" in-between your search texts in quotation marks. For example, searching for **`"Block Account - Generic" or "NGFW Scan"`** returns the two playbooks with those names. Wildcards are not supported in free text search.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Tip</h3><p>If there are additional relevant playbooks in Marketplace that are not in your Org repository, you can click <strong>Explore them now</strong> to see them in the <strong>Playbook Catalog</strong> and choose to adopt.</p></div>
2. Click **Playbook Catalog** to browse all available playbooks in the Marketplace that you can adopt. Click **Playbook Library** to go back to the main **Playbooks** page.
   1. Click a playbook card for a preview of the playbook.
   2.  Click **Adopt this playbook** to add the playbook to your Org repository.

       A confirmation message displays when the playbook is successfully added.
   3. Click **View in Org Playbooks** to select the adopted playbook from the Org repository table.

You can use the playbook as-is or customize it as needed.

### Edit a playbook in Cortex XSIAM

From the list of playbooks in your Org repository, right-click the playbook you want to edit and select **Open in Editor**. Depending on your access level, you can also duplicate, share, change the owner, disable, download, or delete the playbook.

When you adopt a playbook, it is locked, and you can only make limited changes to the playbook settings from the **Playbook Starts** task.

When you adopt a playbook, tasks and sub-playbooks that require configuration appear with a red triangle and an exclamation mark, enabling you to locate and configure all necessary components.

{% hint style="info" %}
### Note

When a task inside a sub-playbook is not configured, the alert is propagated to the main playbook. If multiple sub-playbooks are nested, and any of the sub-playbooks have non-configured components, the alert appears in the main playbook as well as in the sub-playbooks. Alerts also appear for the individual non-configured tasks within the sub-playbooks.
{% endhint %}

To reduce visual noise, you can dismiss certain alerts for unnecessary non-configured components such as sub-playbooks, scripts, and commands. You can dismiss an alert only if leaving the component in its non-configured state will not lead to a playbook error. For example, if the task must execute for the playbook to proceed, you cannot dismiss the alert.

When you click on the red triangle, you have the option to **Dismiss Alert**. After an alert is dismissed, the triangle is grey. Clicking on the grey triangle gives you the option to **Mark as alert** and revert to the red triangle. Alerts can be dismissed in both system and custom playbooks, and you do not need to duplicate a system playbook to dismiss an alert.

For full editing capabilities, right-click and select **Open in Editor** or **Duplicate**, which creates a copy of the playbook to edit, for example, for a system playbook.

In the **Agentic Assistant** pane, start a conversation with the Automation Engineer agent to edit the playbook (preview), or you can manually configure the playbook settings or add AI prompts, scripts, sub-playbooks, or tasks from the **Task Library**.

{% hint style="info" %}
### Tip

* To open multiple playbooks at the same time, edit the first playbook and then click **New** next to the playbook name to create a new tab. You can either create a new playbook, or add an existing one.
* You can view recently modified or deleted playbooks by clicking version history for all playbooks ![versionhistory.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-695013593e8557789bffe0ad41eddd7c47d61ba0%2F3241a048e028b41e16e670e937251d1e832e98edeabd915cc389cb6163d20e20.png?alt=media).
{% endhint %}

### Create a playbook in Cortex XSIAM

1.  In the **Playbooks** page, click **Build New Playbook**.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>You must have the required permissions to create playbooks to view this button. For more information, see <a href="../access-to-playbooks">Manage access to playbooks and scripts</a>.</p></div>
2.  In the **Create new** pop up, enter a name, description, and tags for the playbook and click **Save**.

    A blank playbook opens in the playbook editor. You can then configure the playbook settings or add AI prompts, scripts, sub-playbooks, or tasks from the **Task Library**.
3. In the **Agentic Assistant** pane, start a conversation with the Automation Engineer agent to create the playbook (preview), or manually create it.

#### **Collapse and expand playbook sections**

You can easily navigate playbooks and focus on the parts you need to work on by collapsing and expanding playbook sections. Collapsing sections provides a condensed view of the playbook flow, reducing visual clutter and enabling quick access to specific sections. Expanding sections allows you to view or edit specific parts of a playbook while keeping the rest of the playbook compact and maintaining focus on the relevant playbook details. You can also hover over a section header to highlight all tasks under the section and easily identify the section scope.

To collapse and expand a section, on the **Playbooks** page, after selecting a playbook from the library or creating a new playbook and adding tasks, click <img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-d103249252c445e7d6e88778e574388ebb62170a%2F9599b0c5d30fadc690439560b37750d38e0427800682dfed934ffe7040e845b7.png?alt=media" alt="playbook-expand-collapse.png" data-size="line"> on a section header.

When you collapse a section, you can see the number of tasks included under the section. For example:

![playbook-collapsed-num-tasks.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-02e3bc20e4b35c7bb366db6a13f4a6e3b67b17bc%2Fbf8a781cf2e7cbf3953c5167e5fe21cb37436fdfab37d9dd4327b7d635f81e09.png?alt=media)

Click <img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-e85430f3083fd6cd482c6f70fc2878beb0e81f84%2F98406b9ac8baf6eb6d5615aed9a69b6f57a9e19a71ee566e2a91f4d56bce0d37.png?alt=media" alt="playbook-collpase-expand-all.png" data-size="line"> to collapse or expand the entire playbook.
