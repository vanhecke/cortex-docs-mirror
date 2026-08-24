---
description: Increase Broker VM cache storage for Cortex XSIAM data collection.
---

# Increase Broker VM storage allocated for data caching

Learn more about increasing the storage allocated for data caching in the Broker VM.

The storage allocated for data caching in the Broker VM is fixed at around 346.4 GB using a Logical Volume Manager (LVM). You can increase the disk space allocated to attain better resilience during network and connectivity issues by adding a new disk. The disk needs to be added manually to an applicable hypervisor that your broker supports, so that the Broker VM automatically detects the physical disk and allows you to connect to it. Extending the existing disk is not supported.

When allocating storage for data caching, ensure you are aware of the following:

* You must allocate the entire disk as opposed to portions of the disk.
* You can connect multiple disks to increase the data caching space according to your requirements.
* Once a disk is connected, It's not possible to dismiss a disk that has already been allocated, or to reduce the disk space of the data caching.
* Adding a disk requires formatting and deleting all its contents.

{% hint style="warning" %}
#### Warning

This operation is irreversible, and will make the disk become an integral part of the broker, where disconnecting the disk will result in errors and data loss.
{% endhint %}

### How to increase the Broker VM disk size

1. Gracefully shutdown the applicable Broker VM in the hypervisor to manually add a disk.
2. Add a disk manually through the hypervisor portal. This step involves accessing the portal and attaching a new disk to the VM.

{% hint style="info" %}
#### Note

Follow your hypervisor documentation to understand how to add a persistent disk storage to your VM.
{% endhint %}

3. Power On the applicable Broker VM in the hypervisor.
4. Select Settings → Configurations → Data Broker → Broker VMs.
5. In the Broker VMs table, locate your Broker VM, and wait for a few minutes until the status of the Broker VM is Connected, right-click, and select Configure.
6. Scroll down to the Storage section, verify that your disk is detected with a new line that reads New disk detected with the correct disk name and disk size, and click Add to data caching space.

{% hint style="info" %}
#### Note

If your disk is not listed and you didn't shutdown your Broker VM in your hypervisor before manually adding a disk to the VM, you'll need to reboot the Broker VM before the disk details are detected by the Broker VM. This can be performed either in the hypervisor or directly in the Broker VMs page.
{% endhint %}

7\. In the ARE YOU SURE? dialog box that is displayed, confirm that you want to add the new disk to the broker's data caching space and are aware of all the ramifications by clicking Yes, add. 8. To apply your changes, click Save. Once completed, a notification is added to the Notification Center indicated whether the disk size was increased successfully. If not, the notification includes the errors encountered during the process. In addition, when the disk is added successfully, the total size of the disk space available is updated in the DISK USAGE column on the Broker VMs page.
