# Cloud Security Operations

{% hint style="info" %}
### Notice

Requires Cortex XSIAM Premium, or any other XSIAM license with the Cloud Runtime Security or the Cloud Posture Security add-on.
{% endhint %}

The Cloud Security Operations dashboard helps you rapidly assess your security posture and resolve issues with the largest impact. As a security architect or engineer, you can leverage the dashboard to assess the efficiency with which your team responds to security issues on an ongoing basis, without spending any extra time gathering and grouping issue details, identifying owners, and kickstarting the remediation process. Contextual views also link to other areas of the Cortex Cloud platform for a deeper security context. With the Cloud Security Operations dashboard, you can:

* Reduce noise and maximize impact: Use the dashboard’s curated views to focus on the most important issues prioritized by criticality and impact, and tasks that maximize the output of your efforts.
* Improve situational awareness and visibility: The dashboard interface helps you learn about your security estate, identify security gaps, and track progress against key performance indicators such as Issue Burn Down and Mean Time To Remediation (MTTR)
* Customize your view: The dashboard provides a default view for each of the widgets while giving you the option to customize views to capture the insights you need.

![sec-ops-april.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-22e5b6a83322e59357beda21d68ea5dfc47074fe%2Ff5bab1d448a3f7b26c8e16064e4c7b54969a74a61239ec5ef4d29052767dcbbe.png?alt=media)

{% hint style="info" %}
### Note

Command Center data may not match the counts on the Issues page, and you may observe inconsistencies. This is because dashboard data is a snapshot of issues identified, whereas the Issues page provides the most up-to-date view of risks across your cloud assets. In addition, the Issues pages do not support all the currently available filters on the Command Center dashboard.
{% endhint %}

### **Dashboard Widgets**

The Cloud Security Operations dashboard provides the widgets described below to help you rapidly remediate the issues that require immediate attention.

<table data-header-hidden><thead><tr><th width="200"></th><th></th></tr></thead><tbody><tr><td><strong>Widget</strong></td><td><strong>Description</strong></td></tr><tr><td>Posture Issues Resolved</td><td><p>Provides a count of the total number of Posture issues you have resolved over the selected time period across all issue categories and compares it with the number of issues resolved over the previous equivalent time period. By default, the count reflects the number of Critical and High severity issues you have resolved over the last 7 day period, while the percentage change indicates the relative change from the previous 7-day period.</p><p>Issues are based on rule violations on a specified scope of resources. Select any portion of the issues highlighted to see a list view of resolved issues.</p></td></tr><tr><td>Open Posture Issues</td><td><p>Provides a cumulative snapshot count of the total number of Posture issues that remain unresolved in your environment and tracks the relative change in this count over the selected time frame. By default, the count reflects the total number of Critical and High severity issues still unresolved in your environment, while the percentage change indicates the relative change in this count over the last 7 days.</p><p>Select the <strong>Related Posture Cases</strong> donut chart to see Critical and High issues grouped into remediable Posture Cases. The displayed count shows you the number of Open Issues that can be addressed by resolving the corresponding Posture Case category.</p><p>Choose from one of the time-ranges specified in the filter options to narrow your search.</p></td></tr><tr><td>Open Posture Issues by Age</td><td>Provides a total count of unresolved Posture issues sorted by the time period since they first originated in the system. Select any time range to view a detailed list of Issues defined by how long they have remained unresolved.</td></tr><tr><td>Posture Issue Burndown</td><td><p>Provides a trendline of the total number of open and resolved Posture issues over time across all issue categories. By default, the trendlines track the number of open and resolved issues over the last 7 days.</p><p>This daily point in time snapshot captured can be adjusted by severity level. Select the filter option to narrow issues displayed by Issue Type (Attack Paths, Configuration, Data etc.) or Time Range.</p></td></tr><tr><td>Mean Time to Remediation Issues (MTTR)</td><td><p>Provides a graphical view of the Mean Time to Remediation (MTTR) for issues across all categories, within the Posture domain, over a selected time range. By default, the chart displays the MTTR trends for Critical and High severity issues, as well as, the combined MTTR across both severities over the last 7-day period. Switch to the table view to compare the 7-day average MTTR with the average across the previous 7-day period.</p><p>The severity level displayed in the list view is set by the levels selected in the global filter. This can be adjusted on the <strong>View MTTR Insights</strong> side-panel. The <strong>View MTTR Insights</strong> side-panel also lists the top ten Accounts/Issues with the highest MTTR for further analysis. Select the filter option to narrow down issues displayed by Issue Type (Attack Paths, Configuration, Data etc.) or Severity.</p></td></tr><tr><td>Top 3 Posture Cases</td><td>Top 3 unresolved Posture Cases based on the count of Posture issues within the cases with domain as posture. Click on any Posture Case to be redirected to a detailed view of the case. Select the filter option to narrow down issues displayed by Posture Cases status or time range. Select <strong>View All Posture Cases</strong> to see a comprehensive list of all open Posture Cases containing Crttical and High severity Issues.</td></tr><tr><td>Open Posture Issues by Type</td><td>Provides a breakdown of all open Posture issues listed by all applicable Issue Type (Attack Paths, Configuration, Data, Code, etc.) and Severity. Click on any issue to be redirected to the Issues view. Select the filter option to narrow down issues by a specific time range. You can also toggle between graph and table view here.</td></tr><tr><td>Top Impacted Assets</td><td>Displays the top five assets with the highest number of Posture issues. Additional account and asset details are also provided. Click on any asset to view more details in the Assets side panel. Assets can be filtered by type, category, and time range. Graph and table toggle is also available to customize your view</td></tr><tr><td>Top Impacted Accounts</td><td>Lists the account with the highest number of unresolved Posture issues, sorted by issue count and broken down by severity. Select a filter to narrow your search by time range or issue type.</td></tr></tbody></table>

{% hint style="info" %}
### Note

The Last updated time indicated on each widget may differ as widget data is gathered at varying intervals.
{% endhint %}

### **Generate Reports**

You can also share Cloud Security Operations dashboard reports with stakeholders to keep them abreast of the security status of your cloud assets. Select the **Save as a report template** to create a shareable template. Next, navigate to **Report Templates** to Edit, Delete, or **Generate a Report** that can be scheduled for wider distribution.

### **Filter Options**

Use one of the multiple filter options provided to further focus on the most impactful issues. Filter options include:

* **Severity Filter:** Select a severity level from the drop-down to apply the filter globally across all widgets. Click **Run** to update all existing widgets to the selected severity level. Severity can also be adjusted individually at the widget level. Filter settings at the widget level are saved, global filters are however not saved.
* **Time Range Filter:** By default the time range is set to 7 days. This can be updated to 24 hours, 7 or 30 days, and a Custom time frame and applied across all widgets.
