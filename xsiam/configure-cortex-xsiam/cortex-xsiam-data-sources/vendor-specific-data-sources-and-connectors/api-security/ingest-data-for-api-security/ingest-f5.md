# Ingest F5

Integrate F5 with Cortex XSIAM to start scanning its APIs for potential threats and vulnerabilities.

You need to integrate a dedicated F5 log plugin. This plugin enables seamless traffic ingestion from your F5 gateway to Cortex XSIAM, allowing for comprehensive security measures such as OWASP Top-10, bot detection, access control, and more.

### Settings in Cortex XSIAM

In Cortex XSIAM, set up the F5 data source to integrate with the F5 API Gateway.

1. From Settings → Data Sources & Integrations , click + Add New, search for F5 BIG-IP LTM , then hover over it and click Add or Add Instance.
2. In the F5 BIG-IP LTM Collector wizard, enter a relevant name and then click Create and Proceed.
3. Copy the key and paste it somewhere so that you can access it for later. If you forget to record the key and close the window, you must generate a new key and repeat this process.
4. Click the Download iRules LX Plugin link to download the plugin to upload it from the F5 Gateway.
5. Click Close.

### Settings in F5 BIG-IP LTM

1. Log in to your F5 environment.
2. Verify that the following is configured: Navigate to System → Resource Provisioning and enable iRules Language Extensions (iRulesLX) . Check Provisioning and set to Nominal.
3.  Navigate to Local Traffic → iRules → LX Workspaces and follow the steps under the relevant tab:\
    **LX Workspaces**:

    *   Click Import. In the General Properties page, enter a Name and for Source, select apisec\_bigip\_plugin\_tar.gz.

        <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>Extract the F5 plugin files into a folder before uploading them to F5.</p></div>
    * In the General Properties page, enter:
      * Name: Enter the name panw\_apisec\_workspace.
      * Source: Select apisec\_bigip\_plugin\_tar.gz.
    * Select Import to import the plugin.

    **LX Plugins**:

    * Click Create.
    * In the General Properties page, enter:
      * Name: Enter panw\_apisec\_plugin.
      * From Workspace: Select panw\_apisec\_workspace.
    * Click Finished.
4. Navigate to System → File Management → Data Group File List → Import.
   * From File Name, select the panw\_apisec\_config.txt file that was extracted from the zip that was downloaded from Cortex XSIAM.
   * In the Name field, select Create New and enter panw\_apisec\_config.
   * From File Contents, select String.
   * For Data Group Name, enter panw\_apisec\_config.
   * Click Import.
5. Navigate to System → File Management → Data Group File List.
   * Click panw\_apisec\_config.
   *   In Definition, fill in the values for the following:

       ```
       "context_account_id" := "",
       "context_provider" := "",
       "context_region" := "",
       "cortex_collector_key" := "",
       "cortex_collector_url" := "",
       ```

       * Paste the F5 VIG-IP LTM Collector key you copied from Cortex XSIAM in the `"cortex_collector_key"`.
       *   From Cortex XSIAM, go to Data Sources & Integrations and from F5 BIG\_IP LTM , copy the API URL and paste it in the `"cortex_collector_url"`.

           [![F5\_data\_source.png](https://docs-cortex.paloaltonetworks.com/api/khub/maps/GD6sG6FlxDWxAn13_eZuUQ/resources/Xo1bGgS5DlY6NNvBMhlnQQ-GD6sG6FlxDWxAn13_eZuUQ/content?v=cf4695010465a6a5\&Ft-Calling-App=ft/turnkey-portal)](https://docs-cortex.paloaltonetworks.com/viewer/attachment/GD6sG6FlxDWxAn13_eZuUQ/Xo1bGgS5DlY6NNvBMhlnQQ-GD6sG6FlxDWxAn13_eZuUQ)
       *   The `context_account_id`, `context_provider`, and `context_region` depend on the cloud environment. In this instance, AWS is the example:

           * The provider for `"context_provider"` should always be uppercase.
           * Supported providers: AWS, GCP, Azure, On-prem.

           ```
           "context_account_id" := "12345",
           "context_provider" := "AWS",
           "context_region" := "us-east-2",
           "cortex_collector_key" := "collector key",
           "cortex_collector_url" := "API URL",
           ```
       * Click Update.
6. Navigate to Local Traffic → Virtual Servers → Virtual Server List. The virtual server functions as an API Gateway, handling all incoming and outgoing requests and responses, then forwarding that data to the Cortex XSIAM collector.
   * From the virtual server that serves as the gateway, click Edit.
   * In the Resources tab, under iRules, click Manage.
   *   From the Available list, navigate to /Common/panw\_apisec\_plugin and select panw\_apisec\_data\_collection and panw\_apisec\_set\_ssl\_data, and then click the left arrow button to move them to the Enabled list.

       <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>Select panw_apisec_set_ssl_data only if your client SSL profile is enabled.</p></div>
   * Click Finished.
   * Click the Properties tab.
7. Test the request/response and verify that the logs are sent to Cortex XSIAM. This can be verified by checking that the counter has increased. The scanned API endpoint metadata from f5-bigip is ready for investigation in the API inventory.
