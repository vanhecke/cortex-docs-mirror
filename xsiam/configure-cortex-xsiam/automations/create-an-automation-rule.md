---
description: Learn how to create an automation rule for an issue.
---

# Create an automation rule

Automation rules allow users to automatically respond to events by defining trigger conditions and desired actions to perform once the condition is met. Automation rules can trigger playbooks and Quick Actions. Agentic Response, a feature that allows automation rules to trigger AI agents, is currently in preview and does not appear in your tenant by default. If you would like the Agentic Response feature enabled on your tenant, contact Customer Support.

While per-object access determines who can see, edit, or manually trigger a playbook, any automated execution (including those triggered by automation rules, jobs, or feed-triggered actions) is performed by the system. These actions are not restricted by the organizational scope or object-level access of the user who may have triggered the case. Instead, automated workflows remain governed by the defined scope and permissions of the involved integrations.

{% hint style="info" %}
In addition to the Automation Rules feature, the **XDR Automation** menu item is available if you migrated from Cortex XDR 3.x to Cortex XSIAM and had rules configured in your previous environment.

* **Location:** These legacy rules are located under **Investigation & Response** → **Automation** → **XDR Automation**.
* **Operational but read-only:** Existing rules from your Cortex XDR 3.x environment continue to function as originally configured, but they are now read-only. You cannot edit existing legacy rules or create new rules within this section.
* **Migration:** We recommend transitioning your legacy automation logic to the new Automation Rules, found under **Investigation & Response** → **Automation** → **Automation Rules**.
* **Functional difference:** Legacy XDR Automation rules allowed for multiple independent actions to be assigned to a single trigger. In contrast, the new Automation Rules trigger a single Playbook or Quick Action per issue.
{% endhint %}

<details>

<summary>Rules and playbook access</summary>

When working with automation rules, consider how object-level access affects visibility and configuration:

* **Role permissions for rules**: To create automation rules or edit existing ones that trigger Quick Actions and playbooks, you must have **Scripts** and **Playbooks** enabled in your role (under **Investigation & Response** → **Automations** with **Edit Public Playbooks** selected).
* **Rule visibility vs. playbook access**: You can view all automation rules in the list, including those configured to trigger playbooks you do not have access to. This ensures full visibility into the order and logic of automated workflows in your environment.
* **Playbook selection**: While all rules are visible, you can only select a playbook to which you have at least **Viewer** access.

If certain options are unavailable, contact your administrator. For more information, see [Manage user roles and access management](../../onboard-cortex-xsiam/post-deployment/manage-user-roles-and-access-management).

</details>

<details>

<summary>Rule behavior and structure</summary>

* **Target issues**: Automation rules apply to Medium and higher severity issues. They also apply to Low severity Analytic issues and Low severity ABIOC issues that are tagged with **Identity** or **Cloud**.
* **Evaluation order**: Rules are evaluated in order, and only the first rule that matches the trigger conditions is executed.
* **Trigger timing**: Automation rules trigger only upon the initial ingestion of an issue. Subsequent updates will not re-trigger the rule, even if the issue still meets the criteria.
* **Structure**: The rules consist of three parts:
  * **WHEN**: Stands for the trigger type. **WHEN** is set to **Issue is created**.
  * **IF**: Stands for the conditions that need to be met for the rule to run.
  * **THEN**: The automation that the user wants to execute: playbook, Quick action, or agent.

</details>

In the **Automation Rules** page, you can create or edit an automation rule, use recommended automation rules, edit a playbook, and change the order of priority. You can also delete or disable/enable an automation rule. When you disable an automation rule, the automation does not run for the selected condition.

{% hint style="info" %}
You can also define the conditions that trigger a specific playbook in the playbook editor. For more information, see [Playbooks](playbooks).
{% endhint %}

<details>

<summary>Create or edit an automation rule to trigger a Quick Action or playbook</summary>

Create an automation rule for issues where conditions from the automation rule are met, so that the automation, whether it is a Quick Action or a playbook, automatically runs.

For example, if the **IF** condition is `severity=critical` and the **Then** action is the Quick Action - **Create Jira Ticket**, the automation rule is triggered when a critical severity issue is detected, and then the Jira ticket is created.

1. Select **Investigation & Response** → **Automation** → **Automation Rules**.
2. Click **Add Automation Rule** or right-click a rule, select **Edit rule**, or click the edit button.
3. Enter a rule name.
4. (Optional) Provide a short description of the rule.
5. (Optional) Change the rule status. A rule can be enabled or disabled.
6. Define the rule conditions:
   1.  For **If**, click **Add Condition** and from the **Issues** table, use the filter to set the criteria for the rule, and then click **Save**.

       For example, filter the field **Severity**, and then select the value **Critical**. The **Issues** table returns all issues where the severity=critical.
   2. For **Then**, click **Add Automation**.
      1. If you clicked **Add Agent**, choose an agent from the **Select Agent** window. You can search for an agent or click on any of the agents shown. Hovering over an agent card shows a summary and the option to click **Show agent** to view the full list of actions available to the agent.
   3. Choose the playbook or Quick Action to which you have access from the **Select Automation** window. You can search for an automation or click on any of the Quick Actions and playbooks shown.
      *   **Quick Actions**: After selecting a Quick Action, you can set action parameters. For the **Create Jira Ticket** Quick Action, for example, you can enter the Description, Issue Type, Project Key, and Summary.

          <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>Quick Actions, by default, run using all available integration instances that contain the command. When selecting a Quick Action for an automation rule, you can instead choose one specific integration instance to use.</p></div>

          For more information on Quick Actions, see [Quick Actions](quick-actions).
      *   **Playbooks**: Click ![playbooks\_automation\_view.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-a1f82d3809c3457d64ca4524263cb13ce09f6fe7%2F1170821aad5ced23b8bb93936cc3d065b53722aebde1ba9a761c918845cfc060.png?alt=media) to view the description and playbook preview.

          If you want to use a playbook that is not part of your **Org Playbooks**, show **Playbook Catalog** for a full list of available playbooks. For more information, see [Choose from existing playbooks or create your own](playbooks/build-your-playbook/choose-from-existing-playbooks-or-create-your-own).

          The list of available playbooks is filtered based on your access; you will only see playbooks that you own, that have been shared with you, or that are marked as **Public**. For more information, see [Access to playbooks](playbooks/access-to-playbooks).
   4. Click **OK**.
7. Click **Create**.

**Example**

In this example, there are a number of issues created called **McAfee + Zscaler - Malware Downloaded And Dropped To Disk**. These issues are a result of malware, which was detected by the agent. A custom playbook runs these issues, where if action is detected by the ePO, the playbook either quarantines the machine where the malware is detected or closes the investigation if there is no action. We want to create an automation rule to automatically run the playbook when an issue is created.

1. Create an automation rule called **McAfee + Zscaler - Malware Downloaded And Dropped To Disk**.
2. Define the rule conditions.
3.  In the **Issues** section, filter for the **McAfee + Zscaler - Malware Downloaded And Dropped To Disk** issues.

    The next time an issue is created with the criteria, the playbook runs according to the automation rule.

    The case collects issues that automatically run the custom playbook.
4. Select one of the issues to see that the playbook ran (Work Plan or Case War Room).

</details>

<details>

<summary>Create or edit an automation rule to trigger an agent</summary>

This feature is currently in preview and allows you to create an automation rule that triggers an agent when certain conditions are met.

For example, if the **IF** condition is `severity=critical` and the **Then** action is the **Case Investigation** agent, the automation rule is triggered when a critical severity issue is detected, and then the agent runs using the provided prompt.

{% hint style="info" %}
This feature is currently in preview. If you would like to have this feature enabled on your tenant, contact [Cortex Product Management](mailto:dl-CortexAgentixDesignPartners@paloaltonetworks.com).

Only users with both the **Edit Public Playbooks** permission, located under the **Playbooks** component in the role configuration, and the **Interact with agents** permission, located under the **Cortex Agentic Assistant** → **Agents** component in the role configuration, can create automation rules that trigger agents.
{% endhint %}

1. Select **Investigation & Response** → **Automation** → **Automation Rules**.
2. Click **Add Automation Rule** or right-click a rule, select **Edit rule**, or click the edit button.
3. Enter a rule name.
4. (Optional) Provide a short description of the rule.
5. (Optional) Change the rule status. A rule can be enabled or disabled.
6. Define the rule conditions:
   1.  For **If**, click **Add Condition** and from the **Issues** table, use the filter to set the criteria for the rule, and then click **Save**.

       For example, filter the field **Severity**, and then select the value **Critical**. The **Issues** table returns all issues where the severity=critical.
   2. For **Then**, click **Add Agent**.
   3.  Choose an agent from the **Select Agent** window. You can search for an agent or click on any of the agents shown. Hovering over an agent card shows a summary and the option to click **Show agent** to view the full list of actions available to the agent. Only public agents are available.

       <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>Only public agents can be selected. If you create a custom agent, it must be set as a public agent to use it in an automation rule.</p></div>
   4. Click **Next**.
   5.  Either select a saved prompt from the prompt library or write a new prompt. You can edit a prompt from the prompt library but you cannot save the changes you make to the prompt library. Any edits are only applied to this automation rule.

       For more information on writing prompts, see [Create a prompt](ai-prompts/create-a-prompt).
   6. Click **Test Prompt**.
   7. There are two options to load data for the test.
      *   **Select issue** to select an existing issue to use as sample data. You can switch between existing issues by clicking **Change issue**.

          <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>To avoid making real world changes in third-party systems, we recommend expanding the <strong>Test Data</strong> field and clicking <strong>Edit</strong> to manually change the sample data. When you run the test, third-party actions are executed. For example, if the prompt leads the agent to create a Jira issue as part of the test, an actual Jira issue will be created.</p></div>
      * Expand the **Test Data** section and click **Edit** to manually enter sample issue data.
   8. Use the Agentic Assistant to **Run test**.
   9. Expand the **Plan** and scroll down if needed to view all steps and the outcome for full visibility into step-by-step reasoning, step outputs, artifacts, prompts, and execution plans.
   10. (Optional) If the plan execution does not match your requirements, you can select a different prompt from the prompt library or edit the prompt or prompt input(s) as needed, and then **Run test** again. Note that there is no chat history saved and you cannot view the output of previous tests.
   11. Click **Add to rule**.
7. Click **Create**.

{% hint style="info" %}
* When automation rules trigger agents, there is a limited number of parallel agentic chats. If this limit is reached, there may be delays in execution, but all rules are still applied and agents are still triggered.
* If the agent tries to execute an action that is marked as sensitive and requires manual approval, the pending task shows in the **Resolution Center** and must be approved or denied for the agent to continue.
* Agent runs are logged in the **War Room** and appear in the `agentix_agents_actions` dataset.
* If LLM capabilities are disabled in your tenant, the option to create automation rules to trigger agents is not available. If you have automation rules that trigger agents and then disable LLM capabilities, the rule will fail. If you have LLM capabilities disabled in your tenant, we recommend disabling any automation rule that uses an agent or changing to a Quick Action or playbook.
* If an agent is disabled in the **Agents Hub** and was used as part of an automation rule, the rule will fail. The Automation Rules table will display **Agent Disabled** in the **Automation** column.
{% endhint %}

</details>

<details>

<summary>Add a recommended automation rule</summary>

You can add automation rules recommended by Cortex XSIAM.

1. Select **Investigation & Response** → **Automation** → **Automation Rules**.
2. Click **View Recommendations**.
3.  In the **Automation Rule Recommendations** table, view and select the required recommended automation rules to add to the **Automation Rules** table.

    For playbooks, you can click the playbook name to preview. For Quick Actions, you can view the description and available parameters.
4. Click **Add Selected rules**.
5. Verify the order of the automation rule and change the order (if required),
6. Save the changes to the **Automation Rules** table.

</details>

After you create an automation rule, the rule is added to the **Automation Rules** table. In the **Automation Rules** table, you can do the following:

*   Set the priority of the automation rules, so when an issue is created, the first rule takes priority, then the second, third, etc. Only the first matching rule is executed.

    New rules created manually are added to the bottom of the table.
*   View details of the automation rules that have been created.

    By default, you can see the condition, automation, and the creation dates and source. You can add columns and filters as required. To edit, disable, or delete an automation rule, right-click on the rule.

<details>

<summary>Scope-based access control for automation rules</summary>

Automation rules support SBAC (scope-based access control). The following parameters are considered when editing a rule:

* If **Scope-Based Access Control (SBAC)** is enabled and **Endpoint Scoping Mode** is set to restrictive mode, you can edit an automation rule if you are scoped to all tags in the rule.
* If **Scope-Based Access Control (SBAC)** is enabled and **Endpoint Scoping Mode** is set to permissive mode, you can edit an automation rule if you are scoped to at least one tag listed in the rule.
* As a scoped user who has editing permissions to a rule, you can change the order among other rules that are locked.
* If a rule was added when set to restrictive mode, and then changed to permissive (or vice versa), you will only have view permissions.

</details>
