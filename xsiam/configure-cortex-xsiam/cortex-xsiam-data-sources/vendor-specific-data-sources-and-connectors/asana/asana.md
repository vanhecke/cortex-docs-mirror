---
description: Use Asana data with Cortex XSIAM.
---

# Asana

The capabilities and sub-capabilities listed for this connector are available with any active Cortex XSIAM or Cortex Cloud Posture Security license.

This connector includes the following capabilities and sub-capabilities (if applicable):

* **Security Posture:** Detect, monitor and alert on settings of your SaaS application.
  * **saas-posture-config-remediation:** Help remediate the misconfigured security settings of your SaaS application.

### How to configure the Asana connector

Cortex XSIAM supports the following Asana account plans:

* Enterprise+
* Legacy Enterprise

To access Asana, Cortex XSIAM requires the following information, which you will specify during the connection process.

* **Service Account** **Token**: A token that Asana generates for a service account that you create. The token is an alphanumeric string that Cortex XSIAM uses to authenticate to the Asana API.

Perform the following procedures in the order that they appear below.

#### Task 1: Create an Asana service account token <a href="#step-1-create-a-service-account-in-asana-and-save-the-token" id="step-1-create-a-service-account-in-asana-and-save-the-token"></a>

An Asana service account is a non-human, programmatic identity that Cortex XSIAM uses to scan your Asana workspace. Cortex XSIAM requires a service account an Asana service account token to access the Asana API. This token is displayed only once, so copy and save the token so you can provide it during data connection.

1. Open a web browser to the [Asana website](https://asana.com/) and log in as a Super Admin.

{% hint style="info" %}
To create an Asana service account, you must use an account assigned to the Super Admin role. Service accounts are an exclusive feature for organizations on Asana's Enterprise or Enterprise+ plans.
{% endhint %}

2. Navigate to the Admin Console. Locate your profile picture in the upper-right corner of the Asana webpage and select **\<profile-picture> > Admin console**.
3. In the left navigation pane, select **Apps > Service Accounts**.
4. On the Service Accounts page, click **Add Service Account**.
5. Complete the Add Service Account dialog:
   1. Specify a **Name** for the service account.&#x20;
   2. Under **Permission scopes**, select **Full permissions**.
6. Click **Save changes** to generate the service account token. Copy the service account token and paste it into a text file.

{% hint style="info" %}
Do not proceed to the next step unless you have copied the service account token. You must provide this token during the connection process.
{% endhint %}

#### Task 2: (Optional) Update the token expiration period <a href="#step-2-optional-update-the-token-expiration-period" id="step-2-optional-update-the-token-expiration-period"></a>

By default, the lifespan for service account tokens in Asana is 10 years. To limit the attack window if the token becomes compromised, set service account tokens to expire after 90 days.

1. From the left navigation pane in the Admin Console, select **Apps > Service Accounts**.
2. On the App settings page, locate the **Token Expiration** settings.
3. For the **When should service account tokens expire?** setting, select 90 days.
4. Click **Save changes**.

#### Task 3: **Connect Asana to Cortex XSIAM**

1. In Cortex XSIAM, navigate to **Settings** → **Data Sources & Integrations**.
2. Click **+ Add new**.
3. In the **Add Data Source** page, search for Asana.
4. Under **Recommended**, hover over the new Asana integration and click **Add Instance** to launch the configuration wizard.
5. Under the **Capabilities** tab, Enter a Name for your application.
6. Select Security Posture under **Default Capabilities**.
7. Click **Next**.
8. Under the **Connection** tab, enter the **Service Account Token** details.
9. Under the **Configuration** tab, select a **Sync Interval**. Choose a meaningful **Tag** to distinguish between various applications in different environments.
10. A confirmation message shows that your Asana instance is successfully connected. Confirm the **Summary** details and click **Save instance**.
