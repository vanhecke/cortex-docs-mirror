# Ingest alerts and assets from IoT Security

The Palo Alto Networks IoT Security solution discovers unmanaged devices, detects behavioral anomalies, recommends policy based on risk, and automates enforcement without the need for additional sensors or infrastructure. The Cortex XSIAM IoT Security integration enables you to ingest alerts and device information from your IoT Security instance.

To receive data, configure the settings in Cortex XSIAM for the IoT Security data collector in **Settings** → **Data Sources & Integrations**.

As soon as data collection begins, Cortex XSIAM displays the IoT Security alerts in the Cortex XSIAM Issues table and groups them into cases. The IoT Security issues are updated every 15 minutes. IoT security alerts which were resolved before the integration aren’t added to the Cortex XSIAM table. Cortex XSIAM adds device activities detected by IoT Security into the Cortex XSIAM Assets table. Device activities are updated every five minutes.

Cortex XSIAM automatically creates a new dataset for device activities (`panw_iot_security_devices_raw`) and a new dataset for issues (`panw_iot_security_alerts_raw`), which you can use to initiate XQL Search queries and create Correlation Rules.

Before you configure the **IoT Security Collector**, generate an access key and a key ID for the integration.

1. Log in to the **PAN IoT Security** portal and click your user name.
2. Select **Preferences**.
3. In the **User Role & Access** section, **Create** an API Access Key.
4. Download and save the access key and key ID in a secure location.

For more information about the PAN IoT Secuity API, see [Get Started with the IoT Security API](https://docs.paloaltonetworks.com/iot/iot-security-api-reference/iot-security-api-overview/get-started-with-the-iot-security-api).

Configure the IoT Security alerts and assets collection in Cortex XSIAM.

1. Navigate to **Settings** → **Data Sources & Integrations**.
2. On the **Data Sources & Integrations** page, click **+ Add New**, search for **IoT Security Collector**, then hover over it and click **Add**.
3. Specify the following parameters.
   * **Customer ID**: Tenant domain part of the FQDN used for your **IoT Security** account. For example, in `yourcorp.iot.paloaltonetworks.com`, the customer ID is `yourcorp`. The customer ID is unique and case sensitive. After you save the integration instance, you can't edit the Customer ID.
   * **Access Key** and **Key ID** previously generated for the integration.
   * **Integration Scope**: Select at least one of the two values, **Alerts** and **Devices** depending on which information you want to ingest.
4.  Click **Test** to validate access, and then click **Enable**.

    When events start to come in, a green check mark appears underneath the **IoT Security Collector** configuration with the data and time that the data was last synced.
5.  (Optional) Manage your IOT Security Collector.

    After you enable the IOT Security Collector, you can make additional changes as needed. To modify a configuration, select any of the following options.

    * **Edit** the IOT Security Collector settings.
    * **Disable** the IOT Security Collector.
    * **Delete** the IOT Security Collector.
6. After Cortex XSIAM begins receiving data from IOT Security, you can use the XQL Search to search for logs in the new datasets, `panw_iot_security_devices_raw` for device activities, and `panw_iot_security_alerts_raw` for issues.
