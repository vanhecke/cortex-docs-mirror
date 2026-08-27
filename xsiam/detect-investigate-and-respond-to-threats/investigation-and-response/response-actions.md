---
description: >-
  Use Cortex XSIAM response actions to contain threats and remediate affected
  endpoints.
---

# Response actions

To assist you with your investigation, Cortex XSIAM provides response actions for investigating and remediating endpoints. For example, if you detect a compromised endpoint you can isolate it from your network. This action prevents the endpoint from communicating with other internal or external devices, and thereby reducing an attacker’s mobility on your network.

For response actions that rely on the Cortex XDR agent, the following table describes the supported platforms and minimum agent version. A dash (—) indicates that the setting is not supported.

<table><thead><tr><th width="157">Module</th><th width="97">Windows</th><th width="103">Mac</th><th width="95">Linux</th><th>iOS</th></tr></thead><tbody><tr><td><p><strong>Initiate a Live Terminal Session</strong></p><p>Initiates a remote connection to an endpoint, enabling you to investigate and respond to security events. Using <code>Live Terminal</code> you can manage files in the file system, manage active processes, and run operating system or Python commands.</p></td><td><p>✓</p><p>Agent 6.1 and later</p></td><td><p>✓</p><p>Agent 7.0 and later</p></td><td><p>✓</p><p>Agent 7.0 and later</p></td><td>—</td></tr><tr><td><p><strong>Isolate an Endpoint</strong></p><p>Halts all network access on the endpoint except for traffic to Cortex XSIAM. This prevents a compromised endpoint from communicating with other internal or external devices.</p></td><td><p>✓</p><p>Agent 6.0 and later</p></td><td><p>✓</p><p>Agent 7.3 and later on macOS 10.15.4 and later</p></td><td><p>✓</p><p>Agent 7.7 and later</p></td><td><p>Agent for iOS 9.1 and later.</p><p>This feature is only available on supervised iOS devices where the Network Shield is enabled.</p></td></tr><tr><td><p><strong>Run Scripts on an Endpoint</strong></p><p>Allows executing Python 3.7 scripts on your endpoints directly from Cortex XSIAM, including out-of-the-box scripts or your own Python scripts and code snippets.</p></td><td><p>✓</p><p>Agent 7.1 and later</p></td><td><p>✓</p><p>Agent 7.1 and later</p></td><td><p>✓</p><p>Agent 7.1 and later</p></td><td>—</td></tr><tr><td><p><strong>Remediate Changes from Malicious Activity</strong></p><p>Investigates suspicious causality process chains and cases on your endpoints, and provides suggested actions for remediating processes, files and registry keys on your endpoint that were changed as a result of malicious activity.</p></td><td><p>✓</p><p>Agent 7.2 and later</p></td><td>—</td><td>—</td><td>—</td></tr><tr><td><p><strong>Search and Destroy Malicious Files</strong></p><p>Searches for the presence of known and suspected malicious files on endpoints, and destroys the file on endpoints where it exists.</p></td><td><p>✓</p><p>Agent 7.2 and later</p></td><td><p>✓</p><p>Agent 7.3 and later on macOS 10.15.4 and later</p></td><td>—</td><td>—</td></tr></tbody></table>

{% hint style="warning" %}
Response actions are not supported for Android endpoints.
{% endhint %}
