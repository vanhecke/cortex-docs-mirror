---
description: >-
  Explore workflows for ingesting, enriching, investigating, and acting on
  threat indicators.
---

# Threat Intel Management use cases

**Threat Intel Management use cases**

The following examples illustrate typical use cases for Threat Intel Management analysts.

<details>

<summary>Dynamic allow lists for business-critical SaaS apps</summary>

In this example, Firewall Admins are responsible for ensuring employees can always access SaaS applications such as Zoom and Office 365. They need to manage a stream of inbound change requests from the security team and other business units. Regardless of these daily changes, critical apps must always be allowed. The network infrastructure of SaaS applications is constantly changing/rotating IP addresses and Domains.

![xsiam-use-case.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-e772ba0a02ddfc3cec181f13fead0f8f540261ce%2F42a94ceb87c8bdd566429b1c03aafc1330aa6155f5cced986b183e2fbd8e1163.png?alt=media)

1. Configure a feed integration such as Office 365, Amazon AWS, or Unit 42.
   1. Navigate to **Settings** → **Data Sources & Integrations**.
   2.  Search for and select the relevant integration and click **Add Instance**.

       In this example, add the AWS feed.
   3. Set up the instance. In the **Indicator Reputation** field, select **Benign**.
   4. Test and save the instance.
2. (Optional) Configure a playbook to filter indicators according to your requirements.
3.  Go to the Indicators page and run the following search to return IP, IPv6 or IPv6CIDR results:

    `sourceBrands:"AWS Feed" and expirationStatus:active and type:IP or type:IPv6 or type:IPv6CIDR`
4. Configure the Generic Export Indicator Service integration.
   1. On the **Data Sources & Integrations** page, search for and select Generic Export Indicators Service, and click **Add Instance**.
   2. In the **Indicator Query** field, add the query in step 3.
   3. Add the remaining fields, test, and save.
5. Test the EDL by running the cURL command: `curl -v-u- user:pass https://ext-<tenant>crtx<region>.paloaltonetworks.com/xsoar/instance/execute/<instance-name>`

</details>

<details>

<summary>Proactive blocking of known threats</summary>

The security team needs to leverage threat intelligence to block or alert on known bad domains, IPs, hashes, etc. (indicators). The indicators are collected from many sources, which need to be normalized, scored, and analyzed before pushing to security devices such as firewalls for alerting. Detection tools can only handle limited amounts of threat intelligence data and need to constantly re-prioritize indicators.

![xsiam-use-case-2.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-10c4b968d1c1e5ba31f85e62b9289e78e5a5fdf8%2F0ba8a3daa1d7bc4ea437160df2379b8b63b6aee74f7f992a22317a2e073746c5.png?alt=media)

**Solution**

Indicator prioritization. Cortex XSIAM can ingest phishing issues from email inboxes through integrations. Once an issue is ingested, a playbook is triggered and can have any combination of automated or manual actions that users desire. The playbooks can have filters and conditions that execute different branches depending on certain values.

1. Configure feed integrations such as Unit 42 Feed, TAXII feed, etc.
   1. Navigate to **Settings** → **Data Sources & Integrations**.
   2. Search for and select the relevant threat intel feed integration and select **Add Instance**.
   3.  Set up the instance.

       Leave the **Indicator Reputation** field blank.
   4. Test and save the instance,
2. (Optional) Configure a playbook to filter indicators according to your requirements.
3.  Go to the **XSIAM Indicators** page and run the following search to return IP addresses with the verdict malicious with high reliability:

    `expirationStatus:active and type:IP and verdict:malicious and aggregatedReliablitiy:A - Completely reliable`
4. Configure the Generic Export Indicator Service integration.
   1. Navigate to **Settings** → **Data Sources & Integrations**.
   2. Search for and select Generic Export Indicators Service and click **Add Instance**.
   3. In the **Indicator Query** field, add the query in step 3.
   4. Add the remaining fields, test, and save.
5.  Test the EDL by running the cURL command: `curl -v-u- user:pass https://ext-<tenant>crtx<region>.paloaltonetworks.com/xsoar/instance/execute/<instance-name>`

    You can use this URL in your Next-Generation Firewall.

</details>

<details>

<summary>Issue enrichment</summary>

Case Responders receive an endless stream of issues, usually with little to no context of the external threat. Enriching issues with curated threat intelligence from Unit 42 enables analysts to see the bigger picture and make more informed decisions when responding to issues, ensuring comprehensive containment of the threat.

Most tools that Security Operations Centers and Case Response teams use to respond to issues are very generic. There is little correlation between network data and understanding of threats and attacker movements. There is often a dump of information, including bad IP addresses or domains, and someone has to be assigned to manually resolve to figure out false positives. There is also a lack of understanding of malicious families, hacking tools, and their patterns of attacks.

![alert\_sources.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-0e6a5cfdf673feda011dbd804f0a170eb62904e8%2Fad16d83b4ae53d131bbe7ff3c9b93594727455c4558fe7c079118b44d7efcb73.png?alt=media)

Accelerate issue response with TIM and issue enrichment using threat intelligence data. The case enrichment workflow in Cortex XSIAM leverages threat intelligence from our centralized threat intelligence library, including information on:

* Data from Unit 42 Intel to learn about known malware campaigns or families
* IPs and domains with WHOIS data
* Passive DNS data
* Web categorization data

When investigating an issue, you can see information, such as affected hosts, affected users, and detailed information about the source and destination. You can deep dive into the indicator by clicking the indicator to see the verdict, sources, related issues, file details, and relationships. If the indicator originated from Unit 42, in the Unit 42 Intel tab you can see additional information, such as static and dynamic analysis for a file.

</details>
