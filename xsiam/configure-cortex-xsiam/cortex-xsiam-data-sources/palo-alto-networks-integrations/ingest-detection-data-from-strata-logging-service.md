---
description: >-
  Ingest Palo Alto Networks detection data from Strata Logging Service into
  Cortex XSIAM, migrate legacy collectors to Cortex Native Data Lake, and query
  logs with XQL.
---

# Ingest detection data from Strata Logging Service

{% hint style="warning" %}
The Strata Logging Service and Cortex Data Lake event collectors are deprecated and are no longer available for new Cortex XSIAM tenants. While these collectors remain supported for existing customers who have not yet migrated, all new integrations should use the specific data source connectors for your product.
{% endhint %}

To streamline the connection and management of all Palo Alto Networks generated logs across products in Cortex XSIAM with a Strata Logging Service, Cortex XSIAM can ingest detection data from Strata Logging Service in a more flexible manner using the Strata Logging Service data collector.

You can configure the Strata Logging Service data collector to take logs from other Palo Alto Networks products already logging to 1 or more existing Strata Logging Service.

Cortex XSIAM supports streaming data directly from Prisma Access accounts and New-Generation Firewalls (NGFW) and Panorama devices to your Cortex XSIAM tenants using the Cortex Native Data Lake. Existing integrations should be migrated to the Cortex Native Data Lake. Make sure you select all your devices to connect directly to Cortex XSIAM. Integrations not migrated manually will be migrated automatically 2 weeks before the end of the contract with Strata Logging Service.

For stitched raw data, use the XQL query `xdr_data` dataset or any preset designated for stitched data, such as `network_story`. For query examples, refer to the in-app XQL Library. Cortex XSIAM can also generate Cortex XSIAM issues (Analytics, Correlation Rules, IOC, and BIOC only) when relevant from Strata Logging Service detection data. While Correlation Rules issues are generated on non-normalized and normalized logs, Analytics, IOC, and BIOC issues are only generated on normalized logs.

{% hint style="info" %}
### Note

IOC and BIOC issues are applicable on stitched data only and are not available on raw data.
{% endhint %}

To ingest detection data from Strata Logging Service.

1.  [Activate the Strata Logging Service](https://docs.paloaltonetworks.com/cortex/cortex-data-lake/cortex-data-lake-getting-started/activate-cortex-data-lake-toc/activate-cortex-data-lake-easy).

    You can configure Cortex XSIAM to take Palo Alto generated firewall logs from other Palo Alto Networks products already logging to an existing Strata Logging Service.
2. Select **Settings** → **Data Sources**.
3. In the Strata Logging Service configuration, click the more options icon, and select **Add New Instance**.
4.  **Select Data Lake Instance**.

    Select one or more existing Strata Logging Service instances that you want to connect to this Strata Logging Service instance.
5.  **Save** your Strata Logging Service configuration.

    Once events start to come in, a green check mark appears underneath the **Strata Logging Service** configuration.
6.  (Optional) Manage your Strata Logging Service Collector.

    After you create the Strata Logging Service Collector, you can make additional changes, as needed.

    * **Delete** the Strata Logging Service Collector.
7. After Cortex XSIAM begins receiving data from a Strata Logging Service, you can use XQL Search to search for specific data, using the `xdr_data` dataset.
