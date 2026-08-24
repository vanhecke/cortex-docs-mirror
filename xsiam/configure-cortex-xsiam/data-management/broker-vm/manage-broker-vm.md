---
description: >-
  Manage Broker VM configuration, capacity, updates, and clusters in Cortex
  XSIAM.
---

# Manage Broker VM

After you configure the Broker VMs, you can manage these brokers from the Cortex XSIAM management console in the Broker VMs page.

When managing a Broker VM, the options differ for a standalone Broker VM versus a Broker VM node that is added to a high availability (HA) cluster. Certain configuration options that are only relevant for a Broker VM cluster node, such as Remove from Cluster, are only displayed when the Broker VM is a cluster peer.

Select Settings → Configurations → Data Broker → Broker VMs to view detailed information regarding your registered Broker VMs in the Brokers tab.

### Understanding the Broker VM table

The Broker VMs table enables you to monitor and mange your Broker VM and applet connectivity status, version management, device details, and usage metrics. A status icon is displayed in the following columns, where the colors can indicate different statuses:

* Device Name: Indicates whether the Broker machine is registered and connected to Cortex XSIAM.
  * Black: Disconnected to Cortex XSIAM
  * Red: Disconnected from Cortex XSIAM
  * Green: Connected
* Version: Indicates whether the Broker VM is running the latest version.
  * Orange: Past Version
  * Green: Latest Version
* Apps: Indicates whether the available Broker VM data collector applets are connected to Cortex XSIAM and up-to-date..
  * Green (Connected): Indicates the applet has no issues and is running the latest version.
  * Orange (Warning):
    * Indicates the applet has minor connectivity or configuration issues, such as a new applet version is available.
    * During an active update, the indicator flashes orange and the status displays as **Updating**.
  * Red (Error): Indicates the applet has errors.

{% hint style="info" %}
#### Note

For more information on troubleshooting errors and warnings for these broker applets, see [Troubleshoot Broker VM applet errors](troubleshoot-broker-vm-applet-errors).
{% endhint %}

### Broker VM table field descriptions

The following table describes common fields that you can add to the Brokers table using the column manager and lists the fields in alphabetical order.

{% hint style="info" %}
#### Note

Certain fields are also exposed in the Clusters tab, when a Broker VM node is added to a High Availability (HA) cluster, and each cluster node is expanded to view the Broker VM nodes table. An asterisk (\*) is beside every field that is also included in the Broker VM nodes table for each HA cluster.
{% endhint %}

| Field                  | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ALL interfaces         | All IP addresses of the different interfaces on the device.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| APPS\*                 | List of active or inactive applets and the connectivity status for each.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| CLUSTER NAME\*         | Indicates the name of the HA cluster that the Broker VM has been added to. For a standalone Broker VM, which isn't added to any HA cluster, this field is empty.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| CPU USAGE\*            | CPU usage percentage of the Broker VM device that is synced every 5 minutes.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| CONFIGURATION STATUS\* | <p>Broker VM configuration status. Status is defined by the following according to changes made to any of the Broker VM configurations:</p><ul><li>up to date: Broker VM configuration changes made through the Cortex XSIAM console have been applied.</li><li>in progress: Broker VM configuration changes made through the Cortex XSIAM console are being applied.</li><li>submitted: Broker VM configuration changes made through the Cortex XSIAM console have reached the Broker VM and awaiting implementation.</li><li>failed: Broker VM configuration changes made through the Cortex XSIAM console have failed. Need to open a Palo Alto Networks support ticket.</li></ul> |
| DEVICE ID              | Device ID allocated to the Broker VM by Cortex XSIAM after registration.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| DEVICE NAME\*          | <p>Same as the Device ID.</p><p>A ⚠ icon notifies of an expired Broker VM. To reconnect, generate a new token and re-register your Broker VM as described in steps 1 through 7 of <a href="set-up-and-configure-broker-vm">Configure the Broker VM</a>. Once registered, all previous Broker VM configurations are reinstated.</p>                                                                                                                                                                                                                                                                                                                                                    |
| DISK USAGE\*           | <p>Disk usage percentage from the total allocated for data caching in the Broker VM. Inside the brackets is displayed how much this is in GB from the total disk size in GB.</p><p>A notification is added to the Notification Center whenever the disk space is low disk and whenever the disk size is increased.</p>                                                                                                                                                                                                                                                                                                                                                                |
| EXTERNAL INTERFACE     | <p>The IP interface the Broker VM is using to communicate with the server.</p><p>For AWS and Azure cloud environments, the field displays the <strong>Internal IP</strong> value.</p>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| LAST SEEN              | Indicates when the Broker VM was last seen on the network.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| MEMORY USAGE\*         | Memory usage percentage of the Broker VM that is synced every 5 minutes.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| STATUS\*               | Connection status of the Broker VM. Status is defined by either Connected or Disconnected. Disconnected Broker VMs do not display CPU Usage, Memory Usage, and Disk Usage information. Notifications about the Broker VM losing connectivity to Cortex XSIAM appear in the Notification Center.                                                                                                                                                                                                                                                                                                                                                                                       |
| UPGRADE TIME           | Timestamp of when the Broker VM was upgraded.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| VERSION\*              | <p>Version number of the Broker VM.</p><ul><li><strong>Broker VM version</strong>: If the status indicator is not green, the Broker VM is not running the latest version.</li><li><strong>Applets version</strong>: You can view the current version of an individual applet by clicking the applet in the <strong>APPS</strong> column.</li></ul><p>Notifications about the available new Broker VM version appear in the Notification Center.</p><p><br></p>                                                                                                                                                                                                                        |

### Maintenance releases

Cortex XSIAM updates and enhances the Broker VM automatically through maintenance releases. The Broker VM version release process uses several security measures and tools to ensure that every released version is highly secure. These include the following.

* CIS Server Level 1 and 2 benchmarks (using a 3rd party product)
* Vulnerability scanning for containers running on the Broker VM
* Vulnerability scanning for the host kernel
* Periodic 3rd party penetration testing
