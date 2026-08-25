---
description: >-
  Monitor, investigate, and respond to API attacks, threats, and security issues
  in Cortex XSIAM.
---

# Monitor and investigate API threats

Cortex XSIAM provides a comprehensive solution to counter API threats and attacks. It doesn't just address vulnerabilities, but actively protects against the misuse of legitimate API functions, mitigates risks from misconfigurations, and secures often-forgotten "shadow" or "zombie" APIs. By offering continuous visibility and monitoring, Cortex XSIAM ensures robust, proactive protection for all your APIs, safeguarding your organization against evolving and sophisticated threats.

Cortex XSIAM protects from the following threats:

| Module                               | Threat description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| ------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Advanced Threat Protection           | Advanced Threat Protection (ATP) is a comprehensive security feature designed to detect, prevent, and respond to sophisticated Web and API threats, ensuring robust protection for workloads against evolving risks.                                                                                                                                                                                                                                                                                                                                                                                                                   |
| Authentication bypass                | The Cortex XSIAM authentication bypass module protects against attacks that attempt to circumvent authentication controls through session manipulation, token exploitation, or credential abuse.                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Automation tools                     | Cortex XSIAM detects and protects against automated tools or services that scrape website contents such as Scriptable headless web browsers, command line tools, or HTTP libraries.                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| Cross-Site Scripting (XSS) injection | Cortex XSIAM protects against XSS attacks, in which malicious JavaScript snippets are injected into otherwise benign and trusted websites. In such attacks, attackers try to trick the browser into switching to a JavaScript context and executing arbitrary code.                                                                                                                                                                                                                                                                                                                                                                    |
| CVE exploits                         | Cortex XSIAM protects against exploitation attempts of known vulnerabilities (Common Vulnerabilities and Exposures (CVEs)).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| Malformed Traffic                    | Cortex XSIAM identifies and protects against HTTP requests with anomalies that are not expected from common web browsers.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| Injection attacks                    | Injection attacks are a form of attacks in which attackers attempt to insert malicious input into an application to manipulate its execution. For example, a code injection attack injects code which is interpreted by the application or other runtimes. Command and code payloads can either be injected as part of HTTP requests, or are included from local or remote files (also known as File Inclusion attacks).                                                                                                                                                                                                               |
| Known bots                           | Cortex XSIAM can identify legitimate bots that properly declare their identity and purpose, such as search engine crawlers and authorized web indexers. These bots follow standard protocols and provide verifiable operator information, however some of them might cause undesirable behaviors, such as spam, and you might prefer to block such bots.                                                                                                                                                                                                                                                                               |
| Offensive tools                      | Cortex XSIAM identifies offensive tools that scan web applications for known security vulnerabilities and misconfiguration, and exploit them.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| Sensitive data exposure              | <p>Cortex XSIAM protects workloads from providing responses that could expose sensitive data found in critical system files, including password hashes (/etc/shadow), user account information (/etc/password), and private encryption keys.</p><p>Such examples would be compromised accounts, credential stuffing, and ATO attacks.</p>                                                                                                                                                                                                                                                                                              |
| SQL injection (SQLi)                 | Cortex XSIAM protects against SQLi attacks, which can occur when an attacker successfully inserts a malicious SQL query into the input fields of a web application. A successful attack can read sensitive data from the database, modify data in the database, or run arbitrary commands.                                                                                                                                                                                                                                                                                                                                             |
| Identity-based attacks               | <p>Cortex XSIAM identifies and protects from compromised accounts, credential stuffing, and ATO attacks. These types of attacks involve exploiting stolen or weak login credentials to impersonate legitimate users and gain unauthorized access to accounts and systems.</p><p>The API inventory's category by type (e.g., login, sign-in, sign-up, register, create account, reset password) and sub-type (e.g., add to cart, show cart, general checkout page, add billing address, add credit card, gift card) is crucial. This enables a deeper investigation into potential discrepancies related to identity-based attacks.</p> |

**SOC analyst workflow**

The following workflow outlines a step-by-step action plan as a SOC analyst to monitor, investigate, and respond to API threats.

**SOC analyst role overview**

SOC analysts continuously monitor and analyze security incidents related to APIs. Their goal is to identify, investigate, and mitigate API endpoint attacks, ensuring API integrity, confidentiality, and availability. They prioritize issues based on severity and specific indicators.

* ISSUE DOMAIN: Security
* DETECTION METHOD: API Traffic Monitor
* SEVERITY: High or Critical

**SOC analyst action plan**

The following outlines the streamlined actions a SOC analyst takes when detecting an API threat:

**Step 1:** Initial examination (Cases & Issues):

* **Objective**: Quickly assess the type and severity of the API attack.
* **Actions**: Navigate to **Issues**, filter by key indicators, and review the high-level alert summary (timestamp, affected service, initial notes).

**Step 2:** In-depth analysis (Issue page - Overview tab):

*   **Objective**: Gather detailed attack context, identify affected assets, and collect evidence.

    The API security issues page provides a single window into every API security threat. You get full investigation capabilities that let you immediately drill down to understand the true impact of the attack. An important insight into the issue, you can see the specific details of the attacker and the credentials that were used. All the details included give you a deep understanding of the complete attack narrative.
* **Actions**:
  * **Affected Assets**: Identify targeted API endpoints; click to navigate to their detailed pages for granular review.
  * **Evidence**: Examine findings (request/response logs, payload, timestamps, source IP, user agent) to understand the attack vector.
  *   **Advance your investigation**: The issue page also provides you with advanced investigation options to further analyze the attack narrative.

      Select one of the options:

      *   **Trace the Actor**: Gain full visibility into the actor's complete interaction sequence by viewing all raw API traffic. This allows you to understand every step they took, ensuring nothing is missed in your analysis.

          Click **Run** to run a preconfigured XQL query.
      *   **Hunt for the Payload**: Search is extended to include encoded and modified variations of the attack payload across all API traffic. This comprehensive detection capability ensures you find every single instance of the attack attempt, regardless of how the payload was obscured or altered.

          Click **Run** to run a preconfigured XQL query.
      *   **Scope the Threat**: Access a chronological record of all historical security issues tied to this specific API endpoint. Analyzing this data allows you to quickly identify attack patterns and pinpoint inherent vulnerabilities in the endpoint, enabling targeted hardening and risk reduction.

          Click **Go**, which takes you directly to the **Issues** table to see all historic issues related to the attacked API endpoint.
      *   **Build the Attack Chain**: Instantly display all historical security issues previously triggered by this actor. This automatically generates a clear, chronological timeline of their malicious activities, enabling you to understand their patterns, escalation, and overall risk profile.

          Click **Run** to run a preconfigured XQL query.

      ![issues\_api\_endpoints\_page](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-8ef7ca319d1b96e99d8926fb6d51fac484264b28%2F6e95a27bdaee58920b60aafcc10f0d3b27adce0637cf037050d28dbd14daa5d9.png?alt=media)

**Step 3:** Refer to [Gain visibility and assess risk of API endpoints](gain-visibility-and-assess-risk-of-api-endpoints) for drilled-down details of the API data.

**Step 4:** Post-investigation actions & reporting:

* **Objective**: Mitigate the threat, prevent recurrence, and document findings.
* **Actions**:
  * **Reporting**: Create a detailed incident report (detection, attack type, assets, evidence, vulnerabilities, actions, lessons learned). Communicate findings to stakeholders.
  * **Improvement**: Conduct post-incident review, update policies/playbooks, and recommend security enhancements.
