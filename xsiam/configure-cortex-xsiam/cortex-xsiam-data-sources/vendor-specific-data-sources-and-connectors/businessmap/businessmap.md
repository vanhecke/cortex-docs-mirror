---
description: Use Businessmap data with Cortex XSIAM.
---

# Businessmap

The capabilities and sub-capabilities listed for this connector are available with any active Cortex XSIAM or Cortex Cloud Posture Security license.

This connector includes the following capabilities and sub-capabilities (if applicable):

* **Security Posture:** Detect, monitor and alert on settings of your SaaS application.
  * `saas-posture-config-remediation`: Help remediate the misconfigured security settings of your SaaS application.

### How to configure the Businessmap connector <a href="#how-to-configure-the-asana-connector" id="how-to-configure-the-asana-connector"></a>

Cortex XSIAM supports the following Businessmap account plans:

To access Businessmap, Cortex XSIAM requires the following information, which you will specify during the connection process.

* **Host name**: A unique subdomain for your Businessmap instance, which appears as part of your Businessmap URL.
* **API Key**: A generated character string that identifies a Businessmap administrator to the Businessmap API. Cortex XSIAM requires this API key to authenticate to the API. The key inherits the permissions of the administrator who creates it. Required permissions: The user who generates the API key must have the following Admin privileges: Manage Integrations, Access Audit Logs.

Perform the following procedures in the order that they appear below.

#### **Task 1:** Identify your Host name

1. Open a web browser to the [Businessmap login page](https://businessmap.io/) or your unique company subdomain URL, and log in to the account you identified.
2. After you log in to Businessmap, your host name appears as a unique subdomain in the URL. For example, \<subdomain>.kanbanize.com. Make note of your host name before you continue to the next step. You will provide this host name to Cortex XSIAM during the onboarding process.

#### Task 3: Generate and copy an API key

1. Click your profile icon in the top-right corner of the page and select API. Businessmap opens your My Account settings to the API tab.
2. If an API key was already generated for the account, it is shown on the API tab. If not, click Generate API key.
3. Copy your API key and paste it into a text file. Do not continue to the next step unless you have copied your API key. You will provide this key to Cortex XSIAM during the onboarding process.

#### **Task 3: Connect** Businessmap **to Cortex XSIAM**

1. In Cortex XSIAM, navigate to **Settings** → **Data Sources & Integrations**.<a class="button secondary"></a>
2. Click **+ Add new**.
3. In the **Add Data Source** page, search for Businessmap.
4. Under **Recommended**, hover over the new Businessmap integration and click **Add Instance** to launch the configuration wizard.
5. Under the **Capabilities** tab, Enter a Name for your application.
6. Select Security Posture under **Default Capabilities**.
7. Click **Next**.
8. Under the **Connection** tab, enter the Host Name and API key details.
9. Under the **Configuration** tab, select a **Sync Interval**. Choose a meaningful **Tag** to distinguish between various applications in different environments.
10. A confirmation message shows that your Businessmap instance is successfully connected. Confirm the **Summary** details and click **Save instance**.

