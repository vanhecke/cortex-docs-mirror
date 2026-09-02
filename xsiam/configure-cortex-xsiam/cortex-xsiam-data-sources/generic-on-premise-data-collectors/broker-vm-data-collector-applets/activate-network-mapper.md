---
description: Configure the Network Mapper applet for Cortex XSIAM.
---

# Activate Network Mapper

{% hint style="info" %}
This feature is included with a Cortex XSIAM Premium license. It is also included with any other Cortex XSIAM license that includes endpoints or Cortex Cloud Runtime Security.
{% endhint %}

{% hint style="warning" %}
### Prerequisite

After you have configured and registered your Broker VM, you can choose to activate the Network Mapper application.
{% endhint %}

The Network Mapper allows you to scan your network to detect and identify unmanaged hosts in your environment according to defined IP address ranges. The Network Mapper configurations are used to locate unmanaged assets that appear in the Assets table. For more information, see [All assets](../../../../detect-investigate-and-respond-to-threats/asset-management/all-assets).

1. Select **Settings** → **Configurations** → **Data Broker** → **Broker VMs**.
2. Do one of the following:
   * On the **Brokers** tab, find the Broker VM, and in the **APPS** column, left-click **Add** → **Network Mapper**.
   * On the **Clusters** tab, find the Broker VM, and in the **APPS** column, left-click **Add** → Network Mapper.
3.  In the **Activate Network Mapper** window, define the following parameters:

    | Field                    | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
    | ------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | Scan Method              | Select the either ICMP echo or TCP SYN scan method to identify your network hosts. When selecting TCP SYN you can enter single ports and ranges together, for example **`80-83, 443`**.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
    | Scan Requests per Second | <p>Define the maximum number of scan requests you want to send on your network per second. By default, the number of scan requests are defined as 1000.</p><p>Each IP address range can receive multiple scan requests based on it's availability.</p>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
    | Scanning Scheduler       | Define when you want to run the network mapper scan. You can select either daily, weekly, or monthly at a specific time.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
    | Scanned Ranges           | <p>Select from the list of exiting IP address ranges to scan. Make sure to <a href="https://docs-cortex.paloaltonetworks.com/viewer/attachment/5CAbsl8idaK8R43ZLhoTOw/VCjuKTJTAMzK0ZPB8J~ndQ-5CAbsl8idaK8R43ZLhoTOw"><img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABcAAAATCAYAAAB7u5a2AAAACXBIWXMAABJ0AAASdAHeZh94AAAAB3RJTUUH5AgMCAMAHpkFNgAAAAd0RVh0QXV0aG9yAKmuzEgAAAAMdEVYdERlc2NyaXB0aW9uABMJISMAAAAKdEVYdENvcHlyaWdodACsD8w6AAAADnRFWHRDcmVhdGlvbiB0aW1lADX3DwkAAAAJdEVYdFNvZnR3YXJlAF1w/zoAAAALdEVYdERpc2NsYWltZXIAt8C0jwAAAAh0RVh0V2FybmluZwDAG+aHAAAAB3RFWHRTb3VyY2UA9f+D6wAAAAh0RVh0Q29tbWVudAD2zJa/AAAABnRFWHRUaXRsZQCo7tInAAAAuUlEQVQ4je3UoQ7CMBSF4b+wDDWFIkheAIFE8S4DjeAVMDgk7wBBYEdCgmcGN1EDamqCMLEVMQltMrKbIDimSW/ytTlJq4wxBqG0pOA/LouvTjDZCOFJCtlTCLfFie+vMFrDWTeMX+6wPIJSMOh+h3u2weIApQHfg9nWjaSPmnheVGtRQpa7cb8NveB9X9n+lvgG4Q4UEE0h6LgP+BRr58M+zMdVNVFSHwbHzZvI7z9/K661FsNFO38BxLk0cB8P23EAAAAASUVORK5CYII=" alt="network-mapper-enter.png"></a> after each selection.</p><p>IP address ranges are displayed according to what you defined as your Network Parameters.</p> |
4.  **Activate** the applet.

    After a successful activation, the **APPS** field displays **Network Mapper** with a green dot indicating a successful connection.
5.  In the **APPS** field, left-click the **Network Mapper** connection to view the following scan and applet metrics:

    **Scan Details**

    | Field               | Description                                                                 |
    | ------------------- | --------------------------------------------------------------------------- |
    | Connectivity Status | Whether the applet is connected to Cortex XSIAM .                           |
    | Scan Status         | State of the scan.                                                          |
    | Scan Start Time     | Timestamp of when the scan started.                                         |
    | Scan Duration       | Period of time in minutes and seconds the scan is running.                  |
    | Scan Progress       | How much of the scan has been completed in percentage and IP address ratio. |
    | Detected Hosts      | Number of hosts identified from within the IP address ranges.               |
    | Scan Rate           | Number of IP addresses scanned per second.                                  |

    **Applet Metrics**

    **Resources**: Displays the amount of CPU, Memory, and Disk space the applet is using.
6.  Manage the Network Mapper.

    After the network mapper has been activated, left-click the **Network Mapper** connection in the **APPS** column to display the Network Mapper settings, and select:

    * **Configure** to redefine the network mapper configurations.
    * **Scan Now** to initiate a scan.
    * **Deactivate** to disable the network mapper.
