---
description: Manage personal and system agents in Cortex XSIAM Agentic Assistant.
---

# Manage agents

Agents create and execute step-by-step plans dynamically, choosing relevant actions based on a user's request. Each agent has a model, a user context, a conversation context, and a set of actions that it can perform. Users engage with agents through conversations in the chat interface.

Agents can only use actions that have been assigned to them, and execution is limited by the user's permissions.

Permissions for the Agentic Assistant and the Agentic Assistant Hub can be found under **CORTEX AGENTIC ASSISTANT** in the role permissions when creating or edit a role. For more information, see [Agentic Assistant role-based access control](../agentic-assistant-role-based-access-control)

There are two types of agents in the Cortex Agentic Assistant:

* **Custom agents**: Each user can create one or more agents that have the same or fewer permissions as the user, ensuring agents operate with the least necessary privileges required. These permissions automatically update if the user’s roles or permissions change. When users create custom agents, they can create a private agent only they can access, or a public agent all users can access.
*   **System agents**: System agents come out-of-the-box and are not linked to a specific user; instead, they possess their own defined roles and permissions. A system agent may include actions that the user does not have permission to execute. All users have access to all system agents, but plan execution is limited by the permissions of the individual user.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>System agents can include actions that require additional content packs to be installed and configured. To view all actions assigned to a system agent, including actions not available due to missing content, click on the system agent in the <strong>Agentic Assistant Hub</strong>. There may be actions assigned to a system agent that are not relevant to your organization. For example, the Case Investigation agent includes the action <strong>ServiceNow - Create Ticket</strong>, but you would only install and configure the relevant content pack if you wanted to create tickets in ServiceNow.</p><p>System agents include system actions that may be marked as sensitive and require manual approval to execute. You can change this setting for specific system actions from the the <strong>Actions</strong> tab of the <strong>Agentic Assistant Hub</strong>, by clicking <img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2FORBYsY4Y6C7i1fV0zajJ%2F860e6eb54bd3ae665125051cdb957ddbd3d9c026f75c4b54acce3f0d35f08d04.png?alt=media&#x26;token=24ae450e-c7ee-4c30-95a9-72eb53db0516" alt="three-dots.png"> in the action card and selecting <strong>Mark as sensitive</strong> or <strong>Mark as non-sensitive</strong>.</p></div>

### **Agent management for the** Cortex XSIAM Agentic Assistant

You can edit, delete, disable, or enable custom agents by clicking the more options ![three-dots.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2FORBYsY4Y6C7i1fV0zajJ%2F860e6eb54bd3ae665125051cdb957ddbd3d9c026f75c4b54acce3f0d35f08d04.png?alt=media\&token=24ae450e-c7ee-4c30-95a9-72eb53db0516) icon for the agent.

You can edit, enable, or disable system agents by clicking the more options ![three-dots.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2FORBYsY4Y6C7i1fV0zajJ%2F860e6eb54bd3ae665125051cdb957ddbd3d9c026f75c4b54acce3f0d35f08d04.png?alt=media\&token=24ae450e-c7ee-4c30-95a9-72eb53db0516) for the agent. The edit option for system agents is limited to adding specific instructions for the agent such as tone, style, format, and priorities.

You can click on an Agent to view all actions assigned to the agent. There are three possible statuses for actions assigned to an agent:

* **Enabled** (green circle with a check mark): The action is enabled and available for the agent to use.
* **Disabled** (grey circle with an x): The action has been disabled and is not available for the agent to use.
*   **Unavailable content** (grey circle with a horizontal line): The content the action is based on is not available. To use the action, the content item must be installed and configured.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>In some cases, an agent may include actions with content items that are not relevant for all licenses. If that occurs, the grey circle appears, but you are not able to install the related content.</p></div>

### **Search, filter, and sort existing agents for the** Cortex XSIAM Agentic Assistant

You can use the dropdown filter to search all agents, custom agents, enabled agents, or disabled agents.

You can sort agents by most used, creation time, or update time.
