# Ingest alerts and metadata from Crowdstrike APIs

{% hint style="info" %}
To enable some of the APIs, you may need to reach out to CrowdStrike support.
{% endhint %}

To receive CrowdStrike API real-time alerts and logs, you must first configure data collection from CrowdStrike APIs. You can then configure the data source settings in Cortex XSIAM for the CrowdStrike APIs.

For more information on configuring data collection from CrowdStrike APIs, see the CrowdStrike Documentation.

When Cortex XSIAM begins receiving alerts and logs, it automatically creates a CrowdStrike API XQL dataset (`crowdstrike_falcon_incident_raw`). You can use the issues created by Cortex XSIAM in rules, and search the logs using XQL Search. For example queries, refer to the in-app XQL Library.

In order to ingest alert and host data, they must be configured correctly at both the CrowdStrike and the Cortex XSIAM sides, as explained in the following steps.

1.  Configure data collection from CrowdStrike APIs.

    1. In the CrowdStrike Falcon application, select ![cs-logo.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2FJXfbTd872zIj7JDXSBN2%2Ffalcon_icon.png?alt=media\&token=81ff5673-575f-4e39-8270-168386c53729) Support → API Clients and Keys.
    2. Under the OAuth2 API Clients section, Add new API client.
    3. Configure your new API client with these settings
       * CLIENT NAME: Specify a name for the new API client.
       * DESCRIPTION: (Optional) Specify a description for the new API client.
       * API SCOPES → Event streams: Select the Read permissions check box.
       * API SCOPES → Hosts: Select the Read permissions check box.
    4. Click ADD.
    5.  Copy the values for the CLIENT ID, SECRET, and BASE URL, and save them, because you will need them when you configure the Data Collection settings in Cortex XSIAM.

        Ensure that you save the SECRET value because this is the only time that it is displayed

    f. Click DONE.
2.  Configure the CrowdStrike Platform collection in Cortex XSIAM.

    1. Navigate to Settings → Data Sources & Integrations.
    2. On the Data Sources & Integrations page, click + Add New, search for CrowdStrike Platform, then hover over it and click Add.
    3. Set these parameters:
       * Name: Specify a descriptive name for your log collection configuration, preferably the same CLIENT NAME used when adding a new client API in the CrowdStrike Falcon application, as explained above.
       * Base URL: Specify the BASE URL you received when you created the client API in the CrowdStrike Falcon application, as explained above.
       * Client ID: Specify the CLIENT ID you received when you created the client API in the CrowdStrike Falcon application, as explained above.
       * Secret: Specify the SECRET you received when you created the client API in the CrowdStrike Falcon application, as explained above.
       * Collect: Select the items that you want to collect (Alerts, Hosts).
    4. Click Test to validate access, and then click Enable.

    When events start to come in, a green check mark appears below the CrowdStrike Platform configuration, along with the amount of data received.
