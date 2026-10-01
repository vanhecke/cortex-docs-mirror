---
description: Use Automox data with Cortex XSIAM.
---

# Automox

The capabilities and sub-capabilities listed for this connector are available with any active Cortex XSIAM or Cortex Cloud Posture Security license.

This connector includes the following capabilities and sub-capabilities (if applicable):

* SaaS Posture Configuration Monitoring: Detect, monitor and alert on settings of your SaaS application.
  * saas-posture-config-remediation: Help remediate the misconfigured security settings of your SaaS application.

### How to configure the Automox connector <a href="#how-to-configure-the-asana-connector" id="how-to-configure-the-asana-connector"></a>

Cortex XSIAM supports the following Automox account plans:

* Automate Essentials
* Automate Enterprise

To access Automox, Cortex XSIAM requires the following information, which you will specify during the connection process.

* **API Key**: A unique, alphanumeric string that you generate from an Automox account. Cortex XSIAM uses the key to authenticate to the Automox API. The API key inherits the permissions of the Automox account.
*   **Organization ID**: A unique identifier for your organization within the Automox platform.



Perform the following procedures in the order that they appear below.

#### Task 1: Generate and Copy an API Key for Your Organization <a href="#step-1-generate-and-copy-an-api-key-for-your-organization" id="step-1-generate-and-copy-an-api-key-for-your-organization"></a>

1.  Identify the Automox account that you will use to create the API key.

    Required Permissions: The account that you use to generate the API key must have the following permissions that SaaS Security requires. To adhere to the principle of least privilege, create a custom role with this exact set of permissions and assign it to the account. The API key inherits these permissions.

* Personal API Keys: Manage
* Organization: Read & Manage
* All API Keys: Read & List
* Groups: Read
* Patch Policy Management: Read
* User Management: Read

2. Using the credentials of the account you identified, log in to the [Automox console](https://console.automox.com/).
3. Locate the settings menu icon (⋮) in the upper-right corner of the console and select Secrets & Keys.
4. On the Secrets & Keys page, scroll to the API Keys section and click Add.
5. Fill out the fields of the Create an API Key dialog and click Create. Automox adds the new key to the list of API keys.
6. From the API key's entry in the list, click the copy icon to copy the key. Paste the key into a text file.

{% hint style="info" %}
Do not continue to the next step unless you have copied the API key. You must provide this key to Cortex XSIAM during the onboarding process.
{% endhint %}

#### Task 2: Identify Your Organization ID <a href="#step-2-identify-your-organization-id" id="step-2-identify-your-organization-id"></a>

1. Click the organization selector icon in the upper-right corner of the console and select Manage Orgs and Users.
2. On the Setup and Configuration page, select the Organizations tab.
3. From the list of organizations, copy your Organization ID and paste it into a text file.

{% hint style="info" %}
&#x20;Do not continue to the next step unless you have copied the Organization ID. You must provide this information to Cortex XSIAM during the onboarding process.
{% endhint %}

#### **Task 3: Connect** Automox **to Cortex XSIAM**

1. In Cortex XSIAM, navigate to **Settings** → **Data Sources & Integrations**.
2. Click **+ Add new**.
3. In the **Add Data Source** page, search for Automox.
4. Under **Recommended**, hover over the new Automox integration and click **Add Instance** to launch the configuration wizard.
5. Under the **Capabilities** tab, Enter a Name for your application.
6. Select Security Posture under **Default Capabilities**. Click **Next**&#x20;
7. Under the **Connection** tab, enter the API key and Organization ID details.
8. Under the **Configuration** tab, select a **Sync Interval**. Choose a meaningful **Tag** to distinguish between various applications in different environments.
9. A confirmation message shows that Automox is successfully connected. Confirm the **Summary** details and click **Save instance**.
