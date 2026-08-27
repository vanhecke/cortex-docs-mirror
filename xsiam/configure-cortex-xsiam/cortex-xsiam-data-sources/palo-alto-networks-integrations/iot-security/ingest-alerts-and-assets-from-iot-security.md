---
description: Ingest legacy IoT Security data into Cortex XSIAM.
---

# Ingest alerts and assets from IoT Security (Deprecated)

{% hint style="warning" %}
**Important**

Legacy IoT Security data collectors will be discontinued in the near future. We recommend migrating to the new Device Security data collector to ensure uninterrupted data collection. For more information, see [Ingest alerts and assets from Device Security](ingest-alerts-and-assets-from-device-security).
{% endhint %}

The Palo Alto Networks IoT Security (Deprecated) solution discovers unmanaged devices, detects behavioral anomalies, recommends policy based on risk, and automates enforcement without the need for additional sensors or infrastructure. The Cortex XSIAM IoT Security (Deprecated) integration enables you to ingest alerts and device information from your IoT Security (Deprecated) instance.

### Data Collection Behavior

* **Issues and alerts**: Cortex XSIAM displays IoT Security (Deprecated) alerts in the Cortex XSIAM Issues table and groups them into cases. These issues are updated every **15 minutes**. IoT security alerts that were resolved before the integration was established are not added to the table.
* **Assets and device activities**: Device activities detected by IoT Security (Deprecated) are populated in the Cortex XSIAM Assets table. These activities are updated every **5 minutes**.
* **Datasets**: Cortex XSIAM automatically creates two distinct datasets which you can use to initiate XQL Search queries and create Correlation Rules:
  * `panw_iot_security_alerts_raw` (for alerts/issues)
  * `panw_iot_security_devices_raw` (for assets/device activities)

### Prerequisites

Before you configure the IoT Security (Deprecated) data collector, generate an access key and a key ID for the integration.

1. Log in to the **PAN IoT Security** portal and click your user name.
2. Select **Preferences**.
3. In the **User Role & Access** section, **Create** an API Access Key.
4. Download and save the access key and key ID in a secure location.

For more information about the PAN IoT Security API, see [Get Started with the IoT Security API](https://docs.paloaltonetworks.com/iot/iot-security-api-reference/iot-security-api-overview/get-started-with-the-iot-security-api) (Deprecated).

### Configure the IoT Security Collector (Deprecated)

1. Navigate to **Settings** > **Data Sources & Integrations**.
2. On the **Data Sources & Integrations** page, click **+ Add New**, search for **IoT Security** **(Deprecated)**, then hover over it and click **Add**.
3. Specify the following parameters.

* **Customer ID**: Tenant domain part of the FQDN used for your **IoT Security** account. For example, in `yourcorp.iot.paloaltonetworks.com`, the customer ID is `yourcorp`. The customer ID is unique and case sensitive. After you save the integration instance, you can't edit the Customer ID.
* **Access Key** and **Key ID** previously generated for the integration.
* **Integration Scope**: Select at least one of the two values, **Alerts** and **Devices** depending on which information you want to ingest.

4. Click **Test** to validate access, and then click **Enable**.\
   When events start to come in, a green checkmark appears underneath the **IoT Security (Deprecated)** data collector configuration with the data and time that the data was last synced.

### Managing the Collector

You can continue to manage your existing configuration by selecting the integration in your settings to:

* **Edit** the collector settings.
* **Disable** data collection temporarily.
* **Delete** the collector instance entirely.

{% hint style="info" %}
**Note**

If you disable or delete this legacy collector, you will need to follow the migration path to deploy the **Device Security** data collector to maintain continuous asset and alert monitoring.
{% endhint %}
