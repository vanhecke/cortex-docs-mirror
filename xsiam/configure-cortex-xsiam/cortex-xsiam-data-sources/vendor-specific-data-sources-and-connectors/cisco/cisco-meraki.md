---
description: Use Cisco Meraki data with Cortex XSIAM.
---

# Cisco Meraki

The capabilities and sub-capabilities listed for this connector are available with any active Cortex XSIAM or Cortex Cloud Posture Security license.

This connector includes the following capabilities and sub-capabilities (if applicable):

* Security Posture: Detect, monitor and alert on settings of your SaaS application.
  * saas-posture-config-remediation: Help remediate the misconfigured security settings of your SaaS application.

## How to configure the Cisco Meraki connector <a href="#how-to-configure-the-asana-connector" id="how-to-configure-the-asana-connector"></a>

To access Cisco Meraki, Cortex XSIAM requires the following information, which you will specify during the connection process.

* **API Key**: The token is an alphanumeric string that Cortex XSIAM uses to authenticate to the Cisco Meraki API.

Perform the following procedures in the order that they appear below.

#### **Task 1: Create a Cisco Meraki** **API Key**

To access a Cisco Meraki API, Cortex XSIAM requires an API key that an organization administrator generates. This administrator must also enable access to the Cisco Meraki dashboard API. The API key inherits the permissions of the administrator who generates the key.

1. Log in to Cisco Meraki  as an organization administrator with full permissions.
2. If more than one Cisco Meraki account and organization are associated with your login email address, Cisco Meraki prompts you to select an organization. Navigate to the organization for which you'll be generating the API access key.
3. From the Cisco Meraki dashboard, navigate to your profile. Locate your login email address in the upper-right corner of the dashboard and select \<login\_name> > My Profile.
4. On your profile page, locate the API access section and click **Generate new API key**. Administrators can have only two keys associated with their account. If you already have two API keys, you will need to revoke one before you can generate a new API key.
5. Cisco Meraki generates and displays your new key.
6. Copy your API key and paste it into a text file. Do not continue to the next step unless you have copied the API key. You must provide this key to Cortex XSIAM during the onboarding process.
7. Enable access to the Cisco Meraki dashboard API.
   1. Select **Organization > Settings** to open the Organization Settings page.
   2. On the Organization Settings page, locate the Dashboard API access section. Select **Enable access to the Cisco Meraki Dashboard API** and click **Save Changes**.

#### **Task 2: Connect** Cisco Meraki **to Cortex XSIAM**

1. In Cortex XSIAM, navigate to **Settings** → **Data Sources & Integrations**.
2. Click **+ Add new**.
3. In the **Add Data Source** page, search for Cisco Meraki .
4. Under **Recommended**, hover over the new Cisco Meraki integration and click **Add Instance** to launch the configuration wizard.
5. Under the **Capabilities** tab, Enter a Name for your application.
6. Select Security Posture under **Default Capabilities**.
7. Click **Next**.
8. Under the **Connection** tab, enter the **API key** details.
9. Under the **Configuration** tab, select a **Sync Interval**. Choose a meaningful **Tag** to distinguish between various applications in different environments.
10. A confirmation message shows that your Cisco Meraki instance is successfully connected. Confirm the **Summary** details and click **Save instance**.

