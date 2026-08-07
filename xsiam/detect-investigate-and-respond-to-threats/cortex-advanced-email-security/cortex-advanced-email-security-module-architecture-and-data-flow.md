---
description: >-
  The Cortex Advanced Email Security module, a cloud-native system, integrates
  multiple components to ingest, analyze, and respond to email-borne threats
  effectively.
---

# Cortex Advanced Email Security module architecture and data flow

The Cortex Advanced Email Security module is composed of several logical components, deployed in a cloud-native architecture. These components work together to ingest, analyze, and respond to email-borne threats.

![Simplified\_Email\_Security\_Architecture\_\_2\_.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-d543e1cf518c9d3d9c0940e3a30c4467a1747b3e%2Fa6bfccbd461fb732860c13341fef2bd4e0af61eb236e0ae7264847fc03cb37b8.png?alt=media)

<details>

<summary>Data collector</summary>

The data collector connects to the email platform via secure APIs to ingest message metadata, content, URLs, attachments, authentication verdicts, and user context (for example, group membership, privilege level). Collection occurs on a continuous basis with support for incremental deltas where applicable.

</details>

<details>

<summary>Detection engines</summary>

The module supports a multi-layered detection architecture composed of three distinct detection engines, each focused on a different analytical layer:

* Artifact-based engine
  * Analyzes discrete components embedded in the email such as file attachments and URLs.
  * Leverages hash matching, sandbox integration (where available), and URL reputation systems to identify known or behaviorally malicious artifacts.
* Metadata Analytics engine
  * Evaluates risk based on email metadata, sender-recipient relationship history, header anomalies, and identity context (for example, VIP status, role, group associations).
  * Detects impersonation, spoofing, newly seen senders, and anomalous communication patterns based on statistical baselining and heuristic rules.
  * Surfaces signals associated with business email compromise (BEC), supply chain impersonation, and domain lookalikes.
* LLM-based engine
  * Processes the plain-text and HTML content of the email using large language models.
  * Extracts semantic signals such as urgency, intent, emotional tone, and topic-based impersonation(for example, finance, HR, IT support).
  * Feeds these high-level attributes into a broader social graph used to understand message deviation from historical tone and role-based communication patterns.
  * Enhances detection of sophisticated phishing and text-only social engineering attacks that evade traditional signatures.

</details>

<details>

<summary>Issue processing and correlation layer</summary>

This layer normalizes output from the detection engines into a standardized issue format. It then correlates multiple issues into cases where shared indicators, for example, sender, URL, or theme, are identified. This layer also assigns a Score (using SmartScore) and enrichment metadata for downstream workflows.

</details>

<details>

<summary>Response engine</summary>

This engine executes response actions either automatically based on policy or manually via analyst intervention. It supports message removal, sender blocking, and false positive handling where platform permissions allow. All actions are logged with timestamp, executor, and result status.

</details>

<details>

<summary>User interface and admin console</summary>

The module includes a web-based management interface for the following:

* Viewing Issues and case timelines
* Investigating threat artifacts
* Configuring detection policies
* Managing exclusions and remediation rules
* Monitoring dashboard statistics and risky user profiles

</details>
