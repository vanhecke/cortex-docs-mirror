---
description: >-
  Configure Cortex XSIAM Web and API Security profiles to detect, report, or
  block threats on Linux workloads.
---

# Set up Web and API Security profiles

{% hint style="info" %}
### Note

Web and API Security profiles and policies are currently a Beta feature.
{% endhint %}

You can configure Web and API Security profiles to provide comprehensive real-time detection and protection for web-based applications and APIs running on Linux-based workloads. These profiles can be applied to policies for such workloads.

For each setting that you want to override, clear the corresponding option to **Use Default**, and then select the setting of your choice.

{% hint style="info" %}
### Note

In this profile, the **Report** options configure the workload to report the corresponding malicious applications or APIs to Cortex XSIAM, without blocking them. The **Disabled** options configure the workloads to neither analyze nor report the corresponding malware or behavior.
{% endhint %}

1. Add a new profile and define basic settings.
   1. From Cortex XSIAM, select **Inventory** → **Endpoints** → **Policy Management** → **Prevention** → **Profiles**. Click **+Add Profile**, and select whether to create a new profile, or to import a profile from a file.
   2. Select the **Linux** platform, and **Web & API Security** as the profile type.
   3. Click **Next**.
   4. Enter a unique **Profile Name** for the profile. The name can contain only letters, numbers, or spaces, and must be no more than 30 characters. The name will be visible from the list of profiles when you configure a policy rule.
   5. (Optional) Enter a description that describes the intention or business purpose of the profile.
2.  Configure **Action Mode** options. If you choose **Enable**, you can then configure each item separately.

    | Item                       | Options                                                | More details                                                                                                                                                                                                                                                                                                                                                                                                                                   |
    | -------------------------- | ------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | Action Mode                | <ul><li>Enable</li><li>Disable</li></ul>               | When set to **Enable**, Cortex XSIAM performs the configured action for each of the options.                                                                                                                                                                                                                                                                                                                                                   |
    | XSS                        | <ul><li>Block</li><li>Report</li><li>Disable</li></ul> | <p>When Cortex XSIAM detects cross-site scripting (XSS) injection, it performs the configured action.</p><p>XSS attacks are attacks in which malicious JavaScript snippets are injected into otherwise benign and trusted websites. In such attacks, attackers try to trick the browser into switching to a JavaScript context and executing arbitrary code.</p>                                                                               |
    | SQL Injection              | <ul><li>Block</li><li>Report</li><li>Disable</li></ul> | <p>When Cortex XSIAM detects SQL injection (SQLi) attempts, it performs the configured action.</p><p>(SQLi) attacks can occur when an attacker successfully inserts a malicious SQL query into the input fields of a web application. A successful attack can read sensitive data from the database, modify data in the database, or run arbitrary commands.</p>                                                                               |
    | Injection Attacks          | <ul><li>Block</li><li>Report</li><li>Disable</li></ul> | <p>When Cortex XSIAM detects injection attacks, it performs the configured action.</p><p>Injection attacks are a form of attacks in which attackers attempt to insert malicious input into an application to manipulate its execution. Command and code payloads can either be injected as part of HTTP requests, or are included from local or remote files (also known as File Inclusion attacks).</p>                                       |
    | CVE Exploits               | <ul><li>Block</li><li>Report</li><li>Disable</li></ul> | When Cortex XSIAM detects known vulnerabilities (Common Vulnerabilities and Exposures (CVEs)), it performs the configured action.                                                                                                                                                                                                                                                                                                              |
    | Sensitive Data Exposure    | <ul><li>Block</li><li>Report</li><li>Disable</li></ul> | <p>When Cortex XSIAM protects workloads from exposing sensitive data, it performs the configured action.</p><p>This module protects workloads from providing responses that could expose sensitive data found in critical system files, including password hashes (/etc/shadow), user account information (/etc/passwd), and private encryption keys.</p>                                                                                      |
    | Authentication Bypass      | <ul><li>Block</li><li>Report</li><li>Disable</li></ul> | <p>When Cortex XSIAM detects attempts to bypass authentication controls, it performs the configured action.</p><p>This module protects against attacks that attempt to circumvent authentication controls through session manipulation, token exploitation, or credential abuse.</p>                                                                                                                                                           |
    | Advanced Threat Protection | <ul><li>Block</li><li>Report</li><li>Disable</li></ul> | <p>When Cortex XSIAM detects evolving threats, it performs the configured action.</p><p>Advanced Threat Protection (ATP) is a comprehensive security feature designed to detect, prevent, and respond to sophisticated web and API threats, ensuring robust protection for workloads against evolving risks.</p>                                                                                                                               |
    | Offensive Tools            | <ul><li>Block</li><li>Report</li><li>Disable</li></ul> | Cortex XSIAM identifies offensive tools that scan web applications for known security vulnerabilities and misconfiguration, and exploit them. When such tools are found, this module can block or report them.                                                                                                                                                                                                                                 |
    | Malformed Traffic          | <ul><li>Block</li><li>Report</li><li>Disable</li></ul> | When Cortex XSIAM detects HTTP requests with anomalies that are not expected from common web browsers, it performs the configured action.                                                                                                                                                                                                                                                                                                      |
    | Automation Tools           | <ul><li>Block</li><li>Report</li><li>Disable</li></ul> | <p>When Cortex XSIAM detects automated tools, it performs the configured action.</p><p>Malicious automated tools or services can scrape website contents such as Scriptable headless web browsers, command line tools, or HTTP libraries.</p>                                                                                                                                                                                                  |
    | Known Bots                 | <ul><li>Block</li><li>Report</li><li>Disable</li></ul> | <p>When Cortex XSIAM detects known bots, it performs the configured action.</p><p>Cortex XSIAM can identify legitimate bots that properly declare their identity and purpose, such as search engine crawlers and authorized web indexers. These bots follow standard protocols and provide verifiable operator information, however some of them might cause undesirable behaviors, such as spam, and you might prefer to block such bots.</p> |
3. To save the profile, click **Create**.

What to do next

If you are ready to apply your new profile to endpoints, you do this by adding it to a policy rule. If you still need to define other profiles, you can do this later. During policy rule creation or editing, you select the endpoints to which to assign the policy. There are different ways of doing this, such as:

<details>

<summary>Create a policy rule from the Prevention Profiles page</summary>

1. Navigate to **Inventory** → **Endpoints** → **Policy Management** → **Prevention** → **Profiles**.
2. Right-click your new profile, and select **Create a new policy rule using this profile**.
3. Configure the policy rule.

</details>

<details>

<summary>Edit an existing policy rule from the Policy Rules page</summary>

1. Navigate to **Inventory** → **Endpoints** → **Policy Management** → **Prevention** → **Policy Rules**.
2. Right click an existing policy and select **Edit**.
3. Add your new profile to the policy rule.

</details>

<details>

<summary>Create a new policy rule from the Policy Rules page</summary>

1. Navigate to **Inventory** → **Endpoints** → **Policy Management** → **Prevention** → **Policy Rules**.
2. Click **Add Policy**.
3. Configure a new policy that includes your new profile.

</details>
