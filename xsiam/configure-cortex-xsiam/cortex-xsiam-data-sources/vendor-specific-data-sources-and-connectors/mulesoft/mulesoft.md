---
description: Use MuleSoft data with Cortex XSIAM.
---

# MuleSoft

The capabilities and sub-capabilities listed for this connector are available with any active Cortex XSIAM or Cortex Cloud Posture Security license.

This connector includes the following capabilities and sub-capabilities (if applicable):

* SaaS Posture Configuration Monitoring: Detect, monitor and alert on settings of your SaaS application.
  * saas-posture-config-remediation: Help remediate the misconfigured security settings of your SAAS application.

### How to configure the MuleSoft connector

Cortex XSIAM gets access to your MuleSoft instance through an OAuth 2.0 application that you create. In the Anypoint Platform, an OAuth 2.0 application is called a Connected App. During onboarding, you supply Cortex XSIAM with the application credentials (Client ID and Client Secret) for your Connected App. Cortex XSIAM uses these credentials to access the Anypoint Platform API.

Cortex XSIAM scans are supported for all MuleSoft paid plans.

To access your MuleSoft instance, Cortex XSIAM requires the following information, which you specify during the data connection process:

* **Hosted Region**: MuleSoft operates multiple independent regional sites worldwide. Since these regional environments are entirely separate from one another, you must provide Cortex XSIAM with the region where MuleSoft hosts your data. You can determine your region from the MuleSoft URL displayed in your browser's address bar.
* **Client ID**: Cortex XSIAM accesses an Anypoint Platform API through a Connected App that you create in the Anypoint Platform. The Anypoint Platform generates the Client ID to uniquely identify this Connected App.
* **Client Secret**: Cortex XSIAM accesses an Anypoint Platform API through a Connected App that you create in the Anypoint Platform. The Anypoint Platform generates the Client Secret, which Cortex XSIAM uses to authenticate to the API through the Connected App.

To onboard your MuleSoft instance, complete the following actions in the specified order .

#### Task 1: Identify the Anypoint platform account <a href="#step-1-identify-the-anypoint-platform-account" id="step-1-identify-the-anypoint-platform-account"></a>

1. Identify the Anypoint Platform account that you will use to create your Connected App.\
   Required Permissions: To create the Connected App, you must use an Anypoint Platform account assigned to the Organization Administrator role.
2. Open a web browser to the [MuleSoft Anypoint Platform login page](https://anypoint.mulesoft.com/login/) and log in to the Organization Administrator account you identified.

#### Task 2: Identify Your Hosted Region

Use the following table to determine your region based on the MuleSoft URL displayed in your browser's address bar. You will provide this region information to Cortex XSIAM during data connection.

| URL                       | Region                          |
| ------------------------- | ------------------------------- |
| anypoint.mulesoft.com     | US                              |
| eu1.anypoint.mulesoft.com | Europe                          |
| ca1.anypoint.mulesoft.com | Canada                          |
| jp1.anypoint.mulesoft.com | Japan                           |
| gov.anypoint.mulesoft.com | Gov (MuleSoft Government Cloud) |

{% hint style="info" %}
MuleSoft Government Cloud is a dedicated, high-security instance of Anypoint Platform tailored for U.S. public sector organizations, including federal, state, and local agencies and their authorized partners
{% endhint %}

#### Task 3: Create Your Connected App <a href="#step-4-create-your-connected-app" id="step-4-create-your-connected-app"></a>

Cortex XSIAM uses this Connected App to authenticate to an Anypoint Platform API to run scans. You configure the Connected App to allow access to only the scopes that Cortex XSIAM requires.

1. From the Anypoint Platform home screen, navigate to the Access Management page. In some interface versions, a link to Access Management is on the home screen. If you do not see a link on the home screen, locate the Access Management link under the main navigation menu in the top-left corner of the Anypoint Platform page.
2. From the left navigation pane of the Access Management page, select Connected Apps.
3. On the Connected Apps page, click **Create app**.
4. On the Create App page, complete the following actions:
   1. Specify a Name for your Connected App. For example, Cortex XSIAM Integration.
   2. For the Type of application, select App acts on its own behalf (client credentials).
   3. Click Add Scopes and add the following scopes:
      1. View Policies
      2. Access Controls Viewer
      3. View Connected Applications
      4. View Environment
      5. View Organization
      6. View Users in a particular organization
5. Click **Save**. The Anypoint Platform creates the Connected App and displays it in the list of Connected Apps.
6. From the list on the Connected Apps page, click the name of your Connected App. The Anypoint Platform displays the Update App page, which shows the Connected App credentials (Client ID and Client Secret) that Cortex XSIAM uses to authenticate to an Anypoint Platform API.
7. Copy the Client ID and Client Secret and paste them into a text file. Do not continue to the next step unless you have copied the Client ID and Client Secret. You must provide this information to Cortex XSIAM during the onboarding process.

#### **Task 4: Connect** MuleSoft **to Cortex XSIAM**

1. In Cortex XSIAM, navigate to **Settings** → **Data Sources & Integrations**.
2. Click **+ Add new**.
3. In the **Add Data Sources or Integrations** page, search for MuleSoft.
4. Under **Recommended**, hover over the new MuleSoft integration and click **Add Instance** to launch the configuration wizard.
5. Under the **Capabilities** tab, Enter a Name for your application.
6. Select Security Posture under **Default Capabilities**.
7. Click **Next**.
8. Under **Connection**, enter the Client ID, Client Secret, and Hosted Region for your Connected App.
9. Under **Configuration** tab, select a **Sync Interval**. Choose a meaningful **Tag** to distinguish between various applications in different environments.
10. A confirmation message indicates that MuleSoft is successfully connected. Confirm the Summary details and click **Save instance**.

<a class="button secondary"></a><br>
