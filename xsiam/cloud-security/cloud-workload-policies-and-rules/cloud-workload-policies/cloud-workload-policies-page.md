# Cloud Workload Policies page

The **Cloud Workload Policies** page allows users to manage policies that define security and compliance actions for cloud workloads. Users can create, edit, filter, and manage policies through a structured table and widget panel.

{% hint style="info" %}
### Note

Keep the following caveats in my mind when working with Policies:

* Instance Administrators are able to view all facets of policies without restrictions, even if Scope Based Access Control (SBAC) roles are in effect. Learn more about [SBAC](../../../onboard-cortex-xsiam/post-deployment/manage-user-roles-and-access-management/manage-user-scope).
* If you’ve been assigned a custom role with View/Edit permissions limited by SBAC, you may not be able to view certain policies.
* You can further narrow your search on the Inventory page by using SBAC to limit the scope of the finding, issue, and case counts.
{% endhint %}

The Cloud Workload Policies page displays all the configured policies with the following fields.

**Policy table columns**

<table data-header-hidden><thead><tr><th width="201.5"></th><th></th></tr></thead><tbody><tr><td><strong>Field</strong></td><td><strong>Description</strong></td></tr><tr><td><strong>Policy Type</strong></td><td>Defines the policy category: <strong>Misconfigurations, Secrets, Malware, Trusted Images</strong>.</td></tr><tr><td><strong>Policy Name</strong></td><td>The user-defined name of the policy.</td></tr><tr><td><strong>Action</strong></td><td>Defines the action taken when conditions match: <strong>Create an Issue</strong> (logs an issue) or <strong>Prevent and Create an Issue</strong> (prevents the action and logs an issue).</td></tr><tr><td><strong>Severity</strong></td><td>The severity level of the issue created: <strong>Critical, High, Medium, Low, or Informational</strong>.</td></tr><tr><td><strong>Asset Groups</strong></td><td>Predefined groups of assets to which the policy applies.</td></tr><tr><td><strong>Open Issues</strong></td><td>The number of unresolved issues associated with the policy.</td></tr><tr><td><strong>Conditions</strong></td><td>Define the detection rule by specifying the criteria that match relevant malware, secret, or trusted image findings.</td></tr><tr><td><strong>Exceptions</strong></td><td>Defines the exclusion criteria to omit malware, secret, or trusted image findings that meet specific conditions you want to exclude from the policy.</td></tr><tr><td><strong>Evaluation Stage</strong></td><td>Indicates at which stage in the <strong>SDLC</strong> the policy is evaluated.</td></tr><tr><td><strong>Description</strong></td><td>Additional details about the policy.</td></tr><tr><td><strong>Created By</strong></td><td>The user who created the policy.</td></tr><tr><td><strong>Last Modified</strong></td><td>The timestamp of the last modification.</td></tr></tbody></table>

### **Widgets panel**

The **Cloud Workload Policies** page includes a widget panel that provides a visual summary of policies:

* **Policies by Type:** Displays policies categorized as misconfiguration, secret, trusted images, or malware.
* **Policies by Evaluation Stage:** Shows the distribution of policies based on SDLC evaluation stages: Runtime, Deploy, or CI.

#### **Show or hide the widget panel**

The widget panel provides a visual summary of policies based on policy type or evaluation stage.

To hide the widget panel, do the following:

1. Navigate to **Posture Management** → **Rules & Policies** → **Policies** → **Cloud Workload**.
2. On the **Cloud Workload Policies** page, click the **Widget Panel** icon at the top of the page.
3. The panel toggles between visible and hidden states.

### **Change the layout of the policies table**

1. Navigate to **Posture Management** → **Rules & Policies** → **Policies** → **Cloud Workload**.
2. In the **Cloud Workload Policies** page, click the **More Options** icon (**⋮**).
3. In the **Layout** tab, do the following:
   * To remove columns, go to the **In View** section and search for a specific column. Click **-** next to the column to remove it from the table.
   * To reorder columns, go to the **In View** section. Click and drag columns up or down to rearrange the columns.
   * To add new columns, go to the **Add Columns** section. Click **+** next to the columns to include them in the table.
4. The table layout updates automatically based on your selections.

### **Policy details panel**

The policy details panel is displayed when you click a policy in the policy table. To view details of a cloud workload policy:

1. Navigate to **Posture Management** → **Rules & Policies** → **Policies** → **Cloud Workload**.
2. In the **Cloud Workload Policies** page, select the policy you want to check.

The policy panel displays the following details related to the selected policy:

* Policy details.
* Related rule settings.
* The number of issues opened as part of the policy. You can click on the link to navigate to the **Issues and Cases** section to check the issue details.

From the policy detail panel, you can:

* Enable or disable the policy
* Edit the policy
* Save as new
* Delete the policy
