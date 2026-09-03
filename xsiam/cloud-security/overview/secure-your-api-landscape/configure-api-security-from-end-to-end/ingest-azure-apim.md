---
description: >-
  Ingest Azure API Management traffic into Cortex XSIAM for API security
  analysis, risk assessment, and threat detection.
---

# Ingest Azure APIM

Integrate Azure APIM with Cortex XSIAM to start scanning its APIs for potential threats and vulnerabilities.

You need to set up a policy that enables you to customize the behavior of managed APIs. You can configure the sending of HTTP request/response data to Cortex XSIAM. The data is saved and analyzed by API security modules, which provide information on the security risks associated with the APIs.

{% hint style="info" %}
Microsoft Azure APIM service must be running before starting to configure the integration.
{% endhint %}

<details>

<summary>Settings in Cortex XSIAM</summary>

In Cortex XSIAM, set up the **Azure API Management** data source to integrate with the Azure API Gateway.

1. From **Settings** → **Data Sources & Integrations** , click **+ Add New**, search for **Azure API Management**, then hover over it and click **Add** or **Add Instance**.
2. In the **APIM Collector** wizard, enter a relevant name and then click **Create and Proceed**.
3.  Copy the key and paste it somewhere so that you can access it for later.

    If you forget to record the key and close the window, you must generate a new key and repeat this process.
4. Click **Close**.

</details>

<details>

<summary>Settings in Azure APIM policy</summary>

Configure an inbound and outbound policy to send HTTP traffic data of the APIs to Cortex XSIAM. You can configure a policy for individual operations (endpoints) or all operations of a single API.

Follow the steps to configure the policy.

1. Log in to [Microsoft Azure](https://portal.azure.com/).
2. Go to **API Management services** and select the relevant service.
3.  From the left-hand menu, select APIs → Named values.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>From the URL, save the UUID and the resource group - <code>/resource/subscriptions/&#x3C;UUID>/resourceGroups/&#x3C;ResourceGroup></code>.</p><p>The UUID is the Azure account/subscription ID and the resource group, which is the group where the APIM Service is defined.</p></div>
4.  Configure the settings in each of the sections. Follow the steps in the order they are listed.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>Use the search to navigate to the specific section.</p></div>

    **Named values**: Add the values:

    * cloud-account-id
      * **Type**: Plain
      * **Value**: The UUID you saved from the previous step.
    * cloud-resource-group
      * **Type**: Plain
      * **Value**: The resource group you saved from the previous step.
    * cortex-api-key
      * **Type**: Secret
      * **Value**: The token that you saved from data sources in Cortex.
    * cortex-api-url
      * **Type**: Plain
      * **Value**: The API URL from data sources in Cortex.
    * cortex-http-body-size-limit-bytes
      * **Type**: Plain
      *   **Value**: 131072

          <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>131072 bytes = 128 KB. This value determines the size (in bytes) of request and response bodies to send to Cortex. Any bytes beyond this limit are truncated.</p></div>

    **APIs**: From the left-hand menu, go to APIs → APIs.

    1. You can create a policy on a specific API or choose to create a policy on all APIs.
    2.  From **Inbound Processing**, click ![code\_bracket.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-c5673e4ef7e94b589b516d382d6073cc7c001274%2Fd54a3a065972e9c602cd8f935fd5653bf6f0af9961209a7acadbb3a55b8d0fa9.png?alt=media).

        The Policies screen opens. There are three sections:

        * `<inbound>`
        * `<backend>`
        * `<outbound>`

        The `<inbound>` includes the request before it's sent to the `<outbound>`. The parameters are saved before they're sent.

        Add the following inside the `<inbound>`:

        ```programlisting
         <!-- Save the request body and headers to be sent to Cortex. This should always be placed at the very beginning of the inbound element. -->
                <set-variable name="requestBody" value="@((context.Request?.Body?.As<string>(preserveContent: true)) ?? string.Empty)" />
                <set-variable name="requestHeaders" value="@(JsonConvert.SerializeObject(context.Request.Headers))" />
                <!-- End of setting variables for sending to Cortex -->
        ```

        <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>If any other inbound policies should be added, they must be added after these elements.</p></div>

        The `<outbound>` includes the request before it returns a response.

        Add the following inside the \<outbound> element, at the end, after the other child elements:

        ```programlisting
         <!-- Send data to Cortex. This should always be placed at the very end of the outbound element. -->
                <send-request mode="new" response-variable-name="mirrorMessage">
                    <set-url>{{cortex-api-url}}</set-url>
                    <set-method>POST</set-method>
                    <set-header name="Content-Type" exists-action="override">
                        <value>application/json</value>
                    </set-header>
                    <set-header name="Authorization" exists-action="override">
                        <value>{{cortex-api-key}}</value>
                    </set-header>
                   <set-body>@{
                                string requestBody = context.Variables.GetValueOrDefault<string>("requestBody");
                                string responseBody = context.Response.Body.As<string>(preserveContent: true);
                                int bodySizeLimit = {{cortex-http-body-size-limit-bytes}};
                                bool requestBodySizeExceedsLimit = requestBody.Length > bodySizeLimit;
                                bool responseBodySizeExceedsLimit = responseBody.Length > bodySizeLimit;

                                return JsonConvert.SerializeObject(new {
                                    accountId               = "{{cloud-account-id}}",
                                    serviceId               = context.Deployment.ServiceId,
                                    requestId               = context.RequestId,
                                    url                     = context.Request.OriginalUrl,
                                    httpMethod              = context.Request.Method,
                                    requestBody             = requestBodySizeExceedsLimit ? requestBody.Substring(0, bodySizeLimit) : requestBody,
                                    requestBodyTruncated    = requestBodySizeExceedsLimit,
                                    requestHeaders          = JsonConvert.DeserializeObject(context.Variables.GetValueOrDefault<string>("requestHeaders")),
                                    timestamp               = new DateTimeOffset(context.Timestamp).ToUnixTimeMilliseconds(),
                                    requestIpAddress        = context.Request.IpAddress,
                                    statusCode              = context.Response.StatusCode,
                                    responseBody            = responseBodySizeExceedsLimit ? responseBody.Substring(0, bodySizeLimit) : responseBody,
                                    responseBodyTruncated   = responseBodySizeExceedsLimit,
                                    responseHeaders         = context.Response.Headers,
                                    region                  = context.Deployment.Region,
                                    subscription            = context.Subscription,
                                });
                            }
                    </set-body>
                </send-request>
                <!-- End of sending data to Cortex -->
        ```

        <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Important</h3><p>If you want to add additional data to the &#x3C;outbound>, add it at the start of the &#x3C;outbound> code.</p></div>
    3.  Click **Save**. Your APIM traffic collection is now configured.

        Request and response data for the configured endpoints are sent to Cortex XSIAM for inspection by API security modules.
5. Go to **Azure API Management** data source to validate that data is ingested from Azure APIM.
6. Do the following to remove the integration of Azure APIM with Cortex XSIAM:
   * Remove the snippets you added to the policies.
   * Remove the named values from the API service.
   * Delete the HTTP log collector from **Data Sources & Integrations** in Cortex.

</details>
