---
description: Configure this scanner for Cortex XSIAM.
---

# Activate Cortex Network Scanner

The Cortex Network Scanner identifies and analyzes devices, services, and vulnerabilities in your internal network. It discovers responsive hosts within specified IP ranges, including on-premises and cloud environments. The scanner supports both non-authenticated and authenticated vulnerability scanning, with authenticated scans providing deeper insights through credential-based access. Scan results are seamlessly integrated into the inventory and vulnerability management views in Cortex XSIAM, providing a centralized view of all discovered assets, vulnerabilities, and issues.

Cortex Network Scanner is installed as an applet on a Broker VM.

{% hint style="info" %}
This feature is included with a Cortex XSIAM Premium license. It is also included with an active Cortex XSIAM NG SIEM and Cortex XSIAM Enterprise license that has the Exposure Management add-on.
{% endhint %}

{% hint style="warning" %}
**Important**

The Cortex Network Scanner applet is not supported for FedRAMP customers.

Cortex Network Scanner does not support high availability (HA) Broker VM configuration.
{% endhint %}

### Prerequisites

* Review the Cortex Network Scanner [deployment recommendations](../../../../../detect-investigate-and-respond-to-threats/exposure-management/cortex-network-scanner#deployment-recommendations) and complete any prerequisites.
* [Set up and configure Broker VM](../../../data-management/broker-vm)

### How to activate Cortex Network Scanner

1. Navigate to Settings → Configurations → Data Broker → Broker VMs.
2. Right click the Broker VM, and select Add App → Network Scanner.
3. After the applet has installed, the scanner should automatically connect to the tenant. If the connection is successful, you’ll see a green dot next to Network Scanner in the Apps column of the Broker VMs table.\
   A red dot indicates that an error occurred and the scanner is not connected.
4. (Optional) Click on the network scanner in the table to display details about the scanner or to deactivate it.
5. Validate the installation. Navigate to Modules → Vulnerability & Exposure Management → Network Scanners → Network Scanners and find your new scanner in the list. The Network Scanners page displays all your deployed and configured scanners, along with additional details about each of them. After setting up a Broker VM and activating Cortex Network Scanner, refer to [Get started with Cortex Network Scanner](../../../../../detect-investigate-and-respond-to-threats/exposure-management/cortex-network-scanner#get-started-with-cortex-network-scanner) for information about adding networks, adding credentials for authenticated scans, and configuring scans.
