---
description: Use Asana data with Cortex XSIAM.
---

# Asana

The capabilities and sub-capabilities listed for this connector are available with any active Cortex XSIAM or Cortex Cloud Posture Security license.

This connector includes the following capabilities and sub-capabilities (if applicable):

* **Security Posture:** Detect, monitor and alert on settings of your SAAS application.
  * **saas-posture-config-remediation:** Help remediate the misconfigured security settings of your SAAS application.

### Prerequisites&#x20;

For Cortex XSIAM to detect posture risks in your Asana instance, you must connect your Asana instance to Cortex. Through the onboarding process, Cortex XSIAM connects to the Asana API by using an API token that you generate from the Asana admin console. After connecting to the Asana API, Cortex XSIAM scans your Asana workspace for misconfigured settings and account risks.

The supported Asana account plans for SaaS Security scans are:

* Enterprise+
* Legacy Enterprise

To access your Asana instance, SaaS Security requires the following information, which you specify during the onboarding process.

**API Token**: A service account token that Asana generates for a service account that you create. The token is an alphanumeric string that SaaS Security uses to authenticate to the Asana API and leverage the service account's permissions.

To onboard your Asana instance, complete the following actions.

***

#### Step 1: Create a Service Account in Asana and Save the Token <a href="#step-1-create-a-service-account-in-asana-and-save-the-token" id="step-1-create-a-service-account-in-asana-and-save-the-token"></a>

An Asana service account is a non-human, programmatic identity that SaaS Security uses to scan your Asana workspace. When you create a service account, Asana generates and displays a service account token that SaaS Security uses to access the Asana API. Asana displays this token only once, so copy and save the token so you can provide it during onboarding.

1. Open a web browser to the [Asana website](https://asana.com/) and log in as a Super Admin. \
   **Note**: To create an Asana service account, you must use an account assigned to the Super Admin role. Service accounts are an exclusive feature for organizations on Asana's Enterprise or Enterprise+ plans.
2. Navigate to the Admin Console. Locate your profile picture in the upper-right corner of the Asana webpage and select \<profile-picture> > Admin console.
3. In the left navigation pane, select Apps > Service Accounts.
4. On the Service Accounts page, click Add service account.
5. Fill in the Add service account dialog:
   1. Specify a Name for the service account. For example, SaaS Security Service Account.
   2. Under Permission scopes, select Full permissions.
6. Click Save changes to generate the service account token. Copy the service account token and paste it into a text file.

**Important**: Do not continue to the next step unless you have copied the service account token. You must provide this token to SaaS Security during the onboarding process.

***

#### Step 2: (Optional) Update the Token Expiration Period <a href="#step-2-optional-update-the-token-expiration-period" id="step-2-optional-update-the-token-expiration-period"></a>

By default, the lifespan for service account tokens in Asana is 10 years. To limit the attack window if the token becomes compromised, set service account tokens to expire after 90 days.

1. From the left navigation pane in the Admin Console, select Apps > Service Accounts.
2. On the App settings page, locate the Token Expiration settings.
3. For the **When should service account tokens expire?** setting, select 90 days.
4. Click Save changes.

### Configure Asana&#x20;

Once you have setup your Asana instance, follow the steps outlined in the Cortex Asana data connector configuration wizard to complete the connection process. Provide the Tenant ID, Client ID, and Client Secret, of your Asana instance, under the **Connections** step when prompted.<br>
