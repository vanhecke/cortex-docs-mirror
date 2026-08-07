# Ingest logs from Corelight Zeek

If you use Corelight Zeek sensors for network monitoring, you can still take advantage of Cortex XSIAM investigation and detection capabilities by forwarding your network connection logs to Cortex XSIAM. This enables Cortex XSIAM to examine your network traffic to detect anomalous behavior. Cortex XSIAM can use Corelight Zeek logs as the sole data source, but can also use logs in conjunction with Palo Alto Networks or third-party firewall logs. For additional endpoint context, you can also use Cortex XSIAM to collect and alert on endpoint data.

As soon as Cortex XSIAM starts to receive logs, the app can begin stitching network connection logs with other logs to form network stories. Cortex XSIAM can also analyze your logs to generate Analytics issues, and can apply IOC, BIOC, and Correlation Rule matching. You can also use queries to search your network connection logs.

To integrate your logs, you first need to set up an applet in a Broker VM within your network to act as a Syslog Collector. You then configure forwarding on your Corelight Zeek sensors (using the default Syslog export option of RFC5424 over TCP) to send logs to the Syslog Collector.

1. [Activate the Syslog Collector](../activate-syslog-collector). During activation, you define the Listening Port over which you want the Syslog Collector to receive logs. You must also set TCP as the transport Protocol and Corelight as the Syslog Format.
2. Increase log storage for Corelight Zeek logs. For proper sizing calculations, test the log sizes and log rates produced by your Corelight Zeek Sensors. Then adjust your Cortex XSIAM log storage. For more information, see Manage Your Log Storage within Cortex XSIAM.
3. Forward logs to the Syslog Collector.Cortex XSIAM can receive logs from Corelight Zeek sensors that use the Syslog export option of RFC5424 over TCP.
4. In the Syslog configuration of Corelight Zeek (Sensor → Export), specify the details for your Syslog Collector including the hostname or IP address of the Broker VM and corresponding listening port that you defined during activation of the Syslog Collector, default Syslog format (RFC5424), and any log exclusions or filters.
5. Save your Syslog configuration to apply the configuration to your Corelight Zeek Sensors. For full setup instructions, see the Corelight Zeek documentation.
