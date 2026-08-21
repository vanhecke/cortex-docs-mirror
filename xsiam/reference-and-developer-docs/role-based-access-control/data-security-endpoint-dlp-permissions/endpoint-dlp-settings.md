---
description: Configure endpoint Data Loss Prevention settings in Cortex XSIAM.
---

# Endpoint DLP Settings

Endpoint DLP Settings provide global options that dictate the overarching behavior of the Data Loss Prevention (DLP) engine across all endpoints.

Users access Endpoint DLP Settings by going to **Modules** → **Data Security** → **Endpoint Data-in-Motion Rules** → **Endpoint DLP Settings**.

{% hint style="warning" %}
### Caution

Modifications made on this page, such as changing the default action (allow/block file movement), adjusting rule suppression thresholds, or altering browser extension installation modes, will globally affect all Data-in-Motion Rules and overall DLP enforcement. Proceed with caution when adjusting thresholds.
{% endhint %}

| Permission | Description                                                                                                                                                                                                                                | Recommended Roles                                                                                                                                                                                                                   |
| ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| None       | Users cannot access the **Endpoint DLP Settings** page. These users cannot see any DLP settings, browser extension configurations, or default action settings.                                                                             | <ul><li>SOC Tier-1 Analyst: DLP settings are outside Tier-1 scope.</li><li>DLP engine settings management is outside the IT infrastructure administration scope.</li></ul>                                                          |
| View       | Read-only access to view current settings. Users can view the default action configuration, corporate account domain names, browser extension installation modes, rule suppression thresholds, and user interaction notification settings. | <ul><li>SOC Tier-2 and 3 Analysts: May need to review DLP settings when troubleshooting DLP-related cases/advanced analysis.</li><li>Threat Hunter: DLP settings are not typically relevant to threat hunting activities.</li></ul> |
| View/Edit  | Full control over the DLP engine settings. Users can modify the default action, add/remove corporate domains, change browser extension modes, adjust rule suppression thresholds, and configure user notifications.                        | <ul><li>Security Engineer: Responsible for configuring and tuning DLP settings.</li><li>Security Admin: Full administrative access to all DLP configurations.</li></ul>                                                             |

**Required and recommended permissions**

Endpoint DLP Settings act as the global baseline for the DLP engine. To safely modify these settings, administrators need visibility into the specific rules that enforce the data security posture and the agents that deploy them.

| Permission            | Permission Level | Reason                                                                                                                                                                                                                                      |
| --------------------- | ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Data-in-Motion Rules  | View             | Strongly recommended. Global DLP settings (like default actions and browser extensions) directly dictate how Data-in-Motion rules operate. Understanding the currently active rules provides critical context before making global changes. |
| Agent Administrations | View             | Strongly recommended. Recommended. DLP settings and browser extensions are deployed via the endpoint agent. Viewing agent statuses helps administrators verify that global DLP configurations are being successfully deployed.              |
| Data Classification   | View             | Recommended. Endpoint DLP Settings are closely related to the tenant's broader Data Classification configurations, which define what the DLP engine considers sensitive data.                                                               |
