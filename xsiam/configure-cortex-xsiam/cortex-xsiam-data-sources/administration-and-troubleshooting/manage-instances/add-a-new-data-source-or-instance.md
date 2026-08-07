# Add a new data source or instance

You can add a new data source with the Data Source Onboarder. The Onboarder installs the data source, sets up an instance, configures playbooks and scripts, and other recommended content. The Onboarder offers default (customizable) options and displays all configured content in a summary screen at the end of the process.

1. Navigate to the Settings → Data Sources & Integrations page.
2. Select one of the following options:
   * Add a new data source: Click **+ Add New**.
   * Add a new data source integration instance: Select an existing data source and click **Add Instance**. Then skip to Step 4.
3.  Select a data source to onboard and click **Add**.

    Hovering over a data source displays information about the data source and its integrations. Data sources that are already integrated are highlighted green and show **Connect Another Instance**. To see details of existing integrations, click on the number of integrations.

    The data sources are drawn from the Marketplace, Custom Collectors, and integrations. If you search for a data source and **No Data Sources Found**, click **Try searching the Marketplace**, to view the marketplace page prefiltered for your search. If there are no available options in the Marketplace, you can use one of the Custom Collectors to build your own.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><ul><li>If a data source contains multiple integrations, the integration configured as the default integration will used by the Data Onboarder. The default integration of the content pack is indicated in each content pack's documentation. The other integrations are available for configuration in the <strong>Data Sources &#x26; Integrations</strong> page after installing the content pack.</li><li>Not all content packs are supported.</li><li>When adding XDR data sources, the Data Source Onboarder is not available. However, you can still enable the data source; Cortex XSIAM creates an instance and lists it on the <strong>Data Sources &#x26; Integrations</strong> page.</li></ul></div>
4.  In the settings configuration pane, complete the mandatory fields in the **Connect** section.

    For more information about the fields, click the question mark icon.
5. (Optional) Under **Collect**, select **Fetched alerts** and complete the fields.
6.  Under **Recommended Content**, review and customize the options.

    The items in this section are content-specific. Some options are view only, and others are customizable. Click on each option for more information:

    * **Classifiers & Mappers**
    * **Data Normalization**: Parsing rules and data models
    * **Correlations**: Correlation rules included in the pack
    *   **Automation**: **Playbooks** and **Scripts** included in the pack.

        You can select the **Playbooks** and **Scripts** that you want to enable. By default, recommended options are selected. Any unselected content is added as disabled content. Depending on the selected playbook, some scripts are mandatory.
    * **Dashboards & Reports**: Recommended dashboards, widgets, and reports

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Notes</h3><ul><li><p>If you are adding a new instance to an existing data source, these options are <strong>View</strong> only.</p><p>You can adjust the view-only options on the relevant page in the system, for example Correlations, Playbooks, or Scripts.</p></li><li>Cortex XSIAM automatically installs content packs with required dependencies and updates any pre-installed optional content packs. You can also <strong>Select additional content packs</strong> with optional dependencies to be configured during connection.</li></ul></div>
7.  **Test** the configuration.

    If the test fails, you can **Run Test & Download Debug Log** to debug the error.
8. **Connect** the data source.
9.  Review the configuration in the summary screen.

    If errors occurred during the test, you can click **See Details** and **Back to Edit** to revise your configuration. For advanced configuration, click on any item to open a new window to the relevant page in the system (for example, Correlations or Playbooks) filtered by the configuration.
10. Click **Finish** to return to the **Data Sources & Integrations** page.
