---
description: Ingest Salesforce logs and data into Cortex XSIAM.
---

# Ingest logs and data from Salesforce

Cortex XSIAM supports the collection of Salesforce near-real-time (NRT) events, Setup Audit Trail, Content Metadata, Accounts, event log files, and snapshots. This integration improves threat detection accuracy and eliminates duplicate alerts by ensuring critical multi-event alerts are captured in near-real-time rather than relying on hourly or daily log files.

<details>

<summary>Collection methods</summary>

The Salesforce data collector utilizes two primary methods for data ingestion:

* Streaming (Default): Collects Salesforce near "Real-Time Events" via streaming or SOQL queries. Events are generated in near-real-time and collected every minute.
  * **Dataset**: `salesforce_realtime_raw`
* Batch (Legacy): Collects Salesforce `EventLogFiles`. Files are generated every hour or 24 hours and collected by Cortex XSIAM every 30 seconds.
  * **Dataset**: `salesforce_eventlogfiles_raw`

{% hint style="info" %}
### Note

Both methods collect the Setup Audit Trail from Salesforce.
{% endhint %}

{% hint style="warning" %}
### Important

**Existing customers keep in mind**: Changing your collection method updates the log schema, which will impact existing correlation rules. While it is strongly recommended to use NRT security logs for improved detection, you can keep both methods enabled in parallel during a transition period to ensure continuous protection while you update your rules.
{% endhint %}

**Existing customers keep in mind**: Changing your collection method updates the log schema, which will impact existing correlation rules. While it is strongly recommended to use NRT security logs for improved detection, you can keep both methods enabled in parallel during a transition period to ensure continuous protection while you update your rules.

</details>

<details>

<summary>Supported data types</summary>

Cortex XSIAM collects various data types from Salesforce. Use the table below to understand what is collected and where to find more information.

| Data Category     | Included Objects / Description                                                                                                                                           | More Information                                                                                                                                                                               |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Real-time events  | High-speed security events (such as `ApiEvent`, `ReportAnomalyEvent`).                                                                                                   | For more information, see [Real-Time Event Monitoring Objects](https://developer.salesforce.com/docs/atlas.en-us.platform_events.meta/platform_events/platform_events_objects_monitoring.htm). |
| Setup Audit Trail | Tracks recent configuration changes made by administrators.                                                                                                              | For more information, see [SetupAuditTrail](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_setupaudittrail.htm).                  |
| Event log files   | Legacy batch logs generated hourly or daily.                                                                                                                             | For more information, see [EventLogFile](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_eventlogfile.htm).                        |
| Content metadata  | `"Document"`, `"ContentFolder"`, `"Attachment"`, `"ContentDistribution"`                                                                                                 | For more information, see [Salesforce Objects](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_list.htm).                          |
| Accounts          | `Account` objects                                                                                                                                                        | For more information, see [Salesforce Objects](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_list.htm).                          |
| Snapshots         | `ConnectedApplication`, `PermissionSet`, `Profile`, `Group`, `GroupMember`, `User`, `UserRole`, `TenantSecurityLogin`, `TenantSecurityUserPerm`, `UserAccountTeamMember` | For more information, see [Salesforce Objects](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_list.htm).                          |

</details>

{% hint style="warning" %}
### Prerequisite

* Cortex XSIAM:
  * To manage collection integration in Cortex XSIAM, requires View/Edit RBAC permissions for Log Collections and Data Sources (under Configurations → Data Collection).
* Salesforce:
  * **Edition**: Professional (with API access), Enterprise, or higher.
  * **License**: A Salesforce Shield license is required to avoid limited data fetching and errors. For more information, see [Salesforce Shield](https://help.salesforce.com/s/articleView?id=xcloud.shield_learning_map.htm\&type=5).
  * To use the client credentials flow required for Salesforce–Cortex XSIAM integration, you must create a connected app for Cortex XSIAM in Salesforce, and configure its OAuth settings and access policies, as described in this procedure. The connected app must be created by a Full System Admin.
  *   Ensure your organization has a Salesforce Shield license.

      For more information, see [Salesforce Shield](https://help.salesforce.com/s/articleView?id=xcloud.salesforce_shield.htm\&type=5).

      For more information, see [Event Monitoring Introduction](https://trailhead.salesforce.com/content/learn/modules/event_monitoring/event_monitoring_intro).

      Ensure that you have the required licenses. If these prerequisites are not met, fetching of security and NRT event data will be severely limited, and errors will be generated.
  * In Setup → Event Monitoring Settings, ensure that Generate event log files is enabled.
    * In Setup, verify that there are event log files in the Event Log File Browser.
    * In Setup → Permissions Sets, verify that there is a permission set called Event Monitoring.
  * **Near-real-time event settings**: You must manually toggle each desired event, such as `ApiEvent` and `ReportAnomalyEvent`, to Enabled under Setup → Event Monitoring Settings.
  * Legacy Batch access: If collecting `EventLogFiles`, ensure Generate event log files is enabled under Setup → Event Monitoring Settings; in Setup, verify that files exist in the Event Log File Browser, and in Setup → Permissions Sets verify a permission set named Event Monitoring exists.
  *   **Administrative access**: To use the client credentials flow required for the Salesforce and Cortex XSIAM integration, a Full System Admin must create an External Client App in Salesforce and configure its OAuth settings and access policies as described in the configuration tasks below.

      For more detailed reference information, see the following:

      * [Create an External Client App](https://help.salesforce.com/s/articleView?id=xcloud.create_a_local_external_client_app.htm\&type=5)
      * [Configure an External Client App for the OAuth 2.0 Client Credentials Flow](https://help.salesforce.com/s/articleView?id=xcloud.configure_client_credentials_flow_for_external_client_apps.htm\&type=5)

      Unlike other data collector setups, in this case, the setup includes obtaining an OAuth 2.0 code from Salesforce, and this code is only valid for 15 minutes. Therefore, make sure that you enable the data collector within 15 minutes of obtaining the authorization code.
{% endhint %}

### How to configure the Salesforce data source

Perform the following procedures in the order that they appear, below.

<details>

<summary>Task 1. Configure Salesforce External Client App</summary>

Salesforce is deprecating "Connected Apps"; it is recommended to use an External Client App.

1. In Salesforce on the **Setup** page, search for **App Manager** and click **New External Client App**.
2. Provide a name (such as `panw_cortex_integration`), and your email address (used to retrieve the **Consumer Key** and **Consumer Secret**).
3. Under **API (enable OAuth settings)**, select **Enable OAuth**.
4. Enter the following **Callback URLs** on separate lines (replacing `{tenant external URL}` with your tenant name):
   * `https://login.salesforce.com/services/oauth2/callback`
   * `https://{tenant external URL}.paloaltonetworks.com/configuration/data-sources`
5. Select these **OAuth Scopes**: `Manage user data via APIs (api)` and `Perform requests at any time (refresh_token, offline_access)`.
6. Enable only these checkboxes after **OAuth Scopes: Require Secret for Web Server Flow**, **Require Secret for Refresh Token Flow**, and **Enable Client Credentials Flow**. For more information, see [Salesforce Client Credentials Flow](https://help.salesforce.com/s/articleView?id=xcloud.remoteaccess_oauth_client_credentials_flow.htm\&type=5).
7. Click **Save**, then **Continue**.

</details>

<details>

<summary>Task 2. Retrieve credentials</summary>

Consumer Key will be used for `client_id`, and Consumer Secret will be used for `client_secret` in OAuth 2.0.

1. On the **Setup** page, search for **External Client App Manager**.
2. Find your application (the one that you defined for Cortex XSIAM), click the arrow button in the last column, and select **Edit Settings**.
3. In the **OAuth Settings** area, click **Consumer Key and Secret**.
4. Go back to the Salesforce **Verify Your Identity** page, paste the code received via email in the `Verification Code` box, and click **Verify**. One of the following will happen:
   * The **Consumer Key** and **Consumer Secret** will be sent to the email address that you configured earlier for the Cortex XSIAM External Client App.
   * On the Salesforce **External Client App Name** page, the **Consumer Details** area will display the **Consumer Key** and **Consumer Secret**, and you will be able to copy them from here when required in the following procedures.

</details>

<details>

<summary>Task 3. Configure the refresh token expiration policy</summary>

1. On the **Setup** page, search for **External Client App Manager**.
2. Find your application (the one that you defined for Cortex XSIAM), click the arrow button in the last column, and select **Edit Policies**.
3. In the **OAuth Policies** area:
   * Under **Plugin Policies - Permitted Users**, select **All users can self-authorize**.
   * Set the refresh token policy to **Expire refresh token if not used for specific time** (recommended). For example, select this option and set it for 7 days.

</details>

<details>

<summary>Task 4. Configure OAuth 2.0</summary>

Configure the OAuth 2.0 application to call the Salesforce API using `client_id` (**Consumer Key**) and `client_secret` (**Consumer Secret**). For more information, see [Configure an External Client App OAuth 2.0 Client Credentials Flow](https://help.salesforce.com/s/articleView?id=xcloud.remoteaccess_oauth_client_credentials_flow.htm\&type=5).

</details>

<details>

<summary>Task 5. Configure Cortex XSIAM</summary>

1. In Cortex XSIAM, create a Salesforce data collector instance:
   1. Navigate to **Settings** → **Data Sources & Integrations**.
   2. On the **Data Sources & Integrations** page, click **Add Data Source**, search for and select Salesforce, and click **Connect**.
2. Enter a unique **Name** for the instance, the **Salesforce Domain Name**, and the **Consumer Key** (`client_id`) and the **Consumer Secret** (`client_secret`) credentials obtained earlier in this workflow. For example, the domain could be the API URL from which logs are received, such as `https://MyDomainName.my.salesforce.com/services/data/vXX.X/resource/`.
3.  (Optional) Clear unwanted data types (**Content metadata** (default), **Accounts**, and **Event Log Files**). When these options are cleared, only these data types will be omitted from collection. All other data will be collected as usual.\\

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>Selecting <strong>Event Log Files</strong> enables Batch mode instead of near-real-time.</p></div>
4.  Click **Enable**.

    A popup which redirects you to your Salesforce instance appears, to get OAuth 2.0 authorization credentials and access.
5.  Click **OK**.

    In Salesforce, a new tab appears.
6. Enter your **username** and **password**, and **Log In**.
7.  When you are asked to allow access, select **Allow**.

    A Salesforce data collection instance is created, and an authorization token is created and returned to Cortex XSIAM. Data collection begins.

</details>

<details>

<summary>Task 6. (Optional) Edit or test existing Salesforce collector settings</summary>

You can edit and test an existing collector instance after a successful initial connection between Salesforce and Cortex XSIAM. Do this by right-clicking and selecting **Edit** for the collector instance. The log collection window will be displayed, where you can make changes or test, by clicking **Test**.

{% hint style="warning" %}
### Important

If a “connected application” for Cortex XSIAM data collection already exists, you are not required to migrate to an “External Client App”, but since Connected Applications are deprecated by Salesforce, it is recommended to migrate.
{% endhint %}

</details>

### Troubleshooting

If the authorization token is not created and sent to Cortex XSIAM after the 15-minute timeout period, an authorization failure error will be returned. To retry:

1. In Cortex XSIAM, right click the collector instance and select **Edit**.
2. The log collection window will display again, allowing you to edit settings and retry getting the authorization code.
