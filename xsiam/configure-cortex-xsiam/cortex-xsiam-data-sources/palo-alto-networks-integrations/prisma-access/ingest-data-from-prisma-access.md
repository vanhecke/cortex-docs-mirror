---
description: Ingest Prisma Access data into Cortex XSIAM.
---

# Ingest data from Prisma Access

You can forward data from Prisma Access to Cortex XSIAM. When your Cortex XSIAM tenant begins receiving detection data, it begins stitching logs with other Palo Alto Networks-generated logs to form stories. Use the XQL Search to query the data.

Collection of data from multiple accounts is supported. Super User permissions on both the Cortex XSIAM tenant accounts and the Prisma Access accounts are required for this use case.

New tenants (and tenants upgraded from XDR to XSIAM) will work with the new direct integration of Next-Generation Firewall and Panorama into Cortex. For such tenants, there’s no option to use the Strata Logging Service integration.

For tenants where customers have integrated directly with Strata Logging Service, the configured integrations, such as Next-Generation Firewall and Prisma Access, can be migrated to Cortex XSIAM in either of the following ways before the license expires:

* More than two weeks before the license for existing integrations with Strata Logging Service expires, manually migrate the integrations, using the corresponding **Migrate Devices** buttons on the **Data Sources & Integrations** page. Make sure you select all your devices to connect directly to Cortex XSIAM.
*   Two weeks prior to the end of your Strata Logging Service license, Cortex XSIAM will automatically migrate your integrations to your Strata Logging Service.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>Roll-back of Strata Logging Service integration migration is not supported.</p></div>

{% hint style="warning" %}
### Prerequisite

Configuration of data ingestion from multiple accounts requires Super User permissions in both Cortex XSIAM tenant and Prisma Access accounts.
{% endhint %}

{% hint style="info" %}
### Note

If you change a device region, you must first disconnect the device from Cortex XSIAM and then reconnect it after the region change is complete.
{% endhint %}

The logs ingested by Prisma Access are the same as the logs ingested by Next-Generation Firewall. For more information, refer to [Ingest data from Next-Generation Firewall](../next-generation-firewall/ingest-data-from-next-generation-firewall).

To ingest detection data from Prisma Access:

1. Navigate to **Settings** → **Data Sources & Integrations**.
2.  On the **Data Sources & Integrations** page, click **+ Add New**, search for **Prisma Access**, then hover over it and click **Add** or **Add Instance**.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>Cortex XSIAM does not validate your Prisma Access account credentials. You must ensure the account has been deployed for data to stream.</p></div>
3. In the **Connect Prisma Access** dialog box, you can choose to connect Prisma Access to this account or other accounts.
   * To connect Prisma Access to this account, continue to the next step.
   * To connect Prisma Access to other accounts, click **Connect Prisma Access from other accounts** and select the account from the accounts listed.
4. **Select log types**: You can either select the specific logs to ingest from this instance, or choose **Select all** to ingest all of them.
5.  Click **Connect**.\
    Connection can take up to several minutes.

    On the **Data Sources & Integrations** page, expand Prisma Access to track the status of your instance.
6.  Validate that your data is streaming.

    To ensure the data is streaming into your tenant, using XQL, query Next-Generation Firewall raw datasets `panw_ngfw_<*>_raw` using the field: `is_prisma_mobile`.
7.  (Optional) Manage your Instance.

    After you create the Prisma Access instance, on the **Data Sources & Integrations** page, expand the Prisma Access integration to track the connection, or, if you want, to **Delete** the instance.
