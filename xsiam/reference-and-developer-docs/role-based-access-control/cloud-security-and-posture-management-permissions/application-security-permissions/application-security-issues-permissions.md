---
description: Configure Application Security issue permissions in Cortex XSIAM.
---

# Application Security - Issues permissions

Issues display security findings discovered across your code repositories, container images, and CI/CD pipelines. To view Issues, go to **Modules** → **Application Security** → **Issues**, and select one of the issues, such as IaC Misconfigurations, vulnerabilities, and Secrets.

| Permission | Description                                                                                                                                                                                                                         | Roles Example                                                                                                                                                                                                                                                              |
| ---------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| None       | No access to Application Security Issues.                                                                                                                                                                                           | SOC Tier-1 Analyst: Focus on issue triage and initial case response. Application Security findings are not part of their primary workflow.                                                                                                                                 |
| View       | Read-only access to all issue categories. Users can browse, filter, search, and export issues. They can view issue details and findings. They cannot change issue status, assign issues, create exclusions, or trigger remediation. | <ul><li>SOC Tier-2 and 3 Analysts: SOC Tier-2 analysts may need to investigate code-related cases or correlate AppSec findings with security issues.</li><li>Threat Hunter: Needs to correlate code-level findings with threat intelligence and attack patterns.</li></ul> |
| View/Edit  | Full access to manage and remediate issues. Includes all View capabilities plus: change issue status, assign issues, create exclusions, trigger remediation, perform bulk operations, and add comments.                             | Security Engineer: Responsible for triaging, assigning, and remediating AppSec issues.                                                                                                                                                                                     |

**Required and recommended permissions**

Consider adding the following permissions:

| Permission     | Permission Level  | Reason                                                                                                                                                                               |
| -------------- | ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Query Center   | View or View/Edit | <ul><li>View: Recommended. Run XQL queries on issue data for advanced investigation.</li><li>View/Edit: Recommended. Execute custom queries against AppSec issue datasets.</li></ul> |
| Cases & Issues | View or View/Edit | <ul><li>View: Recommended. Link AppSec issues to incident cases for correlation.</li><li>View/Edit: Recommended. Create incident cases directly from AppSec issues.</li></ul>        |
| Dashboards     | Enabled           | View AppSec issue summary widgets on dashboards.                                                                                                                                     |
