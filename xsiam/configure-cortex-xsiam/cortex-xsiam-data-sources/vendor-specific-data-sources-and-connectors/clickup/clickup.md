---
description: Use ClickUp data with Cortex XSIAM.
---

# ClickUp

The capabilities and sub-capabilities listed for this connector are available with any active Cortex XSIAM or Cortex Cloud Posture Security license.

This connector includes the following capabilities and sub-capabilities (if applicable):

* Security Posture: Detect, monitor and alert on settings of your SaaS application.
  * saas-posture-config-remediation: Help remediate the misconfigured security settings of your SaaS application.

### How to configure the ClickUp connector <a href="#how-to-configure-the-aha-connector" id="how-to-configure-the-aha-connector"></a>

To access ClickUp, Cortex XSIAM requires the following information, which you will specify during the connection process.

* ClickUp instance account information

#### **Task 1:** Collect Information for Accessing Your ClickUp Instance

To access your ClickUp instance, Cortex XSIAM  requires connection information. During the onboarding process, you specify the following required and optional information.

* **User Email**: The login email address of a ClickUp administrator account. Required Permissions: The user must be assigned to the Admin role, or a role with greater permissions.
* **Password**: The password for the ClickUp administrator account.
* **MFA Secret Key**

(Optional) A key that is used to generate one-time passcodes for multi-factor authentication.

As you complete the following steps, make note of the values of the items described in the preceding table. You will need to enter these values during onboarding to access your ClickUp instance from Cortex XSIAM.

1. Identify the ClickUp account that Cortex XSIAM will use to access your ClickUp instance. Verify that the account is assigned to the Admin role, or a role with greater permissions.
2. (Optional) Generate and copy an MFA secret key.

MFA provides an extra layer of security when accessing the ClickUp administrator account. To enable this extra layer of security, the administrator account must be configured for MFA that uses time-based one-time passcodes. These one-time passcodes are generated from authenticator apps such as Google Authenticator by using an MFA secret key. Like an authenticator app, Cortex XSIAM uses the MFA secret key for passcode generation.

1. Log in to your ClickUp administrator account.
2. Navigate to your My Settings page. Locate your account avatar in the lower-left corner of the page and select \<account-avatar> > My Settings.
3. On your My Settings page, locate the Two-factor authentication (2FA) section and turn on the toggle for Authenticator App (TOTP).
4. A pop-up is displayed, instructing you to install an authenticator app on your cellphone. Decide which authenticator app you will use and download it to your cellphone. After you install the authenticator, click Yes, ready to scan, but do not scan the QR code that is displayed.
5. A pop-up window displays your MFA key as a text string and also as a QR code. Copy and paste the MFA key text string into a text file so you can provide it to Cortex XSIAM during onboarding. Then continue configuring your authenticator app by scanning the QR code or by manually entering the MFA key.

{% hint style="info" %}
MFA is optional. However, if you want Cortex XSIAMto connect to the administrator account by using MFA, do not continue to the next step unless you have copied the MFA Secret Key. You will provide this key to Cortex XSIAM during the onboarding process.
{% endhint %}

#### **Task 2:** ClickUp **to Cortex XSIAM**

1. In Cortex XSIAM, navigate to **Settings** → **Data Sources & Integrations**.
2. Click **+ Add new**.
3. In the **Add Data Sources or Integrations** page, search for ClickUp.
4. Under **Recommended**, hover over the new ClickUp integration and click **Add Instance** to launch the configuration wizard.
5. Under the **Capabilities** tab, Enter a Name for your application.
6. Select Security Posture under **Default Capabilities**.
7. Click **Next**.
8. Under **Connection**, enter the administrator login credentials and, optionally, the MFA secret key.
9. Under **Configuration** tab, select a **Sync Interval**. Choose a meaningful **Tag** to distinguish between various applications in different environments.
10. A confirmation message indicates that ClickUp is successfully connected. Confirm the Summary details and click **Save instance**.
