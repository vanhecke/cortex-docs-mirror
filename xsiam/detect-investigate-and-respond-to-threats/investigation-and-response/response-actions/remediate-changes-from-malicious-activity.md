---
description: Use Cortex XSIAM to remediate endpoint changes caused by malicious activity.
---

# Remediate changes from malicious activity

When investigating cases and causality chains you might need to restore and revert changes made to your endpoints as result of a malicious activity. To avoid manually searching for the affected files and registry keys on your endpoints, you can request remediation suggestions.

{% hint style="warning" %}
To initiate remediation suggestions, you must have the following system requirements:

* An App Administrator, Privileged Responder, or Privileged Security Admin role permissions which include the remediation permissions.
* EDR data collection enabled.
* Agent version 7.2 or above on Windows endpoints.
{% endhint %}

### How to initiate remediation suggestions in Cortex XSIAM

1.  You can initiate a remediation suggestions analysis from the following places:

    *   In the **Cases** view, click the more options icon in the cases panel and select **Remediation Suggestions**.

        <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>Endpoints that are part of the <strong>Case</strong> view and do not meet the required criteria are excluded from the remediation analysis.</p></div>
    * In the **Causality View**:
      * Right-click any process node involved in the causality chain and select **Remediation Suggestion**.
      * Select **Actions →** **Remediation Suggestions**.

    Analysis can take a few minutes. You can minimize the analysis pop-up if desired while navigating to other pages.
2. Review the remediation suggestion summary and details.
3. Select one or more rows, right-click and select **Remediate**.
4.  Track your remediation process.

    Go to **Investigation & Response → Response → Action Center →** **All Actions** and locate your remediation process in the **Action Type** field. Right-click **Additional data** to open the **Detailed Results** window.

<details>

<summary>Field descriptions</summary>

<table><thead><tr><th width="193">Field</th><th>Description</th></tr></thead><tbody><tr><td>Original Event Description</td><td>Summary of the initial event that triggered the malicious causality chain.</td></tr><tr><td>Original Event Timestamp</td><td>Timestamp of the initial event that triggered the malicious causality chain.</td></tr><tr><td>Endpoint Name</td><td>Hostname of the endpoint.</td></tr><tr><td>IP Address</td><td>IP address associated with the endpoint.</td></tr><tr><td>Endpoint Status</td><td>Connectivity status of the endpoint.</td></tr><tr><td>Domain</td><td>Domain or workgroup to which the endpoint belongs, if applicable.</td></tr><tr><td>Endpoint ID</td><td>Unique ID assigned by Cortex XSIAM that identifies the endpoint.</td></tr><tr><td>Suggested Remediation</td><td><p>Action suggested by the remediation scan for you to apply to the causality chain process:</p><ul><li>Delete File.</li><li>Restore File.</li><li>Rename File.</li><li>Delete Registry Value.</li><li>Restore Registry Value.</li><li><p>Terminate Process</p><p>Available when selecting Remediation Suggestions for a node in the Causality View.</p></li><li><p>Terminate Causality</p><p>Terminate the entire causality chain of processes that have been executed under the process tree of the listed Causality Group Owner (GCO) process name.</p></li><li><p>Manual Remediation</p><p>Requires you to take manual action to revert or restore.</p></li></ul></td></tr><tr><td>Suggested Remediation Description</td><td>Summary of the remediation suggestion to apply to the file or registry.</td></tr><tr><td>Remediation Status</td><td>Status of the applied remediation.</td></tr><tr><td>Remediation Date</td><td>Displays the timestamp of when all of the endpoint artifacts were remediated. If missing a successful remediation, the field will not display the timestamp.</td></tr></tbody></table>

</details>
