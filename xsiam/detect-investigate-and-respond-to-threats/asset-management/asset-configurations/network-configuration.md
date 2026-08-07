---
description: >-
  Configure your internal network parameters, trusted networks, and external IP
  ranges to help Cortex XSIAM identify and map your network assets.
---

# Network configurations

Network asset visibility is an investigative tool for discovering rogue devices and preventing malicious activity within your environment. By defining your network boundaries, you reduce the amount of manual research required to distinguish between managed and unmanaged assets, identify internal assets, and monitor data communications moving in and out of your network.

**Configure network parameters**

Navigate to **Inventory** → **Assets** → **Configurations** → **Network** to define the boundaries of your organization's network. The configuration page allows you to set:

**Internal IP Address Ranges**

By default, Cortex XSIAM automatically populates private network ranges based on industry-approved reserved ranges. To define custom internal ranges, click **Add New Range**. You can manually enter a name and IP address, range, or CIDR notation, or you can upload a CSV file.

{% hint style="info" %}
### Note

You can add a new range that is fully contained within an existing range, but you cannot add a new range that partially intersects with another.
{% endhint %}

**External IP Address Ranges**

{% hint style="info" %}
### Notice

This feature is included with the Attack Surface Management (ASM) add-on.
{% endhint %}

All external IPv4 and IPv6 address ranges that Cortex XSIAM has discovered through ASM scans and attributed to your organization are listed here, including details such as the first/last IP address, active responsive IPs count, and ASN handles.

**Internal Domain Suffixes**

Internal domain suffixes are DNS domain suffixes that are used within your internal network. Adding your domains here allows Cortex XSIAM to use them for analytics engine profiling. Click **+Add** to enter a new domain suffix to your domains list.

**Trusted Networks**

You can define networks that are considered safe or authorized within your environment. To add a trusted network, click **Add trusted network**. You can manually provide a name, optional description, and the CIDR block or you can upload a CSV file to bulk import multiple networks.

**Configure your network parameters**

Internal IP address ranges and domain names must be defined in order to track and identify assets in the network. This enables Cortex XSIAM to analyze, locate, and display your network assets.

<details>

<summary>Define internal IP address ranges</summary>

1. In Cortex XSIAM, select **Assets** **Network Configuration**.
2.  Define an IP address range.

    By default, Cortex XSIAM creates **Private Network** ranges that specify reserved industry-approved ranges. These ranges can only be renamed.

    To **Add New Range**, select either:

    * **Create New**.
      1.  In the **Create IP Address Range** dialog box, enter the IP address **Name** and **IP Address, Range or CIDR values**.

          <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>You can add a range that is fully contained in an existing range, however, you cannot add a new range that partially intersects with another range.</p></div>
      2. Click **Save**.
    * **Upload from File**
      1. In the **Upload IP Address Range** dialogue box, drag and drop or search for a CSV file listing the IP address ranges. **Download example file** to view the correct format.
      2. Click **Add**.

</details>

<details>

<summary>View external IP address ranges</summary>

{% hint style="info" %}
### Notice

Viewing external IP address ranges requires the Attack Surface Management add-on.
{% endhint %}

An external IP address range is an IPv4 or IPv6 address range that Cortex XSIAM has discovered through ASM scans and attributed to your organization. The complete list of external IP Address Ranges can be viewed on the External IP Address Ranges page, as explained in the following steps. External IP address range information is also available on asset details pages when an external IP address is used to attribute an asset to your organization.

1. In Cortex XSIAM, select **Assets → Network Configuration → IP Address Ranges → External IP Address Ranges**.
2.  Review your external IP address ranges, as needed.

    The IP Address Ranges table displays the following fields:

    * First IP Address: First IP address value of the defined range
    * Last IP Address: Last IP address value of the defined range.
    * IPs Count: Number of IP addresses in the range.
    * Active Responsive IPS count: Number of IP addresses in the range that are currently active and responsive.
    * Business Units: Business units associated with this external IP range.
    * Date Added: The first time that Cortex XSIAM identified this IP Range.
    * Organization Handles: Unique identifiers for the organizations managing the IP range.
3. Display details about an external IP range by selecting a row in the table.

The detailed view is displayed to the right of the table. External IP address range details include registration data, which Cortex XSIAM pulls from public RIR (Regional Internet Registries) databases. Registration data includes network records and organization records.

</details>

<details>

<summary>Define domain names</summary>

1. Select Assets → Network Configuration → **Internal Domain Suffixes**.
2. In the **Internal Domain Suffixes** section, **+Add** the domain suffix you want to include as part of your internal network. For example, **`acme.com`**.
3. Select ![network-mapper-enter.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-1bae499399c7e33bf961f3e38fede70604d4d5d8%2F74e0fe79ef021bc9355f21d7aa7eba932faf3c58e9b1fc3b82819f379ef4fc6e.png?alt=media) to add to the **Domains List**.

</details>

<details>

<summary>IP address ranges fields</summary>

| FIELD                 | DESCRIPTION                                                                                                               |
| --------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| Range Name            | Name of the IP address range defined.                                                                                     |
| First IP Address      | First IP address value of the defined range.                                                                              |
| Last IP Address       | Last IP address value of the defined range.                                                                               |
| Active Assets         | Number of assets within the defined range that have reported Cortex Agent logs or appeared in your Network Firewall Logs. |
| Active Managed Assets | Number of assets within the defined range reported Cortex XSIAM Agent logs.                                               |
| Modified By           | Username of the user who last changed the range.                                                                          |
| Modification Time     | The timestamp shows when this range was last changed.                                                                     |

</details>

<details>

<summary>Define trusted networks</summary>

1. Select Assets → Network Configuration → **Trusted Networks**.
2. Click **Add trusted network**:
   * To manually add a trusted network, select **Create new** and enter the name, description, and CIDR. Click **Update** to add the network.
   * To upload .CSV file, select **Upload from file**. Every row in the file must contain a value for name and CIDR range. You can download a sample file to view the correct format. Click **Upload** to add the networks.

</details>
