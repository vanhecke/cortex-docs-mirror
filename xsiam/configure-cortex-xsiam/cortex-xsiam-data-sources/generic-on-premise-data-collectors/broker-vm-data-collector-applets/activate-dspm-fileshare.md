---
description: Configure the DSPM Fileshare applet for Cortex XSIAM.
---

# Activate DSPM Fileshare

{% hint style="info" %}
**License**

This feature is included with a Cortex XSIAM Premium license. It is also included with a Cortex XSIAM NG SIEM and Cortex XSIAM Enterprise license that has the Cloud Posture Security or Cloud Runtime Security add-on.
{% endhint %}

The DSPM Fileshare applet is an application installed directly onto the Broker VM. The applet’s primary role is to establish and manage connections with your on-premise network file shares, including those using the SMB (Server Message Block) and NFS (Network File Sharing) protocols.

Once configured, this applet continuously:

* Accesses the designated file share paths.
* Ingests the file and folder metadata.
* Classifies files and identifies sensitive information.
* Transmits the collected metadata and results securely through the Broker VM to Cortex XSIAM.

By activating the DSPM Fileshare applet, you extend security coverage to your physical infrastructure, enabling classification for SMB and NFS file shares. This allows you to automatically discover stored content, identify sensitive data, and locate shadow backups, ensuring continuous visibility and consistent governance across hybrid and legacy environments.

{% hint style="warning" %}
Prerequisite

* [Set up and configure Broker VM](../../../data-management/broker-vm/set-up-and-configure-broker-vm)
* Know the complete path to the files and folders that you want Cortex XSIAM to monitor.
* Necessary user permissions to access the network shares. For the SMB connection type, you need the user name and password.
{% endhint %}

### How to activate the DSPM Fileshare applet

1. Select **Settings** → **Configurations** → **Data Broker** → **Broker VMs**.
2.  Do one of the following:

    * On the **Brokers** tab, find the Broker VM, and in the **APPS** column, left-click **Add** → **DSPM Fileshare**.
    * On the **Clusters** tab, find the Broker VM, and in the **APPS** column, left-click **Add** → **DSPM Fileshare**.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>The applet list displays only the applets for which you have permissions.</p></div>
3.  Configure the DSPM Fileshare settings.

    #### File Share Connection

    | Field                  | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
    | ---------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | File Share Connection  | Replace the text with a name for the new connection.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
    | Connection Type        | <p>* <strong>NFS (Network File System):</strong> A distributed file system protocol that lets networked computers share files remotely, making them appear as if they're stored locally. Operating at the application layer, it uses Remote Procedure Calls (RPCs) for clients to access a server's files and directories.<br><br>* <strong>SMB (Server Message Block):</strong> A network file-sharing protocol that provides shared access to resources like files, printers, and serial ports across a network. It enables client applications to remotely interact with files and other assets stored on a server. It is the default file-sharing protocol for Microsoft Windows operating systems. This connection type requires a username and a password.</p> |
    | Path                   | Specify the host and path to the folder containing the files that you want Cortex XSIAM to monitor.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
    | Username               | For the SMB connection type only.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
    | Password               | For the SMB connection type only.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
    | Classification         | Decide whether to turn on the **Classification** toggle. This enables 2,500 random files to be scanned and classified each time.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
    | Scan every             | Select the cadence of how often the files are to be scanned. If you want the scans to occur less frequently, choose the **Custom** option and enter the amount of days, weeks, or months that you require.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
    | Test Connection        | Select to validate the connection permissions.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>By default, all configured connections are saved.</p></div>
4. (Optional) Click **Add Connection** to define another database connection. You can add multiple connections under one DSPM Fileshare applet instance.
5. Activate the DSPM Fileshare applet.\
   After a successful activation, the **APPS** field displays DSPM Fileshare with a green dot indicating a successful connection.

### Other actions

Once the DSPM Fileshare applet is activated, you can perform the following actions:

* Edit
* **Deactivate:** On the Broker VMs screen, in the ADD column, in the context menu, click Deactivate.
* **Delete:** On the File Share Connection screen, click the Delete icon next to the connection you want to remove.

### Inventory list

Each new connection that is created correlates to an asset in the inventory. You can see the connections by clicking **Inventory** → **All Assets** → **Data** → **Storage Buckets**.
