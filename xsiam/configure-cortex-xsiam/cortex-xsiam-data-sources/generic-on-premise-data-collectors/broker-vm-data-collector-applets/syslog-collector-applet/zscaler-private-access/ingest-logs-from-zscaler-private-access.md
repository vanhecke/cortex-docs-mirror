# Ingest logs from Zscaler Private Access

If you use Zscaler Private Access (ZPA) in your network as an alternative to VPNs, you can forward your network logs to Cortex XSIAM for analysis. This enables you to take advantage of Cortex XSIAM anomalous behavior detection and investigation capabilities. Cortex XSIAM can use the network logs from ZPA as the sole data source, and can also use these network logs from ZPA in conjunction with Palo Alto Networks network logs.

When Cortex XSIAM starts to receive logs, the following actions are performed:

* Stitching network connection logs with other logs to form network stories. Cortex XSIAM can also analyze your logs to apply IOC, BIOC, and Correlation Rules matching. You can also use queries to search your network connection logs.
* Creates a Zscaler Cortex Query Language (XQL) dataset (`zscaler_zpa_raw`), which enables you to search the logs using XQL Search.

To integrate your logs, you first need to set up an applet in a Broker VM within your network to act as a Syslog Collector. You then configure forwarding on your log devices to send logs to the Syslog collector in a LEEF format. To provide seamless log ingestion, Cortex XSIAM automatically maps the fields in your traffic logs to the Cortex XSIAM log format.

**Prerequisite Step**

Before you can add a log receiver in Zscaler Private Access, as explained in the task below, you must first deploy your App Connectors. For more information, see [App Connector Deployment Guides for Supported Platforms](https://help.zscaler.com/zpa/app-connector-management/app-connector-deployment-guides-supported-platforms).

To ingest logs from Zscaler Private Access (ZPA):

1. [Activate the Syslog Collector](../activate-syslog-collector).
2. Increase log storage for ZPA logs. For more information, see Manage Your Log Storage.
3. Configure ZPA log forwarding in Zscaler Private Access to the Syslog Collector in a LEEF format.
   1. In the Zscaler Private Access application, select Administration → Log Receivers.
   2.  Click Add Log Receiver.

       For more information on configuring the parameters on the screen, see the Zscaler Private Access (ZPA) documentation for [Configuring a Log Receiver](https://help.zscaler.com/zpa/configuring-log-receiver).
   3. In the Add Log Receiver window, configure the following fields on the Log Receiver tab:
      * Name: Specify a name for the log receiver. The name cannot contain special characters, with the exception of periods (.), hyphens (-), and underscores ( \_ ).
      * Description: (Optional) Specify a log receiver description.
      * Domain or IP Address: Specify the fully qualified domain name (FQDN) or IP address for the log receiver that you set when activating the Syslog Collector in Cortex XSIAM. See [Activate Syslog Collector](../activate-syslog-collector).
      * TCP Port: Specify the TCP port number used by the log receiver that you set when activating the Syslog Collector in Cortex XSIAM. See [Activate Syslog Collector](../activate-syslog-collector).
      * TLS Encryption: Toggle to Enabled to encrypt traffic between the log receiver and your Syslog Collector in Cortex XSIAMusing mutually authenticated TLS communication. To use this setting, the log receiver must support TLS communication. For more information, see [About the Log Streaming Service](https://help.zscaler.com/zpa/about-log-streaming-service#tlsencryption).
      * App Connector Groups: (Optional) Select the App Connector groups that can forward logs to the receiver, and click Done. You can search for a specific group, click Select All to apply all groups, or click Clear Selection to remove all selections.
   4. Click Next.
   5. Configure the following fields in the Log Stream tab:
      *   Log Type: Select the log type you want to collect, where only the following logs types are currently supported to collect with your Syslog Collector in Cortex XSIAM:

          You can only configure a ZPA log receiver to collect one type of log with your Syslog Collector in Cortex XSIAM. To configure more that one log type, you'll need to add another log receiver.

          * User Activity: Information on end user requests to applications. For more information, see [User Activity Log Fields](https://help.zscaler.com/zpa/about-user-activity-log-fields).
          * User Status: Information related to an end user's availability and connection to ZPA. For more information, see [User Status Log Fields](https://help.zscaler.com/zpa/about-user-status-log-fields).
          * App Connector Status: Information related to an App Connector's availability and connection to ZPA. For more information, see [About App Connector Status Log Fields](https://help.zscaler.com/zpa/about-connector-status-log-fields).
          * Audit Logs: Session information for all admins accessing the ZPA Admin Portal. For more information, See [About Audit Log Fields](https://help.zscaler.com/zpa/about-audit-log-fields) and [About Audit Logs](https://help.zscaler.com/zpa/about-audit-logs).
      * Log Template: Select a Custom template.
      *   Log Stream Content: Create the log template that you require, according to the Log Type you've selected, using the Zscaler documentation mentioned in previous steps as a reference.

          If you copy and modify the following examples in the table below, validate your log template using an editor, ensuring that there are no additional spaces or line breaks, and then copy and paste it into the Log Stream Content field.

          <table data-header-hidden><thead><tr><th></th><th></th></tr></thead><tbody><tr><td>Log type</td><td>Log template</td></tr><tr><td>User activity</td><td><pre><code>LEEF:1.0|Zscaler|ZPA|4.1|%s{ConnectionStatus}%s{InternalReason}|cat=ZPA User 
          Activity\tdevTime=%s{LogTimestamp:epoch}\tCustomer=%s{Customer}\tSessionID=%s
          {SessionID}\tConnectionID=%s{ConnectionID}\tInternalReason=%s{InternalReason}
          \tConnectionStatus=%s{ConnectionStatus}\tproto=%d{IPProtocol}
          \tDoubleEncryption=%d{DoubleEncryption}\tusrName=%s{Username}
          \tdstPort=%d{ServicePort}\tsrc=%s{ClientPublicIP}\tsrcPreNAT=%s{ClientPrivateIP}
          \tClientLatitude=%f{ClientLatitude}\tClientLongitude=%f{ClientLongitude}
          \tClientCountryCode=%s{ClientCountryCode}\tClientZEN=%s{ClientZEN}
          \tpolicy=%s{Policy}\tConnector=%s{Connector}\tConnectorZEN=%s{ConnectorZEN}
          \tConnectorIP=%s{ConnectorIP}\tConnectorPort=%d{ConnectorPort}
          \tApplicationName=%s{Host}\tApplicationSegment=%s{Application}\tAppGroup=%s{AppGroup}
          \tServer=%s{Server}\tdst=%s{ServerIP}\tServerPort=%d{ServerPort}
          \tPolicyProcessingTime=%d{PolicyProcessingTime}\tServerSetupTime=%d{ServerSetupTime}
          \tTimestampConnectionStart:iso8601=%s{TimestampConnectionStart:iso8601}
          \tTimestampConnectionEnd:iso8601=%s{TimestampConnectionEnd:iso8601}
          \tTimestampCATx:iso8601=%s{TimestampCATx:iso8601}
          \tTimestampCARx:iso8601=%s{TimestampCARx:iso8601}
          \tTimestampAppLearnStart:iso8601=%s{TimestampAppLearnStart:iso8601}
          \tTimestampZENFirstRxClient:iso8601=%s{TimestampZENFirstRxClient:iso8601}
          \tTimestampZENFirstTxClient:iso8601=%s{TimestampZENFirstTxClient:iso8601}
          \tTimestampZENLastRxClient:iso8601=%s{TimestampZENLastRxClient:iso8601}
          \tTimestampZENLastTxClient:iso8601=%s{TimestampZENLastTxClient:iso8601}
          \tTimestampConnectorZENSetupComplete:iso8601=%s{TimestampConnectorZENSetupComplete:iso8601}
          \tTimestampZENFirstRxConnector:iso8601=%s{TimestampZENFirstRxConnector:iso8601}
          \tTimestampZENFirstTxConnector:iso8601=%s{TimestampZENFirstTxConnector:iso8601}
          \tTimestampZENLastRxConnector:iso8601=%s{TimestampZENLastRxConnector:iso8601}
          \tTimestampZENLastTxConnector:iso8601=%s{TimestampZENLastTxConnector:iso8601}
          \tZENTotalBytesRxClient=%d{ZENTotalBytesRxClient}\tZENBytesRxClient=%d{ZENBytesRxClient}
          \tZENTotalBytesTxClient=%d{ZENTotalBytesTxClient}\tZENBytesTxClient=%d{ZENBytesTxClient}
          \tZENTotalBytesRxConnector=%d{ZENTotalBytesRxConnector}
          \tZENBytesRxConnector=%d{ZENBytesRxConnector}
          \tZENTotalBytesTxConnector=%d{ZENTotalBytesTxConnector}
          \tZENBytesTxConnector=%d{ZENBytesTxConnector}\tIdp=%s{Idp}\n
          </code></pre></td></tr><tr><td>User status</td><td><pre><code>LEEF:1.0|Zscaler|ZPA|4.1|%s{SessionStatus}|cat=ZPA User Status
          \tdevTime=%s{LogTimestamp:epoch}\tCustomer=%s{Customer}
          \tusrName=%s{Username}\tSessionID=%s{SessionID}\tSessionStatus=%s{SessionStatus}
          \tVersion=%s{Version}\tZEN=%s{ZEN}\tCertificateCN=%s{CertificateCN}
          \tsrcPreNAT=%s{PrivateIP}\tsrc=%s{PublicIP}\tLatitude=%f{Latitude}
          \tLongitude=%f{Longitude}\tCountryCode=%s{CountryCode}
          \tTimestampAuthentication:iso8601=%s{TimestampAuthentication:iso8601}
          \tTimestampUnAuthentication:iso8601=%s{TimestampUnAuthentication:iso8601}
          \tdstBytes=%d{TotalBytesRx}\tsrcBytes=%d{TotalBytesTx}\tIdp=%s{Idp}
          \tidentHostName=%s{Hostname}\tPlatform=%s{Platform}\tClientType=%s{ClientType}
          \tTrustedNetworks=%s(,){TrustedNetworks}\tTrustedNetworksNames=%s(,){TrustedNetworksNames}
          \tSAMLAttributes=%s{SAMLAttributes}\tPosturesHit=%s(,){PosturesHit}
          \tPosturesMiss=%s(,){PosturesMiss}\tZENLatitude=%f{ZENLatitude}
          \tZENLongitude=%f{ZENLongitude}\tZENCountryCode=%s{ZENCountryCode}\n
          </code></pre></td></tr><tr><td>App connector status</td><td><pre><code>LEEF:1.0|Zscaler|ZPA|4.1|%s{SessionStatus}|cat=Connector Status
          \tdevTime=%s{LogTimestamp:epoch}\tCustomer=%s{Customer}\tSessionID=%s{SessionID}
          \tSessionType=%s{SessionType}\tVersion=%s{Version}\tPlatform=%s{Platform}
          \tZEN=%s{ZEN}\tConnector=%s{Connector}\tConnectorGroup=%s{ConnectorGroup}
          \tsrcPreNAT=%s{PrivateIP}\tsrc=%s{PublicIP}\tLatitude=%f{Latitude}
          \tLongitude=%f{Longitude}\tCountryCode=%s{CountryCode}
          \tTimestampAuthentication:iso8601=%s{TimestampAuthentication:iso8601}
          \tTimestampUnAuthentication:iso8601=%s{TimestampUnAuthentication:iso8601}
          \tCPUUtilization=%d{CPUUtilization}\tMemUtilization=%d{MemUtilization}
          \tServiceCount=%d{ServiceCount}\tInterfaceDefRoute=%s{InterfaceDefRoute}
          \tDefRouteGW=%s{DefRouteGW}\tPrimaryDNSResolver=%s{PrimaryDNSResolver}
          \tHostStartTime=%s{HostStartTime}\tConnectorStartTime=%s{ConnectorStartTime}
          \tNumOfInterfaces=%d{NumOfInterfaces}\tBytesRxInterface=%d{BytesRxInterface}
          \tPacketsRxInterface=%d{PacketsRxInterface}\tErrorsRxInterface=%d{ErrorsRxInterface}
          \tDiscardsRxInterface=%d{DiscardsRxInterface}\tBytesTxInterface=%d{BytesTxInterface}
          \tPacketsTxInterface=%d{PacketsTxInterface}\tErrorsTxInterface=%d{ErrorsTxInterface}
          \tDiscardsTxInterface=%d{DiscardsTxInterface}\tTotalBytesRx=%d{TotalBytesRx}
          \tTotalBytesTx=%d{TotalBytesTx}\n
          </code></pre></td></tr><tr><td>Audit logs</td><td><pre><code>LEEF:1.0|Zscaler|ZPA|4.1|%s{auditOperationType}|cat=ZPA_Audit_Log\t
          devTime=%s{modifiedTime:epoch}\t
          creationTime=%s{creationTime:iso8601}\t
          requestId=%s{requestId}\t
          sessionId=%s{sessionId}\t
          auditOldValue=%s{auditOldValue}\t
          auditNewValue=%s{auditNewValue}\t
          auditOperationType=%s{auditOperationType}\t
          objectType=%s{objectType}\t
          objectName=%s{objectName}\t
          objectId=%d{objectId}\t
          accountName=%d{customerId}\t
          usrName=%s{modifiedByUser}\n
          </code></pre></td></tr></tbody></table>
      * (Optional) You can define a streaming Policy for the log receiver. This entails configuring the SAML Attributes, Application Segments, Segment Groups, Client Types, and Session Statuses. For more information on configuring these settings, see the [Log Stream instructions](https://help.zscaler.com/zpa/configuring-log-receiver#Step2).
   6. Click Next.
   7. In the Review tab, verify your log receiver configuration.
   8. Click Save.
