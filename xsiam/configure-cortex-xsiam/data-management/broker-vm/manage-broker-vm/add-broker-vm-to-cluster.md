---
description: Add a Cortex XSIAM Broker VM to a cluster.
---

# Add Broker VM to cluster

Learn more about adding a Broker VM to a high availability cluster.

You can add standalone Broker VMs to a high availability (HA) cluster from either the Brokers tab or Clusters tab.

You can only add a Broker VM to a cluster, when the Broker VM version is 19.0 and later, the STATUS is Connected, and the Broker VM version isn't older than the cluster version.

Once you add a Broker VM to a cluster, the Broker VM becomes a cluster node and is added to the cluster folder in the Clusters tab. If it is the only peer Broker VM in the cluster, it is designated as the Primary node; otherwise, it is designated as a standby node.

1. Select Settings → Configurations → Data Broker → Broker VMs.
2. Add a Broker VM in one of the following tabs:

{% tabs %}
{% tab title="Brokers tab" %}
1) Right-click a standalone Broker VM, and select Add Broker to Cluster.
2) In the Select Cluster field, choose the cluster that you want this Broker VM to be added to.
{% endtab %}

{% tab title="Clusters tab" %}
1. Right-click a cluster node, and select Add Broker to Cluster.
2. In the Select broker field, choose the standalone Broker VM that you want to add to this cluster.
{% endtab %}
{% endtabs %}

3. Click Add Broker. Adding a Broker VM to a cluster overrides all previous Broker VM settings and disables all active applets on this Broker VM. When the Broker VM is added to a cluster, the cluster configuration and cluster applet settings propagate to the Broker VM. The state of the applets on the Broker VM is dependent on the applet mode and Broker VM node role in the cluster. When the operation completes, a notification is added to the Notification Center.
