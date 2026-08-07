# Add applet to cluster

You can add an applet to a high availability (HA) cluster from the Clusters tab of the Brokers VM page.

You can always add an applet to a cluster, even if the cluster status is Unavailable or Error. When an applet is added to a cluster without any Broker VM nodes, the cluster status is Unavailable and the cluster APPS status displays as Inactive.

1. Select Settings → Configurations → Data Broker → Broker VMs, and select the Clusters tab.
2. In the Clusters table, locate the cluster that you want to add an applet.
3. You can either right-click the cluster, and select Add App → , or in the APPS column, left-click Add → . The applet is only available for you to add to the cluster if it hasn't already been added.
4. Configure your applet. The various applets that you can configure are the same as when configuring a standalone Broker VM. For more information on a particular applet configuration, locate the applet in the Set up Broker VM section in the Cortex XSIAM Admin Guide. The applet is listed with a status indicator in the APPS column, where the colors depict the following statuses:

* Green (Connected): Indicates the applet has no issues.
* Orange (Warning): Indicates the applet has minor issues.
* Red (Error): Indicates the applet has errors.
* White (Inactive): Indicates the applet is inactive.

{% hint style="info" %}
#### Note

For more information on troubleshooting errors and warnings for these applets, see [Troubleshoot Broker VM applet errors](../../troubleshoot-broker-vm-applet-errors).
{% endhint %}

Once the applet configuration is changed in a cluster, the changes are automatically applied to the cluster nodes depending on the applet and cluster node role. For example, if you add the Kafka Collector, which is an "active/passive" applet, the applet is automatically initiated and enters an active state on the Primary node and is on standby on the standby nodes. While if you add the Syslog Collector "active/active" applet, the changes automatically propagate so that the applet is active on all cluster nodes, including Primary and standby.
