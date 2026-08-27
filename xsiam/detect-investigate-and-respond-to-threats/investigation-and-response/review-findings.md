---
description: >-
  Review findings for an asset to gain insights into an asset’s posture status
  in Cortex XSIAM.
---

# Review findings

In Cortex XSIAM findings provide knowledge about an asset by leveraging the data we collect from various sources. This process helps build a more accurate and comprehensive understanding of the asset’s current state, including its configuration, behavior, and context within the environment. Additionally, findings provide visibility into potential exposures and vulnerabilities, contributing to a clearer assessment of the asset’s risk level. By continuously analyzing and updating findings, we can maintain an up-to-date view of the asset’s security posture and support more informed decision-making for detection, prioritization, and remediation efforts. For more information, see [Issues, findings, and events](case-concepts/issues-findings-and-events).

Click on a finding from any location in the UI to open the findings card. To view all findings, go to **Issues** → **Findings table**. You can also see findings for a specific asset by opening the asset card.

<details>

<summary>Show me more</summary>

![Findings.gif](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-1474019cb5765e3a904d682ef9415d7c690c6766%2Fe6fcd8a6704cee0bb26294e67a2688d47197a85e16040e7c99e024c6cd2c7813.gif?alt=media)

</details>

### Types of findings

The following table describes the different types of findings:

{% hint style="info" %}
### Note

Some finding types require the Cortex XSIAM Premium license, or any other XSIAM license with the Cloud Posture Security or Cloud Runtime Security add-on.
{% endhint %}

<table><thead><tr><th width="136">Type</th><th>Description</th></tr></thead><tbody><tr><td>Code</td><td>Discovery of security issues within application source code, such as bugs, logic flaws, and insecure coding practices.</td></tr><tr><td>Compliance</td><td>Discovery of compliance violations that do not adhere to the security standards for your organization.</td></tr><tr><td>Configuration</td><td>Discovery of incorrect settings or configurations in systems, applications, or devices that reduce the environment's resilience and increase the potential for compromise.</td></tr><tr><td>Data</td><td>Discovery of sensitive data misuse, secrets, and shadow data.</td></tr><tr><td>Identity</td><td>Discovery of suspicious user identities, highlighting authentication and access control to prevent unauthorized access and minimize the risk of over-permissive access rights that could lead to security breaches.</td></tr><tr><td>Malware</td><td>Discovery of malicious files within cloud workloads.</td></tr><tr><td>Posture</td><td>Discovery of posture risks that might expose critical assets to potential cyberattacks and operational disruption.</td></tr><tr><td>Vulnerability</td><td>Discovery of weaknesses or flaws in software or hardware that attackers can exploit to gain unauthorized access, disrupt operations, or steal data. Includes the Contextual Asset ID (e.g., the specific Image Name, Container Instance ID) to help distinguish if the vulnerability is a host OS issue or originates from a nested workload.</td></tr></tbody></table>

### Set up rules to trigger issues from findings

Findings themselves are not issues, but findings that match a specific logic can generate issues. You can also set up your own policies and rules to trigger issues when the following types of findings are recorded:

* Compliance, Malware, or Secrets findings, for more information, see [Cloud workload policies and rules](../../cloud-security/cloud-workload-policies-and-rules).
* Vulnerability findings, for more information, see [Vulnerability policies](../vulnerability-management/vulnerability-policies).

### Query findings data

You can query finding data in the `findings` data set.

**Example:** The following query searches for all findings for AssetA:

```programlisting
dataset = findings | filter xdm.finding.asset_name = "AssetA"
```
