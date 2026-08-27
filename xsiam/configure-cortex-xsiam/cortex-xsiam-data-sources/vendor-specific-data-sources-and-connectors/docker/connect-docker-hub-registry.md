---
description: Connect a Docker Hub registry to Cortex XSIAM for container image scanning.
---

# Connect Docker Hub registry

The Docker Hub registry data source allows you to connect your public or private Docker Hub account to scan and secure container images against vulnerabilities, malware, and exposed secrets.

{% hint style="info" %}
**License type**: This feature is included with a Cortex XSIAM Premium license. It is also included with any other Cortex XSIAM product that has the Cloud Posture Security or the Cloud Runtime Security add-on.
{% endhint %}

### How to connect Docker Hub registry

Follow the wizard to connect your Docker Hub registry with Cortex XSIAM.

1. Navigate to **Settings** → **Data Sources & Integrations** and click **+ Add New**.
2. On the **Add Data Sources or Integrations** page, search for **Docker Hub**, then hover over it and click **Add**.
3. The **Instance Name** is automatically populated. You can change it to a more meaningful name.
4. Choose the **Scan Mode**, and then follow the steps for that mode to configure the connection.

<details>

<summary>Cloud Scan</summary>

Security scanning is performed in the Cortex XSIAM environment when you select this mode.

1.  Select the appropriate **Cloud Provider** and **Region** for the Cortex Cloud environment to use for registry scanning.

    As a best practice, choose the region closest to your registry deployment to achieve the best scanning throughput and potentially reduce cloud costs.
2. (Optional) Enable **Allow access by IPs** to specify a static IP address for the scanner to use. Make sure the static IP is allowed through your firewall so the scanner can access the registry during the scanning process.
3. Choose the relevant **Repository Access** for scanning:
   1. **Authenticated access**: Discover and scan private and public repositories within the given account.
      1. Under **Authentication Method**, enter your private Docker Hub account credentials (**Username** and **Password**) for authentication.
   2. **Public access only**: Discover and scan images within a specific public repository.
      1.  Enter your public Docker Hub **Repository Name**.

          To specify an official Docker Hub repository, enter `library/`, followed by the short string used to designate the repo. For example, to scan the images in the official Alpine Linux repository, enter `library/alpine`.
      2. Under **Authentication Method**, enter your public Docker Hub account user credentials (**Username** and **Password**) for authentication.
4. Select **Next**.

</details>

<details>

<summary>Scan with Outpost</summary>

Security scanning is performed on infrastructure deployed to a cloud account that you own. This mode requires additional cloud provider permissions and may incur extra costs.

{% hint style="warning" %}
#### Prerequisite

Ensure an [Outpost](../../cloud-service-provider-csp-onboarding/outpost-onboarding) is connected to your tenant.
{% endhint %}

1.  Choose a **Cloud Provider** to initialize registry scanning.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h4>Note</h4><p>If you choose <strong>Azure</strong> as the <strong>Cloud Provider</strong>, you must also select the <strong>Tenant Id</strong>. The <strong>Tenant Id</strong> is required to approve Cortex as an enterprise application in your Azure tenant.</p></div>
2.  **Choose Outpost** account to use for this instance. If no **Outposts** are shown, you can **Create a new one**. For more details, see [Outposts](../../../cloud-service-provider-csp-onboarding/outpost-onboarding/outpost-creation-workflow#phase-2-creating-the-outpost).

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h4>Note</h4><p>If you choose <strong>Azure</strong> as the cloud provider, only <strong>Outposts</strong> associated with the selected tenant ID are displayed.</p></div>
3. Select the **Region** where the registry is hosted.
4. (Optional) Enable **Allow access by IPs** if you want to specify a static IP address for the scanner to use. Make sure the static IP is allowed through your firewall so that the scanner can access the registry during the scanning process.
5. Choose the relevant **Repository Access** for scanning:
   1. **Authenticated access**: Discover and scan private and public repositories within the given account.
      1. Under **Authentication Method**, enter your private Docker Hub account credentials (**Username** and **Password**) for authentication.
   2. **Public access only**: Discover and scan images within a specific public repository.
      1.  Enter your public Docker Hub **Repository Name**.

          To specify an official Docker Hub repository, enter `library/`, followed by the short string used to designate the repo. For example, to scan the images in the official Alpine Linux repository, enter `library/alpine`.
      2. Under **Authentication Method**, enter your public Docker Hub account user credentials (**Username** and **Password**) for authentication.
6. Select **Next**.

</details>

<details>

<summary>Scan with Broker VM</summary>

Security scanning in private networks is done using broker VM infrastructure when you select this mode.

{% hint style="warning" %}
#### Prerequisite

* [Set up and configure Broker VM](../../../data-management/broker-vm/set-up-and-configure-broker-vm)
* [Configure High Availability Cluster](../../../data-management/broker-vm/broker-vm-high-availability-cluster/configure-high-availability-cluster)
{% endhint %}

1. Choose a **Scan with Broker VM mode** to initiate registry scanning. You can select either a standalone **Broker VM** or a High Availability (HA) **Cluster**.
2.  Select **Applicable Broker VMs**.

    Choose the appropriate **Broker VM** or **Cluster** from the list configured in your tenant.

    * The list of Broker VMs displays only VMs that support registry scanning.
    * The list of high-availability Clusters displays only clusters that contain at least one VM supporting registry scanning.
    * The registry scanning status for each VM appears in brackets if it was previously activated for that specific VM.

    If the list does not display any Broker VMs or Clusters, Add New Broker VM or Add New Cluster. For more details, see [Set up and configure Broker VM](../../../data-management/broker-vm/set-up-and-configure-broker-vm).
3. Choose the relevant **Repository Access** for scanning:
   1. **Authenticated access**: Discover and scan private and public repositories within the given account.
      1. Under **Authentication Method**, enter your private Docker Hub account credentials (**Username** and **Password**) for authentication.
   2. **Public access only**: Discover and scan images within a specific public repository.
      1.  Enter your public Docker Hub **Repository Name**.

          To specify an official Docker Hub repository, enter `library/`, followed by the short string used to designate the repo. For example, to scan the images in the official Alpine Linux repository, enter `library/alpine`.
      2. Under **Authentication Method**, enter your public Docker Hub account user credentials (**Username** and **Password**) for authentication.
4. Select **Next**.

</details>

5. In **Initial Scan Configuration**, set your scanning process to focus on recently added or modified container images and exclude older ones that do not align with your current scanning objectives. This setting helps avoid unnecessary scans. Choose one of the following options:
   * **All**: Scans all container images, including all versions (tags), in all discovered repositories.
   * **Latest Tag**: Scans only images tagged '**latest**' in all discovered repositories.
   * **Days Modified**: Scans container images created or modified in the last few days. You can select a range of up to **90** days for the scan.
6.  Select **Save**.

    When the **Docker Hub** data source is saved, a new data connector is created, and the initial discovery scan begins. The connection process may take up to 15 minutes.
7. To check the connector status and scan results, follow these steps:
   1. Navigate to **Settings** → **Data Sources & Integrations**.
   2. Find the **Docker Hub** instance from the list of **3rd Party Data Sources** connectors, or use **Search**.
   3. In the **Docker Hub** instance row, select **View Details**. The **Docker Hub Instances** page appears.
   4. On the **Docker Hub Instances** page, you can filter results by any heading and value.
   5.  Select an **Instance Name** to open the details pane. The details pane contains the following granular information:

       <table><thead><tr><th width="166.32421875">Instance Details</th><th>Description</th></tr></thead><tbody><tr><td><strong>Status</strong></td><td>Shows the status of the connector: <strong>Connected</strong>, <strong>Error</strong>, <strong>Warning</strong>, <strong>Disabled</strong>, or <strong>Pending</strong>.</td></tr><tr><td><strong>Applet Status on Broker VM</strong></td><td>Shows the status of the <strong>Registry Scanner</strong> applet on the <strong>Broker VM</strong> page. This status is visible only when the Scan with <strong>Broker VM</strong> mode is selected.</td></tr><tr><td><strong>Repositories</strong></td><td>Shows the number of scanned repositories in the registry.</td></tr><tr><td><strong>Scan Mode</strong></td><td>Shows the selected scan mode for the data connector, such as <strong>Cloud Scan</strong>, <strong>Scan with Outpost</strong>, or <strong>Scan with Broker VM</strong>.</td></tr><tr><td><strong>Security Capabilities</strong></td><td>Shows a breakdown of the security capabilities enabled on the instance and their individual statuses. For example, select <strong>Registry Scanning</strong> when it shows a warning or error status to see the open errors and issues that contributed to the status.</td></tr></tbody></table>
8.  After the scan is complete, you can view the scanned images on the **Container Images Inventory** page. For more details, see [Container Image assets](https://app.gitbook.com/s/cyIgISZgANJYkmLlnwdK/detect-investigate-and-respond-to-threats/asset-management/asset-classes/compute-assets/container-image-assets).

    If you have selected the **Scan with Broker VM** option, then a **Registry Scanner** applet is created on the selected **Broker VM** or **Cluster**. For details, see [Verify Registry Scanner connection](https://app.gitbook.com/s/cyIgISZgANJYkmLlnwdK/configure-cortex-xdr/cortex-xdr-data-sources/generic-on-premise-data-collectors/broker-vm-data-collector-applets/activate-registry-scanner#verify-registry-scanner-connection).

<figure><img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2FYuZqoJgEKHf1L7Estps0%2Fregistry-broker-vm.png?alt=media&#x26;token=7239ef79-a1a8-40cb-afe9-51fed4d841b0" alt=""><figcaption></figcaption></figure>

<br>
