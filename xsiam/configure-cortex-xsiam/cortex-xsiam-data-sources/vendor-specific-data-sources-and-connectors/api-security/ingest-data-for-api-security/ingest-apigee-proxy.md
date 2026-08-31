---
description: Collect Apigee Proxy data with Cortex XSIAM.
---

# Ingest Apigee Proxy

Integrate Apigee Proxy with Cortex XSIAM to begin scanning the APIs for potential threats and vulnerabilities.

The integration uses the Apigee’s JavaScript (JS) policy, implemented within a shared flow and deployed as a pre-proxy and post-proxy flow-hook in selected environments. The JS policy is designed to capture both request and response data from all traffic entering and exiting the proxy.

### Settings in Cortex XSIAM

In Cortex XSIAM, set up the Apigee data source to integrate with the Apigee Gateway.

1. From Settings → Data Sources & Integrations, click +Add New, search for Apigee, then hover over it and click Add or Add Instance.
2. In the Apigee Collector wizard, enter a relevant name and then click Create and Proceed.
3. Copy the key and paste it somewhere so that you can access it for later. If you forget to record the key and close the window, you must generate a new key and repeat this process.
4. Click the Download Configuration Script link to download the plugin, which you can then upload from the Apigee Gateway.
5. Click Close.

First, download the resource file and then select the method to set up the integration with Apigee.

### Run an automated script to deploy configurations to Apigee

Use the script for full deployment (with or without connecting a flow hook).

{% hint style="info" %}
**Note:** The following steps cover prerequisites for automated deployment. For manual configuration, refer to Manual deployment.
{% endhint %}

1.  Edit `deploy.sh` and add values for the following:

    | Variable         | Description                                                                                                                             |
    | ---------------- | --------------------------------------------------------------------------------------------------------------------------------------- |
    | PROJECT\_ID      | Google project ID where Apigee is provisioned.                                                                                          |
    | ORG              | Apigee organization. By default, this is the same as PROJECT\_ID.                                                                       |
    | ENV              | In Apigee, from the left-side menu, click Environments and copy the name of the environment you want to use.                            |
    | TARGET\_URL      | Copy the URL for your Apigee Collector from the Custom Collectors page. For example, `https://api-{tenant external URL}/logs/v1/event.` |
    | APIsec\_API\_KEY | Token generated from Cortex XSIAM.                                                                                                      |
2.  Check that the GCP user running the script has `IAM` permissions.

    ```
    apigee.resourcefiles.list
    apigee.resourcefiles.create
    apigee.resourcefiles.update
    apigee.sharedflows.get
    apigee.sharedflows.create
    apigee.deployments.create
    apigee.sharedflowrevisions.deploy
    apigee.flowhooks.attachSharedFlow
    apigee.keyvaluemaps.create
    apigee.keyvaluemaps.delete
    apigee.keyvaluemapentries.create
    ```
3.  Run the `deploy.sh` script:

    ```
    chmod +x
    ./deploy.sh
    ```
4.  Verify that the JavaScript policies have been added to the shared flows:

    Go to Apigee → Proxy development → Shared Flows and check that the following policies have been added.

    * `sf-api-sec-extension-postflow`
    * `sf-api-sec-extension-preflow`
5.  Validate data ingestion:

    Send a request to the gateway and go to the Apigee data source to validate that the data has been received from Apigee.
6. (Optional) Exclude unwanted domains from being tracked by APIsec:
   1. Uncomment: DOMAIN\_EXCLUSION\_LIST.
   2. Add the domains to exclude.
   3.  Edit `deploy.sh` and set the following variables:

       ```
       export DOMAIN_EXCLUSION_LIST="domain1,domain2"
       ```
7. Discontinue the integration:
   1.  Edit `undeploy.sh`:

       ```
       export PROJECT_ID=example-project-id
       export ORG=$PROJECT_ID
       export ENVIRONMENT=example-env
       ```
   2.  Run the undeploy.sh script:

       ```
       chmod +x
       ./undeploy.sh
       ```

       Go to Apigee → Proxy development → Shared Flows and check that the following policies have been removed.

       * `sf-api-sec-extension-postflow`
       * `sf-api-sec-extension-preflow`

### Configure Apigee's JavaScript for manual deployment

You can customize the shared flow and apply it to an existing flow hook (pre-proxy, post-proxy).

Set up Apigee's JavaScript policy to send Apigee Collector's API data to Cortex XSIAM.

{% hint style="info" %}
**Note:** If you have an existing hookand would like to integrate with the shared flow, run the `deploy.sh` script, and select `n`' and exit at the prompt to create a new hook. Refer to the section Connect to existing hook.
{% endhint %}

1. Edit `panw-api-sec-extension-configuration.properties` file:
   * Enter the `targetUrl` and `projectID`.
   * You can update 127KB of `maxBodyInspectionSizeKB`.
   *   For domain exclusion, uncomment the line and add the URL to exclude.

       ```
       targetUrl=<Cortex collector url>
       projectID=<GCP project id of apigee>
       maxBodyInspectionSizeKB=127 // This is default 
       and can be modified if needed.
       commonBinaryContentType=audio/,video/,image/,
       application/octet-stream,application/ogg,application/
       pdf,application/zip,application/gzip,application/
       vnd.rar,application/x-7z-compressed
       #domainExclusionList=example.com,example2.com/shopping
       ```
2. Upload the edited `property set`:
   1.  Get a token to upload updates via an API request. For more information, refer to [property sets](https://cloud.google.com/apigee/docs/api-platform/cache/property-sets).

       Input:

       ```
       gcloud config config-helper --force-auth-refresh --format
       ```

       Output:

       <pre><code>configuration:
         active_configuration: 
         properties:
           compute:
             region: 
             zone:     
       core:
             account: 
             disable_usage_reporting: 
             project: 
       credential:
       <strong>  access_token: &#x3C;Copy this value>
       </strong>  id_token: 
         token_expiry: 
       sentinels:
         config_sentinel: 
       </code></pre>
   2. Copy the `<access_token>` value from the output.
3.  Upload the `property set` to Apigee:

    ```
    curl --silent -X GET 
    "https://apigee.googleapis.com/v1/organizations/
    <ORG>/environments/<ENVIRONMENT>/resourcefiles/
    properties" -H 
    "Authorization: Bearer <access_token from above>"
    ```
4.  Generate Key Value Map (KVM), which stores the Cortex API key that's encrypted

    ```
    curl --silent -X POST 
    "https://apigee.googleapis.com/v1/organizations/
    <ORG>/environments/<ENVIRONMENT>/keyvaluemaps" -H 
    "Authorization: Bearer <access_token from above>" 
    -H "Content-Type: application/json" --data-raw 
    '{"name": "'"APISec-KVM"'", "encrypted": true}'
    ```

    If there's an error when creating the KVM because of an existing name, delete the KVM and recreate.

    ```
    curl --silent -X DELETE 
    "https://apigee.googleapis.com/v1/organizations/
    <ORG>/environments/<ENVIRONMENT>/keyvaluemaps/
    $APISEC_KVM_NAME" -H "Authorization: Bearer 
    <access_token from above>"
    ```

    Add the Cortex API key entry to the created KVM.

    ```
    curl --silent -X POST "https://apigee.googleapis.com/
    v1/organizations/<ORG>/environments/<ENVIRONMENT>/
    keyvaluemaps/$APISEC_KVM_NAME/entries" -H 
    "Authorization: Bearer <access_token from above>" 
    -H "Content-Type: application/json" --data-raw 
    '{"name": "api-key","value": "'"<Generated key 
    from cortex env>"'"}'
    ```
5.  Upload the shared flows:

    **Shared flows**:

    * `sf-api-sec-extension-postflow`
    * `sf-api-sec-extension-preflow`

    **Upload**

    Replace the `<sf>` with the shared flows:

    ```
    curl --silent -X POST --data-binary "<sf>.zip" -H 
    "Content-Type: application/octet-stream" -H 
    "Authorization: Bearer <access_token from above>" 
    "https://apigee.googleapis.com/v1/organizations/$ORG/
    sharedflows?action=import&name=<sf>"
    ```

    **Deploy**

    Input:

    ```
    curl --silent -X GET "https://apigee.googleapis.com/
    v1/organizations/<ORG>/sharedflows/<sf>" -H 
    "Authorization: Bearer <access_token from above>"
    ```

    Output:

    ```
    {
      "metaData": {
        "createdAt": "1736952161610",
        "lastModifiedAt": "1736952161610",
        "subType": "SharedFlow"
      },
      "name": "sf-api-sec-extension-postflow",
      "revision": [
        "1" // This is the revision number
      ],
      "latestRevisionId": "1"
    }
    ```
6.  Deploy `<sf>`:

    ```
    curl --silent -X POST -H "Authorization: 
    Bearer <access_token from above>" 
    "https://apigee.googleapis.com/
    v1/organizations/$ORG/environments/<ENVIRONMENT>/
    sharedflows/$sf/revisions/<REVISION>/
    deployments?override=true"
    ```
7.  Verify API security shared flows were created:

    Go to Apigee → Proxy development → Shared Flows and check that the following policies have been added.

    * `sf-api-sec-extension-postflow`
    * `sf-api-sec-extension-preflow`

### Connect to an existing hook

Follow the steps if you have an existing hook and would like to integrate with a shared flow.

1. Check for existing flow hooks.
   1. Go to Apigee → Management → Environments and select the environment to hook the shared flow.
   2. In the Flow Hooks tab, select the relevant flow hook.
2.  Configure the policy for the shared flow to the existing hook.

    1.  Go to Apigee → Proxy development → Shared Flows and select the flow hook from the relevant environment.

        <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note:</strong> Start with the hook in pre-proxy.</p></div>
    2. From the Develop tab, expand Policies and select Flow Callout.
    3. Enter a meaningful name and select the Sharedflow: `sf-api-sec-extension-preflow` , and then click Create.
    4. From the Develop tab, select Shared flows and expand Default.
    5. From Select policy, select Select existing policy, and select the policy just created and then click Add.
    6. Repeat the previous steps for the post-proxy hook. Select the Sharedflow: `sf-api-sec-extension-postflow`.
    7. Click Save and Deploy.

    The steps automatically run without linking to the hooks.

    <div data-gb-custom-block data-tag="hint" data-style="warning" class="hint hint-warning"><p><strong>Important:</strong> This should only be done when there are already existing hooks, and API security shared flows can't be hooked as a standalone. Run the deployment script, but skip step 9 by passing <code>n</code>. This step publishes API security shared flows to the desired Apigee environment without setting them to flow hooks.</p></div>

Limitations:

*   The API security extension deployment scripts currently do not support archive-deployment Apigee environments. Refer to [Manage archive deployment](https://cloud.google.com/apigee/docs/api-platform/deploy/manage-archive-deployments) for more information.

    Archive deployments are currently in preview and are subject to change.
* The API security extension for Apigee relies on flow-hooks, which are available only with Intermediate or Comprehensive Apigee Environment types. Refer to [Environments](https://cloud.google.com/apigee/docs/api-platform/fundamentals/environments-overview#environment-types) for more information.
* For requests/responses with binary payloads, the binary payload is not sent to the collector for analysis; only the metadata (for example, HTTP headers, query parameters, etc.) is sent.
