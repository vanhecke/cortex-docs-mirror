---
description: Use Contentful data with Cortex XSIAM.
---

# Contentful

The capabilities and sub-capabilities listed for this connector are available with any active Cortex XSIAM or Cortex Cloud Posture Security license.

This connector includes the following capabilities and sub-capabilities (if applicable):

* SaaS Posture Configuration Monitoring: Detect, monitor and alert on settings of your SAAS application.
  * saas-posture-config-remediation: Help remediate the misconfigured security settings of your SAAS application.

### How to configure the Contentful connector <a href="#how-to-configure-the-asana-connector" id="how-to-configure-the-asana-connector"></a>

To access Asana, Cortex XSIAM requires the following information, which you will specify during the connection process.

* &#x20;**Contentful personal access token**

Perform the following procedures in the order that they appear below.

#### **Task 1:** Create a Personal Access Token in Contentful

In Contentful, create a personal access token for an administrator account. The access token enables Cortex XSIAM to carry out actions that require administrator permissions.

1. Open a web browser and go to the Contentful login page at [be.contentful.com/login](https://be.contentful.com/login).
2. Log in as an administrator.
3. Locate your profile icon and select \<profile-icon> > Account settings.
4. On the Account Settings page, navigate to the CMA Tokens tab and click Create personal access token.
5. In the **Create personal access token** dialog, specify a name and expiration date for the access token. You can also specify that the token should never expire.

{% hint style="info" %}
Cortex XSIAM uses the access token to establish the initial connection to your Contentful instance and to perform scans at regular intervals. These scans will fail after the token expires, and you will need to onboard your Contentful instance again.
{% endhint %}

6. Click Generate. Contentful generates and displays your personal access token.
7. Copy the generated token and paste it into a text file.

{% hint style="info" %}
Do not continue to the next step unless you have copied the access token. You must provide this token to SaaS Security during the onboarding process.
{% endhint %}

#### **Task 2: Connect** Contentful **to Cortex XSIAM**

1. In Cortex XSIAM, navigate to **Settings** → **Data Sources & Integrations**.
2. Click **+ Add new**.
3. In the **Add Data Source** page, search for Asana.
4. Under **Recommended**, hover over the new Asana integration and click **Add Instance** to launch the configuration wizard.
5. Under the **Capabilities** tab, Enter a Name for your application.
6. Select Security Posture under **Default Capabilities**.
7. Click **Next**.
8. Under the **Connection** tab, enter enter your personal access key.
9. Under the **Configuration** tab, select a **Sync Interval**. Choose a meaningful **Tag** to distinguish between various applications in different environments.
10. A confirmation message shows that your Asana instance is successfully connected. Confirm the **Summary** details and click **Save instance**.
