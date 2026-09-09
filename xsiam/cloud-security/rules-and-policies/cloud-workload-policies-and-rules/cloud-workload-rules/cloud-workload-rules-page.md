---
description: >-
  Use the Cortex XSIAM Cloud Workload Rules page to view, filter, and manage
  built-in and custom rules.
---

# Cloud Workload Rules page

The **Cloud Workload Rules** page allows users to manage rules. Users can create, edit, filter, and manage rules.

{% hint style="info" %}
### Note

Keep the following caveats in mind when working with Rules:

* Instance Administrators can view all facets of Rules without restrictions, even when Scope-Based Access Control (SBAC) roles are in effect.
* If you’ve been assigned a custom role with View/Edit permissions limited by SBAC, you may not be able to view specific Rules.
* You can further narrow your search in a Rules table by using SBAC to limit the scope of the findings, issues, and case counts.
{% endhint %}

The Widget section enables users to get 'at-a-glance' information based on **Platform**, **Rule type,** and **Scanner** type.

The Cloud Workload Rules page displays both the default rules and user-configured rules, with the following fields.

### **Rules table columns**

<table data-header-hidden><thead><tr><th width="198.5"></th><th></th></tr></thead><tbody><tr><td>Column Name</td><td>Description</td></tr><tr><td><strong>Rule ID</strong></td><td>A unique identifier assigned to each rule.</td></tr><tr><td><strong>Rule Name</strong></td><td>The name of the rule, typically defined by the user or system.</td></tr><tr><td><strong>Description</strong></td><td>A brief summary of the rule's purpose and functionality.</td></tr><tr><td><strong>Policies</strong></td><td>Lists the policies in which the rule is included.</td></tr><tr><td><strong>Controls</strong></td><td>Compliance controls associated with the rule for regulatory adherence.</td></tr><tr><td><strong>Platform</strong></td><td>Specifies the platform or environment the rule applies to. For example: <strong>Linux, Windows</strong> or <strong>Kubernetes</strong>.</td></tr><tr><td><strong>Scanner</strong></td><td>The tool or method used to evaluate findings, such as <em>Inventory Scanner</em>, <em>Agentless Disk Scan, Host Scanner, Kubernetes Connector or Kubernetes File System Scanner</em> .</td></tr><tr><td><strong>Severity</strong></td><td>Defines the severity of the rule.</td></tr><tr><td><strong>Data Type</strong></td><td>The type of data the rule evaluates. For example: <strong>Hosts</strong> or <strong>Kubernetes Resources</strong></td></tr><tr><td><strong>Created By</strong></td><td>The user who created the rule.</td></tr><tr><td><strong>Last Modified</strong></td><td>The date and time the rule was last updated.</td></tr><tr><td><strong>Rule Type</strong></td><td>Indicates whether the rule is a <strong>Built-in</strong> or <strong>Custom</strong> rule.</td></tr><tr><td><strong>Remediation</strong></td><td>Defines the remediation steps to address the detected misconfiguration.</td></tr><tr><td><strong>Applicable assets</strong></td><td>Supported applicable asset types.</td></tr><tr><td><strong>Available actions</strong></td><td>Indicates whether the available action is <strong>Prevent and Create an Issue</strong> or <strong>Create an Issue</strong></td></tr><tr><td><strong>Standards</strong></td><td>Associated compliance standards or controls</td></tr><tr><td><strong>Open issue</strong></td><td>No. of open issue related to this rule.</td></tr></tbody></table>

### **Filter page results**

You can use **Show filter Panel** button in the upper-right corner of the Rules page to filter the existing rules based on different filter criteria, as described below:

Table 6. Rule Filter table

<table data-header-hidden><thead><tr><th width="203"></th><th></th></tr></thead><tbody><tr><td>Filter</td><td>Allowed Values</td></tr><tr><td>Rule Name</td><td>Rule names and empty values</td></tr><tr><td>Description</td><td>Rule description and empty values</td></tr><tr><td>Policies</td><td>No. of policies</td></tr><tr><td>Controls</td><td>No. of controls</td></tr><tr><td>Platform</td><td><em>Linux, Windows and Kubernetes</em></td></tr><tr><td>Scanner</td><td><em>Agentless Disk Scan, Host Scanner, Kubernetes Connector, Kubernetes File System Scanner</em> and <em>Inventory Scanner</em></td></tr><tr><td>Data type</td><td><em>Hosts, Kubernetes Resources</em></td></tr><tr><td>Severity</td><td><em>Informational, Low, Medium, High</em> and <em>Critical</em></td></tr><tr><td>Created by</td><td>System or specific username</td></tr><tr><td>Last modified</td><td>Selected date and time</td></tr><tr><td>Rule type</td><td><em>Built-in</em> and <em>Custom</em></td></tr><tr><td>Remediation</td><td>Remediation values</td></tr><tr><td>Applicable assets</td><td>Supported applicable asset types</td></tr><tr><td>Available actions</td><td><em>Prevent and Create an Issue</em> and <em>Create an Issue</em></td></tr><tr><td>Standards</td><td>Associated compliance standards or controls</td></tr><tr><td>Open Issues</td><td>No. of open issue</td></tr><tr><td>Rule ID</td><td>Unique Id of a rule</td></tr></tbody></table>

### **Change the layout of the rules table**

1. Navigate to **Posture Management > Rules > Cloud Workload**.
2. In the **Cloud Workload Rules** page, click the **More Options** icon (**⋮**).
3. In the **Layout** tab, do the following:
   * To add or remove columns, search for a specific column and:
     * Click **+** to add it to the table.
     * Click **-** to remove it from the table.
   * To reorder columns, go to the **In View** section and **click and drag** columns up or down.
   * To add new columns, go to the **Add Columns** section and click **+** to include them in the table.
4. The table layout updates automatically based on your selections.

### **Rule details panel**

The rule panel displays the following details related to the selected rule:

* Details of the rule like scanner details, remediation details, and more.
* Compliance Controls for the rule.

This panel enables you to:

* Edit the rule
* Save as new
* Delete the rule
