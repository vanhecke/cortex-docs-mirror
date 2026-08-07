---
description: Activate the DSPM Fileshare applet on a Broker VM.
---

# Activate DSPM Fileshare

{% hint style="info" %}
The data sources are included in the Cloud Posture Security, Cloud Runtime Security, or Cortex XSIAM Premium license.
{% endhint %}

{% hint style="info" %}
Prerequisites:

* [Set up and configure Broker VM](../../../data-management/broker-vm/set-up-and-configure-broker-vm)
* Know the complete path to the files and folders that you want Cortex XSIAM to monitor.
* Necessary user permissions to access the network shares. For the SMB connection type, you need the username and password.
{% endhint %}

1. Select Settings → Configurations → Data Broker → Broker VMs.
2.  On the Brokers tab, find Broker VM, and in the APPS column, click + ADD. In the list of applets, click DSPM Fileshare.

    The applet list displays only the applets for which you have permissions.
3.  Configure the DSPM Fileshare settings according to the following steps.

    **File Share Connection**

    | Field           | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
    | --------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | Connection Type | <ul><li><strong>NFS (Network File System):</strong> A distributed file system protocol that lets networked computers share files remotely, making them appear as if they're stored locally. Operating at the application layer, it uses Remote Procedure Calls (RPCs) for clients to access a server's files and directories.</li><li><strong>SMB (Server Message Block):</strong> A network file-sharing protocol that provides shared access to resources like files, printers, and serial ports across a network. It enables client applications to remotely interact with files and other assets stored on a server. It is the default file-sharing protocol for Microsoft Windows operating systems. This connection type requires a username and a password.</li></ul> |
    | Path            | Specify the host and path to the folder containing the files that you want Cortex Cloud Data Security to monitor.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
    | Username        | For the SMB connection type only.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
    | Password        | For the SMB connection type only.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
    | Test Connection | Select to validate the connection permissions.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |

    By default, all configured connections are saved.
4.  On the File Share Connection screen, click + Add a Connection.

    For details regarding the connection fields, see the table above under File Share Connection.
5. In the File Share Connection field, replace the text with a name for the new connection.
6. Select a connection type.
7. Provide the path to the shared folder (the host and path).
8. For SMB connections only, provide a username and password.
9. Optionally, do the following:
   1. Turn on the Classification toggle. This enables 2,500 random files to be scanned and classified each time.
   2. In the Scan every list, select the cadence of how often the files are to be scanned. If you want the scans to occur less frequently, choose the Custom option and enter the number of days, weeks, or months that you require.
10. Click Test Connection to ensure the connection works properly.
11. Click Save.

{% hint style="info" %}
You can add multiple connections under a single instance of the DSPM Fileshare applet by returning to the File Share Connection screen and clicking Add Connection. Each new connection can be of either the NFS or SMB connection type.
{% endhint %}

**Other actions**

Once the DSPM Fileshare applet is activated, you can perform the following actions:

* Edit
* **Deactivate:** On the Broker VMs screen, in the ADD column, in the context menu, click Deactivate.
* **Delete:** On the File Share Connection screen, click the Delete icon next to the connection you want to remove.

**Inventory list**

Each new connection that is created correlates to an asset in the inventory. You can see the connections by clicking Inventory → All Assets → Data → Storage Buckets.

<br>
