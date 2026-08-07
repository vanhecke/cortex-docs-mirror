# Upgrade Broker VM

Learn more about upgrading the Broker VM from the Cortex XSIAM management console.

If your Broker VM was deployed using an image downloaded before February 22, 2026 (running Ubuntu 20.04 or earlier), you must reinstall the broker with a new image (running Debian 13 or later) before you can upgrade to the latest version. For more information, see [Learn more about migrating to the latest broker VM image](../../../../migrating-to-a-new-broker-vm-image/migrating-to-a-new-broker-vm-image).

1. Select Settings → Configurations → Data Broker → Broker VMs.
2. In either the Brokers or Clusters tab, locate your Broker VM, right-click, and select Upgrade Broker version. Upgrading your Broker VM takes approximately 5 minutes.

{% hint style="warning" %}
#### Important

After a Broker VM upgrade, your broker may require a reboot to finish installing important updates. A notification about this will be sent to your Cortex XSIAM console Notification Center.
{% endhint %}
