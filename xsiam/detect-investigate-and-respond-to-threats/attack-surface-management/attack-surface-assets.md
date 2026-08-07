---
description: >-
  The assets discovered in an attack surface management scan are called External
  Surface assets.
---

# Attack surface assets

The internet-facing assets that were discovered in an attack surface management (ASM) scan and attributed to your organization are available in the inventory on the **Inventory** → **Assets** → **All Assets** → **External Surface** pages. For information about **External Surface** assets, including domains, certificates, services, and websites, see [External Surface assets](../asset-management/asset-classes/external-surface-assets).

To view your external IP address ranges in the inventory, navigate to **Inventory** → **Assets** → **Network Configuration** → **IP Address Ranges** → **External IP Address Ranges**. For information about external IP address ranges, see [Configure your network parameters](../../onboard-cortex-xsiam/deployment-steps/cortex-xsiam-analytics/configure-cortex-xsiam-network-parameters).

## **Upload or remove ASM assets**

In Cortex XSIAM, you can upload assets or remove assets from your inventory through the UI. This feature simplifies inventory management by enabling you to make ad hoc inventory updates yourself as needed. To make large-scale scope changes to your inventory (for example, a merger with a new organization), contact your Customer Success Architect for assistance.

{% hint style="info" %}
### Note

You must have the Instance Administrator role to upload or remove assets.
{% endhint %}

### **Upload assets**

You can add assets to your inventory by submitting an asset upload request, in the form of a CSV file, through the Cortex XSIAM UI. After submitting an asset upload request, the requested assets will appear in the **Asset Uploads/Removal** table with the status **Pending Review**. Cortex XSIAM will respond to your upload request within five days of submission. The status of each asset will be updated in the **Asset Uploads/Removal** table to either **Accepted**, which indicates that the asset has been added to your inventory, or **Rejected**. Rejected assets will have an explanation for the rejection.

Guidelines and restrictions for asset uploads

Before you submit an asset upload request, familiarize yourself with the following guidelines and restrictions:

* You can upload domains (paid-level domains and subdomains) and IPv4 ranges. You can upload a single IPv4 address, but it must be submitted as an IPv4 range asset type. Upload of certificates and IPv6 ranges is not yet supported.
* An asset upload request can include up to 500 assets.
* The asset upload request must follow the CSV formatting requirements described in the [CSV format for upload requests](#UUID-6fb6d2ed-0189-d8e8-5daf-48b48095d30b_section-idm234627043560313) section.
* You cannot upload an asset that was added or rejected in a previous upload request. This will cause an error that must be fixed before you can submit the upload request.
* You cannot upload an asset that was previously removed in an asset removal request. Instead, you can undo an asset removal request, which will result in the asset being added back to your inventory. See [Remove assets](#remove-assets) for details.

{% hint style="info" %}
### Note

If an asset upload request has an invalid CSV or includes one or more invalid assets, the entire request will fail, and none of the assets will be uploaded. If this happens, Cortex XSIAM will display an error message indicating what caused the error, so you can fix the problem and resubmit if you choose.
{% endhint %}

#### How to submit an asset upload request

1. Create and save a CSV file that lists the assets you want to add to your inventory. It is important to format the CSV file correctly, or the upload might fail. Refer to [CSV format for upload requests](#csv-format-for-upload-requests) for an example and details about upload request CSV file formatting.
2. Navigate to **Settings** → **Configurations** → **Asset Management** → **Asset Uploads/Removals**.
3. Click the **Asset Upload/Removal** button and select **Add Asset(s)**.
4.  Drag and drop or browse to your CSV file to upload it to Cortex XSIAM.

    The assets will be added to the **Asset Uploads/Removals** table with the status **Pending**,
5.  Check the status of your asset upload request as needed on the **Asset Uploads/Removals** page.

    Within five days of submitting your request, each asset will be **Accepted** and added to the inventory or **Rejected**. Assets that were rejected will include an explanation in the **Decision Reason** field.

<details>

<summary>CSV format for upload requests</summary>

An asset upload request is a CSV file that lists the assets you want to add along with the asset types and business units they will be assigned to. It is important to format the CSV file to match the following requirements. Incorrect formatting or typos may cause the upload to fail.

Upload request example

This example shows the correct CSV format for an asset upload request, including the supported values for asset types and supported IP range notation. The headers in your CSV must match the headers shown here.

| BusinessUnits | AssetType | Asset                |
| ------------- | --------- | -------------------- |
| BU1, BU2      | Domain    | example.com          |
| BU3           | Domain    | example1.com         |
| BU1           | IP\_Range | 192.0.2.0/32         |
| BU2           | IP\_Range | 192.0.2.0-192.0.2.0  |
| BU1, BU3      | IP\_Range | 192.0.2.0-192.0.2.24 |
| BU2, BU3      | IP\_Range | 192.0.2.0/27         |

Upload request CSV details

The following table provides details about each field that is required in an asset upload request CSV file.

| Field          | Details                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| -------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Business Units | <p>This is the business unit you want to assign to the asset upon upload.</p><p>The header for this field must be written as <strong>BusinessUnits</strong>.</p><p>The business units in your CSV must already exist in Cortex XSIAM and must use the exact same spelling and capitalization.</p><p>If you aren't sure which business units are available in your tenant, follow these steps to download the complete list of business units:</p><p>1. Go to <strong>Settings</strong> → <strong>Configurations</strong> → <strong>Asset Management</strong> → <strong>Asset Uploads/Removals</strong>.</p><p>2. In the upper righthand corner, click the <strong>Asset Upload/Removal</strong> button and select <strong>Asset Upload</strong>.</p><p>3. In the <strong>Add List of Assets</strong> dialog box, click on <strong>Business Unit Directory</strong> to download the list of business units.</p> |
| Asset Type     | <p>The header for this field must be written as <strong>AssetType</strong>.</p><p>Supported values are <strong>Domain</strong> and <strong>IP_Range</strong>.</p>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| Asset          | <p>This is the specific domain or IPv4 range you want to add to your inventory.</p><p>The header for this field must be written as <strong>Asset</strong>.</p><p>IP ranges can be specified using the following types of notation:</p><ul><li>CIDR notation</li><li>&#x3C;First IP address>-&#x3C;Last IP address></li></ul><p>Individual IP addresses can be specified using the following notation:</p><ul><li>192.0.2.0/32</li><li>192.0.2.0-192.0.2.0</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                            |

</details>

<details>

<summary>Rejection reasons for upload requests</summary>

After submitting an upload request, Cortex XSIAM will accept or reject each individual asset. Rejected assets will indicate the reason for the rejection in the **Decision Reason** column of the **Asset Uploads/Removal** table. Rejection reasons include the following:

* The asset you uploaded shows registration information that is attributable to an unrelated organization.
* The asset you uploaded is currently for sale.
* The asset you uploaded is a cloud IP address or the asset you uploaded is a cloud or reserved internal IANA IP address. We do not add these asset types to customer maps.
* The asset you uploaded contains your customer’s content. Cortex XSIAM focuses on corporate infrastructure for our telecommunications, ISPs, and other customer leasing organizations.

</details>

### **Remove assets**

You can remove assets from your inventory by submitting an asset removal request, in the form of a CSV file, through the Cortex XSIAM UI. After you've submitted an asset removal request, the requested assets appear in the **Asset Uploads/Removal** table with the status **Removed**. Within 24 hours of submitting the request, Cortex XSIAM will remove the assets from the inventory and remove associated alerts, incidents, and services,

Guidelines and restrictions for asset removals

Before you submit an asset removal request, familiarize yourself with the following guidelines and restrictions:

* You can remove domains (paid-level domains and subdomains), certificates, and IPv4 ranges. Removal of IPv6 ranges is not supported.
* The asset removal request CSV file must be less than 2 MB.
* You cannot remove an asset that was uploaded in a previous upload request. This will cause an error that must be fixed before you can submit the upload request.
* When you remove a paid-level domain, related subdomains are also removed.
* When you remove an IPv4 range, the individual IPv4 addresses in that range are also removed.
* You can undo a removal request, which will result in the asset being added back to your inventory. See [Undo an asset removal](#undo-an-asset-removal) for more information.
* Removing assets will not result in a reduction to your contract price. Contract pricing will be reevaluated at the time of contract renewal.

{% hint style="info" %}
### Note

If an asset removal request has an incorrectly formatted CSV or includes one or more invalid assets, the entire request will fail, and none of the assets will be removed. If this happens, Cortex XSIAM will display an error message indicating what caused the error, so you can fix the problem and resubmit if you choose.
{% endhint %}

How to submit an asset removal request

An asset removal request is a CSV file that lists all the assets you want to remove from your inventory. It is important that the data and formatting of the CSV file are correct, or the entire request might be rejected.

1. Create and save a CSV file that lists the assets you want to remove from your inventory. Be sure to provide the correct asset information and follow the formatting requirements described in [CSV format for removal requests](#csv-format-for-asset-removal-requests).
2. Navigate to **Settings** → **Configurations** → **Asset Management** → **Asset Uploads/Removals**.
3. Click on the **Asset Upload/Removal** button and select **Remove Asset(s)**.
4.  Drag and drop or browse to your CSV file to upload it to Cortex XSIAM.

    As soon as the file has been successfully uploaded, the assets will appear in the **Asset Uploads/Removals** table with the status **Removed**. Within 24 hours, the assets will be removed from the inventory and related incidents, alerts, and services will also be removed.

<details>

<summary>CSV format for asset removal requests</summary>

An asset removal request is a CSV file that lists the assets you want to remove from the inventory. It is important to format the CSV file to match the following requirements. Incorrect formatting or typos may cause the upload to fail.

Remove request example

This example shows the correct CSV format for an asset removal request, including the supported asset types and IP range notation. The headers in your CSV must match the headers shown here.

| AssetType | Asset               |
| --------- | ------------------- |
| Domain    | example.com         |
| Domain    | example1.com        |
| IP\_Range | 192.0.2.0/32        |
| IP\_Range | 192.0.2.0-192.0.2.0 |
| IP\_Range | 192.0.2.0-192.0.24  |
| IP\_Range | 192.0.2.0/27        |

Remove request CSV details

The following table provides details about each field that is required in an asset removal request CSV file.

| Field      | Details                                                                                                                                                                                                                                                                                                                                                                                              |
| ---------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Asset Type | <p>The header for this field must be written as <strong>AssetType</strong>.</p><p>Supported values are <strong>Domain</strong>, <strong>IP_Range</strong>, and <strong>Certificate</strong>. Use the <strong>IP_Range</strong> asset type to remove individual IP addresses.</p>                                                                                                                     |
| Asset      | <p>This is the specific domain, certificate, or IP range you want to add to your inventory.</p><p>IP ranges can be specified using the following types of notation:</p><ul><li>CIDR notation</li><li>&#x3C;First IP address>-&#x3C;Last IP address></li></ul><p>Individual IP addresses can be specified using the following notation:</p><ul><li>192.0.2.0/32</li><li>192.0.2.0-192.0.2.0</li></ul> |

</details>

<details>

<summary>Undo an asset removal</summary>

There may be situations where you want to add an asset back to your inventory that was previously removed. Cortex XSIAM will not allow you to upload an asset that was previously removed, but you can undo the removal to add that asset back to the inventory.

A common use case for undoing a removal is when an IP range has been removed, but you want to add back an IP address that falls within that range. In that case you can undo the removal of the range, and then submit a new removal request for the ranges before and after the IP address that you want to add back. For example, if you removed IP range 192.0.2.0 -192.0.2.24, but then realized you need to include 192.0.2.10 in your inventory, you would:

1. Undo the removal for IP range 192.0.2.0 -192.0.2.24.
2. Submit a new asset removal request that includes IP ranges 192.0.2.0 - 192.0.2.9 and 192.0.2.11 - 192.0.2.24

How to undo an asset removal

1. Navigate to **Settings** → **Configurations** → **Asset Management** → **Asset Uploads/Removals**.
2. In the **Asset Uploads/Removals** table, find the asset you want to add back to the inventory. An asset must be in the **Removed** state to undo the removal (and add it back to the inventory).
3.  Right-click the row and select **Undo Asset Removal**. Click **Yes** to confirm the removal.

    After confirming the Undo Asset Removal action, the asset will no longer appear in the table.

</details>
