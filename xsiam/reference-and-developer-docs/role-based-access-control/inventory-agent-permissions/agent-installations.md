# Agent Installations

**Agent Installations**

Manages the deployment of XDR agents, such as downloading agent installation packages, viewing installation status and history, and tracking deployment progress.

For more information, see [Create an agent installation package](../../../../onboard-cortex-xsiam/deployment-steps/install-cortex-xdr-agents#UUID-de47a28d-9479-0584-e7b5-5ebd6f68fdce).

{% hint style="warning" %}
### Caution

Installation tokens provide access to deploy agents. Protect tokens carefully and implement token rotation policies. Consider limiting View/Edit access to dedicated deployment personnel.
{% endhint %}

| Permissions | Description                                                                                                                                | Roles Example                                                                                                                                                                                                                                                                                                          |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| None        | Cannot view the **Agent Installations** page (**Inventory** → **Endpoints** → **Installations)**.                                          | <ul><li>SOC Tier-1 Analyst: Installation packages are not relevant for alert triage. Tier-1 analysts don't need to see deployment packages.</li><li>Threat Hunter: Installation packages are not relevant for hunting activities. Hunters focus on detection, not deployment.</li></ul>                                |
| View        | View the Agent Installations page for installation packages, status, and tokens.                                                           | <ul><li>SOC Tier-2 Analyst: May be useful for understanding agent deployment during investigations. Can help identify if an endpoint has an outdated installer.</li><li>SOC Tier-3 Analyst: Rarely needed for investigations, but may provide context about agent deployment history and available versions.</li></ul> |
| View/Edit   | All view capabilities, plus actions such as generating a custom package, configuring installation parameters, and managing agent versions. | Security Engineer: Essential for managing agent deployment and distribution. Must see available packages to plan deployments.                                                                                                                                                                                          |

**Required and recommended permissions**

Consider adding the following permissions:

| Permissions               | Permission Level | Reason                                                                                                                                                                                                                                                                                                                               |
| ------------------------- | ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Agent Administrations     | View             | Required. Installation packages deploy agents to endpoints. Without endpoint visibility, users cannot assess deployment coverage or identify unmanaged endpoints. View/Edit: Agent upgrades (Agent Management sub-option) require knowing available installation packages. Installation and endpoint management are tightly coupled. |
| Agent Prevention Policies | View             | Recommended. Understanding which policies will apply to newly deployed agents helps ensure proper protection from deployment.                                                                                                                                                                                                        |
| Agent Groups              | View             | Strongly recommended. Deployment targeting uses groups. Understanding group structure is essential for planning phased rollouts.                                                                                                                                                                                                     |
| Agent Profiles            | View             | Strongly recommended. Installation packages may include profile configurations. Understanding profiles ensures correct agent configuration during deployment.                                                                                                                                                                        |
