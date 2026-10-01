---
description: Use Gainsight data with Cortex XSIAM.
---

# Gainsight

The capabilities and sub-capabilities listed for this connector are available with any active Cortex XSIAM or Cortex Cloud Posture Security license.

This connector includes the following capabilities and sub-capabilities (if applicable):

* Security Posture: Detect, monitor and alert on settings of your SaaS application.
  * saas-posture-config-remediation: Help remediate the misconfigured security settings of your SaaS application.

### How to configure the Gainsight connector <a href="#how-to-configure-the-aha-connector" id="how-to-configure-the-aha-connector"></a>

To access Gainsight, Cortex XSIAM requires the following information, which you will specify during the connection process.

* Gainsight account information

#### **Task 1: Collect** Gainsight **account information**

To access your Gainsight instance, Cortex XSIAM requires the following information, which you specify during the onboarding process.

* **ItemDescription**: The login email address of a Gainsight PX administrator account.
* **Email ID**: The password of the Gainsight PX administrator account.
* **Password**
* **Subscription ID**: A unique identifier for your Gainsight subscription.

As you complete the following steps, make note of the values of the items described in the preceding table. You will need to enter these values during onboarding to access your Gainsight PX instance from Cortex XSIAM.

1. Identify the Gainsight administrator account that SaaS Security will use to access your Gainsight instance. Required Permissions: To enable SaaS Security to scan your Gainsight PX instance, the account must have administrator access.
2. Identify your Gainsight subscription ID.
3. Open a web browser to the Gainsight login page at [app.aptrinsic.com/authentication/login](https://app.aptrinsic.com/authentication/login) and log in as an administrator.
4. In the left navigation pane, select Administration > SET UP > Company & Timezone.
5. Copy the subscription ID and paste it into a text file.

{% hint style="info" %}
Do not continue to the next step unless you have copied the subscription ID. You must provide this identifier to SaaS Security during the onboarding process.
{% endhint %}

#### **Task 2: Connect** Gainsight **to Cortex XSIAM**

1. In Cortex XSIAM, navigate to **Settings** → **Data Sources & Integrations**.
2. Click **+ Add new**.
3. In the **Add Data Sources or Integrations** page, search for Gainsight.
4. Under **Recommended**, hover over the new Gainsight integration and click **Add Instance** to launch the configuration wizard.
5. Under the **Capabilities** tab, Enter a Name for your application.
6. Select Security Posture under **Default Capabilities**.
7. Click **Next**.
8. Under **Connection**, enter the administrator login credentials and the subscription ID details.
9. Under **Configuration** tab, select a **Sync Interval**. Choose a meaningful **Tag** to distinguish between various applications in different environments.
10. A confirmation message indicates that Gainsight is successfully connected. Confirm the Summary details and click **Save instance**.

