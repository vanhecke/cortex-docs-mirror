# Remove cluster

Learn more about removing a high availability cluster.

You can remove a high availability (HA) cluster in the Clusters tab of the Broker VMs page.

When removing a cluster, the cluster is disassembled and the cluster object is deleted. All nodes in the cluster are reverted back to standalone Broker VMs with their settings reset to default as a newly created Broker VMs.

If you've configured load balancing for any "active/active" applets configured, you need to update your Load Balancer configuration settings to stop sending logs to these Broker VM nodes.

You cannot remove a cluster that is used as a download source from which the Cortex XDR agents retrieve release upgrades and content updates. You'll need to change the cluster's current designated role before removing a cluster.

1. Select Settings → Configurations → Data Broker → Broker VMs.
2. In the Clusters tab, right-click a cluster, and select Remove Cluster.
3. Follow the instructions in the REMOVE CLUSTER window, whose instructions differ depending on the type of cluster you are trying to remove, and Remove the cluster.
