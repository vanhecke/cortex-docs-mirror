---
description: Ingest Device Security alerts and assets into Cortex XSIAM.
---

# Ingest alerts and assets from Device Security

The Palo Alto Networks Device Security solution discovers unmanaged devices, detects behavioral anomalies, recommends policy based on risk, and automates enforcement without the need for additional sensors or infrastructure.

The Cortex XSIAM Device Security integration enables you to ingest alerts and device information from your Device Security instance.

### Data collection behavior

* **Issues and alerts**: Cortex XSIAM displays Device Security alerts in the Cortex XSIAM Issues table and groups them into cases. These issues are updated every **15 minutes**. Device security alerts that were resolved before the integration was established are not added to the table.
* **Assets and device activities**: Device activities detected by Device Security are populated in the Cortex XSIAM Assets table. These activities are updated every **30 seconds**.
* **Datasets**: Cortex XSIAM automatically creates two distinct datasets which you can use to initiate XQL Search queries and create Correlation Rules:
  * `panw_iot_security_alerts_raw` (for alerts/issues)
  * `panw_iot_security_devices_raw` (for assets/device activities)

{% hint style="info" %}
**Note**

Data mapping and schemas for both datasets remain completely identical to the **IoT Security (Deprecated)** collector, ensuring your existing XQL queries and Correlation Rules continue to function seamlessly.
{% endhint %}

### Prerequisites

Before you configure the Device Security data collector, generate a Strata Cloud Manager (SCM) service account Client ID and a Client Secret for the integration.

1. Log in to the Strata Cloud Manager instance you use for Device Security using a role that has write access.
2. Select **Settings** > **Identity & Access** > **Access Management**.
3. Click **Add Identity** to open the **Add New Identity** configuration wizard.
4. Configure the Identity Information. When finished, click **Next**.
   * Identity Type: **Service Account**
   * Service Account Name: Name for the service account
5. Copy the **Client ID** and **Client Secret** from the **Client Credentials** screen and save them in a secure location. When finished, click **Next**.
6. Assign roles to your service account.
   * Apps & Services: **All Apps & Services**
   * Role: **Superuser**
7. Click **Submit** to create the new service account, and then verify that your service account appears in the Access Management table.

For more information about the PAN IoT Security Public API, see [Get Started with the IoT Security Public API](https://pan.dev/iot/api/iot-public-api-new/).

### Configure the Device Security collector

1. Select **Settings** > **Data Sources & Integrations**.
2. On the **Data Sources & Integrations** page, click **+ Add New**, search for the **Device Security** data collector, then hover over it and click **Add**.
3.  Specify the following parameters.

    * **TSG ID**: The unique Tenant Service Group ID for your Strata Cloud Manager instance. You can find this ID at the top of your **SCM Identity & Access** page next to your tenant name.\\

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong><br>The <strong>TSG ID</strong> is unique and case-sensitive. You cannot edit it after saving the integration instance.</p></div>

    * **Client Id** and **Client Secret** for the SCM service account previously generated during the prerequisite steps.
    * **Integration Scope**: Select at least one of the two values, **Alerts** and **Devices**, depending on the information you want to ingest.
4. Click **Test** to validate access, and then click **Enable**.\
   When events start to come in, a green checkmark appears underneath the **Device Security** data collector configuration with the data and time that the data was last synced.

### Managing the Collector

You can continue to manage your existing configuration by selecting the integration in your settings to:

* **Edit** the collector settings.
* **Disable** data collection temporarily.
* **Delete** the collector instance entirely.
