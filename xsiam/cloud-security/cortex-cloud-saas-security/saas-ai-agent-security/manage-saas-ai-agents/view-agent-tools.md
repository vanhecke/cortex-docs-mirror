---
description: View tools connected to SaaS AI agents in Cortex XSIAM.
---

# View Agent Tools

The SaaS Agent Tools security page moves beyond assessment of tools to the real security surface the—Tool Wrapper (or "Agent Tool" instance). This is the configuration layer where an agent author defines how a tool is used. This analysis often reveals risks like overprivileged access, or insecure credentialing that arise here and not in the underlying function code.

An Agent Tool is a specific instance of a tool being utilized by a specific agent. It acts as a wrapper that encapsulates:

1. Metadata Aliases: Custom names and descriptions provided by the agent author Configuration Settings: How the tool is pointed at specific data stores or environments
2. Authentication/Identity: Whether the tool executes using a System Credential, a specific Service Account, or prompts the User on-the-fly.

The SaaS Agent Tool page and dashboard focuses exclusively on posture risks introduced by the misconfiguration of the Agent Tool Wrapper layer.

<img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2FEFjdVlNgadB1hh9hGVo3%2Funknown.png?alt=media&#x26;token=ac5762a3-f0a9-4cc6-ad51-8968247b3c00" alt="" height="361" width="624">

Utilize the SaaS Agent tools widgets to view the potential risks introduced. These widgets provide insights into the total number of Providers and the Risk Breakdown. Select any provider from the page view to see a detailed breakdown of the following:

* Overview: Provides detailed information information on the tool Metadata
* AI Ecosystem: This node-based graph shows the specific Parent Agent and all the Datastores and API connections accessed by the Tool.
* Related Agents: Lists linked agents using this specific tool configuration.

<img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2FMfq4641ZGXqP5uBTl4g8%2Funknown.png?alt=media&#x26;token=fb8f927c-3042-4e5d-be79-938fd5e336db" alt="" height="411" width="624">
