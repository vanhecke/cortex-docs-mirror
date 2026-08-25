---
description: Learn about out-of-the-box and custom cloud security rules in Cortex XSIAM.
---

# Cloud security rules

Cloud security rules are a set of conditions that apply to a specific cloud, code, or host resource. They define security detection logic or XQL queries used to identify threats or misconfigurations. Cloud security rules are designed to examine specific attributes within asset configurations to determine if those configurations could lead to threats. The rules are checked against all matching assets in your environment and findings are generated if resources matching the rule criteria are found.

<img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-731bbe021b75aab2718930e6cd47c792265e6f19%2Fca4e9362b3c90385e03eedbc236e96b75bb7f5aa83ed4cfc27052b4a7c4b2293.png?alt=media" alt="image1.png" width="343">

Cloud includes out-of-the-box cloud security rules and allows you to create custom cloud security rules:

| **Rule type**             | **Description**                                                                                                                                                                                                                                                                             |
| ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Out-of-the-box (OOTB)** | <p>The out-of-the-box rules (or “Default” rules) are rule-based and heuristic-based (using AI and machine learning).</p><p>The out-of-the-box cloud security rules are based on security research, CIS benchmarks, customer requests, and Palo Alto Network’s internal threat research.</p> |
| **Custom**                | You can create custom cloud security rules and use them in rule-based cloud security policies. See LINK.                                                                                                                                                                                    |

**Findings**

Findings are proactively gathered from your cloud environment to provide security context and are often non-actionable on their own. For example: “Workload X is attached to a role that grants access to databases”.

For more information about findings, see [Issues, findings, and events](../../detect-investigate-and-respond-to-threats/investigation-and-response/case-concepts/issues-findings-and-events) and [Review findings](../../detect-investigate-and-respond-to-threats/investigation-and-response/review-findings).

{% hint style="info" %}
### Note

Findings are only generated for OOTB rules.
{% endhint %}
