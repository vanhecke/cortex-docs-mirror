---
description: >-
  Use the Cortex Agentic Assistant to investigate cases, perform threat hunting,
  and create scripts. Embed and run LLM prompts in playbooks. View AI case
  summaries.
---

# Agentic AI in Cortex XSIAM

Cortex XSIAM integrates advanced artificial intelligence to streamline security operations. Through the Cortex Agentic Assistant, the platform provides a unified interface for interacting with both system-provided and custom AI agents capable of creating and executing multi-step plans. These agents leverage specific capabilities to perform actions across your infrastructure, facilitating deep case investigations and proactive threat hunting while allowing for the creation of tailored automation.

#### Key AI Capabilities

* **Agentic Assistant Hub**: A centralized hub for managing agents and actions. System agents can be enabled and disabled, and you can create custom agents tailored to your organizational needs, including the ability to execute custom scripts.
* **Automation Engineer Agent**: Provides a natural language interface to draft, refine, and deploy automation scripts.
* **MCP Integration**: Supports the configuration of integrations that communicate with external MCP servers, enabling agents to access third-party tools and data sources via a standardized protocol.
* **Embedded AI Prompts**: Facilitates the inclusion of generative AI tasks within playbooks. These prompts function as standalone workflow steps to analyze data or generate content without requiring a dedicated agent.
* **AI-Generated Case Summaries**: Automatically generate technical overviews of security incidents. These summaries consolidate complex telemetry and impact data into high-level reports to accelerate initial triage and stakeholder reporting.

#### Cortex Agentic Assistant

Cortex Agentic Assistant is the autonomous "brain" of Cortex XSIAM. It utilizes AI agents that plan, reason, and investigate complex threats, such as cloud identity theft or container breaches. Cortex Agentic Assistant enables security operations teams to use natural language prompts to interact with AI agents. The agents have access to case context and can create plans and perform actions such as running commands, playbooks, and scripts, as well as visualizing data or investigations.

You can also interact directly from Slack with the Agentic Assistant. This enables you to trigger agents, investigate, and perform remote executions within your collaboration workflow without needing to log into Cortex XSIAM.

To enable the Cortex Agentic Assistant, go to **Settings** → **Configurations** → **General** → **Server Settings** → **Agentic Assistant**.

{% hint style="info" %}
### Note

By default, you have access to the Cortex Assistant, which includes a natural language interface for entity investigation and provides a list of recommended responses such as running a playbook, performing a scan, or collecting support files.

If you enable the Cortex Agentic Assistant, it replaces the Cortex Assistant interface entirely.

For more information, see [Compare Agentic Assistant with Cortex Assistant](agentic-ai-in-cortex-xsiam/compare-agentic-assistant-with-cortex-assistant).
{% endhint %}

Cortex Agentic Assistant is based on an ecosystem of agents and actions.

The Cortex Agentic Assistant includes system agents that are mission-focused, as well as the ability to create custom agents. An analyst focused on threat hunting, for example, might communicate primarily with the system Threat Intel agent, while analysts focused on general investigations might build custom agents that include all the actions required to perform their daily tasks.

Each agent is assigned actions it can execute. System actions can be based on playbooks, scripts, commands, or AI prompts. You can also register custom actions, which are based on scripts, commands, or AI prompts.

Access to the Cortex Agentic Assistant and the ability to manage agents and actions is restricted by role-based access controls. Actions marked as sensitive require manual approval, and all actions an agent executes are logged.

{% hint style="info" %}
### Tip

The system **Help Center** agent delivers fast, context-aware assistance to answer your questions. You can ask natural language questions, such as "How do I create a dashboard?" or "Where can I review my data retention policies?" and the agent retrieves concise, relevant information from the documentation. If a question remains unresolved, the agent assists you in creating a support case.
{% endhint %}

Within the **XSIAM Command Center** dashboard, you can click **Cortex Agentic Assistant** to view how your organization utilizes the Agentic Assistant, including information on agent plans, user prompts, as well as open cases. For more information, see [XSIAM Command Center](../detect-investigate-and-respond-to-threats/monitor-dashboards-and-reports/dashboard-reference/command-center-reference/xsiam-command-center).

#### Supported regions

The Cortex Agentic Assistant is currently available for tenants in the following regions:

* Australia (AU)
* Canada (CA)
* France (FA)
* Germany (DE)
* India (IN)
* Japan (JP)
* Netherlands (EU)
* Singapore (SG)
* South Korea (KR)
* United Kingdom (UK)
* United States (US)

{% hint style="info" %}
### Note

In multi-tenant/MSSP environments, agentic AI features are not available on the main tenant.
{% endhint %}

#### Frontier Models

**EU and US Regions**

Tenants in the EU and US regions can use the following frontier AI models:

| Name     | Model             |
| -------- | ----------------- |
| Flash    | Gemini 3.5 Flash  |
| Thinking | Claude Sonnet 4.6 |
| Pro      | Claude Opus 4.8   |

Claude Sonnet 5 is available upon request in the US and EU regions.

{% hint style="info" %}
**NOTE**

Only tenants in the EU and US regions have the model selector. Using the model selector, you can choose between different frontier models per chat, AI prompt, and AI prompt task.
{% endhint %}

**SG, JP, IN, and UK regions**

Tenants in the SG, JP, IN, and UK regions have Gemini 3.5 Flash.
