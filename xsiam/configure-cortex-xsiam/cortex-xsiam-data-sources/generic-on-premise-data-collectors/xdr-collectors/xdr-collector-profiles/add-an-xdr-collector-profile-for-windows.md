# Add an XDR Collector profile for Windows

{% hint style="info" %}
Ingestion of log events larger than 5 MB is not supported.
{% endhint %}

### Profile types

XDR Collector profiles define the data that is collected from a Windows collector machine, and define automatic upgrade settings for the XDR collector. For Windows, you can configure a Filebeat profile, a Winlogbeat profile, and a Settings profile.

### Filebeat profile

Use an XDR Collector Windows Filebeat profile to collect file and log data using the Elasticsearch Filebeat default configuration file, called `filebeat.yml`.

#### Supported versions and architectures

Cortex XSIAM supports the following Elasticsearch Filebeat versions with the operating systems listed in the Elasticsearch support matrix that conform with the collector machine operating systems supported by Cortex XSIAM:

* **64-bit XDR Collectors**: Supports Filebeat version 8.15.
* **32-bit XDR Collectors**: Supports Filebeat version 7.17.1

Cortex XSIAM supports the input types and modules available in Elasticsearch Filebeat.

{% hint style="info" %}
**Note**

Fileset validation is enforced. You must enable at least one fileset in the module, because filesets are disabled by default.
{% endhint %}

#### Log format constraints

* Cortex XSIAM collects all logs in either an uncompressed JSON or text format.
* Compressed files, such as the gzip format, are not supported.
* Logs in single line format or multiline format are supported. For more information about handling messages that span multiple lines of text in Elasticsearch Filebeat, see [Manage Multiline Messages](https://www.elastic.co/guide/en/beats/filebeat/current/multiline-examples.html).

#### Related Information

* [Elasticsearch Filebeat Overview Documentation](https://www.elastic.co/guide/en/beats/filebeat/current/filebeat-overview.html#filebeat-overview)
* [Configure Filebeat Inputs in Elasticsearch](https://www.elastic.co/guide/en/beats/filebeat/current/configuration-filebeat-options.html)
* [Configure Filebeat Modules in Elasticsearch](https://www.elastic.co/guide/en/beats/filebeat/current/configuration-filebeat-modules.html)
* [Elasticsearch Support Matrix](https://www.elastic.co/support/matrix)
* [XDR Collector machine requirements and supported operating systems](../xdr-collector-machine-requirements-and-supported-operating-systems)
* Collection of Windows DHCP logs and Windows DNS Debug logs:
  * [Windows DHCP logs](ingest-logs-from-windows-dhcp-using-elasticsearch-filebeat)
  * [Windows DNS Debug logs](ingest-windows-dns-debug-logs-using-elasticsearch-filebeat)

### Winlogbeat Profile

Use an XDR Collector Windows Winlogbeat profile to collect event log data, using the Elasticsearch Winlogbeat default configuration file, called `winlogbeat.yml`.

#### Supported versions and architectures

Cortex XSIAM supports the following Elasticsearch Winlogbeat versions with the Windows versions listed in the Elasticsearch support matrix that conform with the collector machine operating systems supported by Cortex XSIAM:

* **64-bit XDR Collectors**: Supports Winlogbeat version 9.3.2.
* **32-bit XDR Collectors**: Supports Winlogbeat version 7.17.1.

Cortex XSIAM supports the modules available in Elasticsearch Winlogbeat.

#### Data ingestion and normalization

After ingestion, Cortex XSIAM normalizes and saves the Windows event logs collected by the Winlogbeat profile in the dataset `xdr_data`. The normalized logs are also saved in a unified format in `<vendor>_<product>_raw` if the product and vendor are defined, and otherwise, in `microsoft_windows_raw`. You can search the data using Cortex Query Language XQL queries, build correlation rules, and generate dashboards based on the data.

#### Related information

* [Elasticsearch Winlogbeat Overview Documentation](https://www.elastic.co/guide/en/beats/winlogbeat/current/_winlogbeat_overview.html)
* [Winlogbeat Modules in ElasticSearch](https://www.elastic.co/guide/en/beats/winlogbeat/current/winlogbeat-modules.html)
* [Elasticsearch Support Matrix](https://www.elastic.co/support/matrix)
* [XDR Collector machine requirements and supported operating systems](../xdr-collector-machine-requirements-and-supported-operating-systems)
* Collection of Windows DHCP logs and Windows DNS Debug logs:
  * [Windows DHCP logs](ingest-logs-from-windows-dhcp-using-elasticsearch-filebeat)
  * [Windows DNS Debug logs](ingest-windows-dns-debug-logs-using-elasticsearch-filebeat)

### Settings profile

Use an **XDR Collector Settings profile** to configure automatic upgrade settings for XDR Collector releases.

### Policy mapping

To map your XDR Collector profile to a collector machine, you must use an XDR Collector policy. After you have created your profile, map it to a new or existing policy.

### How to configure XDR Collector profiles

#### **Filebeat configuration**

In the Filebeat Configuration File editor, you can define the data collection for your Elasticsearch Filebeat configuration file called `filebeat.yml`.

Cortex XSIAM provides YAML templates for DHCP, DNS, IIS, XDR Collector Logs, NGINX, and any templates added by the content packs installed from the XSIAM Marketplace.

1. In Cortex XSIAM, select Settings → Configurations → XDR Collectors → Profiles → +Add Profile → Windows.
2. Select Filebeat, then click Next.
3. Configure the General Information parameters.
   * Profile Name: Enter a unique name to identify the profile. The name can contain only letters, numbers, or spaces, and must be no more than 30 characters. The name that you enter here will be displayed in the list of profiles when you configure a policy.
   * (Optional) Add description here: To provide additional context for the purpose or business reason for your new profile, enter a profile description.
4. In the Filebeat Configuration File editing box, type or paste the contents of your configuration file, or use a template. To add a template, select one from the list, and click Add.
5.  Cortex XSIAM supports all sections in the `filebeat.yml` configuration file, such as support for Filebeat fields and tags. You can use the "Add fields" processor to identify the product/vendor for the data collected by the XDR Collectors, so that the collected events go through the ingestion flow (Parsing Rules). To configure the product/vendor, ensure that you use the default `fields` attribute (do not use the target attribute), as shown in the following example:

    ```
    processors:
      - add_fields:
          fields:
            vendor: <Vendor>
            product: <Product>
    ```

    For more information about the "Add fields" processor, see [Add\_fields](https://www.elastic.co/guide/en/beats/filebeat/current/add-fields.html).
6.  To finish creating your new profile, click Create.

    Your new profile will be listed under the applicable platform on the XDR Collectors Profiles page.
7. Apply profiles to XDR Collector machine policies by performing one of the following:
   * Right-click a profile, and select Create a new policy rule using this profile.
   * Launch the new policy wizard from XDR Collectors → Policies → XDR Collectors Policies.

#### **Winlogbeat configuration**

In the Winlogbeat Configuration File editor, you can define the data collection for your Elasticsearch Winlogbeat configuration file called `winlogbeat.yml`.

Cortex XSIAM provides YAML templates for Windows Security, and any templates added by the content packs installed from the XSIAM Marketplace. To add a template, select it and click Add.

1. In Cortex XSIAM, select Settings → Configurations → XDR Collectors → Profiles → +Add Profile → Windows.
2. Select Winlogbeat profile, then click Next.
3. Configure the General Information parameters.
   * Profile Name: Enter a unique name to identify the profile. The name can contain only letters, numbers, or spaces, and must be no more than 30 characters. The name that you enter here will be displayed in the list of profiles when you configure a policy.
   * (Optional) Add description here: To provide additional context for the purpose or business reason for your new profile, enter a profile description.
4. In the Winlogbeat Configuration File editing box, type or paste the contents of your configuration file, or use the template. To add the template, click Select template, and then click Windows Security. Click Add.
5.  Cortex XSIAM supports all sections in the `winlogbeat.yml` configuration file, such as support for Winlogbeat fields and tags. You can use the "Add fields" processor to identify the product/vendor for the data collected by the XDR Collectors, so that the collected events go through the ingestion flow (Parsing Rules). To configure the product/vendor, ensure that you use the default `fields` attribute (do not use the `target` attribute), as shown in the following example:

    ```
    processors:
      - add_fields:
          fields:
            vendor: <Vendor>
            product: <Product>
    ```

    For more information about the "Add fields" processor, see [Add\_fields](https://www.elastic.co/guide/en/beats/filebeat/current/add-fields.html).
6.  To finish creating your new profile, click Create.

    Your new profile will be listed under the applicable platform on the XDR Collectors Profiles page.
7. Apply profiles to XDR Collector machine policies by performing one of the following:
   * Right-click a profile, and select Create a new policy rule using this profile.
   * Launch the new policy wizard from XDR Collectors → Policies → XDR Collectors Policies.

#### **Settings configuration**

You can configure automatic upgrades for XDR Collector releases. By default, this is disabled, and the Use Default (Disabled) option is selected. To implement automatic upgrades, follow these steps:

1. In Cortex XSIAM, select Settings → Configurations → XDR Collectors → Profiles → +Add Profile → Windows.
2. Select Settings profile, then click Next.
3. Configure the General Information parameters.
   * Profile Name: Enter a unique name to identify the profile. The name can contain only letters, numbers, or spaces, and must be no more than 30 characters. The name that you enter here will be displayed in the list of profiles when you configure a policy.
   * (Optional) Add description here: To provide additional context for the purpose or business reason for your new profile, enter a profile description.
4. Clear the Use Default (Disabled) checkbox.
5.  For Collector Auto-Upgrade, select Enabled.

    Additional fields are displayed for defining the scope of the automatic upgrade.
6. Configure the scope of automatic upgrades:
   * To ensure the latest XDR Collector release is used, leave the Use Default (Latest collector release) checkbox selected.
   * To configure only a particular scope, perform the following steps:
     1. Clear the Use Default (Latest collector release) checkbox.
     2.  For Auto Upgrade Scope, select one of the following options:

         | Option                                          | More details                                                                                                                                                                                                      |
         | ----------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
         | Latest collector release                        | Configures the scope of the automatic upgrade to whenever a new XDR Collector release is available including maintenance releases and new features.                                                               |
         | Only maintenance release                        | Configures the scope of the automatic upgrade to whenever a new XDR Collector maintenance release is available.                                                                                                   |
         | Only maintenance releases in a specific version | Configures the scope of the automatic upgrade to whenever a new XDR Collector maintenance release is available for a specific version. When this option is selected, you can select the specific Release Version. |
7.  To finish creating your new profile, click Create.

    Your new profile will be listed under the applicable platform on the XDR Collectors Profiles page.
8. Apply profiles to XDR Collector machine policies by performing one of the following:
   * Right-click a profile, and select Create a new policy rule using this profile.
   * Launch the new policy wizard from XDR Collectors → Policies → XDR Collectors Policies.

### **Additional XDR Collector profile management options**

As needed, you can return to the XDR Collectors Profiles page to manage your XDR Collectors profiles. To manage a specific profile, right-click anywhere in an XDR Collector profile row, and select the desired action:

| Option                  | More details                                                                                                                                        |
| ----------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| Edit                    | Lets you edit the XDR Collector profile                                                                                                             |
| Save As New             | Copies the existing profile with its current settings, so that you can make modifications, and save it as a new profile with a unique name          |
| Delete                  | Deletes the XDR Collector profile                                                                                                                   |
| View Collector Policies | Opens a new tab that displays the XDR Collectors Policies page, showing the policies that are currently associated with your XDR Collector profiles |
| Copy text to clipboard  | Copies the text from a specific field in the row of a XDR Collector profile                                                                         |
| Copy entire row         | Copies the text from the entire row of a XDR Collector profile                                                                                      |
