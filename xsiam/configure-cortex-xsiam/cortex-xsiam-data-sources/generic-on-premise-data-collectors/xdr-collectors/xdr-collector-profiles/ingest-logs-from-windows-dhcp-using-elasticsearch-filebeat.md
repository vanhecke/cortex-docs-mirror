# Ingest logs from Windows DHCP using Elasticsearch Filebeat

You can extend visibility into logs from Windows DHCP, and enrich network logs with Windows DHCP data by using one of the following data collectors with Elasticsearch Filebeat :

* XDR Collector profile (recommended)
* Windows DHCP collector

When Cortex XSIAM begins receiving logs, it automatically creates a Windows DHCP dataset (`microsoft_dhcp_raw`). Cortex XSIAM uses Windows DHCP logs to enrich your network logs with hostnames and MAC addresses. Using XQL Search, you will be able to search for these items in the `microsoft_dhcp_raw` dataset.

{% hint style="info" %}
Although this enrichment is available when configuring a Windows DHCP collector for a cloud data collection integration, we recommend configuring Cortex XSIAM to receive Windows DHCP logs with an XDR Collector Windows Filebeat profile, because it is simpler to set up.
{% endhint %}

Related information

* For more information about configuring the `filebeat.yml` file, see [Elasticsearch Filebeat documentation](https://www.elastic.co/guide/en/beats/filebeat/current/configuring-howto-filebeat.html).

#### **Ingest Windows DHCP Logs with an XDR Collector Profile**

When you add an XDR Collector Windows Filebeat profile using the Elasticsearch Filebeat default configuration file, called `filebeat.yml`, you can define whether the collected data undergoes follow-up processing in the backend for Windows DHCP data. You can further enrich network logs with Windows DHCP data by setting `vendor` to `“microsoft”`, and `product` to `“dhcp”` in the `filebeat.yml` file.

{% hint style="info" %}
Configuration activities include editing the `filebeat.yml` file. To avoid formatting issues in this file, use the template provided by Cortex XSIAM to make your customizations. We recommend that you edit the file inside the user interface, instead of copying it and editing it elsewhere. Validate the syntax of the YML file before you finish creating your profile.
{% endhint %}

Configure Cortex XSIAM to receive logs from Windows DHCP using an XDR Collector Windows Filebeat profile:

1. In Cortex XSIAM, select Settings → Configurations → XDR Collectors → Profiles → +Add Profile → Windows.
2. Select Filebeat, then click Next.
3. Configure the General Information parameters:
   * Profile Name: Enter a unique name to identify the profile. The name can contain only letters, numbers, or spaces, and must be no more than 30 characters. The name that you enter here will be displayed in the list of profiles when you configure a policy.
   * (Optional) Add description here: To provide additional context for the purpose or business reason for your new profile, enter a profile description.
4.  In the Filebeat Configuration File editing box, select the DHCP template, and click Add.

    The template's content is displayed in the editing area.
5. Edit the template text as necessary for your system.
6.  To finish creating your new profile, click Create.

    Your new profile will be listed under the applicable platform on the XDR Collectors Profiles page.
7. Apply profiles to XDR Collector machine policies by performing one of the following:
   * Right-click a profile, and select Create a new policy rule using this profile.
   * Launch the new policy wizard from XDR Collectors → Policies → XDR Collectors Policies.

#### **Ingest Windows DHCP Logs with the Windows DHCP Collector**

To receive Windows DHCP logs with this collector, you must configure data collection from Windows DHCP via Elasticsearch Filebeat. This is configured by setting up a Windows DHCP Collector in Cortex XSIAM and installing and configuring an Elasticsearch Filebeat agent on your Windows DHCP Server. Cortex XSIAM supports using Filebeat up to version 8.0.1 with the Windows DHCP Collector.

Certain settings in the Elasticsearch Filebeat default configuration file called `filebeat.yml` must be populated with values provided when you configure the Data Sources settings in Cortex XSIAM for the Windows DHCP Collector. To help you configure the `filebeat.yml` file correctly, Cortex XSIAM provides an example file that you can download and customize. After you set up collection integration, Cortex XSIAM begins receiving new logs and data from the source.

Windows DHCP logs are stored as CSV (comma-separated values) log files. The logs rotate by days (`DhcpSrvLog-<day>.log`), and each file contains two sections: `Event ID Meaning`, and the events list.

{% hint style="info" %}
Configuration activities include editing the `filebeat.yml` file. To avoid formatting issues in this file, use the example file provided by Cortex XSIAM to make your customizations. Do not copy and paste the code syntax examples provided later in this procedure into your `filebeat.yml` file. Validate the syntax of the YML file before you finish creating your profile.
{% endhint %}

Configure Cortex XSIAM to receive logs from Windows DHCP via Elasticsearch Filebeat with the Windows DHCP collector:

1. In Cortex XSIAM, configure the Windows DHCP Collector.
   1. Select Settings → Data Sources.
   2. Click Add Instance to begin a new configuration.
   3. Search for `Windows DHCP`.
   4.  In the Windows DHCP collector box, click Connect.

       The Enable Windows DHCP Log Collection dialog box is displayed.
   5.  (Optional, but recommended) Download the example `filebeat.yml` file.

       To help you configure your `filebeat.yml` file correctly, Cortex XSIAM provides an example `filebeat.yml` file that you can download and customize. To download this file, click the filebeat.yml link provided in this dialog box.
   6. In the Name field, specify a descriptive name for your log collection configuration.
   7.  Click Save & Generate Token. A key is displayed.

       Click the copy icon next to the key, and save the copy somewhere safe. You will need to provide this key when you set the `api_key` value in the Elasticsearch Output section in the `filebeat.yml` file, as explained in [**Step #2**](#UUID-abfc512b-9ba9-cc81-debd-85578ecf307f_N1731590924979). If you forget to record the key and close the window, you will need to generate a new key and repeat this process.
   8. Click Done to close the dialog box.
   9. Expand the Windows DHCP collector that you just created. Click the Copy api url icon, and save the copy somewhere safe. You will need to provide this URL when you set the `hosts` value in the Elasticsearch Output section in the `filebeat.yml` file, as explained in [**Step #2**](#UUID-abfc512b-9ba9-cc81-debd-85578ecf307f_N1731590924979).
2. On your Windows DHCP Server, configure an Elasticsearch Filebeat agent.
   1. Navigate to the Elasticsearch Filebeat installation directory, and open the `filebeat.yml` file to configure data collection with Cortex XSIAM. We recommend that you use the download example file provided by Cortex XSIAM.
   2. Update the following sections and tags in the `filebeat.yml` file. The following code examples detail the specific sections to make these changes in the file.
      *   **Filebeat inputs**: Define the paths to crawl and fetch. The code in the example below shows how to configure the Filebeat inputs section in the `filebeat.yml` file with these paths configured.

          ```
          # ============================== Filebeat inputs ===============================
          filebeat.inputs:
            # Each - is an input. Most options can be set at the input level, so
            # you can use different inputs for various configurations.
            # Below are the input specific configurations.
            - type: log  
              # Change to true to enable this input configuration.  
              enabled: true  
              # Paths that should be crawled and fetched. Glob based paths.  
              paths:       
                - c:\Windows\System32\dhcp\DhcpSrvLog*.log    
          ```

          <br>
      *   **Elasticsearch Output**: Set the `hosts` and `api_key`, where both of these values were obtained when you configured the Windows DHCP Collector in Cortex XSIAM, as explained in **Step #1**. The following code example shows how to configure the Elasticsearch Output section in the `filebeat.yml` file, and indicates which settings need to be obtained from Cortex XSIAM.

          ```
          # ---------------------------- Elasticsearch Output ----------------------------
          output.elasticsearch:  
            enabled: true  
            # Array of hosts to connect to.    
            hosts: ["OBTAIN THIS URL FROM CORTEX XDR"]  
            # Protocol - either `http` (default) or `https`.  
            protocol: "https"  
            compression_level: 5  
            # Authentication credentials - either API key or username/password. 
            api_key: "OBTAIN THIS KEY FROM CORTEX XDR"
          ```

          <br>
      *   **Processors**: Set the `tokenizer` and add a `drop_event processor` to drop all events that do not start with an event ID. The code in the example below shows how to configure the Processors section in the `filebeat.yml` file and indicates which settings need to be obtained from Cortex XSIAM.

          The `tokenizer` definition is dependent on the Windows server version that you are using, because the log format differs.

          * For platforms earlier than Windows Server 2008, use `"%{id},%{date},%{time},%{description},%{ipAddress},%{hostName},%{macAddress}"`
          * For Windows Server 2008 and 2008 R2, use `"%{id},%{date},%{time},%{description},%{ipAddress},%{hostName},%{macAddress},%{userName},%{transactionID},%{qResult},%{probationTime},%{correlationID}"`
          * For Windows Server 2012 and later, use `"%{id},%{date},%{time},%{description},%{ipAddress},%{hostName},%{macAddress},%{userName},%{transactionID},%{qResult},%{probationTime},%{correlationID},%{dhcid},%{vendorClassHex},%{vendorClassASCII},%{userClassHex},%{userClassASCII},%{relayAgentInformation},%{dnsRegError}"`

          ```
          # ================================= Processors =================================
          processors:  
            - add_host_metadata:      
              when.not.contains.tags: forwarded  
            - drop_event.when.not.regexp.message: "^[0-9]+,.*"  
            - dissect:       
              tokenizer: "%{id},%{date},%{time},%{description},%{ipAddress},%{hostName},%{macAddress},%{userName},%{transactionID},%{qResult},%{probationTime},%{correlationID},%{dhcid},%{vendorClassHex},%{vendorClassASCII},%{userClassHex},%{userClassASCII},%{relayAgentInformation},%{dnsRegError}"  
            - drop_fields:       
              fields: ["message"]  
            - add_locale: ~
            - rename:
                fields:
                  - from: "event.timezone"
                    to: "dissect.timezone"
                ignore_missing: true
                fail_on_error: false
            - add_cloud_metadata: ~  
            - add_docker_metadata: ~  
            - add_kubernetes_metadata: ~
          ```

          <br>
3.  Verify the status of the integration.

    Return to the integrations page in Cortex XSIAM, and view the statistics for the log collection configuration.
4. After Cortex XSIAM begins receiving logs from Windows DHCP via Elasticsearch Filebeat, you can use XQL Search to search for logs in the new `microsoft_dhcp_raw` dataset.

<br>
