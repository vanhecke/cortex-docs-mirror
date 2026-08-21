---
description: Manage access to Cortex XSIAM analytics configuration and related settings.
---

# Cortex XDR Analytics permissions

Controls access to the Analytics Engine configuration page through **Settings** → **Configurations** → **Cortex-Analytics**.

{% hint style="warning" %}
### Caution

This permission strictly controls access to enable or configure the backend Analytics engines. It does not control analytics rules management. Analytics rules (such as BIOCs and Correlation rules) are managed through the Detection Rules permission under the Threat Management section
{% endhint %}

### On-demand analytics

Cortex XDR Analytics (on-demand analytics) includes the following:

* Cortex Analytics Engine: Analyzes your endpoint data to develop a baseline and raise Analytics and Analytics BIOC alerts when anomalies and malicious behaviors are detected.
*   Identity Analytics: Allows the Cortex Analytics engine to aggregate and display user profile details, activities, and alerts related to a user-based Analytics type alert and Analytics BIOC rule during an investigation.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Notice</h3><p>Requires the Identity Analytics add-on.</p></div>
* AI Detection & Response: Gain visibility into AI/ML usage in the cloud with a new dashboard that highlights related issues and cases.

For more information, see [Cortex XSIAM - Analytics](../../../onboard-cortex-xsiam/deployment-steps/cortex-xsiam-analytics).

| Permission | Description                                                                                                                         | Roles Example                                                                                                                                                                                   |
| ---------- | ----------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| None       | No access to the **Cortex-Analytics** page.                                                                                         | SOC Tier-1 Analyst: No need to access or modify analytics configuration.                                                                                                                        |
| View       | Read-only access to the **Cortex-Analytics** page. Can see the status, but the enable buttons are disabled.                         | <ul><li>SOC Tier-2 and 3 Analysts: Should understand analytics settings during investigations</li><li>Threat Hunter: May need to understand analytics coverage during threat hunting.</li></ul> |
| View/Edit  | Full access to the **Cortex-Analytics** page, including enabling Cortex Analytics, Identity Analytics, and AI Detection & Response. | Security Engineer: Often responsible for tuning analytics detection settings                                                                                                                    |

### Required and recommended permissions

Consider adding the following permissions:

| Permission            | Permission Level | Reason                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| --------------------- | ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Detection rules       | View             | <ul><li>View: View analytics rules (BIOC, Correlation) that the analytics engine processes. Strongly Recommended.</li><li>View/Edit: Consider View/Edit if creating and modifying analytics rules. Recommended.</li></ul><div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>If users need to create or modify these rules, they must have View/Edit for Detection Rules and View/Edit for the Query Center.</p></div> |
| Agent Administrations | View             | View agent count and status. Strongly Recommended.                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| Cases & Issues        | View             | Analytics-generated alerts create cases that feed into case management. Strongly Recommended.                                                                                                                                                                                                                                                                                                                                                                                        |
| Auditing              | View             | Track analytics configuration changes for compliance. Recommended.                                                                                                                                                                                                                                                                                                                                                                                                                   |
| Dashboards            | Enabled          | View analytics dashboards showing detection coverage and engine performance. Recommended.                                                                                                                                                                                                                                                                                                                                                                                            |
| Forensics             | View             | Investigate analytics-generated alerts with forensic data. Recommended.                                                                                                                                                                                                                                                                                                                                                                                                              |
| Host Insights         | View             | Correlate analytics detections with host-level context. Recommended.                                                                                                                                                                                                                                                                                                                                                                                                                 |
| Action Center         | View             | View response actions triggered by analytics-generated issues. Recommended.                                                                                                                                                                                                                                                                                                                                                                                                          |
