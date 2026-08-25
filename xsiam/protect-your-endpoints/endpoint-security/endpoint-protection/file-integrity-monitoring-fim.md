---
description: >-
  Use Cortex XSIAM File Integrity Monitoring to detect changes to endpoint files
  and folders.
---

# File Integrity Monitoring (FIM)

File Integrity Monitoring (FIM) serves as a security control designed to detect unauthorized or anomalous modifications to files and folders in the file system. Any change, such as, a new file being created or an existing file being modified, will trigger an event that is sent to the Cortex Platform.

Cortex XDR agent integrates FIM capabilities directly into its endpoint detection and response engine, enhancing the fidelity and actionable intelligence derived from file events. This also allows seamless deployment of FIM capabilities over workstations and servers with the XDR agent installed.

File Integrity Monitoring requires a Cortex XDR agent with version 8.9.0 and above. FIM capabilities can be enabled on the following platforms and environments. See [Where can I install the Cortex XDR agent?](https://app.gitbook.com/s/fZ8QSMnkjnXpuOeuRcam/) for full platform options.

| Platform   | Available Implementation   |
| ---------- | -------------------------- |
| Windows    | Servers and workstations   |
| Linux      | User mode and Kernel mode  |
| Kubernetes | Containerized environments |

**Configuration and implementation**

FIM rules are used to define which files and folders should be monitored, and FIM rule groups are used to consolidate multiple FIM rules into a single entity.

Creating, modifying and viewing FIM rule groups and rules is be done in the Rule Groups page, located at the **Inventory** → **Endpoints** → **File Integrity Monitoring** menu.

First, create a rule group by choosing **+ New Group**. See [Add a new FIM rule group](#add-a-new-fim-rule-group).

After defining the general settings of the group, set up FIM rules in the Rules section by selecting **+ Add rule** with the following properties:

* Description: a brief description of the rule and its purpose
* Path: the path of the file or folder to monitor. See [File and Folder path configuration](#file-and-folder-path-configuration).
* Events To Monitor: type of events that should be monitored. **Any** will capture all events on the defined file path, **Specific events** allows the selection of specific event types as Delete, Create, Modify. When choosing Any, new types of events that may be added in the future will also be monitored.

Once created, a FIM rule group must be assigned to a specific File Integrity Monitoring extension profile. See [Apply File Integrity Monitoring profiles to your endpoint policies](#apply-file-integrity-monitoring-profiles-to-your-endpoint-policies).

{% hint style="info" %}
It is recommended to create a policy that targets only the necessary files and folders.
{% endhint %}

<details>

<summary>Add a new FIM rule group</summary>

### Add a new FIM rule group

Create a new FIM rule group, then set up FIM rules in the Rules section by selecting **+ Add rule**

1. In **Endpoints** → **File Integrity Monitoring** → **Rule groups**, select **+New Group**.
2. Fill in the **General Settings**.
   * Assign a profile **Name**
   * Add a brief **Description** to describe the rule group and its purpose.
3.  Select the **Platform**.

    * For Linux, define the monitoring mode: **Host** or **Containers**

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>Platform cannot be changed once a rule group has been created</p></div>
4. For each rule, add an optional description and the required path. See [File and Folder path configuration](#file-and-folder-path-configuration).
5. Specify the events to monitor.
   * **Any** will capture all events on the defined file path. New types of events that may be added in the future will also be monitored.
   * **Specific events** allow the selection of the event types: Delete, Create, Modify.

{% hint style="info" %}
### Note

A rule group can contain up to 100 rules.
{% endhint %}

</details>

<details>

<summary>Add a new FIM rule group profile</summary>

1. In **Inventory** → **Endpoints** → **Policy management** → **Extensions** → **Profiles**, select **+Add Profile** and then select either **Create New** or **Import from File**.
2. Select a **Platform** and click **File Integrity Monitoring** → **Next**.
3.  Fill in the **General Information**.

    Assign the profile **Name** and add an optional **Description**.
4. Select the **Platform**. For Linux, define the monitoring mode, **Host** or **Containers**
5.  In FIM Rule Group Select **+Manage Group**.

    Select the required FIM Rule Groups.
6. To save the FIM rule group definitions, click **Create**.
7. It is allowed to add up to ten rule groups to a profile.

</details>

<details>

<summary>Apply File Integrity Monitoring profiles to your endpoint policies</summary>

### Apply File Integrity Monitoring profiles to your endpoint policies

After you define the required File Integrity Monitoring profiles, configure policies with File Integrity Monitoring and enforce them on your endpoints. Cortex XSIAM applies File Integrity Monitoring policies on endpoints from beginning to end, as you’ve ordered them on the page. The first policy that matches the endpoint is applied. If no policies match, the default policy that enables all devices is applied.

1.  In **Inventory** → **Endpoints** → **Policy management** → **Extensions** → **Policy Rules**, select **+ New Policy** or **Import from File**.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>When importing a policy, select whether to enable the associated policy targets. Rules within the imported policy are managed as follows:</p><ul><li>New rules are added to the top of the list.</li><li>Default rules override the default rule in the target tenant.</li><li>Rules without a defined target are disabled until the target is specified.</li></ul></div>
2. Configure settings for the File Integrity Monitoring policy.
   1. Assign a policy name and select the platform. You can add a description.
   2. Assign the File Integrity Monitoring profile you want to use in this rule.
   3. Click **Next**.
   4.  Select the target endpoints on which to enforce the policy.

       Use filters or manual endpoint selection to define the exact target endpoints of the policy rules. If exists, the **Group Name** is filtered according to the groups within your defined user scope.
   5. Click **Done**.
3.  Configure policy hierarchy.

    Drag the policies in the desired order of execution. The default policy that enables all devices on all endpoints is always the last one on the page and is applied to endpoints that don’t match the criteria in the other policies.
4.  **Save** the policy hierarchy.

    After the policy is saved and applied to the agents, Cortex XSIAM enforces the File Integrity Monitoring policies on your environment.
5.  (Optional) Manage your policy rules.

    In the **Prevention Policy Rules** table, you can view and edit the policy you created and the policy hierarchy.

    1. View your policy hierarchy.
    2. Right-click to **View Policy Details**, **Edit**, **Save as New**, **Disable**, and **Delete**.
    3. Select one or more policies, right-click and select **Export Policies**. You can choose to include the associated **Policy Targets**, **Global Exceptions**, and endpoint groups.

</details>

### File and Folder path configuration

| Platform | Path restrictions                                                                                                                                                                                                                                                                                       |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Windows  | <ul><li>Must start with a valid root (e.g., C:\ or *&#x3C;/li></li><li>Has at least one valid segment or wildcard (asterisk) after each slash</li><li>Cannot end in a bare slash unless followed by a filename or wildcard (asterisk)</li><li>Cannot contain invalid characters: &#x3C; > : "</li></ul> |
| Linux    | <ul><li>Must start with a valid root (/)</li><li>Rules used to monitor folders must end with a forward slash (/)</li><li>Wildcard (asterisk) is supported by regex, but only at the last element of the path (basename)</li><li>Cannot contain invalid characters: &#x3C; > : "</li></ul>               |

<details>

<summary>View File Integrity Monitoring events</summary>

After you apply File Integrity Monitoring rules in your environment, use the **Inventory** → **Endpoints** → **File Integrity Monitoring** page to monitor events. The most recent events are displayed on the page. You can sort the results and use the filters menu to narrow down the results.

Use XQL to view all FIM events by querying the ‘xdr\_dataset’ with the filter ‘fim\_event = TRUE’.

{% hint style="info" %}
### Note

It is possible to ingest up to 15,000 events per day (24 hours) for each host/container.
{% endhint %}

</details>
