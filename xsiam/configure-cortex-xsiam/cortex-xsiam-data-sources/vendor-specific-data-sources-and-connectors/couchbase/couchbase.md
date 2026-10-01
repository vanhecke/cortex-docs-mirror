---
description: Use Couchbase data with Cortex XSIAM.
---

# Couchbase

This connector includes the following capabilities and sub-capabilities, if applicable:

* SaaS Posture Configuration Monitoring: Detect, monitor and alert on settings of your SaaS application.
  * saas-posture-config-remediation: Help remediate the misconfigured security settings of your SaaS application.

### How to configure the Couchbase connector <a href="#how-to-configure-the-asana-connector" id="how-to-configure-the-asana-connector"></a>

Cortex XSIAM supports the following Couchbase account plans:

* Developer Pro
* Enterprise

To access Couchbase, Cortex XSIAM requires the following information, which you will specify during the connection process.

* **API Key**: A unique, confidential alphanumeric string that you generate using an Organization Owner account on the Couchbase Capella platform. This credential, which Couchbase calls the API Secret, proves your identity and grants Cortex XSIAM the authority to authenticate and interact with your Couchbase instance. Couchbase displays this sensitive API Secret only once during key generation.

Perform the following procedures in the order that they appear below.

#### **Task 1:** Generate and Copy the API Key for Your Organization

1.  Identify the Couchbase account that you will use to create the API key.

    Required Permissions: You will need to assign the API key to the Organization Owner role. For this reason, the account that you use to create the key must also be assigned to the Organization Owner role.
2. Open a web browser to the [Couchbase login page](https://cloud.couchbase.com/sign-in) and log in to the Organization Owner account.
3. From the navigation bar at the top of the Couchbase page, navigate to Settings.
4. From the settings menu in the left-hand navigation, select **API Keys**.
5. On the Management API Keys page, click **+ Generate Key**.
6. On the Generate Management API Key page, complete the following actions:
   1. Specify a Key Name for the key. For effective logging and auditing, give the key a meaningful name. For example, Cortex XSIAM  Integration.
   2. (Optional) Provide a Description of the API key. For example, API key to enable Cortex XSIAM  scans.
7. Under Organization Roles, assign your key to the Organization Owner role.
8. Specify a Key Expiration period. The default expiration period is 180 days, because this key is assigned to the highly-privileged Organization Owner role, we recommend that you set the period to 90 days or less to enforce regular key rotation.
9. Click **Generate Key**. Couchbase generates the API key and its associated API secret.
10. Copy the API secret and paste it into a text file.

{% hint style="info" %}
Although Cortex XSIAM prompts you for an API key during onboarding, the value you enter in the API Key field is the API secret. Because Couchbase displays this API secret only once, do not continue to the next step without copying the API secret.
{% endhint %}

#### Task 2: Connect Couchbase to Cortex XSIAM

1. In Cortex XSIAM, navigate to **Settings** → **Data Sources & Integrations**.
2. Click **+ Add new**.
3. In the **Add Data Source** page, search for Couchbase.
4. Under **Recommended**, hover over the new Couchbase integration and click **Add Instance** to launch the configuration wizard.
5. Under the **Capabilities** tab, Enter a Name for your application.
6. Select Security Posture under **Default Capabilities**.
7. Click **Next**.
8. Under the **Connection** tab, enter the API secret in the API key field.
9. Under the **Configuration** tab, select a **Sync Interval**. Choose a meaningful **Tag** to distinguish between various applications in different environments.
10. A confirmation message shows that your Couchbase instance is successfully connected. Confirm the **Summary** details and click **Save instance**.
