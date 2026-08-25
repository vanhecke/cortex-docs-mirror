---
description: >-
  Configure Kong API gateway traffic ingestion into Cortex XSIAM for API
  security analysis and threat detection.
---

# Ingest Kong

Integrate Kong with Cortex Cloud to start scanning its APIs for potential threats and vulnerabilities.

You need to integrate a dedicated Kong HTTP log plugin. This plugin enables seamless traffic ingestion from your Kong API gateway to Cortex Cloud, allowing for comprehensive security measures such as OWASP Top-10, bot detection, access control, and more.

<details>

<summary>Settings in Cortex XSIAM</summary>

In Cortex Cloud, set up the **Kong** data source to integrate with the Kong API Gateway.

1. From **Settings** → **Data Sources & Integrations**, click **+ Add New**, search for **Kong**, then hover over it and click **Add** or **Add Instance**.
2. In the **Kong Collector** wizard, enter a relevant name and then click **Create and Proceed**.
3.  Copy the key and paste it somewhere so that you can access it later.

    If you forget to record the key and close the window, you must generate a new key and repeat this process.
4. Click the **Download Custom Plugin** link to download the plugin, which you can then upload from the Kong API Gateway.
5. Click **Close**.

</details>

Follow the steps to integrate Kong's API gateway with Cortex XSIAM.

<details>

<summary>Download the Cortex custom plugin</summary>

Download the custom plugin gzip file. The file includes the `handler.lua`, `utils.lua`, and `schema.lua` files that make up the custom plugin.

{% hint style="info" %}
### Note

Contact support to obtain the custom plugin file.
{% endhint %}

</details>

<details>

<summary>Provision Kong API gateway with the custom plugin</summary>

To deploy the custom plugin, refer to the Kong API documentation online:

* [Kong Gateway](https://docs.konghq.com/gateway/latest/plugin-development/distribution/)
* [Kong Konnect](https://docs.konghq.com/konnect/gateway-manager/plugins/add-custom-plugin/)
* [Kong Ingress Controller](https://docs.konghq.com/kubernetes-ingress-controller/latest/plugins/custom/)

Kong as docker container

1.  Add the plugin by mounting the plugin directory, adding it to the `Lua` package path variable, and then adding the plugin name to Kong’s plugin list variable.

    This can be done by passing the following arguments to the `docker run` command, assuming `./plugin_directory/kong` is the directory containing the `plugins/panw-apisec-http-log/ directory`.

    ```programlisting
    -v "./plugin_directory/kong:/tmp/custom_plugins/kong" \
    -e "KONG_LUA_PACKAGE_PATH=/tmp/custom_plugins/?.lua;;" \
    -e "KONG_PLUGINS=bundled,panw-apisec-http-log"
    ```

    You may want to adjust the size of the nginx body buffer which is used by Kong internally. This size sets the upper limit on the amount of HTTP body bytes that can be mirrored by the plugin. By default, this value is 8192 bytes (8 KB). To change it, another argument can be passed to the docker - for example, setting it to 128 KB:

    ```programlisting
    -e "KONG_NGINX_HTTP_CLIENT_BODY_BUFFER_SIZE=128k"
    ```

    See [https://nginx.org/en/docs/syntax.html](https://nginx.org/en/docs/syntax.html) for information on the allowed values of this variable.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Important</h3><p>The size of the buffer must be equal or larger than the <strong>max body size</strong> setting in the plugin configuration, on every data plane node.</p></div>
2.  To verify that the plugin is installed, query Kong’s Admin API using the following command:

    ```programlisting
    curl admin-api-hostname:8001 | jq .configuration.loaded_plugins.'"panw-apisec-http-log"'
    ```

    This prints **true** to the terminal if the plugin is loaded into the Kong instance.

</details>

<details>

<summary>Add and configure the custom plugin</summary>

Add and configure the plugin.

1. From the Kong Manager menu, go to **Plugins**.
2. From the **Plugins** page, scroll down to the **Custom Plugins** section.
3.  Select **panw-apisec-http-log** and click **Edit** to configure the panw-apisec-http-log plugin settings.

    | Configuration  | Description                                                                                                    | Example                     |
    | -------------- | -------------------------------------------------------------------------------------------------------------- | --------------------------- |
    | Protocols      | The request protocols the plugin will be applied to.                                                           | Either http, https, or both |
    | Cloud Context  | Cloud context, such as AWS Account ID, GCP Project ID, Azure Subscription or an appropriate value for on-prem. | 987654321000                |
    | Cloud Provider | Cloud provider where Kong API Gateway is installed.                                                            | AWS.                        |
    | Cloud Region   | Cloud region.                                                                                                  | us-east-2                   |
    | Cloud API Key  | The collector authorization key provided by the Cortex platform.                                               |                             |
    | HTTP Endpoint  | The Cortex collector's endpoint URL.                                                                           |                             |
4.  Click **View Advanced Parameters** to configure optional settings.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>The queue parameters can be updated to change when the plugin mirrors data to Cortex.</p></div>

    | Configuration              | Description                                                                                                                                                                                                                                       | Example                                                         |
    | -------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------- |
    | Instance Name              | A custom name for this plugin instance. This is useful when applying different instances to different scopes.                                                                                                                                     | Empty                                                           |
    | Tags                       | <p>An optional set of strings for grouping and filtering,</p><div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>Use commas to separate tags.</p></div>                             | Empty                                                           |
    | Keepalive                  | An optional value in milliseconds that defines how long an idle connection will live before being closed.                                                                                                                                         | 60000 (60 seconds)                                              |
    | Timeout                    | An optional timeout in milliseconds when sending data to Cortex.                                                                                                                                                                                  | 10000 (10 seconds)                                              |
    | Max body size              | The maximum body size to mirror in bytes (for example: 1024 is 1KB). Any bytes beyond this size are omitted from the request and response bodies. Must be <= 4 MB and <= the value of Kong's **nginx\_http\_client\_body\_buffer\_size** setting. | 131072 (128 KB), or the nginx body buffer size if it’s smaller. |
    | Queue Concurrency Limit    | The number of queue delivery timers. -1 indicates unlimited.                                                                                                                                                                                      | 1                                                               |
    | Queue.Initial Retry Delay  | Time in seconds before the initial retry is made for a failing batch.                                                                                                                                                                             | 0.01 (10 milliseconds)                                          |
    | Queue.Max Batch Size       | Maximum number of entries that can be processed at a time.                                                                                                                                                                                        | 1                                                               |
    | Queue.Max Bytes            | Maximum number of bytes that can be waiting in a queue, requires string content                                                                                                                                                                   | Unlimited                                                       |
    | Queue.Max Coalescing Delay | Maximum number of (fractional) seconds to elapse after the first entry was queued before the queue starts calling the handler.                                                                                                                    | 1                                                               |
    | Queue.Max Entries          | Maximum number of entries that can be waiting in the queue.                                                                                                                                                                                       | 10000                                                           |
    | Queue.Max Retry Delay      | Maximum time in seconds between retries, caps exponential backoff.                                                                                                                                                                                | 60                                                              |
    | Queue.Max Retry Time       | Time in seconds before the queue gives up calling a failed handler for a batch.                                                                                                                                                                   | 60                                                              |
5. Go to **Kong** data source to validate that data is ingested from the Kong API Gateway.

</details>

<details>

<summary>Limitations</summary>

* The plugin supports HTTP and HTTP/S protocols.
* The plugin supports Kong API Gateway version 3.4.x and above.
* The nginx body buffer size on each data plane node must be equal or larger than the **max body size** setting.
* Request and response bodies will not be mirrored if their size exceeds the nginx body buffer size. When this occurs, it is indicated in the metadata that is sent to Cortex along with the HTTP transaction data.
* The mirrored response body is the body returned from the upstream service. This means that changes made to the response body by other plugins, is not reflected in the mirrored data.

</details>
