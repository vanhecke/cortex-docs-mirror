---
description: Add AI Prompt tasks to Cortex XSIAM playbooks for AI-assisted automation.
---

# Add AI Prompt tasks

AI prompt tasks enable automated interaction with the Cortex XSIAM built-in Large Language Model (LLM) as a single step in a playbook. AI prompt tasks contain a prompt with inputs and outputs that guide the LLM to perform specific actions and provide structured results. For example, use an AI prompt task to prompt the LLM to identify malware categories.

You can add the same AI Prompt task more than once to a playbook. Each instance saves its settings locally.

From the Task Library, choose system AI prompt tasks with well-defined prompts for common use cases. Duplicate and edit these tasks, or create a custom AI prompt task for your needs.

{% hint style="info" %}
### Tip

For guidance on structuring your prompts, see [Write effective prompts](../../../ai-prompts/write-effective-prompts).
{% endhint %}

### System AI prompt tasks in the Task Library

The following are examples of available system AI-based tasks.

| Task name                    | Inputs                                                                            | Outputs                                                    | Prompt                           |
| ---------------------------- | --------------------------------------------------------------------------------- | ---------------------------------------------------------- | -------------------------------- |
| `IssueSummaryAndRemediation` | <p><code>issue</code><br>The issue details sent to the LLM for summarization.</p> | <p><code>llm.summary</code><br>The LLM output summary.</p> | See the expandable prompt below. |
| `MalwareReportSummary`       | <p><code>report_id</code><br>The report ID sent to the LLM for summarization.</p> | <p><code>llm.summary</code><br>The LLM output summary.</p> | See the expandable prompt below. |
| `VulnerabilityReportSummary` | <p><code>report_id</code><br>The report ID sent to the LLM for summarization.</p> | <p><code>llm.summary</code><br>The LLM output summary.</p> | See the expandable prompt below. |

<details>

<summary>IssueSummaryAndRemediation prompt</summary>

You are an experienced Security Operations Center (SOC) analyst with a deep understanding of security alert analysis and remediation. Your task is to provide detailed, actionable steps for remediating the security alert that has been provided. First, review the details of the security alert, including the Security Alert and the assessed Alert Severity level. Then, outline the key steps you would take to investigate and remediate the alert, referencing relevant security best practices, frameworks, or industry standards as appropriate. Once you have outlined the steps, provide a clear, concise, and easy-to-follow set of remediation instructions. Your answer should be tailored to the specific security alert and its severity level, and should include any relevant references to security guidelines or resources. Remember to be thorough and precise in your response, as the security analyst will be relying on your guidance to address the alert effectively.

**General Scope and Instructions:**

1. Only provide remediation steps for the alert.
2. Do not provide generic or unrelated recommendations outside of the alert scope.

**Example:**

### Alert Summary

This alert is for a `{ALERT_TYPE}` on the `{AFFECTED_SYSTEM}` system, with a severity level of `{ALERT_SEVERITY}`.

### Potential Impact

If this alert is not addressed, it could lead to significant consequences, such as data breaches, system vulnerabilities, or potential service disruptions.

### Remediation Steps

1. \[Step 1 remediation instruction]
2. \[Step 2 remediation instruction]
3. \[Step 3 remediation instruction]

### Recap

Add a recap section.

Provide detailed remediation steps for the security alert `${alert}` in a professional, well-structured format.

</details>

<details>

<summary>MalwareReportSummary prompt</summary>

You are a highly specialized Malware Analyst, with deep expertise in analyzing and interpreting sandbox execution reports. Your knowledge spans the entire malware execution lifecycle, from initial infection vector to command-and-control and post-exploitation behavior. You are also an expert in mapping malicious activity to the MITRE ATT\&CK framework.

Your sole purpose is to analyze and summarize malware sandbox reports. You do not answer questions or generate responses unrelated to malware behavior analysis in the context of sandbox data. Focus exclusively on:

* Extracting detailed insights from sandbox execution logs and artifacts.
* Mapping observed behaviors to MITRE ATT\&CK techniques.
* Identifying indicators of compromise (IOCs) and tactics, techniques, and procedures (TTPs).
* Only document IOCs with suspicious or malicious context. Do not list known or benign indicators.
* Describing malware behavior across the whole kill chain.
* Recommending remediation actions and next investigation steps.

Analyze the following malware sandbox execution report and provide a comprehensive, structured analysis:

* Summarize malware behavior across the entire attack kill chain: Initial Access → Execution → Persistence → Privilege Escalation → Defense Evasion → Credential Access → Discovery → Lateral Movement → Collection → Exfiltration → C2.
* Map relevant behaviors and activities to the MITRE ATT\&CK framework where applicable.
* Highlight notable techniques, unusual behaviors, or key execution insights.
* List observed IOCs, including domains, IPs, hashes, and file paths.
* Provide remediation recommendations based on observed behavior.
* Suggest additional investigation steps or telemetry to collect if needed.

The final output should be detailed, well-structured, and actionable for incident response teams.

</details>

<details>

<summary>VulnerabilityReportSummary prompt</summary>

You are a vulnerability assessment analyst responsible for reviewing and analyzing vulnerability scan results provided in JSON format. Your objective is to thoroughly examine the scan data, deliver a comprehensive vulnerability analysis, and prioritize vulnerabilities that must be addressed immediately.

**General Instructions:**

1. Only provide recommendations related to the data in the report.
2. Do not provide generic recommendations that are not directly related to the data in the report.

**Steps for Analysis:**

Perform your assessment considering the following key criteria:

1. **Criticality**
   * Consider vulnerability severity ratings: Critical, High, Medium, Low, and Informational.
   * Evaluate CVSS base scores and severity definitions.
2. **Exploitability**
   * Evaluate how easily the vulnerability can be exploited remotely or locally.
   * Analyze exploitation complexity, including attack vector, required privileges, and user interaction.
   * Identify active exploits or proof-of-concept exploits in the wild.
3. **Environmental Factors**
   * Consider asset importance, such as business-critical servers, database hosts, and publicly exposed systems.
   * Assess affected system network accessibility, including internal and externally exposed systems.
   * Reflect on relevant regulatory compliance requirements, such as PCI-DSS, HIPAA, and GDPR.

**Deliverable:**

Provide your analysis in the following structured format:

**1. Executive Summary**

* Briefly summarize overall risk status based on scan results.

**2. Detailed Vulnerability Analysis**

For each vulnerability identified:

* Plugin Name & ID
* CVE Identifier, if applicable
* Affected Asset(s)
* Severity Rating & CVSS Base Score
* Exploitability Assessment:
  * Describe the likelihood and complexity of exploitation.
  * Reference known active exploits.
* Environmental Impact:
  * Explain potential business impact based on asset role and exposure.
  * Highlight compliance risks or regulatory impacts.

**3. Prioritized Recommendations**

* Provide a clearly ranked list of vulnerabilities to remediate, with high priority first.
* Justify prioritization using criticality, exploitability, and environmental factors.
* Suggest remediation actions for each vulnerability.

**Important Considerations:**

* Clearly justify each decision to ensure transparency.
* Maintain concise yet informative language for technical and managerial audiences.
* Emphasize vulnerabilities posing immediate and significant risk to the organization's security posture.

Please analyze the provided vulnerability scan results in detail. For each identified vulnerability:

* Describe the vulnerability clearly, including its type, affected service or component, and relevant technical details.
* Assess severity using industry-standard metrics, such as CVSS score or equivalent.
* Evaluate exploitability, including known public exploits and practical exploitation difficulty.
* Recommend remediation or mitigation steps, such as patching, configuration changes, or compensating controls.

Then, prioritize all vulnerabilities using:

1. Exploitability, including known exploits, attack complexity, and likelihood of exploitation.
2. Severity, including potential impact if exploited.
3. Exposure level, including internet-facing systems and critical internal services.

Provide a ranked list of vulnerabilities and explain each priority. Highlight quick wins where applicable: high-risk vulnerabilities that are easy to fix.

</details>

### Add system AI prompt tasks

System AI prompt tasks include predefined prompts, inputs, and outputs. You cannot edit or remove them. Set inputs using issue context or specific values.

To change a system task, duplicate it from the AI Prompts page. Then edit the copy.

{% stepper %}
{% step %}
From the **Task Library** pane, select **AI Prompts**.
{% endstep %}

{% step %}
On the **System** tab, find the relevant built-in AI prompt task.

Use the search box to find a prompt with free text.
{% endstep %}

{% step %}
Drag the selected AI prompt task to the playbook editor.

The **Task Details** pane opens. **Task Type** is automatically set to **`AI Task`**.
{% endstep %}

{% step %}
Configure the AI prompt task parameters.

**AI prompt task parameter tabs**

| Tab          | Settings                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Inputs**   | <p>System AI prompt task input definitions, including name, description, and type, are fixed and non-editable.</p><p>Includes:</p><ul><li><strong>Prompt</strong>: The prompt passed to the LLM with the inputs. System prompts are not editable. Inputs use <strong><code>${}</code></strong> placeholders that are filled with values. Expand the prompt for improved readability.</li><li><strong>Extracted Inputs</strong>: Set input values using a context path or a specific value. Mandatory inputs have an asterisk.</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| **Outputs**  | AI prompt task outputs in system AI prompts can not be edited. If you need to edit the output options, duplicate the system AI prompt and edit the copy.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| **Advanced** | <p>Includes:</p><ul><li><strong>Register as case timeline record</strong>: If enabled, the results of the task execution appear as a record in the case timeline. If enabled, you must enter a <strong>Record name.</strong> You have the option of adding an <strong>Effective time</strong>, <strong>Description</strong>, <strong>Tags</strong>, and marking the record as evidence and adding an evidence comment.<br><strong>NOTE</strong>: Only enter an <strong>Effective time</strong> if you want the same exact time recorded every time the playbook task executes.</li><li><strong>Extend context</strong>: Appends extracted action results to the context. For example, <code>"newContextKey1=path1::newContextKey2=path2"</code> returns <code>[path1:'aaa',path2: 'bbb', newContexKey1: 'aaa',newContextKey2:'bbb']</code>.</li><li><strong>Ignore outputs</strong>: When <code>true</code>, outputs are not stored in context, except extended outputs.</li><li><strong>Execution timeout (seconds)</strong>: Sets the command execution timeout.</li><li><p><strong>Indicator Extraction mode</strong>: Choose when to extract indicators:</p><ul><li><strong>Use system default</strong>: The default setting.</li><li><strong>None</strong>: Do not extract indicators.</li><li><strong>Inline</strong>: Extract before other playbook tasks.</li><li><strong>Out of band</strong>: Extract while other tasks run.</li></ul></li><li><strong>Mark results as note</strong></li><li><strong>Run without a worker</strong></li><li><strong>Skip this branch if this script/playbook is unavailable</strong></li><li><strong>Quiet Mode</strong>: Tasks do not display inputs or outputs, or extract indicators. Errors and warnings remain documented. Turn quiet mode on or off at the task or playbook level.</li></ul> |
| **Details**  | <p>Includes:</p><ul><li><strong>Tag the result with</strong>: Add a tag to the task result. Use the tag to filter War Room entries.</li><li><strong>Task description (Markdown supported)</strong>: Describe the task. You can include context data objects. For example, use a recipient email address in a communication task. The object value reflects the context whenever the task runs.</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| **On Error** | <p>Includes:</p><ul><li><strong>Number of retries</strong>: Number of retries after an error. Default: <code>0</code>.</li><li><strong>Retry interval (seconds)</strong>: Wait time between retries. Default: <code>30</code> seconds. The maximum is <code>800</code> seconds (13.3 minutes). Values above <code>800</code> are limited to <code>800</code>.</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
{% endstep %}

{% step %}
Click **OK**.
{% endstep %}

{% step %}
Connect the system AI prompt task by dragging and dropping a wire.

To perform actions based on task results, add a conditional task immediately afterwards.
{% endstep %}
{% endstepper %}

#### Add custom AI prompt tasks

Create or edit a custom AI prompt task. You can also edit a duplicated system AI prompt.

{% stepper %}
{% step %}
From the **Task Library** pane, select **AI Prompts**.
{% endstep %}

{% step %}
Choose one of the following options:

* On the **System** tab, select **Local AI Prompt** to create a task.
* On the **Custom** tab, find an existing custom task. Select **Local AI Prompt** to create a task.

To use an existing custom task, drag it to the playbook editor.

{% hint style="info" %}
Selecting **Local AI Prompt** creates a local task version in your playbook. Future Prompts Library updates do not sync to this task.

Choose **Local AI Prompt** when workflow-specific logic must remain unchanged. This prevents future improvements, such as prompt refinements, security patches, and model optimizations, from changing its behavior.
{% endhint %}
{% endstep %}

{% step %}
Configure the AI prompt task in the **Task Details** pane.

1.  Set the AI prompt task name.

    The name must start with a letter. It cannot contain spaces or special characters.
2. Set the AI prompt task parameters.

**Custom AI prompt task parameter tabs**

| Tab          | Settings                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Inputs**   | <p>Expand this section to show:</p><ul><li><strong>Prompt</strong>: Define a natural language prompt passed to the LLM with inputs. Mark input placeholders with square brackets, such as <code>[input]</code>.</li><li><strong>Extracted Inputs</strong>: Lists inputs defined in the prompt, in the same order. Set each input with a context path or specific value. You can set an input as a variable using <code>${&#x26;lt;input name&#x26;gt;}</code>. Mandatory inputs have an asterisk.</li></ul><p>The <strong>Prompt Helper</strong> also provides prompt tips.</p><div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>NOTE:</strong> Tenants in selected regions can select an AI model. Available models include Flash, Thinking, and Pro. For supported models and regions, see <a href="../../../../../../learn-about-cortex-xsiam/agentic-ai-in-cortex-xsiam#frontier-models">Frontier Models</a>.</p></div>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| **Outputs**  | <p>Includes:</p><ul><li><strong>Context path:</strong> The issue field the task results are saved to. For example, <strong>issue.AIseverity</strong>. This enables tasks that follow to locate the correct context and use that context as input.</li><li><strong>Description</strong> (Optional): Description of the output.</li><li><strong>Type</strong> (Optional): <strong>Unknown</strong>, <strong>String</strong>, <strong>Number</strong>, <strong>Date</strong>, <strong>Boolean.</strong></li><li><p><strong>Use Structured output</strong> (Optional)</p><p>You can configure the AI prompt task output to enforce a specific JSON structure by providing a custom JSON schema. This ensures the model's response matches your required format, allowing subsequent playbook tasks to successfully use the output.</p><p>When you select <strong>Use structured output</strong> in the <strong>Outputs</strong> tab you are provided with a JSON template that you can edit or replace entirely.</p><p><strong>Schema rules</strong></p><p>Available top-level keys:</p><ul><li>“type”</li><li>“properties”</li><li>“required”</li><li>“additionalProperties”</li></ul><p>The top-level “type” must be “object.”</p><p>A nested “type” must be one of the following</p><ul><li>array</li><li>boolean</li><li>integer</li><li>null</li><li>number</li><li>object</li><li>string</li></ul><p>If your JSON includes an invalid type, an error message appears and provides a list of the correct types.</p></li></ul> |
| **Advanced** | <p>Includes:</p><ul><li><strong>Extend Issue context</strong>: Appends extracted action results to the context. For example, <code>"newContextKey1=path1::newContextKey2=path2"</code> returns <code>[path1:'aaa',path2: 'bbb', newContexKey1: 'aaa',newContextKey2:'bbb']</code>.</li><li><strong>Ignore outputs</strong>: When <code>true</code>, outputs are not stored in context, except extended outputs.</li><li><strong>Execution timeout (seconds)</strong>: Sets the command execution timeout. Default: <code>10</code> seconds.</li><li><p><strong>Indicator Extraction mode</strong>: Choose when to extract indicators:</p><ul><li><strong>Use system default</strong>: The default setting.</li><li><strong>None</strong>: Do not extract indicators.</li><li><strong>Inline</strong>: Extract before other playbook tasks.</li><li><strong>Out of band</strong>: Extract while other tasks run.</li></ul></li><li><strong>Mark results as note</strong></li><li><strong>Run without a worker</strong></li><li><strong>Skip this branch if this script/playbook is unavailable</strong></li><li><strong>Quiet Mode</strong>: Tasks do not display inputs or outputs, or extract indicators. Errors and warnings remain documented. Turn quiet mode on or off at the task or playbook level.</li></ul>                                                                                                                                                                                                           |
| **Details**  | <p>Includes:</p><ul><li><strong>Tag the result with</strong>: Add a tag to the task result. Use the tag to filter War Room entries.</li><li><strong>Task description (Markdown supported)</strong>: Describe the task. You can include context data objects. For example, use a recipient email address in a communication task. The object value reflects the context whenever the task runs.</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| **Timers**   | <p>Includes:</p><ul><li><strong>Timer.start</strong>: Trigger sending a message or survey to recipients. Change this trigger or add a trigger for <code>Timer.stop</code> or <code>Timer.pause</code>. Select the trigger timer field from the drop-down list.</li><li><strong>Add Trigger</strong>: Add other trigger timer fields from the drop-down list.</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| **On Error** | <p>Includes:</p><ul><li><strong>Number of retries</strong>: Number of retries after an error. Default: <code>0</code>.</li><li><strong>Retry interval (seconds)</strong>: Wait time between retries. Default: <code>30</code> seconds. The maximum is <code>800</code> seconds (13.3 minutes). Values above <code>800</code> are limited to <code>800</code>.</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |

**Prompt Helper tips**

<details>

<summary>Be clear and specific</summary>

Tell the AI exactly what you need. Treat it like a new team member. More precise requests produce better results.

**What to do**

Avoid vague requests such as “Tell me about malware.” Specify:

* **Goal**: For example, summarize, identify, explain, or generate ideas.
* **Topic**: For example, phishing emails, vulnerability reports, or security policies.
* **Details**: For example, last week's incidents, non-technical executives, or critical threats.

**Examples**

* Bad prompt: `Tell me about that virus ${VirusName}.`
* Good prompt: `Analyze the attached malware report from ${Path} and summarize the key indicators of compromise (IOCs) for our incident response team.`

</details>

<details>

<summary>Provide context and background</summary>

Give the AI the full picture. Background information explains the reason for your request.

**What to do**

Include relevant details, such as:

* **Role**: For example, “Act as a security analyst,” “You are a CISO,” or “As a technical writer.”
* **Audience**: For example, a technical audience, a board meeting, or a general user.
* **Key information**: For example, recent network scan results or new compliance regulations.

**Examples**

* Bad prompt: `Write a report.`
* Good prompt: `You are a cybersecurity consultant. Write a brief executive summary report for our CEO detailing the top three critical vulnerabilities identified in our recent penetration test report from ${Path} and suggest immediate actions.`

</details>

<details>

<summary>Ask for the desired format</summary>

State the required output structure. This reduces reformatting work.

**What to do**

* **Lists**: “Provide a bulleted list of...” or “Give me 5 key points.”
* **Tables**: “Create a table with columns for \[X], \[Y], and \[Z].”
* **Summaries or reports**: “Generate a concise summary,” “Draft a formal report,” or “Write a brief email.”
* **Length**: “Keep it under 200 words,” or “Provide a detailed analysis.”

**Examples**

* Bad prompt: `What are the latest threats?`
* Good prompt: `List the top 5 emerging cyber threats relevant to financial services, with a brief explanation for each, presented as a bulleted list.`

</details>

<details>

<summary>Use few-shot prompting</summary>

Use few-shot prompting to teach a pattern or format without extensive fine-tuning. It is useful for tasks with limited data.

**What to do**

Provide several examples of the required input and output.

**Example prompt**

`You are a SOC analyst that needs to enrich CVE ${CVEId}, use the following structure:`

**Sample structures**

* **CVE Description**: Apache Struts 2.5.x before 2.5.14, 2.3.x before 2.3.34, and 2.x.x before 2.3.x.x.x.x allows remote attackers to execute arbitrary code via a crafted Content-Type header.
* **CVSS**: 9.8 (Critical). **Impact**: Remote Code Execution (RCE), potential for complete system compromise, data theft, and denial of service. Affects web applications built with Apache Struts, widely used in enterprise environments.
* **Risk Score**: 10/10 — Extremely High. Exploitability is high due to public exploits and widespread usage of the affected software.
* **CVE Description**: Microsoft Windows MSHTML Remote Code Execution Vulnerability. This vulnerability exists in the way the MSHTML engine handles specially crafted files. An attacker could host a specially crafted website or send a specially crafted document that, when opened, could allow remote code execution.
* **CVSS**: 8.8 (High). **Impact**: Remote Code Execution (RCE), arbitrary code execution in the current user context. Affects all Windows versions. It could lead to system compromise and data exfiltration. Phishing campaigns often exploit it.
* **Risk Score**: 9/10 — Very High. This is a widespread target. User interaction makes it a common attack vector.

</details>
{% endstep %}
{% endstepper %}

3. Click **Save**.

The AI prompt task appears in the playbook editor.

4. Connect the task by dragging and dropping a wire.

To perform actions based on task results, add a conditional task immediately afterwards.

5. Click **Save Playbook**.

#### AI prompt task error handling

Configure error handling, including a return value when an AI prompt task fails. Failures can occur when the LLM times out, returns invalid output, exceeds a threshold, or is disabled.

The War Room logs the failure reason.

{% hint style="info" %}
If an AI prompt task returns **`504 Error`** with status **`DEADLINE_EXCEEDED`**, it likely requires more processing time than the default allows.

Open the AI task's **Task Details** pane. Select **Advanced**, then increase **Execution timeout (seconds)** for the prompt complexity and expected response time. Complex tasks, such as a complete vulnerability report, may require increasing the default from 10 seconds to 120 seconds or more.
{% endhint %}
