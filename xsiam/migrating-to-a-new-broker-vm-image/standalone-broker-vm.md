---
description: >-
  Migrate a standalone Broker VM to the latest Cortex XSIAM broker image,
  including configuration import and log-source updates.
---

# Standalone Broker VM

You can migrate a standalone Broker VM in your environment to the latest broker VM image.

#### How To

1. Install and configure a new Broker VM using the new image from your tenant. For detailed instructions, see [Set up and configure Broker VM](../configure-cortex-xsiam/data-management/broker-vm/set-up-and-configure-broker-vm).
2. Import the Broker VM configuration from an old broker to the new broker with the new image. For more information, see [Import Broker VM Configuration](../configure-cortex-xsiam/data-management/broker-vm/manage-broker-vm/import-broker-vm-configuration).
   *   During the import, use the option to shutdown the old broker (selected by default).

       <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>The shutdown process can take up to 10 minutes while the broker offloads its data cache.</p></div>
3. Update settings to keep receiving logs from external sources (Syslog, Netflow, and WEC) using the new broker. Use one of the following options:
   * (Recommended) Option 1: Change the IP address of the new broker to the IP address of the old broker.
     1. Select Settings → Configurations → Data Broker → **Broker VMs**.
     2. In the Broker VMs table, right-click the new broker VM, and select **Configure**.
     3. In the **Network Interfaces** section, edit the **IP** address by selecting the pencil icon.
     4. Click **Save**.
   * Option 2: Update your network sources to send messages to the IP address of the new broker.
     * Update your network devices to send Syslog messages to the IP address of the new broker.
     * Update your network devices to send Netflow messages to the IP address of the new broker.
     * Update the DNS record of the old broker FQDN to point to the IP address of the new broker.
4. (Optional) Remove the old broker from your tenant.
5. (Optional) Delete the old Broker VM from your hypervisor infrastructure.
