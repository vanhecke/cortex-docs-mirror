---
description: >-
  Learn how to effectively use the Cortex XDR agent for Mac by the different
  options described in this topic.
---

# Use the Cortex XDR Agent for Mac

1.  Open the Cortex XDR Agent application.

    Use one of the following methods:

    * Browse to the Traps folder in Finder.
    * If you enabled access to the agent console, click the Cortex XDR agent icon in the menu bar, and select **Open Console**.
2. View status information about the Cortex XDR agent:
   * **Version**—Displays the agent version.
   *   **Protection**—Displays the active policies in bold.

       <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>On Mac endpoints running macOS 10.15.4, the <strong>Protection Status</strong> in the agent console indicates the status of both Malware and Exploit modules on the endpoint.</p></div>
   * **Connection**—Displays the connection status and, if connected, includes the server to which the agent is connected.
   * **Last Check-in**—Displays the local time on the endpoint of the last check-in with the server.
3.  Manually connect to the server.

    The Cortex XDR agent communicates with the server at a fixed 5-minute heartbeat interval to send status information and retrieve the latest security policy. The agent performs this operation transparently at regular intervals so it is not typically necessary to connect to the server manually. If your **Connection** status is **Not Connected**, you can manually retry your connection. This option is available if you do not want to wait for the automated communication interval to begin.

    To initiate a manual check-in with the server: On the home page of the Cortex XDR agent console, click **Check In Now**. If the agent successfully establishes a connection with the server, the **Connection** status changes to indicated the service to which the agent is connected.
4.  Collect Cortex XDR agent logs in a file that can be sent to a support representative for analysis.

    Select **Generate Support File**. Cortex XDR agent aggregates the logs into a compressed file. Save it, and then send the file to your support representative. For remote endpoints, you can also retrieve logs from the Action Center.
5.  View recent security events that occurred on your endpoint.

    For each event, the agent console displays the local **Time** an event occurred, the name of the **Process** that exhibited malicious behavior, the **Module** that triggered the event, and the mode specified for the type of event (Termination or Notification).
6.  View protected processes on the Mac endpoint.

    The **Protection** tab of the agent console displays all running processes in which the Cortex XDR agent is injected to prevent malicious execution or behavior. The agent console also indicates the process ID (PID) associated with each process.
7.  Configure proxy communication.

    The agent can communicate with Cortex XDR using the system proxy server that you define for the endpoint. For information on [How to Enter Proxy Settings](https://support.apple.com/guide/mac-help/enter-proxy-server-settings-on-mac-mchlp2591/mac), see the documentation for your Mac operating system version. If you prefer to use an application proxy, [configure a Cortex XDR agent specific proxy](https://github.com/iKettles/palo-alto-networks-gitbook/tree/iain/import/document/preview/258824/README.md#UUID-2bfcc435-2e01-cd45-fca5-ce3478100214).
8. Persistent notification from agent that your machine can’t access the network. Only when the issue is resolved, the notification does not appear.
