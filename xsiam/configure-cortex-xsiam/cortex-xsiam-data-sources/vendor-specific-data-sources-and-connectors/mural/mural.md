---
description: Use Mural data with Cortex XSIAM.
---

# Mural

The capabilities and sub-capabilities listed for this connector are available with any active Cortex XSIAM or Cortex Cloud Posture Security license.

This connector includes the following capabilities and sub-capabilities (if applicable):

* SaaS Posture Configuration Monitoring: Detect, monitor and alert on settings of your SaaS application.
  * saas-posture-config-remediation: Help remediate the misconfigured security settings of your SaaS application.

### How to configure the Mural connector <a href="#how-to-configure-the-aha-connector" id="how-to-configure-the-aha-connector"></a>

To access Mural, Cortex XSIAM requires the following information, which you will specify during the connection process.

* **API Key**: A generated character string that gives SaaS Security access to Mural's Enterprise API. You configure this key to limit Cortex XSIAM's access to only the scopes it requires. Required permissions: You must be a Company Admin to create the Enterprise API key.

Perform the following actions in the order specified.

#### **Task 1:** Generate and copy the enterprise API key

1. Identify the Mural account that you will use to generate the Enterprise API key.\
   Required permissions: The account that generates the API key must be assigned to the Company Admin role in Mural.
2. Open a web browser to the [Mural login page](https://app.mural.co/) and log in to the account you identified.
3. Navigate to the Company Dashboard in Mural. Locate your avatar in the upper-right corner of the Mural page and select **\<your-avatar> > Manage company**.
4. From the Company Dashboard's left-hand navigation pane, select **API keys**. The API keys item appears under the Development section.
5. On the API Keys page, click **Create API Key**. The Create API key dialog prompts you to select the API scopes that the key will authorize SaaS Security to access.
6. In the Create API key dialog, select the following scopes, which Cortex XSIAM requires:
   * Member information
   * User activity logs
   * Reports
7. Click **Create API key**. Mural generates and displays the Enterprise API key.
8. Copy the API key and paste it into a text file. Do not continue to the next step unless you have copied the API key. This is the only time that Mural displays the API key, and you must provide this key to Cortex XSIAM during the onboarding process.

#### Task 2: Connect Mural to Cortex XSIAM <a href="#step-4-connect-saas-security-to-your-mural-instance" id="step-4-connect-saas-security-to-your-mural-instance"></a>

1. Log in to Cortex XSIAM.
2. Select **Settings > Data Sources and Integrations > Add New**. You can use the Search bar to find the app you want to connect to.
3. Click the Mural tile.
4. Under **Capabilities**, enter a name for your application.
5. Select Security Posture under Default Capabilities and click Next.
6. Under **Connections**, enter your API key.
7. Under **Configurations**, select a **Sync Interval**. Choose a meaningful **Tag** to distinguish between various applications in different environments.
8. A confirmation message indicates that Harness is successfully connected. Confirm the Summary details and click **Save instance**.
