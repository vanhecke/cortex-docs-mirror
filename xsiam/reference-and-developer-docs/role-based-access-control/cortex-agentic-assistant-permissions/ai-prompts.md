---
description: Configure AI Prompts permissions in Cortex XSIAM.
---

# AI Prompts

Controls access to the AI Prompts Library (**Investigation & Response** → **Automation** → **AI Prompts**), where users create and manage reusable prompt templates (including system instructions and few-shot examples) used to guide the LLM's behavior.

{% hint style="warning" %}
### Caution

To effectively embed AI Prompts directly into playbook workflows, users must be granted the Manage prompts in playbook editor checkbox, and they must also hold View/Edit permissions for the Playbooks module.
{% endhint %}

For more information, see [AI prompts role-based access control](../../../../configure-cortex-xsiam/automations/ai-prompts#UUID-007ebd3e-2261-e143-9f9a-3b7b13dbb6c4).

| Permission | Description                                                                                                                                                                                        | Roles Example                                                                                                                                                                                                                     |
| ---------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| None       | No access to the **AI Prompts** page and can't see prompts in the Playbook editor.                                                                                                                 | SOC Tier-1 Analyst: No need to access AI prompts. They consume agent capabilities through the Agentic Assistant chat interface, not through prompt management.                                                                    |
| View       | Read-only access to the **AI Prompts** page and can view prompts in the Playbook editor.                                                                                                           | SOC Tier-2, Tier-3 Analysts and Threat Hunters: Need visibility to understand the capabilities and logic of the AI assistants they use                                                                                            |
| View/Edit  | <p>Users can do everything in View. When set to View/Edit, the following action checkboxes become available:</p><ul><li>Manage prompts library</li><li>Manage prompts in playbook editor</li></ul> | Security Engineer: Full View/Edit with both checkboxes enabled. They are the primary builders of AI prompts and playbook AI tasks. They create, test, and maintain the prompt library and embed AI tasks into playbook workflows. |

**AI Prompt Sub-permissions**

| Sub-permission                    | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| --------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Manage prompts library            | <p>Controls whether users can create, view, edit, duplicate, and delete prompts on the <strong>AI Prompts</strong> page.</p><ul><li>Checked: The user has full edit access to the <strong>AI Prompts</strong> page, such as create, edit, delete, edit, and save prompts. All management buttons and menu options are visible and functional.</li><li>Unchecked: The user has read-only access to the <strong>AI Prompts</strong> page (equivalent to View level).</li></ul>                                                                                                                                                                                                                                     |
| Manage prompts in playbook editor | <p>Controls the ability to use and manage AI prompts directly within the playbook editor, enabling inline AI task configuration in playbook workflows.</p><ul><li>Checked: The user has full edit access to AI prompt tasks in the Playbook editor, such as adding AI tasks to playbooks, configuring AI task arguments, outputs, and timeout settings.</li><li>Unchecked: The user has read-only access to prompts in the Playbook editor. The user can't create, edit, save, or delete AI prompt tasks.</li></ul><div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>You need to add Playbooks View/Edit permission to edit playbooks.</p></div> |

<details>

<summary>Required and recommended permissions</summary>

Consider adding the following permissions:

| Permission   | Permission Level                            | Reason                                                                                                                                                                                                                                                    |
| ------------ | ------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Scripts      | Enabled or Enabled with checkboxes selected | <ul><li>Enabled: Required for Playbook editor checkbox. The AI prompt tasks in playbooks depend on the script infrastructure.</li><li>Enabled with checkboxes selected: Strongly recommended to create pre/post scripts for AI prompts.</li></ul>         |
| Playbooks    | Enabled or Enabled with checkboxes selected | <ul><li>Enabled: Required for Playbook editor checkbox. Must be able to view playbooks to see AI tasks.</li><li>Enabled with checkboxes selected: Required for Playbook editor checkbox. Must be able to edit playbooks to add/modify AI tasks.</li></ul> |
| Marketplace  | View/Edit                                   | Recommended to install content packs that include AI prompt templates.                                                                                                                                                                                    |
| Query Center | View                                        | Recommended. Some AI prompts generate or reference XQL queries.                                                                                                                                                                                           |

</details>
