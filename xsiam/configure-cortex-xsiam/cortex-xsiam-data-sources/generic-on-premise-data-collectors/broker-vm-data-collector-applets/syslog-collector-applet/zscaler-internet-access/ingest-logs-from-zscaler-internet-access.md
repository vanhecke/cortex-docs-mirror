---
description: Ingest Zscaler Internet Access logs into Cortex XSIAM.
---

# Ingest logs from Zscaler Internet Access

If you use Zscaler Internet Access (ZIA) in your network, you can forward your firewall and network logs to Cortex XSIAM for analysis. This enables you to take advantage of Cortex XSIAM anomalous behavior detection and investigation capabilities. Cortex XSIAM can use the firewall and network logs from ZIA as the sole data source, and can also use these firewall and network logs from ZIA in conjunction with Palo Alto Networks firewall and network logs. For additional endpoint context, you can also use Cortex XSIAM to collect and alert on endpoint data.

To integrate your logs, you first need to set up an applet in a broker VM within your network to act as a Syslog Collector. You then configure forwarding on your log devices to send logs to the Syslog collector in a CEF format. To provide seamless log ingestion, Cortex XSIAM automatically maps the fields in your traffic logs to the Cortex XSIAM log format.

When Cortex XSIAM starts to receive logs, the app performs these actions.

* Begins stitching network connection and firewall logs with other logs to form network stories. Cortex XSIAM can also analyze your logs to generate Analytics issues and can apply IOC, BIOC, and Correlation Rule matching. You can also use queries to search your network connection logs.
* Creates a Zscaler Cortex Query Language (XQL) dataset, which enables you to search the logs using XQL Search. The Zscaler XQL datasets are dependent on the ZIA NSS Feed that you've configured for the types of logs you want to collect.
  * Firewall logs: `zscaler_nssfwlog_raw`
  * Web logs: `zscalar_nssweblog_raw`

To ingest logs from Zscaler Internet Access (ZIA):

1. [Activate the Syslog Collector](../activate-syslog-collector).
2. Increase log storage for ZIA logs. For more information, see Manage Your Log Storage.
3. Configure NSS log forwarding in Zscaler Internet Access to the Syslog Collector in a CEF format.
   1. In the Zscaler Internet Access application, select Administration → Nanolog Streaming Service.
   2. In the NSS Feeds tab, Add NSS Feed.
   3.  In the Add NSS Feed screen, configure the fields for the Cortex XSIAM Syslog Collector.

       The steps below differ depending on the type of NSS Feed you are configuring to collect either firewall logs or web logs. For more information on all the configurations available on the screen, see the ZIA documentation:

       * Firewall logs: See [Adding NSS Feeds for Firewall Logs](https://help.zscaler.com/zia/adding-nss-feeds-firewall-logs).
       * Web logs: See [Adding NSS Feeds for Web Logs](https://help.zscaler.com/zia/adding-nss-feeds-web-logs).

       The following image displays the fields required to add an NSS feed.

       [![zscaler\_add\_nss\_feed.png](https://docs-cortex.paloaltonetworks.com/api/khub/maps/5CAbsl8idaK8R43ZLhoTOw/resources/VPKWFTkqCp5g15op6DFhIw-5CAbsl8idaK8R43ZLhoTOw/content?v=5e39c96765569f28\&Ft-Calling-App=ft/turnkey-portal)](https://docs-cortex.paloaltonetworks.com/viewer/attachment/5CAbsl8idaK8R43ZLhoTOw/VPKWFTkqCp5g15op6DFhIw-5CAbsl8idaK8R43ZLhoTOw)

       * NSS Type: Select either NSS for Web (default) to collect web logs or NSS for Firewall to collect firewall logs.
       * SIEM TCP Port: Specify the port that you set when activating the Syslog Collector in Cortex XSIAM. See [Activate the Syslog Collector](../activate-syslog-collector).
       * SIEM IP Address: Specify the IP that you set when activating the Syslog Collector in Cortex XSIAM. See [Activate the Syslog Collector](../activate-syslog-collector).
       * Feed Escape Character: Specify the feed escape character as `=`.
       * Feed Output Type: Select Custom.
       *   Feed Output Format: Specify the output format, which is dependent on the type of logs you are collecting as defined in the NSS Type field:

           | Log type      | Feed output format                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
           | ------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
           | Firewall logs | `%s{mon} %02d{dd} %02d{hh}:%02d{mm}:%02d{ss} zscaler-nss-fw CEF:0\|Zscaler\|NSSFWlog\|5.7\|%s{action}\|%s{rulelabel}\|3\|act=%s{action} suser=%s{login} src=%s{csip} spt=%d{csport} dst=%s{cdip} dpt=%d{cdport} deviceTranslatedAddress=%s{ssip} deviceTranslatedPort=%d{ssport} destinationTranslatedAddress=%s{sdip} destinationTranslatedPort=%d{sdport} sourceTranslatedAddress=%s{tsip} sourceTranslatedPort=%d{tsport} proto=%s{ipproto} tunnelType=%s{ttype} dnat=%s{dnat} stateful=%s{stateful} spriv=%s{location} reason=%s{rulelabel} in=%ld{inbytes} out=%ld{outbytes} rt=%s{mon} %02d{dd} %02d{hh}:%02d{mm}:%02d{ss} deviceDirection=1 cs1=%s{dept} cs1Label=dept cs2=%s{nwsvc} cs2Label=nwService cs3=%s{nwapp} cs3Label=nwApp cs4=%s{aggregate} cs4Label=aggregated cs6=%s{threatname} cs6label=threatname cn1=%d{durationms} cn1Label=durationms cn2=%d{numsessions} cn2Label=numsessions cs5Label=ipCat cs5=%s{ipcat} cat=%s{threatcat} destCountry=%s{destcountry} avgduration=%d{avgduration}`                                                                 |
           | Web logs      | `%s{mon} %02d{dd} %02d{hh}:%02d{mm}:%02d{ss} zscaler-nss CEF:0\|Zscaler\|NSSWeblog\|5.0\|%s{action}\|%s{reason}\|3\|act=%s{action} app=%s{proto} cat=%s{urlcat} dhost=%s{ehost} dst=%s{sip} src=%s{cip} in=%d{respsize} outcome=%s{respcode} out=%d{reqsize} request=%s{eurl} rt=%s{mon} %02d{dd} %d{yy} %02d{hh}:%02d{mm}:%02d{ss} sourceTranslatedAddress=%s{cintip} requestClientApplication=%s{ua} requestMethod=%s{reqmethod} suser=%s{login} spriv=%s{location} externalId=%d{recordid} fileType=%s{filetype} reason=%s{reason} destinationServiceName=%s{appname} cn1=%d{riskscore} cn1Label=riskscore cs1=%s{dept} cs1Label=dept cs2=%s{urlsupercat} cs2Label=urlsupercat cs3=%s{appclass} cs3Label=appclass cs4=%s{malwarecat} cs4Label=malwarecat cs5=%s{threatname} cs5Label=threatname cs6=%s{dlpeng} cs6Label=dlpeng ZscalerNSSWeblogURLClass=%s{urlclass} ZscalerNSSWeblogDLPDictionaries=%s{dlpdict} requestContext=%s{ereferer} contenttype=%s{contenttype} unscannabletype=%s{unscannabletype} deviceowner=%s{deviceowner} devicehostname=%s{devicehostname}\n` |
   4. Click Save.
   5. Click Save and activate the change according to the [Zscaler Internet Access (ZIA) documentation](https://help.zscaler.com/zia/saving-and-activating-changes-admin-portal).

<br>
