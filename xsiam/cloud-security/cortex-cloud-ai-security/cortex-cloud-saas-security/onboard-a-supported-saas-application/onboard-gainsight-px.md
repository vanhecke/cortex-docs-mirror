---
description: >-
  Connect a Gainsight PX instance to detect posture risks and compliance
  violations.
---

# Onboard Gainsight PX

For SaaS Security to detect posture risks in your Gainsight PX instance, you must onboard your Gainsight PX instance to SaaS Security. Through the onboarding process, SaaS Security logs in to Gainsight PX using administrator account credentials. SaaS Security uses this account to scan your Gainsight PX instance for misconfigured settings. If there are misconfigured settings, SaaS Security suggests a remediation action based on best practices.

To onboard your Gainsight PX instance, complete the following actions:

* Collect information for connecting to your Gainsight PX instance
* Connect SaaS Security to your Gainsight PX instance

***

### Step 1: Collect Information for Connecting to Your Gainsight PX Instance

To access your Gainsight PX instance, SaaS Security requires the following information, which you specify during the onboarding process.

| Item            | Description                                                      |
| --------------- | ---------------------------------------------------------------- |
| Email ID        | The login email address of a Gainsight PX administrator account. |
| Password        | The password of the Gainsight PX administrator account.          |
| Subscription ID | A unique identifier for your Gainsight PX subscription.          |

As you complete the following steps, make note of the values of the items described in the preceding table. You will need to enter these values during onboarding to access your Gainsight PX instance from SaaS Security.

1. Identify the Gainsight PX administrator account that SaaS Security will use to access your Gainsight PX instance.

Required Permissions: To enable SaaS Security to scan your Gainsight PX instance, the account must have administrator access.

2.  Identify your Gainsight PX subscription ID.

    1. Open a web browser to the Gainsight PX login page at [app.aptrinsic.com/authentication/login](https://app.aptrinsic.com/authentication/login) and log in as an administrator.
    2. In the left navigation pane, select Administration > SET UP > Company & Timezone.
    3. Copy the subscription ID and paste it into a text file.

    **Note**: Do not continue to the next step unless you have copied the subscription ID. You must provide this identifier to SaaS Security during the onboarding process.

***

### Step 2: Connect SaaS Security to Your Gainsight PX Instance

By adding a Gainsight PX app in Cortex, you enable SaaS Security to connect to your Gainsight PX instance.

1. Log in to Cortex.
2. Select **Settings > Data Sources and Integrations > Add New**. You can use the Search bar to find the app you want to connect to.
3. Click the Gainsight PX tile.
4. Under **Capabilities**, Enter a Name for your application.
5. Select Security Posture under Default Capabilities and click Next.
6. Under **Connections**, enter the administrator login credentials and the subscription ID.
7. Under **Configurations**, select a **Sync Interval**. Choose a meaningful **Tag** to distinguish between various applications in different environments.&#x20;
8. Click **Next** to complete the onboarding validation process.
