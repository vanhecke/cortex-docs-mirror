---
description: >-
  Use Cortex XSIAM Digital Risk Protection to identify external threats,
  exposure, and brand-related risks.
---

# Digital Risk Protection

Organizations face significant challenges in safeguarding their brand and digital assets from threats such as credential theft and brand impersonation. Using our comprehensive asset inventory, along with embedded intelligence and automation, Cortex XSIAM Digital Risk Protection discovers and helps you mitigate the following risks:

*   **Brand risk domains**

    Brand risk domains pose a threat to organizations because they can be used by threat actors to deceive customers, partners, or employees by impersonating a legitimate brand or application. These domains can be used for phishing attacks, spreading malware, launching social engineering campaigns, or other fraudulent activities. Additionally, malicious brand risk domains can also be used to steal sensitive information such as login credentials, financial data, or intellectual property.
*   **Leaked credentials**

    Leaked Credentials pose a risk to organizations by providing unauthorized access to sensitive systems and data, leading to data breaches, financial losses, and reputation damage.

    Cortex XSIAM focuses on externally reported credential leaks, specifically surfacing those that have occurred within the last six months.

### How to enable Digital Risk Protection

Digital Risk Protection is **disabled** by default. You can enable it by enabling the Brand Risk Domains and Brand Risk Leaked Credentials attack surface rules. When enabled, these rules generate issues that include brand risk domain and leaked credential information on the issue details panel.

1. Navigate to **Modules** → **Attack Surface** → **Policies** → **Attack Surface Rules**.
2.  Filter the list of attack surface rules by **ASM Issue Categories = Brand Protection**.

    ![drp-rules.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-d5bcfa3e6526973c524178a240aadeb39ce7b171%2F39ecc0b3eff443b8e67dbbc9020e2e82c364966cbe648f2fff34b15715dd25a7.png?alt=media)
3. Select either or both rules, right-click and select **Enable**.

{% hint style="info" %}
### Note

Both of these attack surface rules are based on the attributed domain assets that appear in the asset inventory. If there are no attributed domains in your inventory, Cortex XSIAM will not generate Digital Risk Protection findings and issues.
{% endhint %}
