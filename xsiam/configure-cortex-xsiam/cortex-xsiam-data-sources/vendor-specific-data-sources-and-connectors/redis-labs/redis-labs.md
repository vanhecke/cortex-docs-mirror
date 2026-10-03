---
description: Use Redis Labs data in Cortex XSIAM.
---

# Redis Labs

The capabilities and sub-capabilities listed for this connector are available with any active Cortex XSIAM or Cortex Cloud Posture Security license.

This connector includes the following capabilities and sub-capabilities (if applicable):

* SaaS Posture Configuration Monitoring: Detect, monitor and alert on settings of your SaaS application.
  * saas-posture-config-remediation: Help remediate the misconfigured security settings of your SaaS application.

### How to configure the Redis Labs connector <a href="#how-to-configure-the-aha-connector" id="how-to-configure-the-aha-connector"></a>

To access Redis Labs, Cortex XSIAM requires the following information, which you will specify during the connection process.

* **Account key**: An API account key that Redis Labs generates the first time a Redis Labs account owner enables the REST API. The API account key is an alphanumeric string that uniquely identifies your Redis Labs account. Cortex XSIAM uses this key and the API user key to authenticate to a Redis Labs API.
*   **User key**: An API user key that you create in Redis Labs and associate with a particular user. Cortex XSIAM uses this key to authenticate to a Redis Labs API. Redis Labs authorizes requests from Cortex XSIAM based on the key's role, which it inherits from the user associated with the key.



To onboard your Redis Labs instance, complete the following steps.

#### Task 1: Locate and Copy Your API Account Key <a href="#step-1-identify-the-redis-labs-owner-account" id="step-1-identify-the-redis-labs-owner-account"></a>

1. Identify the Redis Labs user who will get the API account key and API user key.\
   Required Permissions: The user must be assigned to the Owner role in Redis Labs. The Owner role is required to enable the Redis Cloud REST API and to create an API user key.
2. Open a web browser to [the Redis Labs login page](https://app.redislabs.com/#/login) and log in as the Owner you identified.
3. Redis Labs generates a unique API account key the first time a Redis Labs account Owner enables the REST API. This API account key appears on the Access Management page.
4. From the left navigation pane, select **Access Management**.
5. On the Access Management page, select the API Keys tab. If another Owner previously enabled the API, the API account key appears on this page. Otherwise, the page contains an **Enable API** button.
6. If necessary, click **Enable API**.
7. Copy the API account key and paste it into a text file. Do not continue to the next step unless you have copied the API account key. You will provide this key to Cortex XSIAM during the onboarding process.

#### Task 2: Create and Copy an API User Key

When you create an API user key, you associate the key with a specific Redis Labs user. The key's permissions are based on the associated user's role.

1. On the Access Management page's API Keys tab, locate the API User Keys section.
2. In the API User Keys section, click the add button **(+)**. Redis Labs displays an empty entry for you to configure your API user key.
3. In the empty entry, complete the following actions:
   1. Specify an API key name. For effective logging, auditing, and future maintenance, supply a descriptive name that clearly identifies the purpose of the key. For example, SaaS Security-integration.
   2. Select a User name from the list. The user you select must be assigned to the Owner role.
   3. Click **Create**. Redis Labs generates and displays your API user key.
4. Copy the API user key and paste it into a text file. Do not continue to the next step unless you have copied the API user key. You will provide this key to Cortex XSIAM during the onboarding process.

#### **Task 3: Connect Redis Labs to Cortex XSIAM**

1. In Cortex XSIAM, navigate to **Settings** → **Data Sources & Integrations**.
2. Click **+ Add new**.
3. In the **Add Data Sources or Integrations** page, search for Redis Labs.
4. Under **Recommended**, hover over the new Redis Labs integration and click **Add Instance** to launch the configuration wizard.
5. Under the **Capabilities** tab, Enter a Name for your application.
6. Select Security Posture under **Default Capabilities**.
7. Click **Next**.
8. Under **Connection**, enter your Account key and User key.
9. Under **Configuration** tab, select a **Sync Interval**. Choose a meaningful **Tag** to distinguish between various applications in different environments.
10. A confirmation message indicates that Redis Labs is successfully connected. Confirm the Summary details and click **Save instance**.

