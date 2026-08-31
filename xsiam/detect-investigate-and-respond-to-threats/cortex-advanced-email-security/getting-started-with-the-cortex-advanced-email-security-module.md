---
description: >-
  Get started with Cortex XSIAM Advanced Email Security using the deployment
  workflow and setup requirements.
---

# Getting started with the Cortex Advanced Email Security module

{% hint style="warning" %}
### Prerequisites

Before you configure the Cortex Advanced Email Security module, ensure you have the following:

* Admin-level access to the target email platform
* Dedicated service account (recommended) for integration purposes (response actions)
* List of domains and mailboxes to be protected (to be used during the wizard configuration)
* Access to an internal phishing reporting mailbox (to collect user-reported phishing - optional)
*   API permissions to read mailbox data, manage remediation (if desired), and access user directories

    | Permission                 | Function                                                                                                                                                                                                                                                                                                                         |
    | -------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | User.Read.All              | Read the full profiles (e.g., department, manager, title) of all users. This is essential for providing context during threat analysis, such as identifying VIPs or spotting potential CEO fraud and impersonation.                                                                                                              |
    | Mail.ReadWrite             | <p>Primary permission for Advanced Email Security.</p><p>Read: Allows the application to scan and collect emails from all mailboxes for threat analysis.</p><p>Write: Allows the application to perform remediation actions, such as deleting a malicious email, moving it to junk, or modifying it to add a warning banner.</p> |
    | Directory.Read.All         | Get a complete list of all users, groups, and other directory objects. This is necessary to discover which mailboxes are part of the organization and require protection.                                                                                                                                                        |
    | AuditLog.Read.All          | Ingest Azure AD audit logs. This allows Advanced Email Security to correlate email-based threats with other suspicious activities in the tenant (e.g., a suspicious login followed by a malicious email, reported as phishing events).                                                                                           |
    | IdentityRiskyUser.Read.All | Access user risk data from Azure AD Identity Protection. This is a critical security signal, allowing Advanced Email Security to apply higher scrutiny to emails from an account that is flagged as at risk (e.g., credentials leaked).                                                                                          |
    | MailboxSettings.Read       | Read all user mailbox settings. This is crucial for detecting common attack techniques, such as an attacker setting up a malicious inbox rule or auto-forwarding rule to exfiltrate data.                                                                                                                                        |
    | ThreatSubmission.Read.All  | Read threat submissions made by the end-users (e.g., via the **Report Phishing** button in Outlook). This provides a valuable feed of human-identified threats directly into Advanced Email Security.                                                                                                                            |
    | ThreatSubmission.ReadWrite | Programmatically submit new threats detected by Advanced Email Security to Microsoft's security systems. This integrates our tool with the wider Microsoft 365 security ecosystem.                                                                                                                                               |
    | Mail.Send                  | Send security notifications and alerts. This is used to send a warning to the end-user about a high-priority threat that was detected and remediated.                                                                                                                                                                            |
    | People.Read.All            | Read users' relevant people lists (derived from communication patterns). This helps build a social graph to better detect anomalies and sophisticated impersonation or Business Email Compromise (BEC) attacks.                                                                                                                  |
    | Contacts.Read              | Read the contacts in all mailboxes. Similar to People.Read.All, this helps analyze communication patterns and identify when a trusted contact may be compromised or impersonated.                                                                                                                                                |
    | Domain.Read.All            | Read the organization's verified domains. This is essential for Advanced Email Security to accurately distinguish between internal and external senders and to detect email spoofing.                                                                                                                                            |
    | Application.Read.All       | Read the list of all applications registered in the tenant. This can be used as part of a broader security posture assessment to identify other potentially risky or misconfigured applications.                                                                                                                                 |
{% endhint %}

**Deployment workflow overview**

A typical deployment follows the following sequence.

1. Provisioning
   * Authenticate to Microsoft 365 as admin
   * Grant API access scopes to Cortex Advanced Email Security module
   * Select domains/mailboxes to protect
2. Verification
   * Confirm data ingestion
   * Generate sample test email for issuing validation
   * Review initial dashboard population
3. Configuration
   * Define phishing report address (optional)
   * Set up issue exclusions and remediation rules
4. Operation
   * Begin issue triage and investigation using issues table and email card view
   * Fine-tune detection rules over time
   * Monitor response actions and refine policies
