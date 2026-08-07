---
description: >-
  Use Cloud Identity Security to achieve the principle of least privilege
  access.
---

# Achieve the principle of least privilege access

{% hint style="info" %}
This feature is included with a Cortex XSIAM Premium license. It is also included with any other Cortex XSIAM license that has the Cloud Posture Security or Cloud Runtime Security add-on.
{% endhint %}

#### Overview

Cloud Identity Security uses audit logs to detect unused permissions. The Review Unused Permissions feature can help you analyze audit logs in order to identify and revoke excessive permissions. This allows you to generate precise IAM policies based on actual usage, reducing your attack surface and strengthening your overall security posture. You can customize the time frame for used permissions according to your specific operational needs.

The Review Unused Permissions feature is supported for these platform entities:

* **Amazon AWS:**
  * IAM roles
  * IAM groups
* **Microsoft Azure:**
  * Service principals
  * IAM groups
* **Google Cloud Platform (GCP):**
  * GCP groups
  * Service accounts

Cloud Identity Security does the following:

*   Analyzes last access data in order to detect the permissions that are being used.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>In the case of Amazon AWS, Cloud Identity Security also uses AWS Identity and Access Management (IAM) Access Advisor insights to expand the coverage of supported actions.</p></div>
* Recommends the removal of unused permissions, displaying recommended actions, such as **Keep** and **Remove**.
* Generates downloadable policies in:
  * **Amazon AWS:** IAM Policy (JSON), HashiCorp® Terraform, CloudFormation
  * **Microsoft Azure:** Role Definition and Role Assignment (JSON), HashiCorp® Terraform
  * **Google Cloud Platform (GCP):** IAM Policy (JSON), HashiCorp® Terraform

#### Reviewing Unused Permissions

1. In the Cloud Identity Security module, under **Identity Asset Inventory**, on the **Cloud Identities** tab, select an identity in the list whose permissions you want to review.
2. On the **Overview** tab, in the **Review Unused Permissions** area, click **Analyze Permissions Usage**, and select a time period in the list.
3. Click **Start Analysis**.
4. On the **Permission Checkup Results** screen, a summary of permissions usage is displayed according to the time period you selected, with the suggested **Remove** number in red and the recommended **Keep** number in blue.
5. If you want to proceed with seeing the recommended changes and how you could reduce unused permissions, click **Adjust Policy**, and select one of these formats in the list:
   * JSON
   * Terraform
   * CloudFormation (for AWS only)
6. A code block with the format you chose now appears. You can do one of the following:
   * Click **Download File** to save a copy of the file.
   * Click **Copy to clipboard** and then paste the code into a file of your choice.
7. You can now click **Back to Checkup Result** to return to the previous screen. You can review the policy list to see and consider the **Cortex Recommendation** column, which displays either **Remove** or **Keep** for each policy file.

{% hint style="info" %}
### Important

If you turn off the audit logs, even briefly, this temporarily impacts the accuracy of the Last Access data, potentially showing permissions as unused when actually they were active. Full accuracy is restored 90 days after you re-enable the audit logs.
{% endhint %}
