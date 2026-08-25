---
description: >-
  Migrate a Broker VM high-availability cluster node to the latest Cortex XSIAM
  broker image, including cluster and load-balancer updates.
---

# Broker VM high availability cluster node

You can migrate a broker node in a High Availability (HA) cluster to the latest broker VM image.

#### How To

1.  Install and configure a new Broker VM using the new image from your tenant. For detailed instructions, see [Set up and configure Broker VM](../configure-cortex-xsiam/data-management/broker-vm/set-up-and-configure-broker-vm).

    Remember to perform the following if applicable:

    * Add SSL Server Certificates to the new broker.
    * Add Trusted CA Certificate to the new broker.
    * Configure your NTP servers for the new broker.
2. Add the new broker to the cluster. For instructions, see [Add Broker VM to cluster](../configure-cortex-xsiam/data-management/broker-vm/broker-vm-high-availability-cluster/manage-broker-vm-clusters/add-broker-vm-to-cluster).
3. Update your Load Balancer configuration to send logs to the new cluster node.
4. Shutdown the old cluster node that you are replacing.
5. (Optional) Update your Load Balancer configuration to stop sending logs to the old cluster node.
6. (Optional) Remove the old Broker VM from your tenant.
7. (Optional) Delete the old Broker VM from your hypervisor infrastructure.
