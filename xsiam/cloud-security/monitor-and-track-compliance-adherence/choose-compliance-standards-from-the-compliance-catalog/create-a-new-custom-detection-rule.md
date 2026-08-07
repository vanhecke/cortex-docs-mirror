---
description: >-
  Create custom detection rules to evaluate assets against tailored compliance
  requirements.
---

# Create a new custom detection rule

Create custom detection rules to check your organization’s assets.

Creating custom detection rules give you the flexibility to define and enforce security best practices tailored to your organization's objectives, as well as regulatory requirements not already covered by the compliance standards in our catalog.

### Before you begin

Ensure you have a custom compliance control defined to associate the Custom Detection Rule to. For more information, see [Use a built-in or custom control](use-a-built-in-or-custom-control).

### Create a custom detection rule

1. Go to **Posture Management** → **Rules & Policies** → **Rules** → **Cloud Workload**.
2. In the **Cloud Workload Rules** page, click **Create Custom Rule**.
3. Enter the following settings:
   * **Rule name**: A descriptive name for the custom rule.
   * **Description**: An optional field for adding additional details or context about the rule, such as its purpose or intended behavior.
4. Select a **Scanner** to execute the Custom Detection Rule and its associated script. The options are:
   * **Agentless Disk Scan**
   * **Kubernetes Connector**
   * **XDR Agent**
5. Configure settings specific to the scanner you select.

<details>

<summary>Agentless Disk Scan settings</summary>

<table><thead><tr><th>Field</th><th>Description</th></tr></thead><tbody><tr><td>Operating System</td><td><p>The operating system targeted by the rule. The available options are:</p><ul><li>Linux</li><li>Windows</li></ul></td></tr><tr><td>Input file(s) path</td><td>The full file path for one or more files. For example, <strong><code>/nfs/an/disks/jj/home/dir/file.txt</code></strong></td></tr><tr><td>Define the Rule (Rego)</td><td><p>Use Rego to define the custom detection logic.</p><p>Use the default code in this box as a reference or starting point. Click <a href="https://www.openpolicyagent.org/docs/latest/policy-language/#learning-rego">read here</a> for more information how to use Rego syntax.<br><br>Example 1<br></p><pre><code>Code
"/var/log/auth.log":
{
"content": "Failed password for invalid user test from 192.168.1.1 port 22 ssh2\n",
"metadata":
{
"file_type": "file",
"gid": 1000,
"last_modified": 1737292449,
"permissions": 436,
"size": 6000,
"uid": 1001
},"path": "/var/log/auth.log"
}
Script
package
panw.complianceimport rego.v1
match contains {"msg": msg}
if {
authLogFile = input["/var/log/auth.log"
]
contains(authLogFile.content, "Failed password")
authLogFile.metadata.permissions == 436
authLogFile.metadata.size > 5000
msg := "Failed login attempts detected in /var/log/auth.log"}
Output
"match": [
{
"msg": "Failed login attempts detected in /var/log/auth.log"
},
]
</code></pre><p>Example 2</p><pre><code>Code
"/etc/passwd":
{
"content": "root0:0:root:/root:/bin/bash\nuser1:*:1001:1001:User One:/home/user1:/bin/bash\n",
"metadata": {
"file_type": "file",
"gid": 1001,
"last_modified": 1737292449,
"permissions": 644,
"size": 100,
"uid": 1002
},"path": "/etc/passwd"
}
Script
package
panw.complianceimport rego.v1
match contains {"msg": msg}
if {
passwdFile = input["/etc/passwd"]
passwdFile.metadata.file_type == "file"
passwdFile.metadata.permissions == 644
passwdFile.metadata.size &#x3C; 200
contains(passwdFile.content, ":*:")
msg := "Empty or suspicious password detected in /etc/passwd"}
Output
"match": [
{
"msg": "Empty or suspicious password detected in /etc/passwd"
},
]
</code></pre><p>Example 3</p><pre><code>Code
"/etc/shadow": {
"content": "root:$6$abc123$abc123abc123abc123abc123abc123abc123abc123abc123abc123abc123abc123abc123abc123abc123abc123:17542:0:99999:7:::",
"metadata": {
"file_type": "file",
"gid": 1001,
"last_modified": 1737292449,
"permissions": 640,
"size": 100,
"uid": 1002
},"path": "/etc/shadow"
}
Script
package
panw.complianceimport rego.v1
match contains {"msg": msg} if {
shadowFile = input["/etc/shadow"]
shadowFile.metadata.file_type == "file"
shadowFile.metadata.permissions != 600
shadowFile.metadata.size > 30
contains(shadowFile.content, "::")
msg := "Empty or weak password detected in /etc/shadow"}
Output
"match": [
{
"msg": "Empty or weak password detected in /etc/shadow"
},
]
</code></pre></td></tr></tbody></table>

</details>

<details>

<summary>Kubernetes Connector Settings</summary>

<table data-header-hidden><thead><tr><th></th><th></th></tr></thead><tbody><tr><td>Field</td><td>Description</td></tr><tr><td>Kubernetes Resources</td><td><p>From the drop down, select one or more from the following:<br></p><ul><li><strong>Namespaces</strong>: Logical partitions within a Kubernetes cluster that allow resource isolation and organization.</li><li><strong>ReplicaSets</strong>: Ensures a specified number of pod replicas are running at all times by automatically scaling up or down.</li><li><strong>Deployments</strong>: Manages and control pod replicas by providing declarative updates for ReplicaSets, enabling rolling updates and rollbacks.</li><li><strong>StatefulSets</strong>: Deploys stateful applications that require persistent identity and storage, ensuring stable pod names and ordered scaling.</li><li><strong>DaemonSets</strong>: Ensures that a copy of a specific pod runs on all or selected nodes in the cluster, commonly used for logging and monitoring agents.</li><li><strong>Jobs</strong>: Runs one-time or short-lived workloads that complete execution and then terminate.</li><li><strong>CronJobs</strong>: Defines scheduled jobs that run at specified times or intervals, similar to Linux cron jobs.</li><li><strong>ClusterRoles</strong>: Defines permissions at the cluster level, granting access to resources across all namespaces.</li><li><strong>Roles</strong>: Defines permissions within a specific namespace, restricting access to resources within that namespace.</li><li><strong>RoleBindings</strong>: Associates a role with a user, group, or service account within a specific namespace.</li><li><strong>ClusterRoleBindings</strong>: Associates a cluster role with users, groups, or service accounts at the cluster-wide level.</li><li><strong>NetworkPolicies</strong>: Defines rules that control the communication between pods and other network entities within the cluster, enforcing security restrictions.</li><li><strong>Services</strong>: Exposes a set of pods as a network service, allowing stable communication within and outside the cluster.</li><li><strong>ServiceAccounts</strong>: Provides an identity for pods to authenticate against the Kubernetes API, allowing controlled access to resources.</li><li><strong>Endpoints</strong>: Represents the actual network addresses of the pods backing a service, dynamically updated as pods start or stop.</li><li><strong>Ingresses</strong>: Manages external access to services, providing HTTP/HTTPS routing, load balancing, and SSL termination.</li><li><strong>ConfigMaps</strong>: Stores non-sensitive configuration data in key-value pairs, allowing applications to retrieve configuration without modifying container images.</li><li><strong>Secrets</strong>: Securely stores and manage sensitive data, such as API keys, passwords, and certificates, in an encrypted format.</li><li><strong>Nodes</strong>: Defines the physical or virtual machines that run the workloads in a Kubernetes cluster.</li></ul></td></tr><tr><td>Define the Rule (Rego)</td><td><p>All custom Rego policies in Cortex must follow this pattern:</p><pre><code>package panw.compliance
import rego.v1
match contains {"msg": msg} if {
# Your detection logic here
msg := "Description of the finding"
}
</code></pre><div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>NOTE</strong></p><p>The custom rule must use the <code>match</code> term (not <code>deny</code> or others) to function properly.</p></div></td></tr></tbody></table>

</details>

<details>

<summary>XDR Agent Settings</summary>

| Field                    | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Custom Code Execution    | <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>NOTE</strong></p><p>Enable this setting for the scanner to perform custom compliance checks by executing user-defined Python scripts.</p><p><br>Only users with the following roles can enable or disable Custom Code Execution:</p><ul><li>Account Admin</li><li>Instance Administrator</li><li>Deployment Admin</li><li>Privileged Security Admin<br></li></ul></div><p>Click Confirm to accept the following terms:</p><ul><li>The Python scripts you provide will be executed in your cloud environment(s).</li><li>This capability is solely for the purpose of enabling you to define the compliance check rules for your cloud environment(s). Any other purposes are expressly prohibited.</li><li>Any actions involving WRITE, MODIFY, or DELETE operations of your cloud environment(s) are strictly prohibited. It is your responsibility to ensure that your custom Python scripts only perform read-only operations of your cloud environment(s) explicitly for compliance check purposes.</li><li>You are solely responsible for the quality, content, use, and execution results of your Python script. You assume all risks and liabilities arising from executing your Python script(s), including any potential errors, damages, or consequences resulting from its use.</li></ul><p>After you confirm accepting the terms, the rest of the XDR Agent settings appear.</p> |
| Operating System         | <p>The operating system targeted by the rule. The available options are:</p><ul><li>Linux</li><li>Windows</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| Define the Rule (Python) | <div data-gb-custom-block data-tag="hint" data-style="warning" class="hint hint-warning"><p><strong>Important</strong></p><p>Use Python to define the custom detection logic.</p><p>This section supports syntax highlighting and validation (IntelliSense) to help users create accurate and efficient rules.</p><p>Use the default code in this box as a reference or starting point.</p><p>The custom Python scripts are intended to be executed exclusively for compliance checks and validations. To ensure the scripts are used properly and no security risks or unintended changes occur, the system implements the following restrictions and safeguards:</p><ul><li>Only a predefined set of Python libraries and functions required for compliance checks are available for use. Libraries or functions that enable writing, deleting, or creating operations are excluded.</li><li>Only authorized users with specific permissions can create or update custom scripts. This ensures that only trusted individuals can define compliance checks.</li></ul></div>                                                                                                                                                                                                                                                                                                                                                                                                               |

</details>

6. For **Compliance Violation Severity**, define the severity level of the compliance violation to ensure proper categorization and prioritization. Possible values are:
   * Critical
   * High
   * Medium
   * Low
   * Informational
7. For **Compliance Controls**, assign the rule to one or more existing compliance controls.

{% hint style="info" %}
**NOTE**

Only Custom Detection Rules (not built-in rules) can be assigned to custom controls.
{% endhint %}

   a. Click **Add**.\
   b. Select a custom compliance control from the list.\
   c. Click **Assign**.

8. For **Remediation**, you can optionally define the remediation steps to address any detected misconfiguration.
9. Click **Create**.\
   \
   The new rule appears in the Rules List.\
   \
   You can now use the rule as a check to either create an issue or monitor adherence to a specific requirement.

### Create an issue

Under **Posture Management → Policies → Cloud Workload**, add the Custom Detection Rule to a **Policy**. This policy automatically runs the rule and creates an issue if the check fails.

### Monitor compliance adherence

Under **Posture Management → Compliance → Catalogs → Standards**, create a custom standard that includes the custom control associated with the Custom Detection Rule, and then create an assessment profile that runs the custom standard. You can then monitor the compliance results in a report. For more information, see [Monitor and track compliance adherence](..).
