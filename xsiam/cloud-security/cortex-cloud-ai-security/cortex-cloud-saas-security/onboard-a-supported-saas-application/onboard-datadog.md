---
description: >-
  Onboard Datadog to Cortex XSIAM for SaaS security posture monitoring and
  compliance visibility.
---

# Onboard Datadog

For SaaS Security to detect posture risks in your Datadog instance, you must onboard your Datadog instance to SaaS Security. Through the onboarding process, SaaS Security connects to a Datadog API and, through the API, scans your Datadog instance for misconfigured settings. If there are misconfigured settings, SaaS Security suggests a remediation action based on best practices.

To onboard your Datadog instance, complete the following actions:

* Collect information for accessing your Datadog instance
* Connect SaaS Security to your Datadog instance

***

### Step 1: Collect Information for Accessing Your Datadog Instance

To access your Datadog instance, SaaS Security requires the following information, which you specify during the onboarding process.

| Item            | Description                                                                                                                                                                                                |
| --------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Region          | Datadog manages a number of independent sites in separate geographic areas around the world. Because these sites are separate from each other, you must specify which regional Datadog site you are using. |
| API Key         | A generated character string that uniquely identifies your organization to the Datadog API. SaaS Security requires this API key to authenticate to the Datadog API.                                        |
| Application Key | A generated character string that the Datadog API uses to determine the access permissions of a calling application. The application key is associated with the administrator who generates the key.       |

As you complete the following steps, make note of the values of the items described in the preceding table. You will need to enter these values during onboarding to access your Datadog instance from SaaS Security.

1. Identify the Datadog administrator account that will generate the API Key and Application Key.

Required Permissions: The administrator must have the Datadog Admin role with the following permissions:

* Org Management
* User App Keys
* API Keys Read
* API Keys Write

2. Identify your Datadog region.
   1. Open a web browser and go to the Datadog login page that you use to access your Datadog instance.
   2. Make a note of the regional Datadog site that your organization is using. Use the following table to determine your region based on the site URL.

| URL                                                    | Region  |
| ------------------------------------------------------ | ------- |
| [https://app.datadoghq.com](https://app.datadoghq.com) | US1     |
| [https://us3.datadoghq.com](https://us3.datadoghq.com) | US3     |
| [https://us5.datadoghq.com](https://us5.datadoghq.com) | US5     |
| [https://app.datadoghq.eu](https://app.datadoghq.eu)   | EU1     |
| [https://app.ddog-gov.com](https://app.ddog-gov.com)   | US1-FED |

**Note**: Do not continue to the next step unless you have recorded the region information. You must provide this information to SaaS Security during the onboarding process.

c. Log in to the administrator account.

3.  Generate an API key for your organization.

    1. Click your Datadog account icon in the top-right corner and select Organization Settings.
    2. On the Organization Settings page, select API Keys.
    3. Click New Key.
    4. In the New API Key dialog, enter a name for the key and click Create Key. Datadog generates and displays your new key.
    5. Click Copy Key and paste the key into a text file.

    **Note**: Do not continue to the next step unless you have copied the API Key. You must provide this key to SaaS Security during the onboarding process.
4.  Generate an Application key to grant SaaS Security access permissions. **Note**: An application key inherits the permissions of the person who creates it, but you can further limit the application's access to certain authorization scopes. If you scope the application key, SaaS Security will be unable to access some of your Datadog instance's settings — up to 19 settings may be inaccessible, preventing SaaS Security from determining if those settings are misconfigured. To avoid restricting SaaS Security' access, create an unscoped application key.

    On the Organization Settings page, select Application Keys.

    1. Click New Key.
    2. In the New Key dialog, enter a name for the key and click Create Key. Datadog generates and displays your new key.
    3. Click Copy Key and paste the key into a text file.

**Note**: Do not continue to the next step unless you have copied the Application Key. You must provide this key to SaaS Security during the onboarding process.

***

### Step 2: Connect SaaS Security to Your Datadog Instance

By adding a Datadog app in Cortex, you enable SaaS Security to connect to your Datadog instance.

1. Log in to Cortex.
2. Select **Settings > Data Sources and Integrations > Add New**. You can use the Search bar to find the app you want to connect to.
3. Click the Datadog tile.
4. Enter a name for your app in the **Capabilities** field.
5. Select Security Posture under **Security Capabilities** and click **Next**.
6. On the **Connections** tab, enter the API Key, Application Key, and Region for your Datadog instance.
7. Click **Next** to complete the onboarding validation process.

\
\
<br>
