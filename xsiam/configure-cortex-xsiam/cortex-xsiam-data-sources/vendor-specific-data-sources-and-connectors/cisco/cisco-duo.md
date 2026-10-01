---
description: Use Cisco Duo data with Cortex XSIAM.
---

# Cisco Duo

The capabilities and sub-capabilities listed for this connector are available with any active Cortex XSIAM or Cortex Cloud Posture Security license.

This connector includes the following capabilities and sub-capabilities (if applicable):

* SaaS Posture Configuration Monitoring: Detect, monitor and alert on settings of your SaaS application.
  * saas-posture-config-remediation: Help remediate the misconfigured security settings of your SaaS application.

### How to configure the Cisco Duo connector

Cortex XSIAM supports the following Cisco Duo editions:

* Duo Essentials
* Duo Advantage
* Duo Premier

To access Cisco Duo, Cortex XSIAM requires the following information, which you will specify during the connection process.

* **API Hostname**: A unique URL that serves as a secure entry point for all API requests between Cortex XSIAM and your Cisco Duo instance. It ensures that Cortex XSIAM is communicating directly with your Cisco Duo account.
* **Integration Key**: Cortex XSIAM accesses the Admin API through an Admin API application that you create in Cisco Duo. Cisco Duo generates an Integration Key to uniquely identify this application. The Integration Key acts as a username for Cortex XSIAM to identify itself during the connection process.
* **Secret Key:** Cortex XSIAM  accesses the Admin API through an Admin API application that you create in Cisco Duo. Cisco Duo generates a Secret Key, which acts as a password that Cortex XSIAM uses to securely authenticate to Cisco Duo.

Perform the following procedures in the order that they appear below.

#### **Task 1:** Create the Admin API application

Creating an Admin API application establishes a secure identity for Cortex XSIAM within your Cisco Duo account. This identity enables Cisco Duo to recognize Cortex XSIAM and authorize its API requests. You control the level of access by selecting specific permissions during the application setup.

1. Identify the Cisco Duo account that you will use to create the Admin API application. Required Permissions: To create an Admin API application, you must use an account assigned to the Owner role.
2. Open a web browser to the [Cisco Duo Admin Login](https://admin.duosecurity.com/) page and log in to the Owner account you identified.
3. From the Dashboard's left navigation menu, select **Applications > Applications**.
4. On the Applications page, select **+ Add application**.
5. On the Application Catalog page, locate the entry for an Admin API application and click **+ Add**.
6. On your application's properties page, complete the following actions:
   1. Under Basic Configuration, specify a meaningful Application name, such as Cortex XSIAM Integration. This name appears in the list of applications on the Applications page and in Cisco Duo administrator logs.
   2.  Under Details, copy the following items and paste them into a text file:

       * Integration key
       * Secret key
       * API hostname

       Do not continue to the next step unless you have copied the Integration key, Secret key, and API hostname. You will provide this information to Cortex XSIAM during the onboarding process.
   3.  Under Permissions, select the following permissions:

       * Grant administrators - Read
       * Grant read the information
       * Grant applications
       * Grant settings
       * Grant read log
       * Grant resource - Read

       d. Click Save&#x20;

#### **Task 2: Connect** Cisco Duo **to Cortex XSIAM**

1. In Cortex XSIAM, navigate to **Settings** → **Data Sources & Integrations**.
2. Click **+ Add new**.
3. In the **Add Data Source** page, search for Cisco Duo.
4. Under **Recommended**, hover over the new Cisco Duo integration and click **Add Instance** to launch the configuration wizard.
5. Under the **Capabilities** tab, Enter a Name for your application.
6. Select Security Posture under **Default Capabilities**.
7. Click **Next**.
8. Under the **Connection** tab, enter the Integration Key, Secret Key, and API Hostname.
9. Under the **Configuration** tab, select a **Sync Interval**. Choose a meaningful **Tag** to distinguish between various applications in different environments.
10. A confirmation message shows that your Cisco Duo instance is successfully connected. Confirm the **Summary** details and click **Save instance**.

<br>
