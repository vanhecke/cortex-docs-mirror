# Investigate an issue using Cortex Response and Remediation playbooks

Issues help you to monitor and control the security of your system framework by alerting you to security risks in your framework. Cortex XSIAM generates issues from the following:

* Agents
* Firewalls
* Analytics
* Integrations

By analyzing an issue, you can better understand the cause of the issue, and take actions where required.

<details>

<summary>Select an issue to investigate</summary>

The **Issues** page displays a table of the issues associated with the incident. By default, the **Issues** page displays the security issues received over the last seven days. To see detailed information about an issue, click an issue to open the issue panel. You can then investigate the issue further by opening the issue investigation panel.

1.  Go to **Cases & Issues** → **Issues**.

    ![issues.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-6062e06893691840f1a06dee87a5e81e056febbf%2F5f135597c3f9142aeafc31ce1d571915274dd8bc9cc6b19f71f9c811e0c1cc15.png?alt=media)
2.  Click the issue and review the information in the issue side panel.

    ![issue\_details.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-0a6cc4ce95284501535d84fddef80dde4078364a%2F9c738126c7841de357098042ce2344f6f156daa35a141bf63d3871c54a1e8354.png?alt=media)
3.  To see more information about the issue, click the **Issue Overview** tab.

    ![alert\_overview.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-804f7c86ac78b5fa3ec435b6e986420ef88938fa%2F9dc94a2dc51b8282b0e85ccb141a7efa51f7be8d4d8b25c96e13d43ce1eabb71.png?alt=media)

</details>

<details>

<summary>Run a Cortex Response and Remediation playbook</summary>

The Cortex Response and Remediation playbooks are a series of tasks, scripts, conditions, commands, and loops that run in a predefined flow to save time and improve the efficiency and results of the investigation and response process. They enable you to automate many security processes, including handling investigations and managing tickets. In the Work Plan tab, you can select a playbook to run on the issue. You can watch the flow of the playbook as it automatically analyzes the issue.

1. Go to **Cases & Issues → Issues**.
2. Click the issue and review the information in the issue side panel.
3. In the Issue Investigation panel, click the **Work Plan** tab. A message appears that recommends which Cortex Response and Remediation playbook you should run on this issue.
4. Click **Run**. A single instance of the playbook will run.

<figure><img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2FG6IrlHYLXaMhjRsqIgQ9%2FResponse_Remediation_Playbook.png?alt=media&#x26;token=3c589f5c-1256-4706-9aab-8d92578b7961" alt=""><figcaption></figcaption></figure>

</details>

<details>

<summary>Adopt a automation rule suggestion</summary>

An automation rule is a filter on an issue that creates conditions, so if an issue with specific characteristics is created (for example by source, severity, or MITRE TTP), a suitable response is issued via a playbook. This saves the analyst time and expense when investigating an issue.

You can assign a playbook to an issue so that whenever the same issue is triggered in the future, the same playbook will automatically run. You can add an automation rule from the **Automation R Recommendations** table. These playbooks are recommended to run whenever the issue is triggered. These recommendations are part of the _Cortex Response and Remediation_ content pack.

1. Go to **Investigation & Response** → **Automation** → **Automation Rules**.
2. Click **View Recommendations**.
3. Select the automation rule you want and click **Add selected rules**.

</details>

<details>

<summary>Reviewing the playbook response</summary>

After running the playbook, you can investigate an issue to gain more information about the cause of the issue, and take any actions required. In the issue investigation panel. The following tabs are common to most issue:

<table><thead><tr><th width="150">Tab</th><th>Description</th></tr></thead><tbody><tr><td>Issue Overview</td><td><p>A summary of the issue, such as issue details, outstanding tasks, and indicators. Some fields are informational and some are editable. Includes the following sections (depending on the layout):</p><ul><li><strong>ISSUE DETAILS</strong>: A summary of the issue, such as type, severity, and when the issue occurred. Update these fields as required.</li><li><strong>COMMAND AND TASK RESULTS</strong>: Lists any manual commands and playbook task results.</li><li><p><strong>WORK PLAN</strong>: When you click on the section, you can view or take action on the following:</p><ul><li><strong>Playbook tasks</strong>: When a playbook runs, any outstanding tasks appear. You can take various actions here or in the Work Plan tab.</li><li><strong>To-Do Tasks</strong>: An ad-hoc item that is not attached to the Work Plan. Create tasks for users to complete as part of an investigation. These are like a To-Do list that you keep in an investigation on an ad-hoc basis rather than the Work Plan which follows a pre-defined process. You can view or create To-Do tasks.</li></ul></li><li><strong>NOTES</strong>: Helps you understand specific actions taken, and allow you to view conversations between analysts to see how they arrived at a certain decision. You can see the thought process behind identifying key evidence and identifying similar incidents.</li><li><strong>MALICIOUS OR SUSPICIOUS INDICATORS</strong>: A list of any malicious or suspicious indicators. If you have the Threat Intel add-on you can pivot to the Indicators page, where you can take further action on the indicator.</li></ul></td></tr><tr><td>Technical Information</td><td>Displays an overview of the information collected about the investigation, such as indicators, email information, URL screenshots, etc. When you run a playbook, the sections are automatically completed.</td></tr><tr><td>Investigation Tools</td><td>Enables you to take action on the issue , such as converting a JSON file to CSV and check if the IP address is in CIDR.</td></tr><tr><td>War Room</td><td>A comprehensive collection of all investigation actions, artifacts, and collaboration. It is a chronological journal of the issue investigation. Each incident has a unique War Room. For information, see <a href="../../../investigate-issues/use-the-war-room-in-an-investigation">Use the War Room in an investigation</a>.</td></tr><tr><td>Work Plan</td><td>A visual representation of the running playbook that is assigned to the incident. For more information, see <a href="../../../investigate-issues/use-the-work-plan-in-an-investigation">Use the Work Plan in an investigation</a>.</td></tr></tbody></table>

**Use the following steps to investigate and triage the issue:**

1. Review the data shown in the issue such as the command-line arguments (CMD), process info, etc.
2.  Analyze the chain of execution in the causality view.

    When the app correlates an issue with additional endpoint data, the **Issues** table displays a green dot to the left of the issue row to indicate the issue is eligible for analysis in the causality view. If the issue has a gray dot, the issue is not eligible for analysis in the causality view. This can occur when there is no data collected for an event, or the app has not yet finished processing the EDR data. To view the reason analysis is not available, hover over the gray dot.
3. Review the timeline of the sequence of events over time. The timeline is available for issues that have been stitched with endpoint data.
4. If deemed malicious, consider responding by isolating the endpoint from the network.
5. Remediate the endpoint and return the endpoint from isolation.

</details>
