---
description: >-
  Configure Apigee Proxy traffic ingestion into Cortex XSIAM for API security
  analysis and threat detection.
---

# Ingest Apigee Proxy

Integrate Apigee Proxy with Cortex Cloud to begin scanning the APIs for potential threats and vulnerabilities.

The integration uses Apigee’s JavaScript (JS) policy, implemented within a shared flow and deployed as a pre-proxy and post-proxy flow-hook in selected environments. The JS policy is designed to capture both request and response data from all traffic entering and exiting the proxy.

<details>

<summary>Settings in Cortex XSIAM</summary>

In Cortex XSIAM, set up the **Apigee** data source to integrate with the Apigee Gateway.

1. From **Settings** → **Data Sources & Integrations** , click **+Add New**, search for **Apigee**, then hover over it and click **Add** or **Add Instance**.
2. In the **Apigee Collector** wizard, enter a relevant name and then click **Create and Proceed**.
3.  Copy the key and paste it somewhere so that you can access it for later.

    If you forget to record the key and close the window, you must generate a new key and repeat this process.
4. Click the **Download Configuration Script** link to download the plugin, which you can then upload from the Apigee Gateway.
5. Click **Close**.

</details>

First, download the resource file and then select the method to set up the integration with Apigee.

<details>

<summary>Run an automated script to deploy configurations to Apigee</summary>

Use the script for full deployment (with or without connecting a flow hook).

{% hint style="info" %}
### Note

The steps include the prerequisites that run the automated script that deploys files and configurations to Apigee. For manual configuration, refer to the section Manual deployment.
{% endhint %}

1.  Edit `deploy.sh` and add values for the following:

    | Variable         | Description                                                                                                                                 |
    | ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
    | PROJECT\_ID      | Google project ID where Apigee is provisioned.                                                                                              |
    | ORG              | Apigee organization. By default, this is the same as PROJECT\_ID.                                                                           |
    | ENV              | In Apigee, from the left-side menu, click **Environments** and copy the name of the environment you want to use.                            |
    | TARGET\_URL      | Copy the URL for your Apigee Collector from the **Custom Collectors** page. For example, `https://api-{tenant external URL}/logs/v1/event.` |
    | APIsec\_API\_KEY | Token generated from Cortex Cloud.                                                                                                          |
2.  Check that the GCP user running the script has `IAM` permissions.

    ```programlisting
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

    ```programlisting
    chmod +x
    ./deploy.sh
    ```
4.  Verify that the JavaScript policies have been added to the shared flows:

    Go to **Apigee** → **Proxy development** → **Shared Flows** and check that the following policies have been added.

    * `sf-api-sec-extension-postflow`
    * `sf-api-sec-extension-preflow`
5.  Validate data ingestion:

    Send a request to the gateway and go to **Apigee** data source to validate that the data has been received from Apigee.
6. (Optional) Exclude unwanted domains from being tracked by APIsec:
   1. Uncomment: DOMAIN\_EXCLUSION\_LIST.
   2. Add the domains to exclude.
   3.  Edit `deploy.sh` and set the following variables:

       ```programlisting
       export DOMAIN_EXCLUSION_LIST="domain1,domain2"
       ```
7. Discontinue the integration:
   1.  Edit `undeploy.sh`:

       ```programlisting
       export PROJECT_ID=example-project-id
       export ORG=$PROJECT_ID
       export ENVIRONMENT=example-env
       ```
   2.  Run the undeploy.sh script:

       ```programlisting
       chmod +x
       ./undeploy.sh
       ```

       Go to **Apigee** → **Proxy development** → **Shared Flows** and check that the following policies have been removed.

       * `sf-api-sec-extension-postflow`
       * `sf-api-sec-extension-preflow`

</details>

<details>

<summary>Configure Apigee's JavaScript for manual deployment</summary>

You can customize the shared flow and apply it to an existing flow hook (pre-proxy, post-proxy).

Set up Apigee's JavaScript policy to send Apigee Collector's API data to Cortex XSIAM.

{% hint style="info" %}
### Note

If you have an existing hook and would like to integrate with the shared flow, run the `deploy.sh` script, and select `n`' and exit at the prompt to create a new hook. Refer to the section Connect to existing hook.
{% endhint %}

1. Edit `panw-api-sec-extension-configuration.properties` file:
   * Enter the `targetUrl` and `projectID`.
   * You can update 127KB of `maxBodyInspectionSizeKB`.
   *   For domain exclusion, uncomment the line and add the URL to exclude.

       ```programlisting
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

       ```programlisting
       gcloud config config-helper --force-auth-refresh --format
       ```

       Output:

       ```programlisting
       configuration:
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
         access_token: <Copy this value>
         id_token: 
         token_expiry: 
       sentinels:
         config_sentinel: 
       ```
   2. Copy the `<access_token>` value from the output.
3.  Upload the `property set` to Apigee:

    ```programlisting
    curl --silent -X GET 
    "https://apigee.googleapis.com/v1/organizations/
    <ORG>/environments/<ENVIRONMENT>/resourcefiles/
    properties" -H 
    "Authorization: Bearer <access_token from above>"
    ```
4.  Generate Key Value Map (KVM), which stores the Cortex API key that's encrypted

    ```programlisting
    curl --silent -X POST 
    "https://apigee.googleapis.com/v1/organizations/
    <ORG>/environments/<ENVIRONMENT>/keyvaluemaps" -H 
    "Authorization: Bearer <access_token from above>" 
    -H "Content-Type: application/json" --data-raw 
    '{"name": "'"APISec-KVM"'", "encrypted": true}'
    ```

    If there's an error when creating the KVM because of an existing name, delete the KVM and recreate.

    ```programlisting
    curl --silent -X DELETE 
    "https://apigee.googleapis.com/v1/organizations/
    <ORG>/environments/<ENVIRONMENT>/keyvaluemaps/
    $APISEC_KVM_NAME" -H "Authorization: Bearer 
    <access_token from above>"
    ```

    Add the Cortex API key entry to the created KVM.

    ```programlisting
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

    ```programlisting
    curl --silent -X POST --data-binary "<sf>.zip" -H 
    "Content-Type: application/octet-stream" -H 
    "Authorization: Bearer <access_token from above>" 
    "https://apigee.googleapis.com/v1/organizations/$ORG/
    sharedflows?action=import&name=<sf>"
    ```

    **Deploy**

    Input:

    ```programlisting
    curl --silent -X GET "https://apigee.googleapis.com/
    v1/organizations/<ORG>/sharedflows/<sf>" -H 
    "Authorization: Bearer <access_token from above>"
    ```

    Output:

    ```programlisting
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

    ```programlisting
    curl --silent -X POST -H "Authorization: 
    Bearer <access_token from above>" 
    "https://apigee.googleapis.com/
    v1/organizations/$ORG/environments/<ENVIRONMENT>/
    sharedflows/$sf/revisions/<REVISION>/
    deployments?override=true"
    ```
7.  Verify API security shared flows were created:

    Go to **Apigee** → **Proxy development** → **Shared Flows** and check that the following policies have been added.

    * `sf-api-sec-extension-postflow`
    * `sf-api-sec-extension-preflow`

</details>

<details>

<summary>Connect to an existing hook</summary>

Follow the steps if you have an existing hook and would like to integrate with a shared flow.

1. Check for existing flow hooks.
   1. Go to **Apigee** → **Management** → **Environments** and select the environment to hook the shared flow.
   2. In the **Flow Hooks** tab, select the relevant flow hook.
2.  Configure policy for shared flow to the existing hook.

    1.  Go to **Apigee** → **Proxy development** → **Shared Flows** and select the flow hook from the relevant environment.

        <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>Start with the hook in pre-proxy.</p></div>
    2. From the **Develop** tab, expand **Policies** and select **Flow Callout**.
    3. Enter a meaningful name and select the **Sharedflow**: `sf-api-sec-extension-preflow` , and then click **Create**.
    4. From the **Develop** tab, select **Shared flows** and expand **Default**.
    5. From **Select policy**, select **Select existing policy**, and select the policy just created and then click **Add**.
    6. Repeat the previous steps for the post-proxy hook. Select the **Sharedflow**: `sf-api-sec-extension-postflow`.
    7. Click **Save and Deploy**.

    The steps automatically run without linking to the hooks.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Important</h3><p>This should only be done when there are already existing hooks, and API security shared flows can't be hooked as a standalone. Run the deployment script, but skip step 9 by passing <code>n</code>. This step publishes API security shared flows to the desired Apigee environment without setting them to flow hooks.</p></div>
3. Limitations:
   *   The API security extension deployment scripts currently do not support archive-deployment Apigee environments. Refer to [Manage archive deployment](https://cloud.google.com/apigee/docs/api-platform/deploy/manage-archive-deployments) for more information.

       <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>Archive deployments are currently in preview and are subject to change.</p></div>
   * The API security extension for Apigee relies on flow-hooks, which are available only with Intermediate or Comprehensive Apigee Environment types. Refer to [Environments](https://cloud.google.com/apigee/docs/api-platform/fundamentals/environments-overview#environment-types) for more information.
   * For requests/responses with binary payloads, the binary payload is not sent to the collector for analysis; only the metadata (for example, HTTP headers, query parameters, etc.) is sent.

</details>
