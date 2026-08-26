---
description: >-
  Connect a Cisco Duo instance in Cortex XSIAM to detect posture risks and
  compliance violations.
---

# Onboard Cisco Duo

For SaaS Security to detect posture risks in your Cisco Duo instance, you must onboard your Cisco Duo instance to SaaS Security. Through the onboarding process, SaaS Security connects to Cisco Duo's Admin API. After connecting to the Admin API, SaaS Security scans your Cisco Duo instance for misconfigured settings and account risks. To enable SaaS Security to connect to the Admin API, you create an Admin API application in Cisco Duo and configure it to grant SaaS Security only the permissions it needs to complete its scans.

The supported Cisco Duo editions for SaaS Security scans are:

* Duo Essentials
* Duo Advantage
* Duo Premier

To access your Cisco Duo instance, SaaS Security requires the following information, which you specify during the onboarding process.

| API Hostname    | A unique URL that serves as a secure entry point for all API requests between SaaS Security and your Cisco Duo instance. It ensures that SaaS Security is communicating directly with your Cisco Duo account.                                                                                |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Integration Key | SaaS Security accesses the Admin API through an Admin API application that you create in Cisco Duo. Cisco Duo generates an Integration Key to uniquely identify this application. The Integration Key acts as a username for SaaS Security to identify itself during the connection process. |
| Secret Key      | SaaS Security accesses the Admin API through an Admin API application that you create in Cisco Duo. Cisco Duo generates a Secret Key, which acts as a password that SaaS Security uses to securely authenticate to Cisco Duo.                                                                |

To onboard your Cisco Duo instance, complete the following actions.

***

### Step 1: Create the Admin API Application

Creating an Admin API application establishes a secure identity for SaaS Security within your Cisco Duo account. This identity enables Cisco Duo to recognize SaaS Security and authorize its API requests. You control SaaS Security' level of access by selecting specific permissions during the application setup.

1. Identify the Cisco Duo account that you will use to create the Admin API application. Required Permissions: To create an Admin API application, you must use an account assigned to the Owner role.
2. Open a web browser to the [Cisco Duo Admin Login](https://admin.duosecurity.com) page and log in to the Owner account you identified.
3. From the Dashboard's left navigation menu, select Applications > Applications.
4. On the Applications page, select + Add application.
5. On the Application Catalog page, locate the entry for an Admin API application and click + Add.
6. On your application's properties page, complete the following actions:
   1. Under Basic Configuration, specify a meaningful Application name, such as SaaS Security Integration. This name appears in the list of applications on the Applications page and in Cisco Duo administrator logs.
   2.  Under Details, copy the following items and paste them into a text file:

       * Integration key
       * Secret key
       * API hostname

       **Note**: Do not continue to the next step unless you have copied the Integration key, Secret key, and API hostname. You will provide this information to SaaS Security during the onboarding process.
   3. Under Permissions, select the following permissions:
      1. Grant administrators - Read
      2. Grant read the information
      3. Grant applications
      4. Grant settings
      5. Grant read log
      6. Grant resource - Read
      7. Click Save to save your Admin API application.

***

### Step 2: Connect SaaS Security to Your Cisco Duo Instance

By adding a Cisco Duo app in Cortex, you enable SaaS Security to connect to your Cisco Duo instance.

1. Log in to Cortex.
2. Select **Settings > Data Sources and Integrations > Add New**. You can use the Search bar to find the app you want to connect to.
3. Click the Cisco Duo tile.
4. Under **Capabilities**, Enter a Name for your application.
5. Select Security Posture under Default Capabilities and click Next.
6. Under **Connections**, provide the Integration Key, Secret Key, and API Hostname.
7. Under **Configurations**, select a Sync Interval. Choose a meaningful Tag to distinguish between various applications in different environments.
8. Click **Next** to complete the onboarding validation process.
