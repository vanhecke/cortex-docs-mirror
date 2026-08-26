---
description: >-
  Connect an SAP Ariba instance in Cortex XSIAM to detect posture risks and
  compliance violations.
---

# Onboard SAP Ariba

SaaS Security connects to your SAP Ariba instance using administrator credentials and your realm name. You can connect directly with credentials or through Microsoft Azure AD (which adds MFA using one-time passcodes).

The onboarding process requires the following information:

| Item     | Description                                                                                                                                                                                                                                |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Username | The username or email address of an SAP Ariba administrator account. The format depends on whether SaaS Security logs in directly or through an identity provider. The account must be registered to the SAP Ariba realm you want to scan. |
| Password | The password for the SAP Ariba administrator account.                                                                                                                                                                                      |
| Realm    | The SAP Ariba realm that SaaS Security will scan for misconfigurations.                                                                                                                                                                    |

If SaaS Security accesses the administrator account directly, you also need:

| Item | Description                                                                                          |
| ---- | ---------------------------------------------------------------------------------------------------- |
| FQDN | The fully qualified domain name for connecting to your SAP Ariba instance. For example: s1.ariba.com |

If you use Azure Active Directory as your identity provider, you also need:

| Item             | Description                                        |
| ---------------- | -------------------------------------------------- |
| Azure 2FA secret | A key used to generate one-time passcodes for MFA. |

***

#### Step 1 — Identify the administrator account

Identify the SAP Ariba account whose login credentials you will supply during onboarding.

Required permissions: The account must have administrator permissions to the SAP Ariba realm you want SaaS Security to scan.

***

#### Step 2 — Choose a login method

Determine whether you want SaaS Security to log in to the administrator account directly, or through Microsoft Azure AD.

Using Microsoft Azure AD adds an extra layer of security by requiring MFA with one-time passcodes. If you use Azure AD, SaaS Security requires additional information for MFA.

***

#### Step 3 — (Azure AD login only) Configure MFA

If you are using Microsoft Azure AD as your identity provider:

1. [Enable third-party software OATH tokens](https://docs.paloaltonetworks.com/saas-security/sspm/onboard-saas-apps-supported-by-sspm/onboarding-an-app-using-azure-ad-credentials#onboarding-an-app-using-azure-ad-credentials_az_enable_mfa) for the administrator account.
2. [Configure the account for MFA and copy the MFA secret key](https://docs.paloaltonetworks.com/saas-security/sspm/onboard-saas-apps-supported-by-sspm/onboarding-an-app-using-azure-ad-credentials#onboarding-an-app-using-azure-ad-credentials_az_copy_mfa).

***

#### Step 4 — Identify your realm name and FQDN

1. Log in to your SAP Ariba realm using the administrator account you identified in Step 1. After login, the URL contains a realm query parameter showing your realm name.
2. From the browser address bar, locate the realm parameter in the URL.
3. Make note of the realm name. You will provide this value during onboarding.
4. (Direct login only) Also make note of the fully qualified domain name shown in the browser address bar. During onboarding, you will select the FQDN from a list. Possible values include s1.ariba.com and s3.ariba.com.

***

#### Step 5 — Connect SaaS Security to SAP Ariba

1. Log in to [Cortex](https://cortex.paloaltonetworks.com).
2. Select Settings > Data Sources and Integrations > Add New and click the SAP Ariba tile.
3. On the **Capabilities** tab, enter a name for this instance.
4. Under Default Capabilities, confirm Security Posture is selected.
5. Click Next.
6. On the **Connections** tab, select how SaaS Security will connect:
   1. Log in with Credentials — for direct login
   2. Log in with Azure — for Azure AD login
7. When prompted, provide the administrator credentials and your realm name.
8. Direct login: Select the FQDN for your SAP Ariba instance.
9. Azure AD login: Provide the Azure 2FA secret for MFA.
10. Click **Next**.
11. On the **Configurations** tab:
    1. Set the Sync Interval.
    2. (Optional) Add a Tag.
12. Click **Next** to complete onboarding.
