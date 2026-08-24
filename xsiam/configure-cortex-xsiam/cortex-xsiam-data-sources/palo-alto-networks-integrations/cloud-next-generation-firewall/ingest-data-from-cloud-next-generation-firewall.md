# Ingest data from Cloud Next-Generation Firewall

Cloud Next-Generation Firewall (CNGFW) is a fully managed, cloud-native security service from Palo Alto Networks. Enabling CNGFW data collection allows for the ingestion of CNGFW logs into the platform by establishing a dedicated connector within the existing data source configuration flow. The connection is established at the CSP account. You can connect resources regardless of whether they are managed by Strata Cloud Manager (SCM). The interface supports:

* Connecting CNGFW to the current account
* Connecting CNGFW from other accounts

Cortex products utilize the Cloud Logging Collection Service (CLCS), a pub/sub service, and the Strata Logging Service (SLS) to stream this data. Adding and removing CNGFW devices is recorded in audit logs, and users can view the consent audit during the process. Any issues related to CNGFW logs are created in the same manner as traditional NGFW issues.

{% hint style="warning" %}
### Prerequisite

* Cortex XSIAM RBAC permissions: Requires **View/Edit** permissions for **Data Sources** (under **Configurations** → **Data Collections**).
*   Cloud Service Provider (CSP) account permissions: Configuration of data ingestion from multiple accounts and regions requires Super User permissions on both the Cortex XSIAM tenant and on the device accounts.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>Cross CSP (Cloud Service Provider) is supported only within the same SFDC hierarchy. Consequently, MSSP use cases where the customer owns one end of the solution are not supported.</p></div>
{% endhint %}

<details>

<summary>Supported log types and datasets</summary>

Once ingested, your data is stored in the `panw_ngfw_*_raw` datasets. You can query this data using Cortex Query Language (XQL).

{% hint style="info" %}
**Note**

When using a multi-tenant firewall with virtual system (vsys) instances, the `_reporting_device_name` field presents the NGFW instance name, vsys\_name, and vsys\_id using the following format; `log_source_name>-<vsys_name>-<vsys_id>`.
{% endhint %}

The following log types are supported for CNGFW ingestion:

| Log Type            | Dataset Name                  |
| ------------------- | ----------------------------- |
| Authentication Logs | `panw_ngfw_auth_raw`          |
| Configuration Logs  | `panw_ngfw_config_raw`        |
| File Data Logs      | `panw_ngfw_filedata_raw`      |
| Global Protect Logs | `panw_ngfw_globalprotect_raw` |
| Hipmatch Logs       | `panw_ngfw_hipmatch_raw`\*    |
| System Logs         | `panw_ngfw_system_raw`        |
| Threat Logs         | `panw_ngfw_threat_raw`\*      |
| Traffic Logs        | `panw_ngfw_traffic_raw`\*     |
| Tunnel Logs         | `panw_ngfw_tunnel_raw`        |
| URL Logs            | `panw_ngfw_url_raw`\*         |
| User ID Logs        | `panw_ngfw_userid_raw`        |

\***Note**: These datasets use the query field names as described in the [Cortex schema](https://docs.paloaltonetworks.com/cortex/cortex-data-lake/log-forwarding-schema-reference.html) documentation. For more information about the logs, see [Strata Logging Service Log Reference](https://docs.paloaltonetworks.com/strata-logging-service/log-reference).

</details>

<details>

<summary>How to ingest detection data from CNGFW:</summary>

1. Select **Settings** → **Data Sources & Integrations**
2. On the **Data Sources & Integrations** page, click **+ Add New**, search for **CNGFW**, then hover over and click **Add**.
3.  In the **Add Cloud Next-Generation Firewall** dialog box, you can choose to connect CNGFW to this account or other accounts.

    * To connect CNGFW from the current account, select **Connect Cloud NGFW from current account** (default), and select the applicable regions.
    *   To connect CNGFW from another account, select **Connect Cloud NGFW from other accounts** and select the applicable regions for the other accounts. You can search and multi-select accounts by account number, account name, or region. For cross-account connections, you must have Super User permissions on the CSP account and the device account.

        <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Important</h3><p>This cross-account support is limited to the same SFDC hierarchy; it does not extend to MSSP scenarios where the customer and provider own separate ends of the solution.</p></div>

    Depending on the regions selected, you may need to read the **Cloud NGFW Connection from other regions** disclaimer and approve the CNGFW connection.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>If you change a device region, you must first disconnect the device from Cortex XSIAM and then reconnect it after the region change is complete.</p></div>
4. **Select log types**: You can either select the specific logs to ingest from this instance, or choose **Select all** to ingest all of them.
5.  Click **Connect** to establish the connection.

    Connection is established regardless of the firewall credential status and can take up to several minutes. Select **Sync now** to refresh your instances.

</details>
