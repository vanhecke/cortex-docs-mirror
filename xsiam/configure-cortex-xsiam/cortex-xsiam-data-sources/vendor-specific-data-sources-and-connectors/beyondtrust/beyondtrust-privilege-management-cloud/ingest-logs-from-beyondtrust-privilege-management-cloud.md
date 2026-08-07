# Ingest logs from BeyondTrust Privilege Management Cloud

If you use BeyondTrust Privilege Management Cloud, you can take advantage of Cortex XSIAM investigation and detection capabilities by forwarding your logs to Cortex XSIAM. This enables Cortex XSIAM to help you expand visibility into computer, activity, and authorization requests in the organization, correlate and detect access violations, and query BeyondTrust Endpoint Privilege Management logs using XQL Search.

When Cortex XSIAM starts to receive logs, Cortex XSIAM can analyze your logs in XQL Search and you can create new Correlation Rules.

To integrate your logs, you first need to configure SIEM settings and an AWS S3 Bucket according to the specific requirements provided by BeyondTrust. You can then configure data collection in Cortex XSIAM by configuring an Amazon S3 data collector for a generic log type using the Beyondtrust Cloud ECS log format.

Before you begin configuring data collection verify that you are using BeyondTrust Privilege Management Cloud version 21.6.339 or later.

Configure BeyondTrust Privilege Management Cloud collection in Cortex XSIAM.

1.  Configure SIEM settings and an AWS S3 Bucket according to the requirements provided in the [BeyondTrust documentation](https://docs.beyondtrust.com/epm-wm/docs/configure-siem-settings).

    Ensure that when you add the AWS S3 bucket in the PMC and set the SIEM settings, you select **ECS - Elastic Common Schema** as the **SIEM Format**.
2.  Configure BeyondTrust logs collection with Cortex XSIAM using an [Amazon S3 data collector for generic data](file:///document/preview/1039055#UUID-d5ace3ce-5a93-86f4-55f2-4943fbf09cbe)Ingest generic logs from Amazon S3.

    Ensure your Amazon S3 data collector is configured with the following settings.

    * **Log Type:** Select **Generic** to configure your log collection to receive generic logs from Amazon S3.
    *   **Log Format:** Select the log format type as **Beyondtrust Cloud ECS**.

        <div data-gb-custom-block data-tag="hint" data-style="success" class="hint hint-success"><p><strong>Note</strong></p><p>For a <strong>Log Format</strong> set to <strong>Beyondtrust Cloud ECS</strong>, the following fields are automatically set and not configurable.</p><ul><li><strong>Vendor: Beyondtrust</strong></li><li><strong>Product: Privilege Management</strong></li><li><strong>Compression: Uncompressed</strong></li></ul></div>
3. After Cortex XSIAM begins receiving data from BeyondTrust Privilege Management Cloud, you can use XQL Search to search your logs using the `beyondtrust_privilege_management_raw` dataset that you configured when setting up your Amazon S3 data collector.
