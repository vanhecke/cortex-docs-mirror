---
description: Ingest Okta logs and configuration data into Cortex XSIAM.
---

# Ingest logs and data from Okta

<details>

<summary>Product availability and licensing</summary>

The options available in the UI depend on your specific product license:

| Feature                   | Cloud Posture Security | Cloud Runtime Security              | Cortex XDR Cloud                                                     | Cortex XSIAM NG SIEM, Cortex XSIAM Enterprise, and Cortex XSIAM Premium | Cortex XSIAM Enterprise Plus |
| ------------------------- | ---------------------- | ----------------------------------- | -------------------------------------------------------------------- | ----------------------------------------------------------------------- | ---------------------------- |
| **Collect Logs**          | Enabled                | Enabled with Data Collection add-on | Enabled with Data Collection add-on                                  | Enabled                                                                 | Enabled                      |
| **Collect Configuration** | Enabled                | Enabled                             | Enabled with Cloud Posture Security or Cloud Runtime Security add-on | Enabled with Cloud Posture Security or Cloud Runtime Security add-on    | Disabled                     |

</details>

{% hint style="warning" %}
**Administrator privileges**: Your Okta user must have a role capable of creating API tokens, such as Read-only Administrator, Super Administrator, or Organization Administrator. For more information, see the [Okta Administrators Documentation](https://help.okta.com/en-us/Content/Topics/Security/Administrators.htm?cshid=ext_Security_Administrators).
{% endhint %}

To receive logs and configuration data from Okta, configure the **Data Sources & Integrations** settings. Once enabled, the system immediately begins ingesting activity logs and identity configuration metadata, according to your configuration settings.

Activity logs are searchable using the Cortex Query Language (XQL). For more information, see [Perform advanced Identity Security investigations using XQL](perform-advanced-identity-security-investigations-using-xql).

Configuration data is used for Identity Security visibility and is searchable in **Identity Security** → **Identity Asset Inventory** and using the `ciem_permissions_with_last_access` dataset.

<details>

<summary>API rate limits and monitoring</summary>

The Okta API enforces concurrent rate limits. To prevent service disruption:

* The Okta data collector includes a mechanism that automatically reduces the amount of requests whenever an error is received from the Okta API indicating that too many requests have already been sent.
* To ensure you are notified when this occurs, an alert is displayed in the **Notification Area** and a record is added to the **Management Audit Logs**.

</details>

<details>

<summary>How to configure the Okta collection?</summary>

**Step 1: Configure Okta for integration**

The same Okta domain, API token, and permissions are used for both log and configuration collection, as both features utilize the same Okta API.

Perform these steps in your Okta Admin Console to prepare for the connection.

1.  Identify your Okta Domain:

    1. From the Okta Dashboard, click the down arrow under your name in the top-right corner.
    2. Copy the **Org URL**, such as `https://example.okta.com`, and save it for the **Okta Domain** field in Cortex Cloud.

    For more information, see the [Okta Documentation](https://developer.okta.com/docs/guides/find-your-domain/findorg/).
2. Obtain your authentication token in Okta:
   1. Select **Security** → **API** → **Tokens**, and click **Create token**.
   2. Set the following parameters for the token:
      * **What do you want your token to be named?**: Specify the name for your token, which is used for tracking API calls.
      * **API calls made with this token must originate from**: Select **Any IP**.
   3. Click **Create token**. You may need to login to Okta again using your MFA administrator credentials.
   4. Your token is successfully created. Copy the **Token Value** and record it immediately. You will need this for the **TOKEN** field in Cortex Cloud. Once you close the dialog box by clicking **Ok, got it**, you won't be able to access the token again and will have to create a new one if you didn't record it.

**Step 2: Configure the Okta Collector in Cortex Cloud**

1. Select **Settings** → **Data Sources & Integrations**.
2. On the **Data Sources & Integrations** page, click **+ Add New**, search for **Okta**, then hover over it and click **Add**.
3. Integrate the Okta authentication service with Cortex Cloud:
   1. Enter the **Okta Domain** (Org URL) and **Token** obtained in Step 1.
   2. **Collect Logs**: Select this option to ingest activity logs.
   3. (Optional) Define an **Event Filter** to configure collection for events of your choosing.
      * All events are collected by default unless you define an Okta API Filter expression, such as `filter=eventType eq “user.session.start”`.
      * For Okta information to be woven into authentication stories, `“user.authentication.sso”` events must be collected.
   4. **Collect Configuration**: Select this option to provide deep visibility into identities and permissions, offering comprehensive insights into users, user groups, and applications. It specifically highlights the permissions granted to Okta users in cloud environments, centralizing group memberships to secure your identity landscape.
   5. **Test** the connection.
   6. Click **Enable**.

**Step 3. Accessing the data**

Data is routed differently depending on which collection option is enabled:

Activity Data (using **Collect Logs**)

* **XQL**: Searchable using the Cortex Query Language (XQL). For more information, see [Perform advanced Identity Security investigations using XQL](perform-advanced-identity-security-investigations-using-xql).

Configuration data (using **Collect Configuration**)

* **Identity inventory**: Access the data in the Identity Asset Inventory within the Cortex Cloud Identity Security module (**Identity Security** → **Identity Asset Inventory**).
* **XQL**: Use the following dataset for CIEM (Cloud Infrastructure Entitlements Management) visibility: `ciem_permissions_with_last_access`

</details>
