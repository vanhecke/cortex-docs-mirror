---
description: Collect Box data from Cortex XSIAM.
---

# Ingest logs and data from Box

Cortex XSIAM can ingest different types of data from Box enterprise accounts using the Box data collector. To receive logs and data from Box enterprise accounts via the Box REST APIs, you must configure the Collection Integrations settings in Cortex XSIAM based on your Box enterprise account credentials. After you set up data collection, Cortex XSIAM begins receiving new logs and data from the source.

When Cortex XSIAM begins receiving logs, the app creates a new dataset for the different types of data that you are collecting, which you can use to initiate XQL Search queries. For example queries, refer to the in-app XQL Library. For all logs, Cortex XSIAM can generate Cortex XSIAM issues (Analytics, Correlation Rules, IOC, and BIOC), when relevant, from Box logs. While Correlation Rules issues are generated on non-normalized and normalized logs, Analytics, IOC, and BIOC issues are only generated on normalized logs.

The following table provides a brief description of the different types of data you can collect, the collection method and fetch interval for new data collected, the name of the dataset to use in Cortex XSIAM to query the data using XQL Search, and whether the data is normalized.

{% hint style="info" %}
**Note:** Fetch intervals are non-configurable.
{% endhint %}

| Type of data                   | Description                                                                                                                                                                                                                                                                                    | Collection method | Fetch interval | Dataset name            | Normalized data                                                                                                                       |
| ------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------- | -------------- | ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| **Events and security alerts** |                                                                                                                                                                                                                                                                                                |                   |                |                         |                                                                                                                                       |
| Events (admin\_logs)           | Retrieves events related to file/folder management, permission changes, access and login activities, user/groups management, folder collaboration, file/folder sharing, security settings changes, tasks, permission changes on folders, storage expiration and data retention, and workflows. | Appends data      | 60 seconds     | `box_admin_logs_raw`    | When relevant, Cortex XSIAM normalizes SaaS audit event logs into stories, which are collected in a dataset called `saas_audit_logs`. |
| Box Shield Alerts              | Retrieves security alerts related to suspicious locations, suspicious sessions, anomalous download, and malicious content. **Note:** Collecting Box Shield Alerts requires implementing [Box Shield](https://www.box.com/shield).                                                              | Appends data      | 60 seconds     | `box_shield_alerts_raw` | —                                                                                                                                     |
| **Directory and metadata**     |                                                                                                                                                                                                                                                                                                |                   |                |                         |                                                                                                                                       |
| Users                          | Lists user data.                                                                                                                                                                                                                                                                               | Overwrites data   | 10 minutes     | `box_users_raw`         | —                                                                                                                                     |
| Groups                         | Lists user group data.                                                                                                                                                                                                                                                                         | Overwrites data   | 10 minutes     | `box_groups_raw`        | —                                                                                                                                     |

{% hint style="info" %}
**Prerequisite**

1.  Set up an [Enterprise](https://www.box.com/pricing) Box plan.

    <div data-gb-custom-block data-tag="hint" data-style="warning" class="hint hint-warning"><p><strong>Important</strong></p><p>To collect Box Shield Alerts, you must purchase <a href="https://www.box.com/shield">Box Shield</a> and it must be enabled on Box enterprise.</p></div>
2. Create a valid Box account that is assigned to a role with sufficient permissions for the data you want to collect. For example, create an account assigned to an Admin role to enable Cortex XDR to collect all metadata for all files, folders, and enterprise events for the entire organization.
3. Enable two-factor authentication for the Box account. For more information, see the [Box documentation](https://support.box.com/hc/en-us/articles/360043697154-Two-Factor-Authentication-Set-Up-for-Your-Account).
{% endhint %}

Configure Cortex XSIAM to receive logs and data from Box.

1. Complete the prerequisites mentioned above for your Box enterprise account.
2. Create a new app in your Box account.
   1. Log in to your Box account, and in the [Dev Console](https://account.box.com/login?redirect_url=%2Fdevelopers%2Fconsole), click **Create New App**.
   2. Select **Custom App.**
   3. **Set these settings in the Custom App dialog:**
      * **Select Server Authentication (Client Credentials Grant).**
      * **Specify an App Name.**
      * **Click Create App.** The new app is created and the opened in the Configuration tab.
   4.  **In the Configuration tab** of the new app, scroll down to the following sections and configure the app.

       * In the **App Access Level** section, select **App + Enterprise Access**.
       *   In the **Application Scopes** section, set the following **Administrative Action** permissions depending on the type of data you want to collect.

           | Administrative action        | Data type                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
           | ---------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
           | Manage users                 | Users                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
           | Manage groups                | <p>Groups</p><div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>There is a current bug with the Groups API from Box. If you don't configure the Box app with the proper permissions for managing groups data, the Groups API from Box won't return an error message to Cortex XSIAM indicating that the API failed to receive the data, and the Groups data will not be collected.</p></div> |
           | Manage enterprise properties | <ul><li>Events (admin_logs)</li><li>Box Shield Alerts</li></ul>                                                                                                                                                                                                                                                                                                                                                                                             |

       Once completed, scroll up in the tab to **Save Changes**.
   5.  In the Authorization tab, click **Review and Submit** to send your changes to the administrator for approval.

       In the **Review App Authorization Submission** dialog that is displayed, you can add a **Description** of the app changes, and then click **Submit**.
3. Ensure the new app changes are approved by an administrator in the Admin Console of the Box account.
   1. Select **Apps → Customer Apps Manager → Server Authentication Apps**.
   2. In the table, look for the **Name** of the Box app with the changes, where the **Authorization Status** is set to **Pending Authorization**, and select the options menu → **Authorize App**.
   3.  **Click Authorize.**

       <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>For any future change that you make to your Box app, ensure that you send the changes for approval to the administrator, who will need to approve them as explained above.</p></div>
4. Navigate to **Settings → Data Sources & Integrations**.
5. On the Data Sources & Integrations page, click **+ Add New**, search for **Box**, then hover over it and click **Add**.
6. **Set the following parameters**, where some values require you to log in to your Box account to copy and paste the values to the applicable fields:
   * **Name:** Specify a descriptive name for this Box instance.
   * **Enterprise ID:** Specify the unique identifier for your organization's Box instance, which is used to access the token request. This field can't be edited once the Box data collector instance is created. You can retrieve this value from your Box account in the the **General Settings** tab, and scrolling to the **App Info** section. Copy the **Enterprise ID** and paste it in this field in Cortex XSIAM.
   * **Client ID:** Specify the client ID or API key for the Box app you created. You can retrieve this value from your Box account in the **Configuration** tab, and scrolling down to the **OAuth 2.0 Credentials** section. COPY the **Client ID** and paste it into this field in Cortex XSIAM.
   * **Client Secret:** The client secret or API secret fort he Box app you created. You can retrieve this value from your Box account in the **Configuration** tab, and scrolling down to the **OAuth 2.0 Credentials** section. Click **Fetch Client Secret**, where you will need to authenticate yourself according to the two-factor authentication method (as explained as one of the prerequisites above) defined in your Box app before the Client Secret is displayed. Copy this value and paste it in this field in Cortex XSIAM.
   * **Collect:** Select the types of data you want to collect from Box. All the options are selected by default.
     * **Events and security alerts**
       * **Events (admin\_logs):** Collects events related to file/folder management, permission changes, access and login activities, user/groups management, folder collaboration, file/folder sharing, security settings changes, tasks, permission changes on folders, storage expiration and data retention, and workflows.
       * **Box Shield Alerts:** Collects security alerts related to suspicious locations, suspicious sessions, anomalous download, and malicious content.
     *   **Directory and metadata**

         <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>Inventory data snapshots are collected every 10 minutes.</p></div>

         * **Users:** Collects user data.
         * **Groups:** Collects user group data.
7. To test the connection settings, click Test.
8. If the test is successful, click Enable to enable Box log collection. When events start to come in, a green check mark appears underneath the Box configuration.
