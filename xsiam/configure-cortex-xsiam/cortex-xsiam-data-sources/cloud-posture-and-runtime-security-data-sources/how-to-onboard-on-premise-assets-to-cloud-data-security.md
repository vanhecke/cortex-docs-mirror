# How to onboard on-premise assets to Cloud Data Security

## How to onboard on-premise assets to Cortex Cloud Data Security

{% hint style="info" %}
### Notice

The data sources are included in Cloud Posture Security, Cloud Runtime Security, or Cortex XSIAM Premium license.
{% endhint %}

The following applets enable you to monitor and secure assets residing in your on-premise environment:

* **File share protection with the DSPM Fileshare applet**: By activating the **DSPM Fileshare** applet, you extend security coverage to your physical infrastructure, enabling classification for SMB and NFS file shares. This allows you to automatically discover stored content, identify sensitive data, and locate shadow backups, ensuring continuous visibility and consistent governance across hybrid and legacy environments.
* **Database visibility with the DSPM Database applet**: The **DSPM Database** applet provides insights into risks associated with data stored in on-premise databases, PostgreSQL and MySQL instances. Whether you are transitioning to the cloud or maintaining assets on-premise, activating this applet offers a customizable way to manage data security and compliance within a single, unified platform.

To extend the capabilities of Cortex Cloud Data Security to your on-premise infrastructure, you use the Broker VM and a specialized application called an applet. The Broker VM is a virtual machine deployed within your local network that acts as a secure, local collector and gateway. It is essential for unifying and packaging data from your on-premise resources before sending them to Cloud Data Security.

For information about working with Broker VM, see [What is the Broker VM?](../../data-management/broker-vm/what-is-the-broker-vm).

{% hint style="info" %}
### Note

Your data is scanned on the Broker VM itself, and only the metadata and classification results are transmitted from the on-premise environment to Cortex XSIAM.
{% endhint %}

**DSPM Fileshare applet**

The **DSPM Fileshare** applet is an application installed directly onto the Broker VM. The applet’s primary role is to establish and manage connections with your on-premise network file shares, including those using the SMB (Server Message Block) and NFS (Network File Sharing) protocols.

Once configured, this applet continuously:

* Accesses the designated file share paths.
* Ingests the file and folder metadata.
* Classifies files and identifies sensitive information.
* Transmits the collected metadata and results securely through the Broker VM to Cortex XSIAM.

{% hint style="info" %}
### Note

For information about activating the **DSPM Fileshare** applet, see [Activate DSPM Fileshare](../generic-on-premise-data-collectors/broker-vm-data-collector-applets/activate-dspm-fileshare).
{% endhint %}

**DSPM Database applet**

The **DSPM Database** applet is an application installed directly onto the Broker VM. It is the core component responsible for auditing and securing your on-premises PostgreSQL and MySQL databases, providing visibility into the risks associated with your stored data.

Once configured, this applet continuously:

* Accesses your on-premise databases, including those containing regulated or confidential information.
* Identifies data that must be stored in accordance with specific compliance standards.
* Classifies database content to identify sensitive information.
* Transmits the collected insights and risk metadata securely through the Broker VM to Cortex Cloud Data Security.

{% hint style="info" %}
### Note

For information about activating the **DSPM Database** applet, see Activate DSPM Database.
{% endhint %}
