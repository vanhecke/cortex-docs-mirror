---
description: >-
  Cortex API security distributes responsibilities across SOC analysts, security
  practitioners, and workload owners.
---

# Personas workflow

The workflow outlines the responsibilities of each persona to detect, assess, protect, and secure the API assets across the organization, focusing on the main API security elements:

* Visibility
* Posture Management & Risk Profiling
* Threat Detection & Response

<details>

<summary>SOC analyst</summary>

**Responsibility**: Real-time threat detection & response

The SOC analyst is the key to identifying and investigating API vulnerabilities and attacks within an organization.

**Steps**:

1. **Visibility**: Reviews the **Cases & Issues** module for new attacks.
2.  **Investigate**: Select a case or an issue, analyze involved APIs and their context, analyze request/response details, and distinguish normal from malicious activity.

    To conduct a deeper investigation to eliminate or contain the threat, investigate the security issue
3. **Decide and Act**: Determine if it's a true attack. If so, initiate an immediate response (often outside the UI) and flag for fixes. Close the case in the UI.

</details>

<details>

<summary>Security practitioner</summary>

**Responsibility**: Proactive posture management & risk reduction

The security practitioner uses the UI for continuous risk assessment and orchestration of remediation.

**Steps**:

1. **Overview of API landscape**: In the **API Security Management** dashboard, review emerging threats and understand the overall security of the API landscape.
2. **Analyze APIs and Risks**: Navigate to API endpoints to view all APIs, their risk factors (e.g., internet exposure, sensitive data, authentication/encryption status), and posture issues. Drill down for details.
3. **Manage OpenAPI Specifications**: Access the OpenAPI specification files. Review findings on the specification file itself (misconfigurations) and verify API traffic conformance to its specification.
4. **Assign Remediation**: Consolidate all findings, group them by application owner, and distribute tasks (via email/tickets with timelines) for fixes (code, gateway, specification updates).

</details>

<details>

<summary>Workload owner</summary>

**Responsibility**: Application security accountability

The workload owner acts on security tasks, primarily outside the UI.

**Steps**:

1. **Receive Tasks**: Get detailed security tasks and timelines from the security practitioner.
2. **Implement Fixes**: Apply necessary fixes to application code, API configurations, or OpenAPI specifications.
3. **Ensure Compliance**: Bring their APIs and assets into alignment with security standards.

</details>
