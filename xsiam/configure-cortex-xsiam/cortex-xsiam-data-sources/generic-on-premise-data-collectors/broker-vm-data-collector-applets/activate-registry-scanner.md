---
description: Configure Registry Scanner for Cortex XSIAM.
---

# Activate Registry Scanner

The **Broker VM** provides a **Registry Scanner** applet that scans and secures your container image registries. It supports Docker V2 or JFrog self-hosted registries located on-premises or in private cloud networks.

{% hint style="info" %}
**License type:** Requires a Cortex XSIAM Premium license. It is also included with any other Cortex XSIAM product that has the Cloud Runtime Security add-on.
{% endhint %}

{% hint style="info" %}
**Note**

* You cannot activate the **Registry Scanner** directly on a new or existing Broker VM. You can only activate or deactivate existing Registry Scanner applets. To activate or deactivate existing applets, see Step 4 under [Verify Registry Scanner connection](#verify-registry-scanner-connection) section.
{% endhint %}

### **Verify Registry Scanner connection**

After the registry scanner is initialized, perform the following steps to verify that the **Registry Scanner** applet is connected to the **Broker VM**:

{% hint style="warning" %}
### Prerequisite:

* To initialize registry scanning on your Broker VM, you must first add the necessary data connectors. For details, see:
  * [Connect Docker Hub registry](broken-reference)
  * [Connect Docker V2 compliant container registry](broken-reference)
  * [Connect GitLab container registry](broken-reference)
  * [Connect Harbor registry](broken-reference)
  * [Connect JFrog container registry](broken-reference)
  * [Connect Sonatype Nexus registry](broken-reference)
* When sizing your Broker VM, consider the following recommendations:
  *   **Disk Size:** Calculate the required disk space by multiplying the average container image size in your environment by 10. This factor accounts for simultaneous operations with a buffer.

      For example, If your average image size is 500 MB, allocate at least 5 GB of disk space (500 MB \* 10 = 5000 MB = 5 GB).
  * **CPU:** Allocate a minimum of 8 CPU cores.
  * **Memory:** Allocate a minimum of 16 GB of RAM.
{% endhint %}

1. Go to **Settings** → **Configurations** → **Data Broker** → **Broker VMs**.
2. On either the **Brokers** or **Clusters tab**, find the Broker VM.
3. In the **APPS** column for the **Broker VM**, verify that the **Registry Scanner** app appears.
4.  Select the **Registry Scanner** app to open a window displaying the following information:

    ![registry-scanner-applet-on-boker-vm-window-panel.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2FndzyzKJVxTqh9cWUzfv6%2Fcontainer-registry.png?alt=media\&token=0d14ee28-3c2a-4f06-b8cd-24377b6ee1b8)

    *   **Connection**: Shows the app's current connection status. You can also **Deactivate** the app.

        To reactivate the **Registry Scanner** app, do one of the following:

        * On the **Brokers** tab, locate the Broker VM, select **+Add** in the **APPS** column, and then choose **Registry Scanner**.
        * On the **Clusters** tab, locate the Broker VM, select **+Add** in the **APPS** column, and then choose **Registry Scanner**.

        If the **Registry Scanner** app is not listed in the drop-down menu when you click **+Add**, it means that the registry scanning was not configured for that **Broker VM**. You must first add the data connectors.
    * **Resources**: Shows the percentage of **CPU**, **Memory**, and **Disk** resources used by the app.
5. To manage the Registry Scanner applet, see:
   * [Manage a Docker Hub connector](broken-reference)
   * [Manage a Docker V2 connector](broken-reference)
   * [Manage a Gitlab Container Registry connector](broken-reference)
   * [Manage a Harbor connector](broken-reference)
   * [Manage a JFrog connector](broken-reference)
   * [Manage a Sonatype connector](broken-reference)
