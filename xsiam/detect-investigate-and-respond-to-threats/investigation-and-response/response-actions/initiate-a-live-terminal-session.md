# Initiate a Live Terminal session

To investigate and respond to security events on endpoints, you can use the Live Terminal to initiate a remote connection to an endpoint. The remote connection is facilitated by the Cortex XDR agent by using a remote procedure call. With the Live Terminal you can manage remote endpoints, and perform investigation and response actions on endpoints. Actions include:

* Navigating and managing files in the file system.
* Managing active processes.
* Running operating system commands and Python commands.
* Downloading files of up to 200 MB and uploading files of up to 40 MB.

Live Terminal is supported for endpoints that meet the following requirements:

<table><thead><tr><th width="162">Operating System</th><th>Requirements</th></tr></thead><tbody><tr><td>Windows</td><td><ul><li>Traps 6.1 or a later release.</li><li>Windows 7 SP1 or a later release.</li><li>Windows update patch for <a href="https://support.microsoft.com/en-us/help/2999226/update-for-universal-c-runtime-in-windows">WinCRT (KB 2999226)</a>. To verify the Hotfixes that are installed on the endpoint, run the <strong><code>systeminfo</code></strong> command from a command prompt.</li><li>Endpoint activity reported within the last 90 minutes (as identified by the <strong>Last Seen</strong> time stamp in the endpoint details).</li></ul></td></tr><tr><td>Mac</td><td><ul><li>Cortex XDR agent 7.0 or a later release.</li><li>macOS 10.12 or a later release.</li><li>Endpoint activity reported within the last 90 minutes (as identified by the <strong>Last Seen</strong> time stamp in the endpoint details).</li></ul></td></tr><tr><td>Linux</td><td><ul><li>Cortex XDR agent 7.0 or a later release.</li><li>Any Linux supported version as listed in <em>Where Can I Install the Cortex XDR Agent?</em> in the Palo Alto Networks Compatibility Matrix.</li><li>Endpoint activity reported within the last 90 minutes (as identified by the <strong>Last Seen</strong> time stamp in the endpoint details).</li></ul></td></tr></tbody></table>

{% hint style="info" %}
You can run PowerShell 5.0 or a later release on Live Terminal of Windows.
{% endhint %}

<details>

<summary>Initiate a Live Terminal session</summary>

1.  You can initiate a Live Terminal session from **Inventory** → **Endpoints** → **All Endpoints** page. Right-click an endpoint and select **Security Operations** → Initiate Live Terminal. It might take the Cortex XDR agent a few minutes to facilitate the connection.

    You can also initiate a Live Terminal as a response action to a security event. If the endpoint is inactive or does not meet the requirements, the option is disabled.
2.  Use the Live Terminal to investigate and take action on the endpoint.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>You can fine-tune the Live Terminal session visibility on the endpoint by adjusting the <strong>User Interface</strong> options in your Agent Settings Profile.</p></div>
3.  When you are finished, **Disconnect** the Live Terminal session.

    After you terminate the Live Terminal session, you can save a session report that logs all actions from the Live Terminal session. The report is available for download as a text file report when you close the live terminal session.



    The following example displays a sample session report:

    ```programlisting
    Live Terminal Session Summary
    Initiated by user username@paloaltonetworks.com on target TrapsClient1 at Jun 27th 2019 14:17:45

    Jun 27th 2019 13:56:13  Live Terminal session has started   [success]
    Jun 27th 2019 14:00:45  Kill process calc.exe (4920)    [success]
    Jun 27th 2019 14:11:46  Live Terminal session end request   [success]
    Jun 27th 2019 14:11:47  Live Terminal session has ended [success]


    No artifacts marked as interesting
    ```

</details>

<details>

<summary>Manage processes from a Live Terminal session</summary>

From the **Live Terminal** you can monitor processes running on the endpoint. The **Task Manager** displays the task attributes, owner, and resources used. If you discover an anomalous process while investigating the cause of a security event, you can take immediate action to terminate the process or the whole process tree, and block processes from running.

1.  From the Live Terminal session, open the **Task Manager** to navigate the active processes on the endpoint.

    You can toggle between a sorted list of processes and the default process tree view (![tree-view.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-95a5ebc0ad109a0c5bbaf152ab566f5465186561%2F5c0b32ee028045968a3299e86224af841efc1478b0b611d92bea24f8c3cffd55.png?alt=media)). You can also export the list of processes and process details to a comma-separated values file. If the process is known as malware, the row displays a red indicator and identifies the file using a malware attribute.
2. Right-click the process to take the following actions:
   * **Terminate process:** Terminate the process or the entire process tree.
   * **Suspend process:** To stop an attack while investigating the cause, you can suspend a process or process tree without killing it entirely.
   * **Resume process:** Resume a suspended process.
   * **Open in VirusTotal:** VirusTotal aggregates known malware from antivirus products and online scan engines. You can scan a file using the VirusTotal scan service to check for false positives or verify suspected malware.
   * **Get WildFire verdict:** WildFire evaluates the file hash signature to compare it against known threats.
   * **Get file hash:** Obtain the SHA256 hash value of the process.
   * **Download Binary:** Download the file binary to your local host for further investigation and analysis. You can download files up to 200MB in size.
   * **Mark as Interesting:** Add an **Interesting** tag to a process so that you can easily locate the process in the session report.
   * **Remove from Interesting:** If no threats are found, you can remove the **Interesting** tag.
   * **Copy Value:** Copy the cell value to your clipboard.
3.  To end the Live Terminal session, select **Disconnect**.

    Choose whether to save the session report including files and tasks marked as interesting. Administrator actions are not saved to the endpoint.

</details>

<details>

<summary>Manage files from a Live Terminal session</summary>

The **File Explorer** enables you to navigate the file system on the remote endpoint and take the following actions:

*   Create, move, delete, or download files, folders, and drives, including connected external drives and devices such as USB drives and CD-ROM.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>Network drives are not supported.</p></div>
* View file attributes, creation and last modified dates, and the file owner.
* Investigate files for malicious content.

#### How to manage files from a Live Terminal

1. From the Live Terminal session, open the **File Explorer**.
2. Double click to navigate through each file directory. To locate a specific file, you can search for any filename rows on the screen from the search bar.
3. From the top right hand menu you can take the following actions:
   * Create a new directory
   * Export the table as a CSV file.
4. Right click a file or folder to see the available actions, including:
   * Rename files and folders.
   * Move and delete files and folders.
   * Download a file.
   * **Open in VirusTotal:** VirusTotal aggregates known malware from antivirus products and online scan engines. You can scan a file using the VirusTotal scan service to check for false positives or verify suspected malware.
   * **Get WildFire verdict:** WildFire evaluates the file hash signature to compare it against known threats.
   * **Get file hash:** Obtain the SHA256 hash value of the file.
   * **Download Binary:** Download the file binary to your local host for further investigation and analysis. You can download files up to 200MB in size.
   * **Mark as Interesting:** Add an **Interesting** tag to a file or directory so that you can easily locate the file in the session report.
   * **Remove from Interesting:** If no threats are found, you can remove the **Interesting** tag.
   * **Copy Value:** Copy the cell value to your clipboard.
5.  Select **Disconnect** to end the live terminal session.

    Choose whether to save the live terminal session report including files and tasks marked as interesting. Administrator actions are not saved to the endpoint.

</details>

<details>

<summary>Run operating system commands from a Live Terminal session</summary>

The Live Terminal provides a command line interface for running operating system commands on a remote endpoint. Each command runs independently and is not persistent.

{% hint style="info" %}
On Windows endpoints, you cannot run GUI-based cmd commands like `winver` or `appwiz.cpl`.
{% endhint %}

#### How to run operating system commands

1. From the Live Terminal session, select **Command Line**.
2.  Type your command on the command line and press **Shift** + **Enter** to execute the command.

    For example, you can manage files or launch batch files. You can enter or paste the commands into the command line interface, or you can upload a script.

    Example 169.

    To chain multiple commands together use `&&`, as shown in the following example:

    ```programlisting
    cd c:\windows\temp\ && <command1> && <command2>
    ```
3.  To end the Live Terminal session, select **Disconnect**.

    Choose whether to save the session report including files and tasks marked as interesting. Administrator actions are not saved to the endpoint.

</details>

<details>

<summary>Run Python commands and scripts from a Live Terminal session</summary>

The Live Terminal provides a Python command line interface for running Python commands and scripts. The Python command interpreter uses Unix command syntax and supports Python 3 with standard Python libraries.

1. From the Live Terminal session, select **Python** to start the python command interpreter on the remote endpoint.
2.  Run Python commands or scripts as required.

    You can enter or paste the commands into the command line interface, or you can upload a script.
3.  When you are finished, **Disconnect** the Live Terminal session.

    Choose whether to save the live terminal session report including files and tasks marked as interesting. Administrator actions are not saved to the endpoint.

</details>

<details>

<summary>Disable Live Terminal sessions</summary>

If you want to prevent Cortex XSIAM from initiating Live Terminal remote sessions on an endpoint that is running the Cortex XDR agent, you can disable this capability during agent installation or through Cortex XSIAM Endpoint Administration. Disabling script execution is irreversible. If you later want to re-enable this capability on the endpoint, you must re-install the Cortex XDR agent.

{% hint style="info" %}
Disabling Live Terminal does not take effect on sessions that are in progress.
{% endhint %}

</details>
