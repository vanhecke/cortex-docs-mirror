# Remove from Cluster

Learn more about removing a Broker VM node from a high availability cluster.

You can remove a Broker VM node from a high availability (HA) cluster in either the Brokers tab or Clusters tab of the Broker VMs page. This option is only available if the Broker VM is currently a member of a cluster.

When a Broker VM node is removed from a HA cluster, it becomes a standalone Broker VM. All its configuration settings, including applet settings, are reset to default like a newly created Broker VM. If you remove a Primary node, an automatic failover occurs.

You can remove a Broker VM node from a cluster if the current node STATUS is Connected.

1. Select Settings → Configurations → Data Broker → Broker VMs.
2. In either the Brokers tab or Clusters tab, right-click a Broker VM node, and select Remove from Cluster.
3. Follow the instructions in the dialog box, and click Remove. When removing the last node in the cluster, all applets in this cluster become Inactive, and the cluster becomes Unavailable. When the Broker VM receives the new configuration, the Broker VM becomes a standalone Broker VM with settings reset to default.

{% hint style="info" %}
#### Note

If you've enabled a Load Balancer Health-Check on the cluster, you need to exclude this Broker VM from your Load Balancer settings.
{% endhint %}
