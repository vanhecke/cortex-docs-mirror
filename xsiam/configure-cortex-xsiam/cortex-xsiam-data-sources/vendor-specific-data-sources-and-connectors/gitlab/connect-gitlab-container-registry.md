---
description: Connect a GitLab container registry to Cortex XSIAM for image scanning.
---

# Connect GitLab container registry

Configure Cortex XSIAM to scan your GitLab Container Registry without using administrator credentials. Use a GitLab Personal Access Token (PAT) to authenticate Cortex to access the GitLab Container Registry. This allows Cortex to list all container registries or images, and secure them from vulnerabilities, malware, and secrets.

{% hint style="info" %}
**License type**: This feature is included with a Cortex XSIAM Premium license. It is also included with any other Cortex XSIAM product that has the Cloud Posture Security or the Cloud Runtime Security add-on.
{% endhint %}

### How to connect GitLab registry

Follow the wizard to connect the GitLab Container Registry connector in Cortex XSIAM.

1. Navigate to **Settings → Data Sources & Integrations**.
2. On the **Add Data Sources** **or Integrations** page, click **+ Add New**, search for **GitLab Container Registry**, then hover over it and click **Add.**
3. The **Instance Name** is automatically populated. You can change it to a more meaningful name.
4. Choose the **Scan Mode**, and then follow the steps provided for that mode to configure the connection.

<details>

<summary>Cloud Scan</summary>

Security scanning is done in the Cortex XSIAM environment when you select this mode.

1.  Select the appropriate **Cloud Provider** and **Region** for the Cortex environment to use for registry scanning.

    As a best practice, choose the region closest to your registry deployment to achieve the best scanning throughput and potentially reduce cloud costs.
2. (Optional) Enable **Allow access by IPs** to specify a static IP address for the scanner to use. Make sure the static IP is allowed through your firewall so the scanner can access the registry during the scanning process.
3.  Choose the relevant **Account Type** for GitLab deployments:

    **GitLab Cloud (Saas)**

    1.  (Optional) Enter the **Group Id**.

        You can enter a single group ID or a list of group IDs separated by a comma. The group ID is used to locate all the registries within a specific group.
    2.  (Optional) Enter the **Project Id**.

        You can enter a GitLab Project ID or a list of project IDs separated by a comma. The project ID is used to locate all the registries located within a specific project.

        <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><ul><li>When both the group ID and project ID are provided, the system retrieves container images from all projects within the specified group as well as from the specified project.</li><li>If neither the group ID nor the project ID is provided, the system retrieves container images from all registries (across all groups and projects) accessible to the authenticated user or token in GitLab.</li></ul></div>
    3. Under **Authentication Method**, enter your GitLab **Access Token**.

    **GitLab Self-Hosted**

    1.  Enter the **Registry URL**.

        If you are using a CA certificate, enter the server IP address instead of the registry url.
    2.  (Optional) Enter the **Group id**.

        You can enter a single group ID or a list of group IDs separated by a comma. The group ID is used to locate all the registries within a specific group.
    3.  (Optional) Enter the **Project Id**.

        You can enter a GitLab Project ID or a list of project IDs separated by a comma. The project ID is used to locate all the registries located within a specific project.

        <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><ul><li>When both the group ID and project ID are provided, the system retrieves container images from all projects within the specified group as well as from the specified project.</li><li>If neither the group ID nor the project ID is provided, the system retrieves container images from all registries (across all groups and projects) accessible to the authenticated user or token in GitLab.</li></ul></div>
    4. Enter the **Api Domain**. Include the GitLab API base URL with the **https://** prefix (for example, `https://gitlab.example.dev`).
    5. Under Authentication Method, enter your GitLab **Access Token**.
    6. (Optional) Expand **Show Advanced Settings**, and then enter the **CA certificate** in PEM format for Cortex to validate the GitLab registry.
4. Select **Next.**

</details>

<details>

<summary>Scan with Outpost</summary>

Security scanning is done on infrastructure deployed to a cloud account that you own. This mode requires additional cloud provider permissions and may incur extra costs.

{% hint style="warning" %}
#### Prerequisite

Ensure an [Outpost](../../cloud-service-provider-csp-onboarding/outpost-onboarding) is connected to your tenant.
{% endhint %}

1.  Choose a **Cloud Provider** to initialize registry scanning.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h4>Note</h4><p>If you choose <strong>Azure</strong> as the <strong>Cloud Provider</strong>, you must also select the <strong>Tenant Id.</strong> The <strong>Tenant Id</strong> is required to approve Cortex as an enterprise application in your Azure tenant.</p></div>
2.  Choose Outpost account to use for this instance. If no Outposts are shown, you can Create a new one. For more details, see [Outposts](../../../cloud-service-provider-csp-onboarding/outpost-onboarding/outpost-creation-workflow#phase-2-creating-the-outpost).

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h4>Note</h4><p>If you choose <strong>Azure</strong> as the cloud provider, only <strong>Outposts</strong> associated with the selected tenant ID are displayed.</p></div>
3. Select the **Region** where the registry is hosted.
4. (Optional) Enable **Allow access by IPs** if you want to specify a static IP address for the scanner to use. Make sure the static IP is allowed through your firewall so that the scanner can access the registry during the scanning process.
5.  Choose the relevant **Account Type** for GitLab deployments:

    **GitLab Cloud (Saas)**

    1.  (Optional) Enter the **Group Id**.

        You can enter a single group ID or a list of group IDs separated by a comma. The group ID is used to locate all the registries within a specific group.
    2.  (Optional) Enter the **Project Id**.

        You can enter a GitLab Project ID or a list of project IDs separated by a comma. The project ID is used to locate all the registries located within a specific project.

        <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><ul><li>When both the group ID and project ID are provided, the system retrieves container images from all projects within the specified group as well as from the specified project.</li><li>If neither the group ID nor the project ID is provided, the system retrieves container images from all registries (across all groups and projects) accessible to the authenticated user or token in GitLab.</li></ul></div>
    3. Under **Authentication Method**, enter your GitLab **Access Token**.

    **GitLab Self-Hosted**

    1.  Enter the **Registry URL**.

        If you are using a CA certificate, enter the server IP address instead of the registry url.
    2.  (Optional) Enter the **Group id**.

        You can enter a single group ID or a list of group IDs separated by a comma. The group ID is used to locate all the registries within a specific group.
    3.  (Optional) Enter the **Project Id**.

        You can enter a GitLab Project ID or a list of project IDs separated by a comma. The project ID is used to locate all the registries located within a specific project.

        <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><ul><li>When both the group ID and project ID are provided, the system retrieves container images from all projects within the specified group as well as from the specified project.</li><li>If neither the group ID nor the project ID is provided, the system retrieves container images from all registries (across all groups and projects) accessible to the authenticated user or token in GitLab.</li></ul></div>
    4. Enter the **Api Domain**. Include the GitLab API base URL with the **https://** prefix (for example, `https://gitlab.example.dev`).
    5. Under Authentication Method, enter your GitLab **Access Token**.
    6. (Optional) Expand **Show Advanced Settings**, and then enter the **CA certificate** in PEM format for Cortex to validate the GitLab registry.
6. Select **Next.**

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
3.  Choose the relevant **Account Type** for GitLab deployments:

    **GitLab Cloud (Saas)**

    1.  (Optional) Enter the **Group Id**.

        You can enter a single group ID or a list of group IDs separated by a comma. The group ID is used to locate all the registries within a specific group.
    2.  (Optional) Enter the **Project Id**.

        You can enter a GitLab Project ID or a list of project IDs separated by a comma. The project ID is used to locate all the registries located within a specific project.

        <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><ul><li>When both the group ID and project ID are provided, the system retrieves container images from all projects within the specified group as well as from the specified project.</li><li>If neither the group ID nor the project ID is provided, the system retrieves container images from all registries (across all groups and projects) accessible to the authenticated user or token in GitLab.</li></ul></div>
    3. Under **Authentication Method**, enter your GitLab **Access Token**.

    **GitLab Self-Hosted**

    1.  Enter the **Registry URL**.

        If you are using a CA certificate, enter the server IP address instead of the registry url.
    2.  (Optional) Enter the **Group id**.

        You can enter a single group ID or a list of group IDs separated by a comma. The group ID is used to locate all the registries within a specific group.
    3.  (Optional) Enter the **Project Id**.

        You can enter a GitLab Project ID or a list of project IDs separated by a comma. The project ID is used to locate all the registries located within a specific project.

        <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><ul><li>When both the group ID and project ID are provided, the system retrieves container images from all projects within the specified group as well as from the specified project.</li><li>If neither the group ID nor the project ID is provided, the system retrieves container images from all registries (across all groups and projects) accessible to the authenticated user or token in GitLab.</li></ul></div>
    4. Enter the **Api Domain**. Include the GitLab API base URL with the **https://** prefix (for example, `https://gitlab.example.dev`).
    5. Under Authentication Method, enter your GitLab **Access Token**.
    6. (Optional) Expand **Show Advanced Settings**, and then enter the **CA certificate** in PEM format for Cortex to validate the GitLab registry.
4. Select **Next.**

</details>

5. In the **Initial Scan Configuration**, set your scanning process to focus on recently added or modified container images and exclude older ones that do not align with your current scanning objectives. This setting helps avoid unnecessary scans. Choose one of the following options:
   * **All:** Scans all container images, including all versions (tags), in all discovered repositories.
   * **Latest Tag**: Scans only images tagged **'latest'** in all discovered repositories.
   * **Days Modified**: Scans container images that have been created in the last few days. You can select a range of up to **90** days for the scan.
6.  Select **Save**.

    When the GitLab data source is saved successfully, a new data connector is created, and the initial discovery scan is started. The connection process may take up to 15 minutes.
7. To check connector status and scan results, follow these steps:
   1. Navigate to **Settings → Data Sources & Integrations**.
   2. Find the **GitLab Container Registry** instance from the list of **3rd Party Data Sources** connectors, or use **Search**.
   3. In the **GitLab Container Registry** instance row, select **View Details**. The **GitLab Instances** page appears.
   4. On the **GitLab Instances** page, you can filter results by any heading and value.
   5.  Select an instance name to open the details pane. The details pane contains the following granular information:

       | Instance Details               | Description                                                                                                                                                                                                                                                       |
       | ------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
       | **Status**                     | Shows the status of the connector: Connected, **Error**, **Warning**, **Disabled**, or **Pending**.                                                                                                                                                               |
       | **Applet Status on Broker VM** | Shows the status of the **Registry Scanner** applet on the **Broker VM** page. This status is visible only when the **Scan with Broker VM** mode is selected.                                                                                                     |
       | **Repositories**               | Shows the number of scanned repositories in the registry.                                                                                                                                                                                                         |
       | **Scan Mode**                  | Shows the selected scan mode for the data connector, such as **Cloud Scan**, **Scan with Outpost**, or **Scan with Broker VM**.                                                                                                                                   |
       | **Security Capabilities**      | Shows a breakdown of the security capabilities enabled on the instance and their individual statuses. For example, select **Registry Scanning** when it shows a **warning** or **error** status to see the open errors and issues that contributed to the status. |
8.  **Next Steps**.

    * After the scan is complete, you can view the scanned images on the **Container Images Inventory** page. For more details, see [Container Images assets](../../../../detect-investigate-and-respond-to-threats/asset-management/asset-classes/compute-assets/container-image-assets).
    *   If you have selected the **Scan with Broker VM** option, then a **Registry Scanner applet** is created on the selected **Broker VM** or **Cluster**. For details, see [Verify Registry Scanner connection](../../../generic-on-premise-data-collectors/broker-vm-data-collector-applets/activate-registry-scanner#verify-registry-scanner-connection).&#x20;

        <figure><img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2FWVVeI7SbPxjm09uZY3nb%2Fbroker-vm-registry-applet.png?alt=media&#x26;token=ec3461c1-9b6e-4602-89ef-84516d57be19" alt=""><figcaption></figcaption></figure>

    <figure><img src="https://docs-cortex.paloaltonetworks.com/api/khub/maps/5CAbsl8idaK8R43ZLhoTOw/resources/9MOUg1Tldqzugfj2ajn4tw-5CAbsl8idaK8R43ZLhoTOw/content?v=dd91287b8369b7dc&#x26;Ft-Calling-App=ft/turnkey-portal" alt=""><figcaption></figcaption></figure>

<br>
