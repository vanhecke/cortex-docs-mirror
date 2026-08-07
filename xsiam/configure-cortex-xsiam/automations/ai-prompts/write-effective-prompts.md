---
description: Tips for creating effective AI prompts.
---

# Write effective prompts

AI prompts enhance your playbooks with the reasoning capabilities of a Large Language Model (LLM). By adding an AI prompt, you can automate complex cognitive work such as summarizing massive raw logs, normalizing disparate data types into standard formats, and performing deep-dive threat feasibility analysis. These tasks transform raw incident data into actionable intelligence in seconds.

While highly capable at processing information, an AI prompt is a focused, single-step instruction. It is designed to work with the data already available in your issue context JSON. Unlike an autonomous AI Agent, a prompt task is not self-executing; it cannot independently browse the live internet, search for external issues, or trigger outgoing actions such as sending emails. Instead, it processes and interprets data within your playbook, generating high-quality outputs that you then use to drive subsequent automated actions and decision branches.

**AI prompt capabilities and limitations**

Understanding what an AI prompt can and cannot do is essential for building effective automations. While the following table provides some common examples, you can use AI prompts for various other functions as well.

| What AI Prompts can do                                                           | What AI Prompts cannot do                                                                                    |
| -------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------ |
| Summarize and report For example: Write emails or create structured reports.     | Take action For example: Cannot send emails or independently search for new issues.                          |
| Extract and normalize For example: Pull specific data (like IOCs) from raw text. | Access the internet For example: Cannot access URLs or live websites; you must provide the content.          |
| Analyze context For example: Evaluate high-severity cases or analyze threats.    | Create logic For example: Cannot create conditional branches on its own; it requires a follow-up logic step. |

**Best practices for prompt construction**

To ensure the LLM provides reliable, accurate, and cost-effective results, use these strategies:

* Provide clear instructions: Explicitly state the task, such as extracting Indicators of Compromise (IOCs) or analyzing a post.
* Use precise context keys: To save on costs and prevent errors, map inputs to specific keys (for example, `${issue.creation_date}`) instead of passing the entire issue object.
* Use the optimizer: Click the **Optimize** button in the prompt editor to refine wording and improve consistency using research-backed logic.

**Bring live data to your prompts**

Connect your prompts to live playbook data to make them dynamic and contextual by doing the following.

* Weave variables inline: Add variables to your prompt text to provide context for the data, such as "Which issues were created before `${date}`?" or Analyze the following post: `${PostKey}`.
* Map to context: The placeholders appear in the **Extracted Inputs** list. Click the **{ }** icon to map them to a specific existing playbook data path (for example, mapping `${PostKey}` to `${incident.raw_log_content}`).

{% hint style="info" %}
An AI prompt cannot create new context keys. It can only refer to existing keys. The output key is the only key an AI prompt can create. If a variable such as `${PostKey}` is not mapped to existing context data, it cannot be used in the prompt.
{% endhint %}

**Follow up with logic**

Because an AI prompt cannot make decisions or execute tasks autonomously, it should be followed by a logic step in a playbook.

{% hint style="info" %}
The LLM's response is always returned in a text format, even if you explicitly ask the LLM to return a structured format such as JSON. Therefore, the subsequent task in your playbook will have to parse the response to extract the relevant data.
{% endhint %}

For example, add a conditional task or parsing script immediately after the prompt to check the AI's text output. Once the response is parsed, if the AI's verdict is Malicious, the playbook can then branch to trigger a script that blocks an indicator or escalates a ticket to Critical.

**Use built-in prompts**

To get started quickly, you can use these out-of-the-box example prompts designed to handle common security workflows, which can be used as-is or customized to fit your specific needs.

<table><thead><tr><th width="141.328125">Prompt Name</th><th width="125.109375">Use Case</th><th>Prompt Text</th></tr></thead><tbody><tr><td>Vulnerability Report Summary</td><td>Analyze scan results to prioritize remediation.</td><td><p>You are analyzing a vulnerability scan report <strong><code>${report_id}</code></strong>. Please analyze the provided vulnerability scan results in detail.</p><p>For each identified vulnerability:</p><ul><li>Describe the vulnerability clearly, including its type, affected service/component, and any relevant technical details.</li><li>Assess severity based on industry-standard metrics (e.g., CVSS score or equivalent).</li><li>Evaluate exploitability, noting whether known public exploits exist and how easily the vulnerability could be leveraged in practice.</li><li>Recommend remediation or mitigation steps to address the issue (e.g., patching, configuration changes, compensating controls).</li><li><p>Then, prioritize all vulnerabilities based on a combination of:</p><ol><li>Exploitability (known exploits, attack complexity, likelihood of exploitation).</li><li>Severity (potential impact if exploited).</li><li>Exposure level (e.g., internet-facing systems, critical internal services).</li><li>Provide a ranked list of vulnerabilities with a clear explanation of why each one should be prioritized. If applicable, highlight quick wins — high-risk vulnerabilities that can be easily fixed.</li></ol></li></ul></td></tr><tr><td>Malware Report Summary</td><td>Transform sandbox execution logs into a structured IR report.</td><td><p>Analyze the following malware sandbox execution report <strong><code>${report_id}</code></strong> and provide a comprehensive, structured analysis:</p><ul><li>Summarize the malware behavior across the entire attack kill chain (Initial Access -> Execution -> Persistence -> Privilege Escalation -> Defense Evasion -> Credential Access -> Discovery -> Lateral Movement -> Collection -> Exfiltration -> C2).</li><li>Map relevant behaviors and activities to the MITRE ATT&#x26;CK framework where applicable.</li><li>Highlight any notable techniques, unusual behaviors, or key insights from the malware execution.</li><li>List any IOCs observed (domains, IPs, hashes, file paths, etc.).</li><li>Provide remediation recommendations based on observed behavior.</li><li>Suggest additional investigation steps or telemetry to collect if needed.</li><li>The final output should be detailed, well-structured, and actionable for incident response teams.</li></ul></td></tr><tr><td>Issue Summary and Remediation</td><td>Provide clear steps for resolving a security alert.</td><td>Provide detailed remediation steps for the security alert <code>${issue}</code> in a professional, well-structured format.</td></tr></tbody></table>
