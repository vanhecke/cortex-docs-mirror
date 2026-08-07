# Issues, findings, and events

Understand how issues, findings, and events are related to cases.

### **Issues**

Issues identify the problems that you need to solve in your environment. Cortex XSIAM creates issues when problems occur in your environment that cross defined thresholds, or surpass your organization's accepted level of risk and threat tolerance.

Each issue comprises a defined framework of:

* **What happened:** A description of the problem
* **How is your environment impacted:** Affected assets or the impact of this issue in your environment
* **Contributing evidence:** Data that supports our analysis and observations
* **Recommended actions:** Automations, playbooks, and manual suggestions

Issues are created from findings or from events that occur in your environment. When an issue is created, Cortex XSIAM assesses the content of the issue and assigns it to a new or existing case. In addition, according to the content of the issue, it is assigned to a domain that reflects the operational use case of the issue, such as **Security** or **Health**. Using case grouping logic, Cortex XSIAM then determines whether to link the issue to a case.

When you open a case, you can see all issues that are linked to the case. Review the **Grouping graph** to see why the issues were grouped together in the case. For more information about how issues are grouped in cases, see [Case grouping](case-grouping).

In addition, Cortex XSIAM offers the flexibility to:

* Manually link and unlink issues from cases. Issues can also be linked to multiple cases. For more information, see [Investigate issues](../investigate-issues).
* Mirror Cortex issues with external applications (for example, Atlassian Jira). For more information, see [Investigate issues](../investigate-issues).
* Create issues from custom rules that you define. For example, correlation rules, malware rules, and vulnerability rules. For more information about setting up rules, see [What are detection rules?](../../threat-management/detection-rules/what-are-detection-rules).

### **Findings and events**

Findings and events form the core of our knowledge data lake.

#### **Findings**

**Findings** are non-actionable, informational objects that provide context about the _current state_ of the assets in your environment.

To gather findings, Cortex XSIAM periodically scans the assets in your environment and collects raw data about vulnerabilities, compliance, exposures, malware, secrets, and other posture-related information about the asset. This raw data is processed, saved to datasets, and recorded as findings.

Each time the assets are scanned, the findings are updated to reflect the current state of the assets. Therefore, the finding for an asset will change over time.

Each finding is categorized according to its context, for example Configuration, Vulnerability, Compliance, or Identity, and is related directly to the scanned asset. When you investigate an asset through the **Asset Inventory**, you can see any findings that were collected for the asset.

Findings themselves are not issues, however findings that match a specific logic can generate issues. You can also set up your own rules to trigger issues when certain types of findings are recorded. For example, you can set up Compliance rules that will create issues if specific compliance fails are identified in compliance findings.

To view findings:

* View all findings. From the the **Issues** page click **Findings**.
* See findings for a specific asset. From the Asset Inventory, select a specific asset to open the asset card. If findings are available for the asset you can click to open the finding card.
* Search the `Findings` data set to see the findings collected over time for an asset.

#### **Events**

**Events** are logged activities that occur in your environment.

Cortex XSIAM collects event logs that audit the activities that occur in your environment. The logs are ingested from various sources, such as Palo Alto Networks Next-Generation Firewall (NGFW), Prisma Access, third-party sources, and EDRs. These logs provide a complete picture of the events that occur in the environment and the activities surrounding the events.

When certain malicious objects (such as malware) are discovered in the event logs, an issue is created. During case investigation, you can query your event logs to see information about the actors and processes that triggered the issue.
