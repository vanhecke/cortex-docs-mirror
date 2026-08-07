---
description: >-
  Ingest assets and vulnerabilities into Cortex Exposure Management from Palo
  Alto Networks sensors and third-party applications.
---

# Ingest assets and vulnerabilities from third-party applications

Cortex Exposure Management gathers asset and vulnerability data from Palo Alto Networks sensors and third-party scanners. See [Learn about Exposure Management](exposure-management) for the list of supported data sources.

## **Ingest assets and vulnerabilities using built-in integrations**

Cortex Exposure Management provides built-in integrations for ingesting assets and vulnerabilities from some third-party applications. These integrations only ingest vulnerabilities and assets associated with CVEs. Ingested assets all appear in Cortex XSIAM with the asset type **Generic Device** . Assets and vulnerabilities ingested through integrations are available in the following XQL data sets:

* {vendor}\_{product}\_assets\_raw
* {vendor}\_{product}\_vulnerabilities\_raw

How to configure built-in integrations to ingest assets and vulnerabilities

1. Navigate to the **Settings** → **Data Sources & Integrations**.
2. Search for the integration you want to set up, and click **+ Add New**.
3.  Complete the **Connect** section on the **New Data Source** page with credentials and other connection details.

    For more information about the fields, click the question mark icon.
4.  In the **Collect** section, select the checkbox for **Fetch assets and vulnerabilities**.

    Depending on the vendor, you may be able to select additional types of data to be ingested in this section.
5. Click **Advanced Settings** to specify the fetch settings.
6. Click **Test** to test the configuration. If the test fails, you can **Run Test & Download Debug Log** to debug the error.
7. Click **Connect**. Review the configuration in the summary screen.
8. Click **Finish** to return to the **Data Sources & Integrations** page.

## **Ingest assets and vulnerabilities using the Vulnerability Ingest API**

The Vulnerability Ingest API is a single API endpoint that ingests asset records along with nested vulnerabilities. This API enables you to import vulnerabilities and related assets from your third-party tools directly into your asset inventory and vulnerability management workflows.

Imported assets will be asset type **Generic Device**, and will include vendor and product fields in the asset record. On findings, the **Findings Source** field will indicate **Third Party Scanner**. Data imported with the Vulnerability Ingest API will not be available in an intermediary XQL data set, but will appear in platform datasets such as asset\_inventory and uvm\_findings.

{% hint style="info" %}
### Note

Uploading assets and vulnerabilities with this API requires the **Manage Vulnerabilities** permission, which is under **Vulnerability Management & Import** on the permissions page, and is included in Instance Admin and other admin roles.
{% endhint %}

See the [Vulnerability Management](../vulnerability-management) API documentation for more information.
