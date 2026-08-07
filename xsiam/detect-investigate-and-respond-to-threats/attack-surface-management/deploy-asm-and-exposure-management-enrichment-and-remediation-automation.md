---
description: >-
  Enable the Cortex Exposure Management playbooks to automate ASM and
  vulnerability issue enrichment and remediation.
---

# Deploy ASM and Exposure Management enrichment and remediation automation

The Cortex Exposure Management pack enables you to automate attack surface management (ASM) and vulnerability issue enrichment and remediation. This content pack includes playbooks that streamline the remediation process by enriching issues with contextual information gathered from out-of-the-box integrations with sources like CMDBs, Cloud Service Providers, and VM solutions, and by automatically remediating some types of ASM and runtime vulnerability issues.

{% hint style="info" %}
### Note

For details and requirements regarding the enrichment information that can be collected and the specific issues that can be remediated automatically, review the Exposure Management Content Pack information in Marketplace.
{% endhint %}

Complete the tasks below to enable automated enrichment and remediation of ASM and vulnerability issues.

**Task 1. Install the Cortex Exposure Management content pack**

Install the Cortex Exposure Management content pack and, optionally, the related content packs.

1. Navigate to Settings → **Configurations** → **Marketplace** → **Browse** and locate the Cortex Exposure Management content pack.
2. Select the content pack and review the contents and other details.
3.  Click **Install** to add the content pack to the **Cart**.

    The \*\*Cart \*\*displays the number of items you are installing, including any additional required content packs. It also displays relevant optional content packs.
4. (Optional) Select the related content packs you want to install, for example ServiceNow and AWS Enrichment and Remediation.
5. Click **Install**.

**Task 2. Add automation rules for ASM and vulnerability issue enrichment and remediation**

Add the automation rules for exposure management issue remediation and enrichment. Automation rules trigger the Cortex Exposure Management playbooks to run on ASM and vulnerability issues. To learn which issues will trigger the playbooks, review the automation rules.

1. Navigate to **Investigation & Response** → **Automation** → **Automation Rules**.
2. Click **View Recommendations**.
3. Select one or more of the Cortex Exposure Management automation rules.
4. Click **Add Selected Rules**.

**Task 3. Set up integrations**

Install and configure relevant 3rd-party integrations, such as ServiceNow and AWS, to enable the Cortex Exposure Management playbooks to collect enrichment information and to automatically remediate some issues.

1. Navigate to **Settings** → **Data Sources & Integrations**.
2. Select the row of the integration you want to add and click **Add Instance**.
3. Add the parameters, as required.
4. **Save & Exit**.

See the Exposure Management Content Pack for a list of supported integrations. See [Administration and troubleshooting](../../configure-cortex-xsiam/cortex-xsiam-data-sources/administration-and-troubleshooting) for more detailed information about setting up integrations.

**Task 4. Configure vulnerability policies**

The Cortex Exposure Management playbooks run on specific types of issues. Review your vulnerability policies to make sure issues are being created for relevant vulnerability findings. For information about vulnerability policies and how to configure them, see [Vulnerability policies](../vulnerability-management/vulnerability-policies).

{% hint style="info" %}
### Note

Cortex Exposure Management playbooks only run on issues that were created after the automation rules have been configured.
{% endhint %}
