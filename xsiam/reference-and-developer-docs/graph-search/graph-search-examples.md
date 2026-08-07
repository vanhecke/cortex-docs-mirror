---
description: Learn how to build Graph Search queries by working through a few examples.
---

# Graph Search examples

{% hint style="info" %}
### Notice

This feature is included with a Cortex XSIAM Premium license. It is also included with any other Cortex XSIAM license that has the Cloud Posture Security or Cloud Runtime Security add-on.
{% endhint %}

{% hint style="warning" %}
### Prerequisite

Graph Search requires **View** or **View/Edit** RBAC permissions for **Graph Search** under **Investigation & Response** → **Search**.
{% endhint %}

Review the following topics:

* [Get started with Graph Search queries](get-started-with-graph-search-queries)
* [How to build Graph Search queries?](how-to-build-graph-search-queries)
* [Understand Graph Search query results](understand-graph-search-query-results)
* [Create Graph Search query](create-graph-search-query)

The best way to learn how to create Graph Search queries is to try out a few examples. The examples below provide a good guide to creating Graph Search queries. One thing to keep in mind if you try these queries in your own environment, the search results can differ according to your collected data.

This example takes you through building a query with asset nodes. The query looks at the virtual machines (VMs) in your network that are connected to the Internet, attached to a Network Interface, are contained in a subnet, and are part of a virtual private cloud (VPC).

**Step 1: Search for all VMs on your network**

* Select **Compute** → **Virtual Machine**, and click **Search**.

**Graph Search results:** A graph displaying all the virtual machines in your network, where some are connected to the internet, and some are not connected to the internet.

**Step 2: Filter the VMs to only display the ones connected to the Internet**

1. Click **Edit Query**, and define the following **WHERE** statement:
   * **Select field** = **Internet Exposed**
   * Leave the equal (**=**) operator.
   * **Select values** = **true**.
2. Click **Search**.

**Graph Search results:** A graph displaying all the virtual machines in your network that are connected to the Internet.

**Step 3. Display the VM connected to the Internet with an attachment to a Network Interface**

1. Click **Edit Query** and then **+**.
2. Define the **THAT** statement by selecting **Network** → **Network Interface**.
3. Click **Search**.

**Graph Search results:** A graph displaying all the virtual machines in your network that are connected to the Internet with a network interface attached.

**Step 4. Display the VM connected to the Internet with an attachment to a Network Interface and is contained in a subnet**

1. Click **Edit Query** and then **+**.
2. Define the **THAT** statement by selecting **Network** → **Subnet**.
3. Click **Search**.

**Graph Search results:** A graph displaying all the virtual machines in your network that are connected to the internet with a network interface attached, and are contained in a subnet.

**Step 5. Display the VM connected to the Internet with an attachment to a Network Interface, is contained in a subnet, and is part of a VPC**

1. Click **Edit Query** and then **+**.
2. Define the **THAT** statement by selecting **Network** → **VPC**.
3. Click **Search**.

**Graph Search results:** A graph displaying all the virtual machines in your network that are connected to the internet with a network interface attached, are contained in a subnet, and are part of a VPC.
