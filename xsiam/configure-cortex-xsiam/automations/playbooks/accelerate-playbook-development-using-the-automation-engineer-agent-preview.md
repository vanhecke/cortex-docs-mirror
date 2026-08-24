---
description: >-
  Learn how to use the preview Automation Engineer agent in Cortex XSIAM to
  create, update, and troubleshoot playbooks with natural language.
---

# Accelerate playbook development using the Automation Engineer agent (preview)

Use the preview Automation Engineer agent in the Cortex XSIAM Agentic Assistant to create, update, and troubleshoot playbooks with natural language.

{% hint style="info" %}
This feature is not enabled by default. To request access, contact Cortex Product Management.
{% endhint %}

### Automation Engineer agent capabilities in Cortex XSIAM

* Creating playbooks\
  Generate a functional playbook for your use case from a natural language prompt.\
  **Example**:\
  “Create a playbook that is triggered by a new network alert containing an IP address. First, run standard IP enrichment and threat intelligence lookups to triage the IP and check for associated malware. Next, add a conditional task to evaluate if the IP is marked as malicious. If it is malicious, use the mail integration to send an email to IT@palo.com containing the IP address, the alert details, and the associated malware context. If it is benign, close the incident.”
* Updating playbooks\
  Modify existing tasks, logic, or integrations using follow-up prompts.\
  **Example**:
  * “Add error handling to this flow”
  * “In the 'Is Malicious' condition, change the target email address to security-ops@palo.com.”
* Querying and explaining existing playbooks\
  Ask the agent questions to understand complex playbook logic, troubleshoot specific tasks, or get AgentiX SDK guidance. You can ask questions about the logic of locked system playbooks (from content packs), though you must duplicate them to apply AI-generated modifications.\
  **Example**:
  * "Explain the logic behind the conditional branch in this playbook?"
  * "How do I use the AgentiX SDK to add a custom header to the outgoing email task in this workflow?"

{% hint style="info" %}
The Automation Engineer agent is available with the Cortex Agentic Assistant, for users with playbook view/edit permissions and Interact with agent enabled.

For more information, see [Agentic Assistant role-based access control](../../configure-the-cortex-agentic-assistant-1/agentic-assistant-role-based-access-control).
{% endhint %}

### Use the Automation Engineer agent in Cortex XSIAM

1. Navigate to **Investigation & Response** → **Automation** → **Playbooks**.
2. Create a new playbook or open an existing one to enter the Playbook Editor.
3. Click the Agentic Assistant icon. The Agentic Assistant pane opens with the Automation Engineer agent automatically selected.
4. In the chat interface, enter a natural language prompt describing the automation you want to build or the change you want to make.\
   The agent automatically uses the active playbook as context. Any request to create, modify, or query details applies specifically to that playbook.\
   Examples:\
   \- "Build a playbook that is triggered by a phishing alert, extracts the sender's domain, and checks its reputation using VirusTotal. If malicious, block the domain in Okta and notify the security team via Slack."\
   \- “Create a playbook that is triggered by a new network alert containing an IP address. First, run standard IP enrichment and threat intelligence lookups to triage the IP and check for associated malware. Next, add a conditional task to evaluate if the IP is marked as malicious. If it is malicious, use the mail integration to send an email to IT@palo.com containing the IP address, the alert details, and the associated malware context. If it is benign, close the incident.”
5. Click the submit arrow or press Enter to submit the prompt.\
   The Agentic Assistant then displays:
   * The plan describing the steps the Automation Engineer agent took, including analyzing the request, retrieving relevant integrations, and generating the playbook logic.
   * A playbook preview card that includes the following details:
     * The playbook name.
     * The playbook revision number (#).
     * Playbook metadata: The number of tasks, inputs, and outputs.
     * An expand icon to view the updated playbook structure visually, with the option to click Use this revision.
     * The options menu **⋮** that includes **Use this revision**.
6. Modify the revision (optional).\
   You can refine the suggested workflow by providing additional instructions. For example, "Add a 10-minute delay before the Slack notification".\
   If the agent cannot find a specific command or script for a task, it creates a placeholder task in the editor for you to complete manually.
7. Click Use this revision to push the AI-generated logic to the Playbook Editor.\
   Revisions can only be applied while in Edit Mode. If you have unsaved manual changes, the system prompts you to confirm before overwriting them.

### Track AI-assisted Cortex XSIAM playbook development

To help maintain visibility into which automations were created or modified by AI:

* Any playbook generated or significantly modified by the agent is automatically assigned the **AI Assisted** tag.
* The Agentic Assistant maintains a history of your conversation and revisions, allowing you to compare versions or revert to an earlier state.

### Automation Engineer agent best practices

You don't need a perfect prompt on the first try. Use iterative feedback to fine-tune your playbook.

**Example**:

* "Add error handling for the VirusTotal task."
* "Change the notification channel from Slack to Microsoft Teams."
* "Ensure the playbook only triggers if the severity is High."
