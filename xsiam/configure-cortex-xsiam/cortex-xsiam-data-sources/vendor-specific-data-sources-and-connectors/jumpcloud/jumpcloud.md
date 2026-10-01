---
description: Use JumpCloud data with Cortex XSIAM.
---

# JumpCloud

The capabilities and sub-capabilities listed for this connector are available with any active Cortex XSIAM or Cortex Cloud Posture Security license.

This connector includes the following capabilities and sub-capabilities (if applicable):

* Security Posture: Detect, monitor and alert on settings of your SaaS application.
  * saas-posture-config-remediation: Help remediate the misconfigured security settings of your SaaS application.

### How to configure the JumpCloud connector <a href="#how-to-configure-the-aha-connector" id="how-to-configure-the-aha-connector"></a>

To access JumpCloud, Cortex XSIAM requires the following information, which you will specify during the connection process.

* **API Key**: A unique, alphanumeric string that JumpCloud generates for a JumpCloud administrator account. SaaS Security uses the key to authenticate to the JumpCloud API. The API key inherits the permissions of the administrator account.
* **Organization ID**: A unique identifier for your organization within the JumpCloud platform.

#### **Task 1:** Generate and Copy an API Key for Your Organization

1. Identify the JumpCloud account that you will use to create the API key.

Required Permissions: To create the API key, you must use an account assigned to the Administrator role in JumpCloud. The account must have API access enabled. To enable API access for the Administrator account, contact an administrator assigned to the Administrator with Billing role. Only administrators assigned to the Administrator with Billing role can enable API access for an Administrator account. The API key inherits the permissions of the Administrator account.

2. Using the credentials of the Administrator account, log in to the [JumpCloud Admin Portal](https://console.jumpcloud.com/login/admin).
3. Locate your profile icon in the upper-right corner of the page and select **\<profile-icon> > My API Key**.
4. In the API Key dialog, specify a Custom expiration date of 365 days and click **Generate New API Key**. JumpCloud generates and displays a new API key.
5. Copy the API key and paste it into a text file. Do not continue to the next step unless you have copied the API key. You must provide this key to Cortex XSIAM during the onboarding process.

#### Task 2: Identify Your Organization ID <a href="#step-2-identify-your-organization-id" id="step-2-identify-your-organization-id"></a>

1. In the JumpCloud Admin Portal, navigate to your Settings page. In the lower-left corner of the Admin Portal, click **Settings**.
2. On the Settings page, navigate to the Organization Profile tab.
3. Copy your Organization ID and paste it into a text file. Do not continue to the next step unless you have copied the Organization ID. You must provide this information to Cortex XSIAM during the onboarding process.

#### **Task 3: Connect** JumpCloud **to Cortex XSIAM**

1. In Cortex XSIAM, navigate to **Settings** → **Data Sources & Integrations**.
2. Click **+ Add new**.
3. In the **Add Data Sources or Integrations** page, search for JumpCloud.
4. Under **Recommended**, hover over the new JumpCloud integration and click **Add Instance** to launch the configuration wizard.
5. Under the **Capabilities** tab, Enter a Name for your application.
6. Select Security Posture under **Default Capabilities**.
7. Click **Next**.
8. Under **Connection**, enter your API Key and Organization ID.
9. Under **Configuration** tab, select a **Sync Interval**. Choose a meaningful **Tag** to distinguish between various applications in different environments.
10. A confirmation message indicates that JumpCloud is successfully connected. Confirm the Summary details and click **Save instance**.

