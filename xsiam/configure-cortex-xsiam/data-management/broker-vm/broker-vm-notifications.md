# Broker VM notifications

Learn about the notifications that are relevant to Cortex XSIAM Broker VMs.

To help you monitor your Broker VM version, connectivity, and high availability clusters, Cortex XSIAM sends notifications to your Cortex XSIAM console Notification Center.

Cortex XSIAM sends the following notifications:

<details>

<summary>Add Cluster</summary>

Notifies when a cluster was added.

</details>

<details>

<summary>Applet Activated</summary>

Notifies when an applet is activated on a cluster.

</details>

<details>

<summary>Applet configuration</summary>

Notifies when an applet on a cluster configuration was updated.

</details>

<details>

<summary>Applet Deactivated</summary>

Notifies when an applet is deactivates on a cluster.

</details>

<details>

<summary>Broker VM Connectivity</summary>

Notifies when the Broker VM has lost connectivity to Cortex XSIAM .

</details>

<details>

<summary>Broker VM Disk Usage</summary>

Notifies when the Broker VM is utilizing over 90% of the allocated disk space.

</details>

<details>

<summary>Cluster Configuration</summary>

* Notifies when a Broker VM node was added to a cluster.
* Notifies when a Broker VM node was removed from a cluster.
* Notifies when the configuration for the cluster needs to be set.

</details>

<details>

<summary>Cluster failover</summary>

* Notifies when a failover is initiated in the cluster from one Broker VM node to another.
* Notifies when a failover completed successfully. The Broker VM is now Primary in the cluster.
* Notifies when a failover in the cluster completed with errors and error message.
* Notifies when couldn't perform a failover in the cluster as there is no available standby node with sufficient redundancy.

</details>

<details>

<summary>Cluster health declined</summary>

* Notifies when failed to detect an available standby Broker VM node in the cluster.
* Notifies when critical errors detected in the cluster and there is no available standby Broker VM node for failover.

</details>

<details>

<summary>Cluster health recovered</summary>

Notifies when detected an available standby Broker VM node in the cluster.

</details>

<details>

<summary>Disk space allocation on broker</summary>

Notifies whether the disk space allocated for data caching in the Broker VM has been increased successfully. If not, the notification includes the errors encountered during the process. For more information on allocating disk space to the Broker VM, see [Increase Broker VM storage allocated for data caching](manage-broker-vm/increase-broker-vm-storage-allocated-for-data-caching).

</details>

<details>

<summary>Broker VM requires a reboot</summary>

Notifies after a Broker VM update whether a broker needs a reboot to finish installing important updates.

</details>

<details>

<summary>New Broker VM Version</summary>

Notifies when a new Broker VM version has been released.

* If the Broker VM Auto Upgrade is disabled, the notification includes a link to the latest release information. It is recommend you upgrade to the latest version.
* If the Broker VM Auto Upgrade is enabled, 12 hours after the release you are notified of the latest upgrade, or you are notified that the upgrade failed. In such a case, open a Palo Alto Networks Support Ticket.

</details>

<details>

<summary>Reinstall Broker VM with a new image</summary>

For all brokers that were deployed with an old Broker VM image downloaded prior to July 9th, 2023 (installed with Ubuntu 18.04 or earlier), the Broker VM must be reinstalled with a new image (installed with Ubuntu 20.04 or later) before upgrading to the latest version. The name of the Broker VM to upgrade is indicated with a link to the instructions.

{% hint style="info" %}
#### Note

For more information on upgrading to a new Broker VM image, see [Migrating to a New Broker VM Image](../../../migrating-to-a-new-broker-vm-image/migrating-to-a-new-broker-vm-image).
{% endhint %}

</details>

<details>

<summary>Remove Cluster</summary>

Notifies when a cluster was removed.

</details>

To ensure you stay informed about Broker VM activity, you can also configure notification forwarding to forward your Broker audit logs to an email distribution list or Syslog server. For more information about the Broker VM audit logs, see Broker VM Activity in the Cortex XSIAM Administrator Guide.
