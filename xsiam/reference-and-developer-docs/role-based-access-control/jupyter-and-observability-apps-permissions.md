---
description: Configure permissions to use Jupyter and Observability applications.
---

# Jupyter and Observability apps permissions

The following permissions enable users to use Jupyter and Observability applications.

{% hint style="warning" %}
### Caution

Usage and management: The permissions allow users to use and access existing application instances. If a user needs to manage, install, configure, or delete application instances, they must be granted the separate Apps permission under the Configurations menu. For more information, see [Apps - Instance permissions](../configuration-permissions#UUID-6cdf81f3-ce41-0fe9-5b3b-08c9f7ecd29f).
{% endhint %}

**Jupyter Notebook permissions**

An interactive notebook environment for creating and running Python-based analyses and automations. Jupyter Notebooks let you explore security data, build custom analytics, and prototype detections.

{% hint style="warning" %}
### Caution

Jupyter Data Access (SBAC): Granting access to Jupyter does not bypass dataset restrictions. Users must have the appropriate Scope-Based Access Control (SBAC) dataset permissions to query specific data via the Cortex SDK within their notebooks.
{% endhint %}

For more information, see [Notebooks](../../detect-investigate-and-respond-to-threats/investigation-and-response/notebooks).

| Component | Description                                                                                                                                                       | Roles Example                                                                                                                                                                                                                                                                                                                                                           |
| --------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| None      | No access to Jupyter Notebooks.                                                                                                                                   | <ul><li>SOC Analyst Tier-1: Focus on issue triage.</li><li>SOC Analyst Tier-2: Standard investigation tools are sufficient. Consider View/Edit if the team performs advanced analysis.</li></ul>                                                                                                                                                                        |
| View/Edit | Full access to Jupyter Notebooks, including installing, creating, editing, saving, and exporting notebooks. You can also execute Python code and access datasets. | <ul><li>SOC Analyst Tier-3: Advanced investigations often require custom analysis, data exploration, and ad-hoc queries.</li><li>Threat Hunter: Critical - Notebooks are essential for hypothesis-driven hunting, custom analytics, and data exploration.</li><li>Security Engineer: Develops custom detection logic, automation scripts, and analysis tools.</li></ul> |

**Jupyter Notebook - required and recommended permissions**

Consider adding the following permissions:

| Permission          | Permission Level                 | Reason                                                                                                                                                                                 |
| ------------------- | -------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Query Center        | View or View/Edit                | <ul><li>View: Required to run XQL queries from notebooks via Cortex SDK.</li><li>View/Edit: Strongly recommended to save and manage queries created in notebooks.</li></ul>            |
| Dataset Permissions | N/a                              | Various. Control which datasets are queryable from notebooks.                                                                                                                          |
| Query Library       | Enabled                          | Strongly recommended to access and save queries.                                                                                                                                       |
| Cases & Issues      | View or View/Edit                | <ul><li>View: Strongly recommended to view cases and issues data for correlation in notebooks.</li><li>View/Edit: Recommended to create/update cases from notebook analysis.</li></ul> |
| Threat Intel        | View                             | Strongly recommended to enrich data with threat intelligence in notebooks.                                                                                                             |
| Playbooks           | Enabled with checkboxes selected | Enabled with **Playbooks** and **Create Playbooks** selected. Recommended to reference and develop playbooks from notebooks.                                                           |
| Scripts             | Enabled with checkboxes selected | Enabled with **Scripts** and **Create Scripts** selected. Recommended to reference and develop scripts alongside notebooks.                                                            |
| Detection Rules     | View/Edit                        | Recommended to view and create detection rules for analysis.                                                                                                                           |
| Forensics           | View/Edit                        | Recommended to access the forensics data for analysis and initiate forensic action.                                                                                                    |
| Action Center       | View/Edit                        | Recommended to view and execute response actions.                                                                                                                                      |

**Observability**

Observability provides infrastructure and application monitoring capabilities within Cortex XSIAM, leveraging Prometheus-based metrics collection, alerting, and visualization through Grafana integration.

{% hint style="info" %}
### Note

Observability is a Beta feature and is still subject to changes. To enable the feature in your tenant, contact your Customer Support Team.
{% endhint %}

| Component | Description                                                                                                           | Roles Example                                                                      |
| --------- | --------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------- |
| None      | No access to Observability.                                                                                           | SOC Analyst Tier-1, 2, and 3, and Threat Hunters who do not need tool development. |
| View/Edit | Full access to Observability, including access to the Observability interface, View Prometheus UI, and Alert Manager. | Security Engineers: Require full access for tool development and configuration.    |

**Observability - required and recommended permissions**

Consider adding the following permissions:

| Permission          | Permission Level  | Reason                                                                                                                         |
| ------------------- | ----------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| Broker VM           | View or View/Edit | Strongly recommended to view Broker VMs hosting Observability collectors and configure Observability collectors on Broker VMs. |
| Alert Notifications | View/Edit         | Recommended to configure alert notifications from Observability alerts.                                                        |
| Data Sources        | View/Edit         | Recommended to manage data sources that feed into Observability.                                                               |
| Cases & Issues      | View/Edit         | Recommended to correlate Observability alerts with security cases and create cases from Observability findings.                |
| Audit               | View              | Recommended to review audit logs for Observability configuration changes.                                                      |
