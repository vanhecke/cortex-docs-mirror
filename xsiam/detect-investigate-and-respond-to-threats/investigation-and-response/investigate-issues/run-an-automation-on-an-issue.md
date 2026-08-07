# Run an automation on an issue

You can automate issue investigation and remediation by running a playbook or Quick Action on one or more issues. Automations can help to improve efficiency by automating and standardizing your workflows, promoting consistent and effective case response and management. For example, automations can automatically remediate a case by interacting with a third-party integration or open tickets in a ticketing system such as Jira.

You can view the playbook that is running on an issue or the playbooks that have already run in the **Work Plan** for an issue. You can view Quick Actions in the **War Room** for an issue.

{% hint style="info" %}
### Note

In addition to automation, some playbooks contain manual tasks that prompt the analyst for input. This enables you to enhance an automation workflow with analyst input.
{% endhint %}

You can run automations in the following ways:

### **Manually run a playbook or Quick Action on one or more issues**

1.  Right-click one or more issues in the Issues table and select Run Automation.

    If there is currently an automation running on one or more of the selected issues, the **Run Automation** option does not appear. If an automation is running on the issue, but has been paused (for example, waiting for a user action), you can select to rerun the automation or select a new automation.
2. If the issues have an automation already assigned, choose Rerun current Automation or Select another Automation. If the issues do not have an automation assigned, Select Automation.
3. If you are not rerunning the current assigned automation, select an automation to run for the selected issue(s).
4. Click Run.

{% hint style="info" %}
### Note

You can also manually select a playbook to run from the Issue **Work Plan** tab.
{% endhint %}

### **Apply automation rules**

You can create automation rules that automatically run a playbook or Quick Action when an issue is created that meets specific criteria. For more information, see [Create an automation rule](../../../configure-cortex-xsiam/automations/create-an-automation-rule).

For more information, see [Automation in Cortex XSIAM](../../../configure-cortex-xsiam/automations/automation-in-cortex-xsiam).
