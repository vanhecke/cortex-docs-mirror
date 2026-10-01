---
description: Use DataDog data with Cortex XSIAM.
---

# DataDog

The capabilities and sub-capabilities listed for this connector are available with any active Cortex XSIAM or Cortex Cloud Posture Security license.

This connector includes the following capabilities and sub-capabilities (if applicable):

* **Security Posture:** Detect, monitor and alert on settings of your SaaS application.
  * `saas-posture-config-remediation`: Help remediate the misconfigured security settings of your SaaS application.

### How to configure the DataDog connector

To access DataDog, Cortex XSIAM requires the following information, which you will specify during the connection process.

* Account information for accessing your Datadog instance

#### Task 1: Collect Information for accessing Your Datadog Instance

To access your Datadog instance, Cortex XSIAM requires the following information, which you specify during the onboarding process.

| Item            | Description                                                                                                                                                                                                |
| --------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Region          | Datadog manages a number of independent sites in separate geographic areas around the world. Because these sites are separate from each other, you must specify which regional Datadog site you are using. |
| API Key         | A generated character string that uniquely identifies your organization to the Datadog API. Cortex XSIAM requires this API key to authenticate to the Datadog API.                                         |
| Application Key | A generated character string that the Datadog API uses to determine the access permissions of a calling application. The application key is associated with the administrator who generates the key.       |

As you complete the following steps, make note of the values of the items described in the preceding table. You will need to enter these values during onboarding to access your Datadog instance from Cortex XSIAM.

1. Identify the Datadog administrator account that will generate the API Key and Application Key.

Required Permissions: The administrator must have the Datadog Admin role with the following permissions:

* Org Management
* User App Keys
* API Keys Read
* API Keys Write

2. Identify your Datadog region.
   1. Open a web browser and go to the Datadog login page that you use to access your Datadog instance.
   2. Make a note of the regional Datadog site that your organization is using. Use the following table to determine your region based on the site URL. Do not continue to the next step unless you have recorded the region information. You must provide this information to Cortex XSIAM during the onboarding process.

| URL                                                    | Region  |
| ------------------------------------------------------ | ------- |
| [https://app.datadoghq.com](https://app.datadoghq.com) | US1     |
| [https://us3.datadoghq.com](https://us3.datadoghq.com) | US3     |
| [https://us5.datadoghq.com](https://us5.datadoghq.com) | US5     |
| [https://app.datadoghq.eu](https://app.datadoghq.eu)   | EU1     |
| [https://app.ddog-gov.com](https://app.ddog-gov.com)   | US1-FED |

3. Log in to the administrator account.
4. Generate an API key for your organization.
   1. Click your Datadog account icon in the top-right corner and select Organization Settings.
   2. On the Organization Settings page, select API Keys.
   3. Click New Key.
   4. In the New API Key dialog, enter a name for the key and click Create Key. Datadog generates and displays your new key.
   5. Click Copy Key and paste the key into a text file. Do not continue to the next step unless you have copied the API Key. You must provide this key to Cortex XSIAM during the data connection process.
5. Generate an Application key to grant Cortex XSIAM access permissions. An application key inherits the permissions of the person who creates it, but you can further limit the application's access to certain authorization scopes. If you scope the application key, Cortex XSIAM will be unable to access some of your Datadog instance's settings — up to 19 settings may be inaccessible, preventing Cortex XSIAM from determining if those settings are misconfigured. To avoid restricting Cortex XSIAM's access, create an unscoped application key.
6. On the Organization Settings page, select Application Keys.
   1. Click New Key.
   2. In the New Key dialog, enter a name for the key and click Create Key. Datadog generates and displays your new key.
   3. Click Copy Key and paste the key into a text file.

#### **Task 2: Connect** Datadog **to Cortex XSIAM**

1. In Cortex XSIAM, navigate to **Settings** → **Data Sources & Integrations**.
2. Click **+ Add new**.
3. In the **Add Data Sources or Integrations** page, search for Datadog.
4. Under **Recommended**, hover over the new Datadog integration and click **Add Instance** to launch the configuration wizard.
5. Under the **Capabilities** tab, Enter a Name for your application.
6. Select Security Posture under **Default Capabilities**.
7. Click **Next**.
8. Under **Connection**, enter the API Key, Application Key, and Region for your Datadog instance.
9. Under **Configuration** tab, select a **Sync Interval**. Choose a meaningful **Tag** to distinguish between various applications in different environments.
10. A confirmation message indicates that Datadog is successfully connected. Confirm the Summary details and click **Save instance**.
