# Connect Docker V2 compliant container registry

A Docker V2-compliant registry is a registry service that complies with the specifications and requirements outlined in the Docker Registry HTTP API V2. This API defines the protocol for interacting with a Docker registry, a repository where Docker images are stored and from which they can be pulled or pushed.

To scan public and private repositories on Docker Hub, use the [Docker Hub](connect-docker-hub-registry) registry connector.

### How to connect Docker V2

Follow the wizard to use the Docker V2 connector in Cortex XSIAM to scan and secure container images from any container registry that supports the Docker V2 protocol, ensuring comprehensive security.

* Navigate to **Settings** → **Data Sources & Integrations** and click **+ Add New**.
* On the **Add Data Sources or Integrations** page, search for **Docker Hub**, then hover over it and click **Add**.
* The **Instance Name** is automatically populated. You can change it to a more meaningful name.
* Choose the **Scan Mode**, and then follow the steps for that mode to configure the connection.

<details>

<summary>Cloud Scan</summary>

Security scanning is performed in the Cortex XSIAM environment when you select this mode.

1.  Select the appropriate **Cloud Provider** and **Region** for the Cortex environment to use for registry scanning.

    As a best practice, choose the region closest to your registry deployment to achieve the best scanning throughput and potentially reduce cloud costs.
2. (Optional) Enable **Allow access by IP’s** to specify a static IP address for the scanner to use. Ensure the static IP is allowed through your firewall so the scanner can access the registry during the scanning process.
3.  Enter the **Registry URL**. This must match the URL you use with the **docker login** command.

    Equivalent URL: `https://docker.io/`

    If you are using a CA certificate for authentication, enter the server IP address instead of the Registry URL.
4.  Under **Authentication Method**, enter the **Username** and **Password** of the registry that you want to connect.

    Use your **Docker ID** as the username (for example, john0907) and **not** your email address.
5.  (Optional) Expand **Show Advanced Settings**, and then enter the CA certificate in PEM format for Cortex to validate the Docker registry v2.

    Ensure that the Custom CA certificate that you use is not revoked by the issuing authority.
6. Select **Next**.

</details>

<details>

<summary>Scan with Outpost</summary>

Security scanning is performed on infrastructure deployed to a cloud account that you own. This mode requires additional cloud provider permissions and may incur extra costs.

{% hint style="warning" %}
#### Prerequisite

Ensure an [Outpost](../../cloud-service-provider-csp-onboarding/outpost-onboarding) is connected to your tenant.
{% endhint %}

1.  Choose a **Cloud Provider** to initialize registry scanning.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h4>Note</h4><p>If you choose <strong>Azure</strong> as the <strong>Cloud Provider</strong>, you must also select the <strong>Tenant Id.</strong> The <strong>Tenant Id</strong> is required to approve Cortex as an enterprise application in your Azure tenant.</p></div>
2.  Choose Outpost account to use for this instance. If no Outposts are shown, you can Create a new one. For more details, see [Outposts](../../../cloud-service-provider-csp-onboarding/outpost-onboarding/outpost-creation-workflow#phase-2-creating-the-outpost).

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h4>Note</h4><p>If you choose <strong>Azure</strong> as the cloud provider, only <strong>Outposts</strong> associated with the selected tenant ID are displayed.</p></div>
3. Select the **Region** where the registry is hosted.
4. (Optional) Enable **Allow access by IP’s** if you want to specify a static IP address for the scanner to use. Make sure the static IP is allowed through your firewall so that the scanner can access the registry during the scanning process.
5.  Enter the **Registry URL**. This must match the URL you use with the **docker login** command.

    Equivalent URL: `https://docker.io/`

    If you are using a CA certificate for authentication, enter the server IP address instead of the Registry URL.
6.  Under **Authentication Method**, enter the **Username** and **Password** of the registry that you want to connect.

    Use your **Docker ID** as the username (for example, john0907) and **not** your email address.
7.  (Optional) Expand **Show advanced settings**, and then enter the **CA certificate** in PEM format for Cortex to validate the Docker registry v2.

    Ensure that the Custom CA certificate that you use is not revoked by the issuing authority.
8. Select **Next**.

</details>

<details>

<summary>Scan with Broker VM</summary>

Security scanning in private networks is performed using broker VM infrastructure when you select this mode.

{% hint style="warning" %}
#### Prerequisite

Ensure one of the following is configured:

* [Set up and configure Broker VM](../../../data-management/broker-vm/set-up-and-configure-broker-vm).
* [Configure High Availability Cluster](../../../data-management/broker-vm/broker-vm-high-availability-cluster/configure-high-availability-cluster).
{% endhint %}

1. Choose a **Scan with Broker VM** mode to initiate registry scanning. You can select either a standalone **Broker VM** or a High Availability (HA) **Cluster**.
2.  Select **Applicable Broker VMs**.

    Choose the appropriate **Broker VM** or **Cluster** from the list configured in your tenant.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h4>Note</h4><ul><li>The list of <strong>Broker VMs</strong> displays only VMs that support registry scanning.</li><li>The list of high-availability <strong>Clusters</strong> displays only clusters that contain at least one VM supporting registry scanning.</li><li>The registry scanning status for each VM appears in brackets if it was previously activated for that specific VM.</li></ul></div>

    If the list does not display any **Broker VMs** or **clusters**, **Add New Broker VM** or A**dd New Cluster**. For more details, see [Set up and configure Broker VM](../../../data-management/broker-vm/set-up-and-configure-broker-vm).
3.  Enter the **Registry URL**. This must match the URL you use with the **docker login** command.

    Equivalent URL: `https://docker.io/`

    If you are using a CA certificate for authentication, enter the server IP address instead of the Registry URL.
4.  Under **Authentication Method**, enter the **Username** and **Password** of the registry that you want to connect.

    Use your **Docker ID** as the username (for example, john0907) and **not** your email address.
5.  (Optional) Expand **Show advanced settings**, and then enter the **CA certificate** in PEM format for Cortex to validate the Docker registry v2.

    Ensure that the Custom CA certificate that you use is not revoked by the issuing authority.
6. Select **Next**.

</details>

5. In the **Initial Scan Configuration**, set your scanning process to focus on recently added or modified container images and exclude older ones that do not align with your current scanning objectives. This setting helps avoid unnecessary scans. Choose one of the following options:
   * **All:** Scans all container images, including all versions (tags), in all discovered repositories.
   * **Latest Tag**: Scans only images tagged **'latest'** in all discovered repositories.
   * **Days Modified**: Scans container images that have been created in the last few days. You can select a range of up to **90** days for the scan.
6.  Select **Save**.

    When the Docker V2 data source is saved successfully, a new data connector is created, and the initial discovery scan begins. The connection process can take up to 15 minutes.
7. To check the connector status and scan results, follow these steps:
   1. Navigate to **Settings → Data Sources & Integrations**.
   2. Find the **Docker V2** integration from the list of data sources, or filter for it.
   3.  Select the **Docker V2 instance** row. A pane opens with a list of integration instances and their details showing the following information:

       | Instance Details               | Description                                                                                                                                                                                                                                                       |
       | ------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
       | **Status**                     | Shows the status of the connector: Connected, **Error**, **Warning**, **Disabled**, or **Pending**.                                                                                                                                                               |
       | **Applet Status on Broker VM** | Shows the status of the **Registry Scanner** applet on the **Broker VM** page. This status is visible only when the **Scan with Broker VM** mode is selected.                                                                                                     |
       | **Repositories**               | Shows the number of scanned repositories in the registry.                                                                                                                                                                                                         |
       | **Scan Mode**                  | Shows the selected scan mode for the data connector, such as **Cloud Scan**, **Scan with Outpost**, or **Scan with Broker VM**.                                                                                                                                   |
       | **Security Capabilities**      | Shows a breakdown of the security capabilities enabled on the instance and their individual statuses. For example, select **Registry Scanning** when it shows a **warning** or **error** status to see the open errors and issues that contributed to the status. |
8. Next Steps
   * After the scan is complete, you can view the scanned images on the **Container Images Inventory** page. For more details, see [Container Images assets](../../../../detect-investigate-and-respond-to-threats/asset-management/asset-classes/compute-assets/container-image-assets).
   * If you have selected the **Scan with Broker VM** option, then a **Registry Scanner applet** is created on the selected **Broker VM** or **Cluster**. For details, see [Verify Registry Scanner connection](../../../generic-on-premise-data-collectors/broker-vm-data-collector-applets/activate-registry-scanner#verify-registry-scanner-connection).

<figure><img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2FYuZqoJgEKHf1L7Estps0%2Fregistry-broker-vm.png?alt=media&#x26;token=7239ef79-a1a8-40cb-afe9-51fed4d841b0" alt=""><figcaption></figcaption></figure>
