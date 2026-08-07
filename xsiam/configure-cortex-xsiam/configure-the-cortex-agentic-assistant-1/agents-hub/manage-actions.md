# Manage actions

Actions wrap diverse capabilities (such as playbooks, scripts, AI prompts, and commands) to make them accessible and executable by an agent. You can use out-of-the-box system actions or register new actions.

{% hint style="info" %}
To manage actions in the Agentic Assistant Hub, you must have the correct permissions. For more information, see [Agentic Assistant role-based access control](../agentic-assistant-role-based-access-control).
{% endhint %}

There are two types of actions in the Agentic Assistant Hub:

*   **System actions**: Cortex XSIAM contains more than 50 out-of-the-box system actions that can be disabled or enabled, but cannot be edited or deleted.

    To find and install additional content packs that include actions, go to **Marketplace** and select **Content pack includes** and **Actions**.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>System actions may rely on content packs that need to be installed and configured.</p></div>
* **Custom actions**: Users can register existing or new scripts, commands, and AI prompts as actions. Custom actions can be edited, deleted, enabled, or disabled.

Any action marked as sensitive to require user approval requires explicit user approval before execution. This is particularly crucial for operations that might alter system reality or affect an organization’s budget, such as isolating an endpoint or revoking user access. System actions are marked sensitive if they affect system reality. When creating custom actions, you decide which actions should be marked as sensitive for your organization.

The execution of system or custom actions that are based on integration commands can be restricted using [integration permissions](../../../reference-and-developer-docs/role-based-access-control/configuration-permissions/integrations-permissions).

**Manage existing actions**

From the **Actions** tab of the **Agentic Assistant Hub**, click ![three-dots.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2FORBYsY4Y6C7i1fV0zajJ%2F860e6eb54bd3ae665125051cdb957ddbd3d9c026f75c4b54acce3f0d35f08d04.png?alt=media\&token=24ae450e-c7ee-4c30-95a9-72eb53db0516) for an action to edit, delete, or disable an existing custom action. System actions can be enabled or disabled, and you can change them from sensitive to non-sensitive or from non-sensitive to sensitive.

**Search, filter, and sort actions**

You can use the dropdown filter to search all actions, custom actions, system actions, enabled actions, disabled actions, sensitive actions, or non-sensitive actions. You can also filter by source types: command, script, or playbook.

You can sort actions by creation time or update time.
