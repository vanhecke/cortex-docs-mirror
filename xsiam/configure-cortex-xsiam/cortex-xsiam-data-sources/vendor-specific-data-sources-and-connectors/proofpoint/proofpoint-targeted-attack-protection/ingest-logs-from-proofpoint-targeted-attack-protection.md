# Ingest logs from Proofpoint Targeted Attack Protection

To receive logs from Proofpoint Targeted Attack Protection (TAP), you must first configure TAP service credentials in the TAP dashboard, and then the Collection Integrations settings in Cortex XSIAM based on your Proofpoint TAP configuration. After you set up data collection, Cortex XSIAM begins receiving new logs and data from the source.

When Cortex XSIAM begins receiving logs, the app creates a new dataset (`proofpoint_tap_raw`) that you can use to initiate XQL Search queries. For example queries, refer to the in-app XQL Library.

Configure the Proofpoint TAP collection in Cortex XSIAM.

1.  Generate TAP Service Credentials in Proofpoint TAP.

    TAP service credentials can be generated in the TAP Dashboard, where you will receive a Proofpoint Service Principal for authentication and Proofpoint API Secret for authentication. Record these credentials as you will need to provide them when configuring the Proofpoint Targeted Attack Protection data collector in Cortex XSIAM. For more information on generating TAP service credentials, see [Generate TAP Service Credentials](https://ptr-docs.proofpoint.com/ptr-guides/integrations-files/ptr-tap/).
2. Configure the Proofpoint TAP collection in Cortex XSIAM.
   1. Navigate to Settings → Data Sources & Integrations.
   2. On the Data Sources & Integrations page, click + Add New, search for Proofpoint Targeted Attack Protection, then hover over it and click Add.
   3. Set these parameters:
      * Name: Specify a descriptive name for your log collection configuration.
      * Proofpoint Endpoint: All Proofpoint endpoints are available on the `tap-api-v2.proofpoint.com` host. You can leave the default configuration or specify another host.
      * Service Principal: Specify the Proofpoint Service Principal for authentication. TAP service credentials can be generated in the TAP Dashboard.
      * API Secret: Specify the Proofpoint API Secret for authentication. TAP service credentials can be generated in the TAP Dashboard.
   4.  Click Test to validate access, and then click Enable.

       Once events start to come in, a green check mark appears underneath the Proofpoint Targeted Attack Protection configuration with the amount of data received.
3.  (Optional) Manage your Proofpoint Targeted Attack Protection data collector.

    After you enable the Proofpoint Targeted Attack Protection data collector, you can make additional changes as needed.

    You can perform any of the following:

    * Edit the Proofpoint Targeted Attack Protection data collector settings.
    * Disable the Proofpoint Targeted Attack Protection data collector.
    * Delete the Proofpoint Targeted Attack Protection data collector.
