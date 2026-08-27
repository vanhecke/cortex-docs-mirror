# Ingest data from Cribl

The Cribl data collector is a standard, out-of-the-box integration that ingests data collected by Cribl from multiple sources and streams it to Cortex XSIAM. This integration ensures that all downstream capabilities, including advanced analytics, are fully available within the platform.

Because the onboarding configuration in Cribl directly impacts the output sent to Cortex XSIAM, certain sources must be implemented according to specific requirements to ensure compatibility.

#### Key requirements and recommendations

* **Data integrity**: Raw data must be collected and streamed "as-is" from the original vendor. Any modifications made within Cribl may interfere with how Cortex XSIAM processes the data.
* **Format consistency**: For data sources supporting multiple collection methods, Cortex XSIAM expects the data format to match its standard collectors.
* **Palo Alto Networks products**: For optimal results, it is recommended to ingest data from Palo Alto Networks products, such as Next-Generation Firewall, using dedicated Cortex XSIAM data collectors rather than through Cribl. Ingesting NGFW data via Cribl will omit the Enhanced Application Logging (EAL) layer.

### Implementation workflow

Perform the following tasks in the order they appear:

{% hint style="info" %}
Tasks 1 through 3 are typically performed once during the initial integration setup.
{% endhint %}

#### Task 1. Create New Data Sources in Cribl

Onboard your data sources in Cribl following the standard [Cribl documentation](https://docs.cribl.io/stream/collectors/).

Ensure you have the necessary credentials and IDs for each source, such as Tenant ID, App ID, and Client Secret.

* **Collector selection**: Use specific collectors from the Cribl catalog when available. If a dedicated collector does not exist, use the generic UUID collector. In this case, verify the log collection method and ensure the data format aligns with Cortex XSIAM ingestion requirements.
* **Data segmentation**: To ensure optimal performance, configure a separate Cribl source collector for each data type to make routing/filtering easier and more efficient. For example, configure separate collectors for Microsoft 365 users, groups, and contacts.
* **Analytics support**: Any data source can be ingested using the generic UUID collector with the correct vendor and product fields. Yet, while parsing and modeling rules can be applied to any source, out-of-the-box (OOTB) analytics are only available for data sources using dedicated UUIDs. For more information, see [Data source UUIDs](ingest-data-from-cribl/data-souce-uuids).

#### Task 2. Generate Credentials in Cortex XSIAM

{% hint style="info" %}
Only one Cribl data collector instance can be configured in Cortex XSIAM. All Cribl sources will share this single connection.
{% endhint %}

1. Select **Settings** → **Data Sources & Integrations**.
2. Search for **Cribl**, select the integration, and click **Add Instance**.
3. In the **Name** field, enter a descriptive name, and click **Save & generate token**.
4. Copy the Authorization Token (by clicking the copy icon) and save it in a secure location immediately. You cannot access this token again once the dialog is closed.
5. On the **Data Sources & Integrations** page, click the link icon for your Cribl instance to **Copy API URL**, and save it for future use.

#### Task 3. Configure the Cortex XSIAM destination in Cribl

Using the credentials from Task 2, configure the Cortex XSIAM destination tile in Cribl.

| Item                | Field               | Details            |
| ------------------- | ------------------- | ------------------ |
| Cortex XSIAM URL    | XSIAM Endpoint      | Paste the API URL. |
| Authorization Token | Authorization Token | Paste the token.   |

For general destination configuration details, see [Cribl documentation.](https://docs.cribl.io/stream/destinations-xsiam/)

#### Task 4. Apply the Palo Alto XSIAM pack and pipelines in Cribl

You must apply the Palo Alto XSIAM pack and configure a dedicated pipeline for each data source.

These steps differ depending on whether you are connecting to a specific data source supported from the Cortex XSIAM Cribl catalog or another product using the generic UUID. For a complete list of the supported data sources in the catalog, see [Data source UUIDs](ingest-data-from-cribl/data-souce-uuids).

<details>

<summary>Apply the XSIAM pack using a collector supported in the Cribl catalog</summary>

1. Install the Palo Alto XSIAM pack.
   1. In Cribl, select **Stream** → **Worker Groups**, and select the default Worker Group that you want to add the pack to.
   2. Select **Processing** → **Packs**.
   3. Select **Add Pack** → **Add from Dispensary**.
   4. Search for **XSIAM**, and install the **Palo Alto XSIAM** pack.
2.  Connect the data source to the XSIAM destination to define the route.

    This step can be performed using either **QuickConnect** or **Routes**. The instructions below explain how to do this using **QuickConnect**.

    1. For the same default worker group, select the **Overview** tab.
    2. Under **QuickConnect**, click **Source**.
    3. Under **Source**, find the data source that you onboarded in Task 1, and from the `+` icon drag and drop to the **XSIAM** destination to define the route.
3. Assign the pack.
   1. Click on the line connecting the data source to the **XSIAM** destination, and click **Pack**.
   2. In the **Add Pack to Connection** window, select the **Palo Alto XSIAM** pack.
   3. Click **Save**.
4.  End-to-end connection.

    The pack includes built-in pipelines for supported sources. Each contains a specific UUID in the `__sourceIdentifier` parameter. This UUID signals to the XSIAM destination, which data source is streaming.

    To enable the connection, the specific source must be enabled in the pack, and the pipeline must route the data using a filter using the format `__inputId=='data_source'`. These filters are usually specific to the environment and is how Cribl Stream is configured.

    1. For the same default worker group, select **Processing** → **Packs**.
    2. Under **Display name**, click **Palo Alto XSIAM**.
    3. On the left pane, expand the third row.
    4. Scroll down to the data source that you connected to **XSIAM**, enable the toggle.
    5.  Click on the name of the data source under **Route** to display the routing information, including the configured route name, filter, and pipeline. The values displayed here must match the data source connected to **XSIAM**.

        <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>To view the configuration of the pipeline, select the <strong>attachment icon</strong> → <strong>Eval</strong>. Under <strong>Evaluate fields</strong>, you can see the <strong>_sourceIdentifier</strong> configured, where the <strong>Value Expression</strong> field should match the UUID for the specific collector from the Cribl catalog. This UUID is automatically configured once you've enabled the data source in the pack.</p></div>
    6. Click **Save**.

</details>

<details>

<summary>Apply XSIAM pack using generic UUID collector</summary>

If you wish to connect a data source not listed in the UUID Cribl catalog, use the generic UUID with the correct vendor and product fields. Make sure the vendor and the product match the existing content packs available in Cortex XSIAM.

1. Install the **Palo Alto XSIAM** pack.
   1. In Cribl **Stream** → **Worker Groups**, select the default Worker Group that you want to add the pack to.
   2. Select **Processing** → **Packs**.
   3. Select **Add Pack** → **Add from Dispensary**.
   4. Search for **XSIAM**, and install the **Palo Alto XSIAM** pack.
2. Create a dedicated pipeline for the new data source to the **Palo Alto XSIAM** pack, such as Fortinet Fortigate.
   1. For the same default worker group, select **Processing** → **Pipelines**.
   2. Select **Add Pipeline** → **Add Pipeline**.
   3. In the **ID** field, provide a name for this data source, such as **GenericDataSource**.
   4. Click **Save**.
3. Add three additional fields to this pipeline.
   1. Click **Add Function**, search for **Eval**, and select **Eval**.
   2. Under **Evaluate fields**, select **Add Field**, and define the following fields:
      * Fields 1:
        * **Name**: `__sourceIdentifier`
        * **Value Expression**: `'af01292940d7426594d3d3e55ae17ee0'`, which is the Generic UUID.
      * Field 2:
        * **Name**: `__vendor`
        * **Value Expression**: `<name of vendor>`, such as `'fortinet'`.
      * Field 3:
        * **Name**: `__product`
        * **Value Expression**: `<name of product>`, such as `'fortigate`

{% hint style="info" %}
**Note**

Data streams into the `vendor_product_raw` dataset in Cortex XSIAM. It should match an existing Marketplace content pack.
{% endhint %}

4. Create a dedicated route between the data source and the newly-created pipeline.
   1. Select the **Routes** tab, and click **Add Route**.
   2. Configure the following:
      * **Route name**: Enter a distinct name for the route.
      * **Filter**: Enter or select a filter using the format `__inputId=='data_source'` so the the pipeline can route the data from the data source. These filters are usually specific to the environment and is how Cribl Stream is configured.
      * **Pipeline**: Enter the name of the pipeline that you created above for the new generic data source, such as **GenericDataSource** as created above.
      * **Description** (optional): Enter a description for this route.
   3. On the blue line of the new route, click the ellipse menu, and select **Group Actions** → **Create Group**.
   4. Define the following:
      * **Group name**: Enter a generic name for these types of generic data sources , such as "Generic Data Sources with PANW assigned UUID".
      * **Description** (optional): Enter a unique description.
   5. Click **Save**.

</details>

#### Task 5. Verification

Verify that data is streaming as expected from Cribl to Cortex XSIAM.

* In Cribl:
  1. Select **Stream** → **Worker Groups**, and select the default Worker Group that you want to add the pack to.
  2. In the **Overview** tab and under **QuickConnect**, click **Source**.
  3. Hover over the data source that you connected to Cortex XSIAM, and click **Configure**.
  4. In the **Charts** tab, verify that streaming is in progress.
* In Cortex XSIAM, on the **Data Sources & Integrations** page, when streaming begins, a green check mark appears below the Cribl configuration, along with the amount of data received.

\
\
<br>
