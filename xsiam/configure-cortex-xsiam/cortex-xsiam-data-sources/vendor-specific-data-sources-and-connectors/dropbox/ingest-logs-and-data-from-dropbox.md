---
description: Collect dropbox data in Cortex XSIAM.
---

# Ingest logs and data from Dropbox

Cortex XSIAM can ingest different types of data from Dropbox Business accounts using the Dropbox data collector. To receive logs and data from Dropbox Business accounts via the Dropbox Business API, you must configure the Collection Integrations settings in Cortex XSIAM based on your Dropbox Business Account credentials. After you set up data collection, Cortex XSIAM begins receiving new logs and data from the source.

When Cortex XSIAM begins receiving logs, the app creates a new dataset for the different types of data that you are collecting, which you can use to initiate XQL Search queries. For example queries, refer to the in-app XQL Library. For all logs, Cortex XSIAM can generate Cortex XSIAM issues (Analytics, Correlation Rules, IOC, and BIOC), when relevant, from Dropbox Business logs. While Correlation Rules issues are generated on non-normalized and normalized logs, Analytics, IOC, and BIOC issues are only generated on normalized logs.

The following table provides a brief description of the different types of data you can collect, the collection method and fetch interval for new data collected, the name of the dataset to use in Cortex XSIAM to query the data using XQL Search, and whether the data is normalized.

{% hint style="info" %}
**Note**

The fetch interval is not configurable.
{% endhint %}

| Type of data               | Description                                                                                                                                                                                                                              | Collection method | Fetch interval | Dataset name                  | Normalized data                                                                                                                       |
| -------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------- | -------------- | ----------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| **Log collection**         |                                                                                                                                                                                                                                          |                   |                |                               |                                                                                                                                       |
| Events                     | Retrieves team events, including access events, administrative events, file/folders events, security settings events, and more. [team\_log/get\_events](https://www.dropbox.com/developers/documentation/http/teams#team_log-get_events) | Appends data      | 60 seconds     | `dropbox_events_raw`          | When relevant, Cortex XSIAM normalizes SaaS audit event logs into stories, which are collected in a dataset called `saas_audit_logs`. |
| **Directory and metadata** |                                                                                                                                                                                                                                          |                   |                |                               |                                                                                                                                       |
| Member Devices             | Lists all device sessions of a team. [team/devices/list\_members\_devices](https://www.dropbox.com/developers/documentation/http/teams#team-devices-list_members_devices)                                                                | Overwrites data   | 10 minutes     | `dropbox_members_devices_raw` | —                                                                                                                                     |
| Users                      | Lists members of a group. [team/members/list\_v2](https://www.dropbox.com/developers/documentation/http/teams#team-members-list)                                                                                                         | Overwrites data   | 10 minutes     | `dropbox_users_raw`           | —                                                                                                                                     |
| Groups                     | Lists groups on a team. [team/groups/list](https://www.dropbox.com/developers/documentation/http/teams#team-groups-list)                                                                                                                 | Overwrites data   | 10 minutes     | `dropbox_groups_raw`          | —                                                                                                                                     |

{% hint style="info" %}
**Prerequisite**

1. Set up an [Advanced](https://www.dropbox.com/plans) Dropbox plan.
2. Create a Dropbox Business [admin account](https://help.dropbox.com/account-access) with **Security admin** permissions, which is required to authorize Cortex XSIAM to access the Dropbox Business account and generate the OAuth 2.0 access token.
{% endhint %}

Configure Cortex XSIAM to receive logs and data from Dropbox.

1. Complete the prerequisite steps mentioned above for your Dropbox Business account.
2. Log in to Dropbox using an admin account designated with **Security admin** level permissions.
3. In the **Dropbox App console**, ensure that you either create a new app, or your existing app is created, with the following settings:
   * **Choose an API:** Select **Scoped access**.
   * **Choose the type of access you need:** Select **Full dropbox** for access to all files and folders in a user's Dropbox.
4.  In the **Permissions** tab of your app, ensure that the applicable permissions are selected under the relevant section heading for the type of data you want to collect:

    | Section heading | Permission         | Data to collect   |
    | --------------- | ------------------ | ----------------- |
    | Account Info    | account\_info.read | All types of data |
    | Team Data       | team\_data.member  | All types of data |
    | Members         | members.read       | Users             |
    |                 | groups.read        | Groups            |
    | Sessions        | sessions.list      | Member Devices    |
    |                 | events.read        | Events            |
5. In the **Settings** tab of your app, copy the **App key** and **App secret** , where you must click **Show** to see the App secret and record them somewhere safe. You will need to provide these keys when you configure the Dropbox data collector in Cortex XSIAM.
6. Navigate to **Settings → Data Sources & Integrations**.
7. On the **Data Sources & Integrations** page, click **+ Add New**, search for **Dropbox**, then hover over and click **Add**.
8. Set the following parameters:
   * **Name:** Specify a descriptive name for this Dropbox instance.
   * **App Key:** Specify the App key, which is taken from the [Settings tab](ingest-logs-and-data-from-dropbox) of your Dropbox app.
   * **App Secret:** Specify the App secret, which is taken from the [Settings tab](ingest-logs-and-data-from-dropbox) of your Dropbox app.
   *   **Access Code:** After specifying an App Key, you can obtain the access code by hovering over the Access Code tooltip, clicking the here link, and signing in with your Dropbox Business account credentials. The URL link is `https://www.dropbox.com/oauth2/authorize?client_id=%APP_KEY%&amp;token_access_type=offline&amp;response_type=code`, where the `%APP_KEY%` is replaced with the App Key value specified.

       <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>When the App Key field is empty, the <strong>here</strong> link in the tooltip is disabled. An incorrect App Key returns a 404 error.</p></div>

       To obtain the Access Code, complete the following steps in the page that opens in your browser:

       1. Read the disclaimer and click **Continue**.
       2. Review the permissions listed, which should match the permissions you configured in your Dropbox app in the [Permissions tab](ingest-logs-and-data-from-dropbox) according to the type of data you want to collect, and click **Allow**.
       3. Copy the **Access Code Generated** and paste it in the **Access Code** field in Cortex XSIAM. The access code is valid for around four minutes from when it is generated.

       <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>Whenever you change Dropbox app permissions, generate a new Access Code. This keeps collector permissions aligned with the app.</p></div>
   * **Collect:** Select the types of data you want to collect from Dropbox. All the options are selected by default.
     * **Log collection**
       *   **Events (get\_events}:** Retrieves team events, including access events, administrative events, file/folders events, security settings events and more.

           <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>Event data is collected every 60 seconds with a 10-minute lag.</p></div>
     * **Directory and metadata**
       * **Member Devices:** Collects all device sessions of a team.
       * **Users:** Collects all members of a group.
       *   **Groups:** Collects all groups on a team.

           <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>Inventory data snapshots are collected every 10 minutes.</p></div>
9. To test the connection settings, click Test.
10. If the test is successful, click Enable to enable Dropbox log collection. After events start to come in, a green check mark appears underneath the Dropbox configuration.
