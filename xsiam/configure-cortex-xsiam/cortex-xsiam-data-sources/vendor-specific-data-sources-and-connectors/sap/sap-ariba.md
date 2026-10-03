---
description: >-
  Configure the SAP Ariba connector for Cortex XSIAM security posture monitoring
  and remediation.
---

# SAP Ariba

The capabilities and sub-capabilities listed for this connector are available with any active Cortex XSIAM or Cortex Cloud Posture Security license.

This connector includes the following capabilities and sub-capabilities (if applicable):

* **Security Posture:** Detect, monitor and alert on settings of your SaaS application.
  * **saas-posture-config-remediation:** Help remediate the misconfigured security settings of your SaaS application.

### &#x20;How to configure the SAP Ariba connector

To access SAP Ariba, Cortex XSIAM requires the following information, which you will specify during the connection process.

* **Username**: The username or email address of an SAP Ariba administrator account. The format depends on whether Cortex XSIAM logs in directly or through an identity provider. The account must be registered to the SAP Ariba realm you want to scan.
* **Password**: The password for the SAP Ariba administrator account.
* **Realm**: The SAP Ariba realm that Cortex XSIAM will scan for misconfigurations.

If Cortex XSIAM accesses the administrator account directly, you also need:

* **FQDN**: The fully qualified domain name for connecting to your SAP Ariba instance. For example: s1.ariba.com

If you use Azure Active Directory as your identity provider, you also need:

* **Azure 2FA secret**: A key used to generate one-time passcodes for MFA.

#### **Task 1: Identify the administrator account**

Identify the SAP Ariba account whose login credentials you will supply during onboarding.Required permissions: The account must have administrator permissions to the SAP Ariba realm you want Cortex XSIAM to scan.

#### **Task  2: Choose a login method**

Determine whether you want Cortex XSIAM to log in to the administrator account directly, or through Microsoft Azure AD.

Using Microsoft Azure AD adds an extra layer of security by requiring MFA with one-time passcodes. If you use Azure AD, Cortex XSIAM requires additional information for MFA.

#### **Task 3: (Azure AD login only) Configure MFA**

If you are using Microsoft Azure AD as your identity provider:

1. [Enable third-party software OATH tokens](https://docs.paloaltonetworks.com/saas-security/sspm/onboard-saas-apps-supported-by-sspm/onboarding-an-app-using-azure-ad-credentials#onboarding-an-app-using-azure-ad-credentials_az_enable_mfa) for the administrator account.
2. [Configure the account for MFA and copy the MFA secret key](https://docs.paloaltonetworks.com/saas-security/sspm/onboard-saas-apps-supported-by-sspm/onboarding-an-app-using-azure-ad-credentials#onboarding-an-app-using-azure-ad-credentials_az_copy_mfa).

#### **Task 4: Identify your realm name and FQDN**

1. Log in to your SAP Ariba realm using the administrator account you identified in Step 1. After login, the URL contains a realm query parameter showing your realm name.
2. From the browser address bar, locate the realm parameter in the URL.
3. Make note of the realm name. You will provide this value during onboarding.
4. (Direct login only) Also make note of the fully qualified domain name shown in the browser address bar. During onboarding, you will select the FQDN from a list. Possible values include s1.ariba.com and s3.ariba.com.

#### **Task 5: Connect** SAP Ariba **to Cortex XSIAM**

1. In Cortex XSIAM, navigate to **Settings** → **Data Sources & Integrations**.
2. Click **+ Add new**.
3. In the **Add Data Sources or Integrations** page, search for SAP Ariba.
4. Under **Recommended**, hover over the new SAP Ariba integration and click **Add Instance** to launch the configuration wizard.
5. Under the **Capabilities** tab, Enter a Name for your application.
6. Select Security Posture under **Default Capabilities**.
7. Click **Next**.
8. Under **Connection**, enter the SAP Ariba user name and password, Realm, FQDN, and MFA Provider details.
9. Under **Configuration** tab, select a **Sync Interval**. Choose a meaningful **Tag** to distinguish between various applications in different environments.
10. A confirmation message indicates that SAP Ariba is successfully connected. Confirm the Summary details and click **Save instance**.
