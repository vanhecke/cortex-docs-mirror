---
description: >-
  Use the Cortex XSIAM CDR Command Center to monitor cloud detection and
  response operations.
---

# Cloud Detection and Response (CDR) Command Center

The Cloud Detection and Respond (CDR) Command Center dashboard provides a dynamic overview of your cloud-based security operations. It includes details about your cloud assets and projects, related cases, risks, and vulnerabilities. From the dashboard, you can drill down to dedicated views for further investigation into your platform.

{% hint style="info" %}
### Notice

Requires Cortex XSIAM Premium, or any other XSIAM license with the Cloud Runtime Security or the Cloud Posture Security add-on.
{% endhint %}

![Cloud\_command\_center.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-7871671c9e7e7d8f9171f331cc9070760ced5d5e%2F9bf51c2f92b2b95c6d59d695ef19b7e3158800390b49136717a1bae2b908737c.png?alt=media)

The following table describes each section on the **Cloud Detection and Respond (CDR) Command Center**:

<table><thead><tr><th width="134">Section</th><th>Details</th></tr></thead><tbody><tr><td>Accounts</td><td><p>Displays information about your cloud accounts, the total number of assets configured per account, and the total number of cloud projects from your cloud accounts. Hover over the total number of assets to see a breakdown by category, and click on an account to drill down to the assets for the selected account.</p><p>Line colors represent the connectivity status of the assets. You can hover over the lines to see a breakdown of data ingestion or details of collection errors.</p></td></tr><tr><td>Cases</td><td>Displays the total number of cases opened in the timeframe that are associated with your cloud assets, broken down by severity. Cases are broken down into automated and manual cases, where automated cases contain at least one playbook. You can also see the top nine open cases as ranked by SmartScore.</td></tr><tr><td>Key performance indicators</td><td><ul><li>Risks identified, including attack paths, configurations, and vulnerabilities.</li><li>Total number of assets discovered in the cloud.</li><li>Cloud data ingested by your cloud platforms in the timeframe, including flow logs and audit logs.</li></ul></td></tr></tbody></table>
