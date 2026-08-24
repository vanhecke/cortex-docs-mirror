---
description: >-
  Use knowledge sources to give Cortex XSIAM Agentic Assistant agents trusted
  business context.
---

# Manage knowledge sources (preview)

The **Knowledge Center** (preview) in the Agentic Assistant Hub enables AI agents to act as personalized extensions of your team instead of relying on general information, delivering more precise and grounded results during investigation and analysis.

{% hint style="info" %}
**Note:**

The **Knowledge Center** preview feature is not enabled by default. To request access, contact Cortex Product Management.
{% endhint %}

You can ground your agents with two kinds of knowledge sources:

* **Organizational-specific (custom) knowledge**: Internal documentation unique to your organization. For example:
  * Standard Operating Procedures (SOPs).
  * Corporate policy documents and cybersecurity frameworks.
  * Historical case context and analyst notes.
* **Cortex (system) knowledge**: Built-in product expertise provided by Palo Alto Networks. For example, intrinsic knowledge of Cortex security entities (cases, issues, findings, and assets).

**Transparency**

The platform ensures transparency for AI decision-making through the following mechanisms:

* Auditing: For full visibility, all knowledge source management activities, including uploads, deletions, and enable/disable sources and agent connections to those are logged in the management audit dataset. If knowledge is used, the name of the knowledge source is included in the audit log.
* Grounding visibility: The Agentic Assistant provides visibility into its grounding by including short source labels or citations within responses to indicate exactly which knowledge was applied.
* In the **Agents** tab, you can verify knowledge source connections for a specific agent by hovering over the agent card and clicking View. Hover over Knowledge sources to open a dropdown displaying all sources connected to that specific agent. DOCX sources can be previewed by download.

**Manage knowledge sources**

In the Knowledge Center, you can:

* Monitor capacity: The top right corner of the **Knowledge Center** displays your tenant's overall **Source limit** alongside a percentage indicator of your current storage usage, helping you track your available knowledge capacity. The **Learning sources** table also indicates the specific size and storage usage percentage of each individual source.
* Manage a source: You can right-click directly on a source in the table to view a **Preview** modal and inspect its text content, creation date, and author. You can also **Edit**, **Enable**/**Disable**, or **Remove** it. Disabled sources remain in the list but show a **Disabled** status.
* Check source status: Newly added sources appear in the **Knowledge Center** immediately but will display a **Learning** status while the system ingests and indexes the content. Once successfully indexed, the status changes to **Connected**. If an issue occurs, the status will show as **Error**.

{% hint style="info" %}
Note:

To manage knowledge sources, you must have view/edit permissions. For more information, see [Agentic Assistant role-based access control](../agentic-assistant-role-based-access-control).
{% endhint %}

**Add a knowledge source**

You can add a knowledge source by uploading a file, linking to external documents, or attaching system knowledge.

{% hint style="info" %}
**Tip:**

File formats can be MD, JSON, JSONL, CSV, DOC, or DOCX.

File size can be up to 5MB.
{% endhint %}

1. In the **Agentic Assistant Hub** > **Knowledge Center** tab, click **+ New Source**.
2.  Select a source type, **File** or **Link**.\
    **Upload a file**

    1. Drag and drop or browse to upload a supported text file.\
       The **Source name** is by default the file name. You can change it.
    2. In the **Shared agents** dropdown, select one or more agents.\
       You can also select all agents. Any later-created agents are included automatically.
    3. Click **Add source**.

    **Add a link**

    1. In the **Data source** dropdown, select an internal knowledge source, for example Atlassian Confluence Cloud or Google Drive.
    2. In the **Instance** dropdown, select the integration instance for the data source.
       * If you select Atlassian Confluence, enter the Page URL, the URL of the Confluence page to retrieve content from.
       * If you select Google Drive, enter the Google Drive file URL. The file must be shared with the logged in user’s email.\
         The **Source name** is by default the knowledge source you are linking to. You can change it.
    3. In the Shared agents dropdown, Select one or more (or all) agents to apply the knowledge source to. If you select all, any subsequently created agents will automatically be included.
    4. Toggle **Auto sync** to automatically sync with the knowledge source integration instance once every 24 hours.
    5. Click **Add source**.
