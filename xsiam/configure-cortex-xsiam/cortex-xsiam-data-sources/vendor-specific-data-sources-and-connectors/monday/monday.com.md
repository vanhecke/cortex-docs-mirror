---
description: Use Monday.com data with Cortex XSIAM.
---

# Monday.com

The capabilities and sub-capabilities listed for this connector are available with any active Cortex XSIAM or Cortex Cloud Posture Security license.

This connector includes the following capabilities and sub-capabilities (if applicable):

* Security Posture: Detect, monitor and alert on settings of your SaaS application.
  * saas-posture-config-remediation: Help remediate the misconfigured security settings of your SaaS application.

### How to configure the Monday.com connector <a href="#how-to-configure-the-aha-connector" id="how-to-configure-the-aha-connector"></a>

To access Monday.com, Cortex XSIAM requires the following information, which you will specify during the connection process.

* **Email**: The login email address of a monday.com administrator. Required Permissions: You must supply Cortex XSIAM with Admin credentials to your monday.com account.
* **Password**: The password of the monday.com administrator.
* **Account Domain**: The custom domain for your monday.com account. After you log in to monday.com, this domain is part of your monday.com URL in the format \<account\_domain>.monday.com.
* **MFA Secret Key**: (Optional) A key that is used to generate one-time passcodes for multi-factor authentication.

#### **Task 1: Gather** Monday.com account details

1. Identify the monday.com administrator whose credentials you will supply to Cortex XSIAM. Required Permissions: You must supply Cortex XSIAM with Admin credentials to your monday.com account.
2. Identify your monday.com account domain.
3. After you log in to monday.com, the account domain is a unique subdomain included in the monday.com URL in the format \<account\_domain>.monday.com. You can also identify your account domain from your profile:
   1. Open a web browser and go to the monday.com login page at [auth.monday.com/auth/login\_monday](https://auth.monday.com/auth/login_monday).
   2. Log in to the administrator account that you identified.
   3. Navigate to the Administration page. Locate your account avatar and select **\<account-avatar> > Administration**.
   4. On the Administration page, select **General > Profile**. The Account URL (Web Address) field shows your account domain.
   5. (Optional) Generate and copy an MFA secret key.

#### Task 2: Set up optional MFA key

MFA provides an extra layer of security when accessing the monday.com administrator account. To enable this extra layer of security, you must configure the administrator account for MFA that uses time-based one-time passcodes. Like an authenticator app, Cortex XSIAM uses the MFA secret key for passcode generation.

1. Decide which authenticator app you will use and download it to your cellphone. You can use any authenticator app that generates time-based one-time passcodes (TOTP), such as Microsoft Authenticator or Google Authenticator.
2. Open a web browser and go to [auth.monday.com/auth/login\_monday](https://auth.monday.com/auth/login_monday) and log in to the administrator account.
3. Navigate to the Administration page. Locate your account avatar and select **\<account-avatar> > Administration**.
4. On the Administration page, select **Security > Login**.
5. Locate the Two-Factor Authentication section and click **Enable Two-Factor Authentication**.
6. When monday.com prompts you to choose your authentication method, select Authentication App and click **Continue**.
7. A pop-up window displays your MFA secret key as a QR code. Do not scan the QR code. Click **Copy code** instead to display a text version of the MFA secret key.
8. Copy and paste the text version of the MFA secret key into a text file. Do not continue to the next step unless you have copied the MFA secret key. You will provide this key to Cortex XSIAM during the onboarding process.
9. Continue configuring your authentication app by scanning the QR code or by manually entering the MFA secret key.

#### **Task 3: Connect** Monday.com **to Cortex XSIAM**

1. In Cortex XSIAM, navigate to **Settings** → **Data Sources & Integrations**.
2. Click **+ Add new**.
3. In the **Add Data Sources or Integrations** page, search for Monday.com.
4. Under **Recommended**, hover over the new Monday.com integration and click **Add Instance** to launch the configuration wizard.
5. Under the **Capabilities** tab, Enter a Name for your application.
6. Select Security Posture under **Default Capabilities**.
7. Click **Next**.
8. Under **Connection**, enter the administrator login credentials, your account domain, and, optionally, the MFA secret key.
9. Under **Configuration** tab, select a **Sync Interval**. Choose a meaningful **Tag** to distinguish between various applications in different environments.
10. A confirmation message indicates that Harness is successfully connected. Confirm the Summary details and click **Save instance**.
