---
description: Create SLA rules to set and track issue-resolution timers and time goals.
---

# Create SLAs for case and issue resolution

Service Level Agreements (SLAs) are formal contracts or agreements that define the expected level of service between service providers and clients or between internal teams. You can configure case and issue resolution SLAs, which are time-based goals for resolution, and timers to track how long it actually takes to resolve your cases and issues.

### Why use SLAs for case and issue resolution?

SLAs provide analyst teams with a defined structure to guide the prioritization remediation efforts. Key drivers for using SLAs include:

* **Meet compliance requirements:** Regulatory frameworks, such as PCI or HIPAA, mandate timely issue resolution. For example, PCI may require critical issues be fixed within a month, while HIPAA sets a 15-day limit for critical findings.
* **Manage risk for critical assets:** Organizations set SLAs based on the sensitivity and criticality of assets. For example, a hospital would prioritize fixing issues impacting patient medical records or payment systems over non-essential displays.
* **Report and measure remediation efforts**: SLAs allow leadership to track the effectiveness of security programs and report progress toward the goal of zero SLA violations.

### Create a Resolution SLA rule

To configure a Resolution SLA for cases or issues, create an SLA rule that defines:

* A time-based goal.
* The specific cases or issues the goal applies to.

Once created, the SLA rule is automatically applied to all matching existing and future cases or issues.

#### How to create a Resolution SLA rule

1. Select **Settings** → **Configurations** → **Object Setup** → **Cases** or **Issues**.
2. Select the **SLA Rules** tab.
3. Select **Create SLA Rule**.
4. Provide the following information, and then click **Next**.
   * **SLA Rule Name**
   * **Description** (optional)
   * **SLA Goal**: Define the SLA goal, which is the maximum time allowed to resolve issues. SLAs must be at least 30 minutes.
5. Define criteria to identify the cases or issues that the SLA will apply to.
   1.  Select the filter icon to define which cases or issues this SLA rule applies to.

       <div data-gb-custom-block data-tag="hint" data-style="warning" class="hint hint-warning"><p><strong>Warning</strong></p><p>If no criteria are defined, the rule doesn’t match any cases or issues.</p></div>
   2. Review the list of cases or issues that match your filtering criteria. If the list is correct, select **Next**.
6.  On the **Summary** page, review the information about the new SLA rule. If it is correct, click **Done**.

    The new SLA rule will appear in the table on the **SLA Rules** tab.
7.  Set the order of evaluation for the new SLA rule. The first SLA rule that matches a case or issue will be the rule that applies to the relevant (case or issue) Resolution SLA.

    By default new SLA rules are added to the bottom of the list. To move a rule up or down in the list, click and hold the arrows in the **Name** column and drag the rule to the desired position in the list.

### Reorder Resolution SLA rules

The order of SLA rules in the SLA Rules table is important. SLA rules operate on a stop-on-first-match basis. In other words, the first SLA rule that matches an issue will be the SLA used for that issue. When you reorder rules, existing issues that match a new higher-priority rule will be updated to use the new SLA.

1. Navigate to **Settings** → **Configurations** → **Object Setup** → **Cases** or **Issues** and select the **SLA Rules** tab.
2. Change the order of the SLA rules by dragging the table rows into place. To drag a table row, click and hold an arrow in the **Name** column and drag the row to the desired position in the table.

### Monitor the status of Resolution SLAs

You can view the following Resolution SLA fields on the **Cases** and **Issues** pages, so you can filter and sort issues based on these values:

* **Resolution SLA**: Indicates the amount of time left to meet the SLA deadline. Also indicates the amount of time past the SLA deadline for issues that are overdue.
* **Resolution Timer**: Indicates how long it took to resolve the issue. The timer starts when the issue status is New, and stops when the issue status is changed to Resolved.

#### How to monitor the status of case Resolution SLAs

You can monitor the status of case Resolution SLAs in the case header for a specific case, or in the cases table as explained below.

{% hint style="info" %}
**Tip**

The case header shows all active SLAs for a case. In addition to the built-in Resolution SLA, you can create additional SLAs to measure separate milestones. For more information, see [Create additional case timers and SLAs](create-slas-for-issue-resolution/create-case-timers-and-slas).
{% endhint %}

1. Navigate to **Cases & Issues → Cases**, click **Display** and select **Table**.
2. Filter on **Resolution SLA > 0** or **Resolution Timer > 0** to find cases that are within the SLA.\
   These filters support filtering of whole days only, for example **Resolution SLA > 1** filters for cases that have a Resolution SLA of greater than one day.
3. Filter on **Resolution SLA < 0** or **Resolution Timer < 0** to find cases that have exceeded the SLA.

#### How to monitor the status of issue Resolution SLAs

1. Navigate to **Cases & Issues** → **Issues**.
2.  Filter on **Resolution SLA > 0** or **Resolution Timer > 0** to find issues that are within the SLA.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>These filters support filtering of whole days only, for example <strong>Resolution SLA > 1</strong> filters for issues that have a Resolution SLA of greater than one day.</p></div>
3. Filter on **Resolution SLA < 0** or **Resolution Timer < 0** to find issues that have exceeded the SLA.

You can also view the issue resolution SLA widgets on the **Vulnerability Management** dashboard.

Resolution SLA and resolution timer are filterable XQL fields. The resolution SLA and resolution timer XQL schemas also include derived fields, so you can build queries, correlation rules, and dashboards that track whether issues are resolved within their defined SLA goals.
