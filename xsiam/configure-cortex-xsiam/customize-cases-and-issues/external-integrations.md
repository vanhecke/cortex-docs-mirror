---
description: >-
  Integrate external threat intelligence and case management services with
  Cortex XSIAM.
---

# External integrations

You can integrate external threat intelligence services with Cortex XSIAM that provide additional verification sources for each key artifact in a case. Cortex XSIAM supports the following integrations:

<details>

<summary>Threat intelligence</summary>

| Integration | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| ----------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| WildFire    | <p>Cortex XSIAM automatically includes WildFire threat intelligence in the case and issue investigation.</p><p>WildFire detects known and unknown threats, such as malware. The WildFire verdict contains detailed insights into the behavior of identified threats. The WildFire verdict is displayed next to relevant <strong>Key Artifacts</strong> in the <strong>Cases</strong> page. See <a href="../../detect-investigate-and-respond-to-threats/investigation-and-response/investigate-files">Review WildFire analysis details</a> for more information.</p>                                                                                |
| VirusTotal  | <p>VirusTotal provides aggregated results from over 70 antivirus scanners, domain services included in the block list, and user contributions. The VirusTotal score is represented as a fraction. For example, a score of 34/52 means out of 52 queried services, 34 services determined the artifact to be malicious.</p><p>To view VirusTotal threat intelligence in cases, you must obtain the license key for the service and add it to the Cortex XSIAM <strong>Configuration</strong>. When you add the service, the relevant VirusTotal (VT) score is displayed in the <strong>Cases</strong> page under <strong>Key Artifacts</strong>.</p> |

</details>

<details>

<summary>Case management</summary>

| Integration                   | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| ----------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Third-party ticketing systems | To manage cases from the application of your choice, you can use the Cortex XSIAM API Reference to send issues and issue details to an external receiver. After you generate your API key and set up the API to query Cortex XSIAM, external apps can receive case updates, request additional data about cases, and make changes such as setting the status and changing the severity or assigning an owner. To get started, see the Cortex XSIAM API Reference guide. |

</details>
