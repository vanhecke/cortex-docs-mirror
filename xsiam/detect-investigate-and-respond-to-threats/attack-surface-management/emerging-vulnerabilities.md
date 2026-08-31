---
description: >-
  Identify external exposures linked to emerging vulnerabilities, zero-day
  exploits, and global threat events on the Emerging Vulnerabilities page in
  Cortex XSIAM.
---

# Emerging Vulnerabilities

{% hint style="info" %}
### Notice

Requires the ASM add-on
{% endhint %}

The **Emerging Vulnerabilities** page streamlines your response to global attack surface threat events and zero-day exploits by aggregating important information about threats and its impact on your organization in one place. From **Emerging Vulnerabilities**, you can accomplish the following:

* **Review a complete list of emergent and global threat events**, and quickly identify the events that impact your organization. The list displays key information about each threat, such as CVSS and EPSS scores, and is sorted by the **Last Policy Update** date.
* **Research a threat event**. Our security research team provides a threat summary, potential exploit consequences, previous exploit activity, and links to other reputable sources for additional information.
* **Assess the impact of a threat event on your organization**. Quickly identify services on your external attack surface impacted by emerging vulnerabilities. Review a detailed list of the affected software, turn on relevant attack surface rules, and access relevant issues, assets, and attack surface test results.
* **Build a Remediation Plan**. The **Emerging Vulnerabilities** page provides remediation guidance for each event and click-throughs to issues to begin remediation.

{% hint style="info" %}
### Note

You must have a role with Attack Surface Rules permission to access the **Emerging Vulnerabilities** page. When setting up Roles Based Access Control (RBAC), you can find Attack Surface Rules in the Detection & Threat Intel component.
{% endhint %}

How to view emerging vulnerabilities

1. Navigate to **Posture Management** → **Vulnerability Management** → **Emerging Vulnerabilities**.
2. Click anywhere in the row of a threat event to open the details page.
3. Review the information on this page to learn about the threat event and build a remediation plan for your organization.

<details>

<summary>Which vulnerabilities are included in Emerging Vulnerabilities?</summary>

Typically, an emerging vulnerability is a critical or high-risk vulnerability that allows threat actors direct access to assets, leading to widespread impact across corporate networks. Devices and applications impacted by such vulnerabilities are at risk of exploitation remotely over the public-facing internet. These threats often allow threat actors to gain remote control of systems.

Cortex XSIAM considers the following questions when evaluating the level of risk of a threat event and whether to include it on the Emerging Vulnerabilities page:

* Is it a vulnerability without a patch?
* Is it a “Known Exploitable Vulnerability” that has been weaponized by threat actors?
* Can it be exploited remotely over the internet in an unauthenticated manner?
* Is a proof of concept readily available? Has active exploitation in the wild been reported?
* How widespread is the impact of the vulnerability? Does it impact many organizations or is limited to a certain section of the industry?
* Is the vulnerability in an application or device that is routinely targeted by attackers?
* Does it have a vendor severity rating of “Critical” or “High”? Does it have a CVSS score of 9 or higher?
* Are there geo-political factors in play? (For example, is an APT targeting groups or individuals from specific countries or regions?)

</details>

<details>

<summary>How often is the Emerging Vulnerabilities page updated?</summary>

Our security research team creates and updates threat events in the **Emerging Vulnerabilities** page in the following situations:

* When a new threat event occurs and the security research team determines the event is critical enough to add to **Emerging Vulnerabilities**.
* When new information is discovered for existing threat events. The information on an Emerging Vulnerabilities page is updated frequently as a threat evolves and exploit details are made public.

</details>
