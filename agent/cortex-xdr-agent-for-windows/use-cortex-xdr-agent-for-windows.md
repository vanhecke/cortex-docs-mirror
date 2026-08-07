---
description: >-
  Learn how to effectively use the Cortex XDR agent for Windows by the different
  options described in this topic.
---

# Use Cortex XDR Agent for Windows

The Cortex XDR agent installs in the `C:\Program Files (x86)\Palo Alto Networks\Traps` folder. If you enabled access to the console, the agent console is also accessible from the notification area (system tray).

1.  Open the Cortex XDR application.

    The console displays active and inactive features by displaying a ![3.1-active-icon.png](https://517755450-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FuBmMrMEHkk0xAv8axZos%2Fuploads%2FE8VaGXSj6x6aYf8xKM6o%2Ff0e5869fdd8b5facfae33e2e07f39f90e4fecd67a1ca98cbb6421cd577149023.png?alt=media\&token=b0158906-e6cf-4b1c-9c86-058f7c98638d) or ![icon-inactive.png](https://517755450-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FuBmMrMEHkk0xAv8axZos%2Fuploads%2Fg3vQoAM6JbOqyBx6YMVe%2F1bb7905d79103bb3b8fecd5e620f8fd30bdea9c7caca6dffc3d084e485a59ec7.png?alt=media\&token=7aa39f86-d0db-4d96-a934-c656cdcde36f) to the left of the feature type. Select the **Advanced** tab to display additional tabs along the top of the console. The tabs allow you to navigate to pages that display additional details about security events, protected processes, and updates to the security policy. Usually, an end user will not need to run the Cortex XDR console, but the information can be useful when investigating a security-related event. You can choose to hide the tray icon that launches the console, or prevent its launch altogether.

    Use one of the following methods:

    * Browse to `C:\Program Files\Palo Alto Networks\Traps` and run the CyveraConsole.exe application.
    * If you enabled access to Cortex XDR from the notification area, double-click the Cortex XDR icon (![icon-traps.png](https://517755450-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FuBmMrMEHkk0xAv8axZos%2Fuploads%2FWDk0ZbCXGUnrUYlAq4ZB%2F6bb9a19dff582336252b3db79f76756519fd0dac56ff4ccff8e1769f7d198132.png?alt=media\&token=f88c6825-b89e-4352-861e-47cc41a6d9ec)) to launch the agent interface.
2.  View status information about the Cortex XDR agent:

    ![xdr-console-main.png](https://517755450-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FuBmMrMEHkk0xAv8axZos%2Fuploads%2FZjZ30CD36rfEObgl0lnb%2F3752e7e3e57bf9bedc00088ab75201eec020330ebac25c2aad3683deabb73600.png?alt=media\&token=8885b30b-f460-44d0-a193-8e0ffab7ac6a)

    * **Advanced Endpoint Protection**—Displays the overall protection status of the endpoint as enabled if one or more protection features are enabled, or disabled if no protection features are enabled.
      * **Anti-Exploit Protection**—Indicates whether or not exploit prevention rules are active in the endpoint security policy.
      * **Anti-Malware Protection**—Indicates whether restriction or malware protection modules are enabled in the endpoint security policy.
    * **Version**—Displays the Cortex XDR agent version.
    * **Connection**—Displays the connection status and, if connected, includes the server to which the agent is connected.
    * **Last Check-in**—Displays the local time on the endpoint of the last check-in with the server.
3.  Manually connect to the server.

    The Cortex XDR agent communicates with the server at a fixed 5-minute heartbeat interval to send status information and retrieve the latest security policy. The Cortex XDR agent performs this operation transparently at regular intervals so it is not typically necessary to connect to the server manually. If your Connection status is Not Connected, you can try to manually connect. This option is available if you do not want to wait for the automated communication interval to become active.

    To initiate a manual check-in with the server, **Check In Now** from the home page of the Cortex XDR console. If the agent successfully establishes a connection with the server, the Connection status changes to Connected.
4.  Collect Cortex XDR agent logs in a file that can be sent to a support representative for analysis.

    Select **Generate Support File**. Cortex XDR agent aggregates the logs into a compressed file. Save it, and then send the file to your support representative. For remote endpoints, you can also retrieve logs from the Cortex Action Center.
5.  View recent security events that occurred on your endpoint.

    ![xdr-console-windows-events.png](https://517755450-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FuBmMrMEHkk0xAv8axZos%2Fuploads%2FMtjYgsdleCDrxOCktwoQ%2Fc955f0e618f798c4e04b9d2652f81b21aba3635e5726aff0afbe8266f8f2427d.png?alt=media\&token=20aa6139-f9d6-4746-b4fc-5850ef3e32cc)

    1. Click **Advanced**, if necessary, to display additional actions that you can perform from the Cortex XDR console.
    2.  Click **Events**.

        For each event, the Cortex XDR console displays the local **Time** that an event occurred, the name of the **Process** that exhibited malicious behavior, the **Module** that triggered the event, and the mode specified for that type of event (Termination or Notification).
6.  System and custom file scans.

    Cortex XDR malware scans on DLLs, executables, and Office files on Windows endpoints can be triggered from the Cortex XDR server, or manually on the endpoint.

    *   **System Scan**—Scans are initiated from the Cortex XDR sever. You can view the **System Scan** progress in your Cortex XDR agent console. However, you cannot control this scan from the endpoint.

        ![scan-system-scan.png](https://517755450-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FuBmMrMEHkk0xAv8axZos%2Fuploads%2FL45CatX9Om6Zn5dZu2Wa%2Ff3eeef1bdd6203bfe04bdf0b7198a4ac42e107bf567b4394d7b211628cee3f85.png?alt=media\&token=fee17c2f-f6a8-4d5a-85ac-26b11225a02c)
    *   **Custom Scan**—You can initiate file scanning on demand on your Windows endpoints and get an immediate verdict from WildFire, before the file is ever executed on the endpoint. This ability is enabled by default in the Cortex XDR agent Malware profile settings.

        To initiate a custom scan on the endpoint:

        1.  Right-click a file or folder and select **Scan with Cortex XDR**.

            ![scan-file.PNG](https://517755450-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FuBmMrMEHkk0xAv8axZos%2Fuploads%2FjCGtnhSP2gJxrFKHOfz6%2Fca97a2e2dfccbcd2c68af429d743e8fc78259a456f1e739e19a09ae990a111ae.png?alt=media\&token=6b62199b-5993-440d-82a6-9c7179485614)

            <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>You will not see this option if <strong>End-user initiated local scan</strong> is disabled on your endpoint.</p></div>
        2. The Cortex XDR agent console opens and you can see the custom scan in progress and eventually the scan verdict for the file. When a malicious file is detected during the custom scan, the event is reported to Cortex XDR directly and will be visible in the Alerts table as **Detected (Scanned)**. However, it will not appear on the **Events** tab of the Cortex XDR agent console. If the file is unknown to WildFire, the agent applies Local Analysis.

        You can scan up to 100 items simultaneously. An item can be single file or a single folder, regardless of the number of files within the folder (for example, a folder containing more than 100 files is considered one item by Cortex XDR).

        <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>If you scan an unsupported file type, the Cortex XDR agent console will not show a notification for it, and the file will be considered non-malicious.</p></div>
7.  Change the display language for the Cortex XDR console.

    The Cortex XDR console is localized in the following languages: English, German, French, Spanish, Chinese (traditional and simplified), and Japanese.

    1. Click **Advanced**, if necessary, to display additional actions that you can perform from the Cortex XDR console.
    2. Click **Settings**.
    3. Select the display language for Cortex XDR (default is English).
8.  Configure proxy communication.

    You can use a proxy server on the endpoint for all communications to and from the endpoint, including the communication between the Cortex XDR agent and Cortex XDR.

    *   **Define proxy settings explicitly**—You can define a proxy thorough the operating system **Network & Internet** settings, or using the **`netsh`** command from a command prompt. For example:

        **`netsh winhttp set proxy proxy-server="`**_**`<protocol>`**_**`=`**_**`<proxyserver>`**_**`:`**_**`<port>`**_**`"`**

        where:

        * `<protocol>` is either http (unsecure) or https (secure) depending on which protocol you use for proxy communication.
        * `<proxyserver>` is the IP address or FQDN for your proxy server.
        * `<port>` is the port number used for communication with the proxy server.

        <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>You can configure Windows to use an unsecure or secure proxy server or you can specify both.</p></div>

        For example, to use different proxy servers for unsecure and secure proxy communication:

        **`netsh winhttp set proxy proxy-server="http=myproxy:8080;https=sproxy:8181"`**

        You can also specify the same server and same port for both unsecure and secure proxy communication.

        There are three options for this command: You can run the command manually (in a command-prompt as an administrator), you can specify the command in a log-in script, or you can use GPO commands.
    *   **Retrieve proxy settings through a proxy auto-config (PAC) file**—Cortex XDR can retrieve automatic proxy settings configured on your endpoint explicitly, in a group policy, or using WPAD. No additional agent settings are required for this use case.

        <div data-gb-custom-block data-tag="hint" data-style="warning" class="hint hint-warning"><h3>Warning</h3><p>If the proxy settings on your endpoint are configured via WPAD or a user setup script, when you isolate an endpoint from the network you will also lose connectivity with Cortex XDR server.</p></div>
9. Persistent notification from agent that your machine can’t access the network. Only when the issue is resolved, the notification does not appear.
