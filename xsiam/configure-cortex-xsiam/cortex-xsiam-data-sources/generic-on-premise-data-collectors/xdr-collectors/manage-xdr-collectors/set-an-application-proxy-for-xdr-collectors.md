# Set an application proxy for XDR Collectors

You can set an application-specific proxy for a Cortex XDR Collector without affecting the communication of other applications on the collector machine.

In environments where Cortex XDR Collectors communicate with the Cortex XSIAM server through a wide system proxy, you can set an application-specific proxy for the XDR Collector without affecting the communication of other applications on the collector machine. You can set the proxy after installation from the XDR Collectors Administration page in Cortex XSIAM as described in this topic. You can assign up to ten different proxy servers per XDR Collector. The proxy server that the agent uses is selected randomly and with equal probability. If the communication between the XDR Collector and the Cortex XSIAM server through the app-specific proxies fails, the XDR Collector resumes communication through the system-wide proxy defined on the collector machine. If that fails as well, the XDR Collector resumes communication with Cortex XSIAM directly.

1. In Cortex XSIAM, select Settings → Configurations → XDR Collectors → Administration.
2. If needed, filter the list of on-premise collector machines.
3. Set an agent proxy.
   1. Select the row of the on-premises collector machine that you want to set as a proxy.
   2. Right-click the collector machine, and select Set Collector proxy.
   3. You can assign up to ten different proxies per XDR Collector. For each proxy, specify the IP address and port number. After each Proxy Address and Port added, select
   4. Click Set when you’re done.
   5. If necessary later, you can disable the collector proxy by selecting Disable Collector Proxy from the right-click menu.\
      When you disable the proxy configuration, all proxies associated with that XDR Collector are removed. The XDR Collector resumes communication with the Cortex XSIAM server through the wide-system proxy if defined; otherwise, if a wide-system is not defined, the XDR Collector resumes communicating directly with the Cortex XSIAM server. If neither a wide-system proxy nor direct communication exist and you disable the proxy, the XDR Collector disconnects from Cortex XSIAM.
