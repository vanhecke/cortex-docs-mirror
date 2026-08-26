---
description: >-
  Connect a Couchbase instance in Cortex XSIAM to detect posture risks and
  compliance violations.
---

# Onboard Couchbase

For SaaS Security to detect posture risks in your Couchbase instance, you must onboard your Couchbase instance to SaaS Security. Through the onboarding process, SaaS Security connects to a Couchbase API by using an API key that you generate from within Couchbase. After connecting to the Couchbase API, SaaS Security scans your Couchbase instance for misconfigured settings and account risks.

The supported Couchbase account plans for SaaS Security scans are:

* Developer Pro
* Enterprise

To access your Couchbase instance, SaaS Security requires the following information, which you specify during the onboarding process.

| API Key | A unique, confidential alphanumeric string that you generate using an Organization Owner account on the Couchbase Capella platform. This credential, which Couchbase calls the API Secret, proves your identity and grants SaaS Security the authority to authenticate and interact with your Couchbase instance. Couchbase displays this sensitive API Secret only once during key generation. |
| ------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

To onboard your Couchbase instance, complete the following actions.

***

### Step 1: Generate and Copy the API Key for Your Organization

1. Identify the Couchbase account that you will use to create the API key.

Required Permissions: You will need to assign the API key to the Organization Owner role. For this reason, the account that you use to create the key must also be assigned to the Organization Owner role.

2. Open a web browser to the [Couchbase login page](https://cloud.couchbase.com/sign-in) and log in to the Organization Owner account.
3. From the navigation bar at the top of the Couchbase page, navigate to Settings.
4. From the settings menu in the left-hand navigation, select API Keys.
5. On the Management API Keys page, click + Generate Key.
6. On the Generate Management API Key page, complete the following actions:
   1. Specify a Key Name for the key. For effective logging and auditing, give the key a meaningful name. For example, SaaS Security Integration.
   2. (Optional) Provide a Description of the API key. For example, API key to enable SaaS Security scans.
   3. Under Organization Roles, assign your key to the Organization Owner role.
   4. Specify a Key Expiration period. The default expiration period is 180 days. Because this key is assigned to the highly-privileged Organization Owner role, we recommend that you set the period to 90 days or less to enforce regular key rotation.
   5. Click Generate Key. Couchbase generates the API key and its associated API secret.
7. Copy the API secret and paste it into a text file.

**Note**: Although SaaS Security prompts you for an API key during onboarding, the value you enter in the API Key field is the API secret. Because Couchbase displays this API secret only once, do not continue to the next step without copying the API secret.

***

### Step 2: Connect SaaS Security to Your Couchbase Instance

By adding a Couchbase app in Cortex, you enable SaaS Security to connect to your Couchbase instance.

1. Log in to Cortex.
2. Select **Settings > Data Sources and Integrations > Add New**. You can use the Search bar to find the app you want to connect to.
3. Click the Couchbase tile.
4. Under **Capabilities**, Enter a Name for your application.
5. Select Security Posture under Default Capabilities and click Next.
6. Under **Connections**, enter the API secret in the API key field
7. Under **Configurations**, select a **Sync Interval**. Choose a meaningful **Tag** to distinguish between various applications in different environments.
8. Click **Next** to complete the onboarding validation process.
