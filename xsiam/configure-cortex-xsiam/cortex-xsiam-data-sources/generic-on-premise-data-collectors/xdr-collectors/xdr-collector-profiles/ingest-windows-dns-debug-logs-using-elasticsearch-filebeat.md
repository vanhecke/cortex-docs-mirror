---
description: Ingest Windows DNS logs into Cortex XSIAM.
---

# Ingest Windows DNS debug logs using Elasticsearch Filebeat

Extend Cortex XSIAM visibility into Windows DNS Debug logs using an XDR Collector Windows Filebeat profile.

During configuration of an XDR Collector Windows Filebeat profile, you can configure the profile to enrich network logs with Windows DNS Debug log data. You do this by editing the Elasticsearch Filebeat default configuration file called `filebeat.yml`. In this file, you can define whether the collected data undergoes follow-up processing in the backend for Windows DNS Debug log data. Cortex XSIAM uses Windows DNS Debug logs to enrich network logs. These logs can be searched using XQL Search. You can search the Windows DNS Debug Cortex Query Language dataset (`microsoft_dns_raw`) for raw data, and the normalized stories using the `xdr_data` dataset with the preset called `network_story`.

1. Enable DNS debug logging in your Windows DNS server settings:
   1. In Windows, open DNS Manager, right-click your Windows DNS Server, and select Properties.
   2. Select Debug Logging → Log packets for debugging, and keep the settings that are automatically configured for collecting regular Windows DNS logs in the Packet direction and Packet contents sections.
   3.  (Optional) To collect detailed Windows DNS logs, under the Other options section, select Details.

       Detailed logs are significantly larger because more information is added to the logs.
   4. In the Log file section, for File path and name, enter the file path and log name of your Windows DNS logs, such as `c:\Windows\System32\dns\DNS.log`. This path will also be configured in your `filebeat.yml` file, as explained in a later step. See the examples below.
   5. Click OK.
2. In Cortex XSIAM, go to Settings → Configurations → XDR Collectors → Profiles → +Add Profile → Windows.
3. Select Filebeat, then click Next.
4. Configure the General Information parameters:
   * Profile Name: Enter a unique name to identify the profile. The name can contain only letters, numbers, or spaces, and must be no more than 30 characters. The name that you enter here will be displayed in the list of profiles when you configure a policy.
   * (Optional) Add description here: To provide additional context for the purpose or business reason for your new profile, enter a profile description.
5.  In the Filebeat Configuration File editing box, select the DNS template of your choice (detailed or non-detailed). If you configured detailed collection in the Windows DNS Manager, select the detailed DNS template here. Click Add.

    The template's content is displayed in the editing area.
6.  Configure the `filebeat.yml` file to collect Windows DNS Debug log data.

    1. In the `filebeat.inputs:` section of the file, for `paths:`, configure the file path to your Windows DNS Debug logs. This file path must be the same as the one configured in your Windows DNS server settings, as explained in an earlier step.
    2. Set `vendor` to `“microsoft”` and `product` to `“dns”`.

    The following examples show how to configure the `filebeat.yml` file to normalize Windows DNS Debug logs with an XDR Collector.

    **Example for non-detailed (regular) Windows DNS log collection**

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>To avoid formatting issues in your <code>filebeat.yml</code> file, we recommend that you validate the syntax of the file.</p></div>

    ```
    filebeat.inputs:
    - type: filestream
      enabled: true
      paths:
        -  c:\Windows\System32\dns\DNS.log
      processors:
        - add_fields:
            fields: 
              vendor: "microsoft"
              product: "dns"
    ```

    Example for detailed Windows DNS log collection:

    ```
    filebeat.inputs:
    - type: log
      enabled: true
      paths:
        -  c:\Windows\System32\dns\DNS.log
      multiline.type: pattern
      multiline.pattern: '^(?:\d{1,2}\/){2}\d{4}\s(?:\d{1,2}\:){2}\d\d\s(?:AM|PM)'
      multiline.negate: true
      multiline.match: after
      processors:
        - add_fields:
            fields: 
              vendor: "microsoft"
              product: "dns"
    ```
7.  To finish creating your new profile, click Create.

    Your new profile will be listed under the applicable platform on the XDR Collectors Profiles page.
8. Apply profiles to XDR Collector machine policies by performing one of the following:
   * Right-click a profile and select Create a new policy rule using this profile.
   * Launch the new policy wizard from XDR Collectors → Policies → XDR Collectors Policies.
