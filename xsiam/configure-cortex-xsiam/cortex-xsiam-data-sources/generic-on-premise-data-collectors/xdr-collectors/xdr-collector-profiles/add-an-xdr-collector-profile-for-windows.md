# Add an XDR Collector profile for Windows

{% hint style="info" %}
**Note**

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
* [How to configure XDR Collector profiles](add-an-xdr-collector-profile-for-windows/how-to-configure-xdr-collector-profiles)

### Winlogbeat Profile

Use an XDR Collector Windows Winlogbeat profile to collect event log data, using the Elasticsearch Winlogbeat default configuration file, called `winlogbeat.yml`.

#### Supported versions and architectures

Cortex XSIAM supports the following Elasticsearch Winlogbeat versions with the Windows versions listed in the Elasticsearch support matrix that conform with the collector machine operating systems supported by Cortex XSIAM:

* **64-bit XDR Collectors**: Supports Winlogbeat version 9.3.2.
* **32-bit XDR Collectors**: Supports Winlogbeat version 7.17.1.

Cortex XSIAM supports the modules available in Elasticsearch Winlogbeat.

#### Data ingestion and normalization

After ingestion, Cortex XSIAM normalizes and saves the Windows event logs collected by the Winlogbeat profile in the dataset `xdr_data`. The normalized logs are also saved in a unified format in `<vendor>_<product>_raw` if the product and vendor are defined, and otherwise, in `microsoft_windows_raw`. You can search the data using Cortex Query Language XQL queries, build correlation rules, and generate dashboards based on the data. For more information, see [Query Windows Event Log records](add-an-xdr-collector-profile-for-windows/query-windows-event-log-records).

#### Related information

* [Elasticsearch Winlogbeat Overview Documentation](https://www.elastic.co/guide/en/beats/winlogbeat/current/_winlogbeat_overview.html)
* [Winlogbeat Modules in ElasticSearch](https://www.elastic.co/guide/en/beats/winlogbeat/current/winlogbeat-modules.html)
* [Elasticsearch Support Matrix](https://www.elastic.co/support/matrix)
* [XDR Collector machine requirements and supported operating systems](../xdr-collector-machine-requirements-and-supported-operating-systems)
* Collection of Windows DHCP logs and Windows DNS Debug logs:
  * [Windows DHCP logs](ingest-logs-from-windows-dhcp-using-elasticsearch-filebeat)
  * [Windows DNS Debug logs](ingest-windows-dns-debug-logs-using-elasticsearch-filebeat)
* [How to configure XDR Collector profiles](add-an-xdr-collector-profile-for-windows/how-to-configure-xdr-collector-profiles)

### Settings profile

Use an **XDR Collector Settings profile** to configure automatic upgrade settings for XDR Collector releases.

### Policy mapping

To map your XDR Collector profile to a collector machine, you must use an XDR Collector policy. After you have created your profile, map it to a new or existing policy.

For more information on configuring an XDR Collector profile for a Settings configuration, see [How to configure XDR Collector profiles](add-an-xdr-collector-profile-for-windows/how-to-configure-xdr-collector-profiles).
