---
description: >-
  To manage Traps functions from the command line on Windows endpoints, use
  Cytool.
---

# Cytool for Windows

Cytool is a command-line interface (CLI) that is integrated into the Cortex XDR agent and enables you to query and manage both basic and advanced functions of the agent. Unless stated otherwise, changes you make using Cytool take effect when the agent receives the next heartbeat communication (every five minutes) from Cortex XDR.

On Windows endpoints, you can access Cytool using a Microsoft command prompt that you run as an administrator. Cytool is located in the `C:\Program Files\Palo Alto Networks\Traps` folder on the endpoint.

The following table displays the Cytool options available on Windows endpoints. Where there is a password required for admin commands, this is the same password as was defined as the Uninstall Password.

{% hint style="info" %}
### Note

Since the Cortex XDR agent 7.6 release for Windows, the cyserver.exe process includes and replaces the previous CyveraService.exe, tlaservice.exe, and twdservice.exe high-privileged processes.
{% endhint %}

<table data-header-hidden><thead><tr><th width="187.8446044921875"></th><th width="599.5780029296875"></th></tr></thead><tbody><tr><td>Command Option</td><td>Description</td></tr><tr><td>adaptive_policy</td><td><p>Adaptive policy agent commands</p><p>Usage <code>cytool adaptive_policy [interval &#x3C;seconds | policy> | collect_stats | recalc | query]</code></p><p>Where:</p><ul><li><code>interval</code> —Sets a recalculation interval override (in seconds), or resets an override. Options are: seconds/policy.</li><li><code>collect_stats</code>—Initiates a collection of internal statistics.</li><li><code>recalc</code>—Triggers a recalculation of the adaptive policy.</li><li><code>query</code>—Querys the current interval and APEX.</li></ul></td></tr><tr><td>cert_enforcement</td><td><p>Perform Certificate enforcement related operations.</p><p>Usage: <code>cytool cert_enforcement &#x3C;operation></code></p><p>Where &#x3C;operation> is one of the following:                                </p><ul><li><code>query</code>—Displays current enforcement status</li><li><code>disable</code>—Forcibly disables enforcement</li><li><code>policy</code>—Sets enforcement by policy</li><li><code>import &#x3C;certificate file path></code>—Imports a proprietary certificate in PEM format as root CA</li><li><code>import clear</code> —Clears all custom root CA certificates.</li></ul></td></tr><tr><td>checkin</td><td><p>Initiate check-in to the server.</p><p>Usage: <code>cytool checkin</code></p><p>To verify the checkin, view the check-in time on the agent console.</p></td></tr><tr><td>clean_and_install</td><td><p>Trigger the XDR Health Helper service to remediate corrupted agent installations or failed upgrades by removing the existing agent and performing a fresh installation.<br>Usage: <code>cytool clean_and_install [-cs "&#x3C;options_json>"]</code> </p><p><br>Where <code>&#x3C;options_json></code> can include one of the following execution modes:</p><ul><li><code>{"ExecutionMode":0}</code> — Removes and reinstalls the current version of the agent.</li><li><code>{"ExecutionMode":1}</code> — Attempts to upgrade to the desired version and stops if the upgrade fails.</li><li><code>{"ExecutionMode":2}</code> — (Default) Attempts to upgrade to the desired version and falls back to reinstalling the current version if the upgrade fails.</li></ul><p>For example:</p><p><code>cytool clean_and_install -cs "{\"ExecutionMode\":0}"</code></p></td></tr><tr><td>edr</td><td><p>Display EDR stats collected on the endpoint.</p><p>Usage: <code>cytool edr stats</code></p></td></tr><tr><td>endpoint_tags</td><td><p>Use Endpoint Tags to identify groups of endpoints.</p><p>Usage: <code>cytool endpoint_tags &#x3C;action></code></p><p>Where action can be:</p><ul><li><code>add</code>—Adds tags to the endpoint tag list.</li><li><code>remove</code>—Removes the given tags from the list of endpoint tags.</li><li><code>list</code>—Displays the available list of endpoint tags.</li></ul><div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>Tags should be passed as one string, separated by commas, and with no spaces.</p></div><p>For example:</p><ul><li><code>cytool endpoint_tags add "tag1[,tage2,...,tagN]"</code></li><li><code>cytool endpoint_tags remove "tag1[,tage2,...,tagN]"</code></li><li><code>cytool endpoint_tags list "tag1[,tage2,...,tagN]"</code></li></ul></td></tr><tr><td>enum</td><td><p>Enumerate protected processes.</p><p>Usage: <code>cytool enum</code></p><div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>If you change the action mode for protected processes in the Exploit Security Profile in Cortex XDR, you must restart the protected processes for the security policy to be enforced on the processes and its forked processes, and only then you will see them on this list.</p></div></td></tr><tr><td>event_collection</td><td><p>Perform event collection (EDR/DSE) operations.</p><p>Usage: <code>cytool event_collection &#x3C;operation></code></p><p>Where &#x3C;operation> can be:</p><ul><li><code>query</code>—Displays the current event collection status.</li><li><code>enable</code>—Start or stop event collection as set by policy.</li><li><code>disable</code>—Forcibly stops event collection.</li><li><code>logstat</code>—Writes internal statistics to the log file.</li></ul></td></tr><tr><td>image</td><td><p>Display information about a PE file (executable or DLL).</p><p>Usage: <code>cytool image &#x3C;filename></code> </p><p></p><p>For example:</p><pre><code><strong>C:\Program Files\Palo Alto Networks\Traps> cytool image json.dll 
</strong>Image Information 
Location: json.dll 
Size: 176.98 KB (181224 bytes) 
File SHA256: a46b8e1ad9a808fb09e7b79bd03b66a611d0c7aa71291c216be555af14d16421 
Architecture: x86-64 
Subsystem: Windows GUI 
PE Size: 156.00 KB (159744 bytes) 
PE SHA256: 8cbca46419bf7260c99aaa3c73a6944e97f5c5b053a8b88e9a17367439b08d7d
</code></pre></td></tr><tr><td>imageprep</td><td><p>Prepare a golden image by submitting files for cloud analysis and generate a threats report.</p><p>Usage: <code>cytool imageprep [scan] [timeout &#x3C;scan timeout>][upload &#x3C;upload timeout>] [path &#x3C;full path>]</code></p><p>where:</p><ul><li><code>&#x3C;scan timeout></code>—The number of hours the scan is permitted to run before reporting an error.</li><li><code>&#x3C;upload timeout></code>—The number of minutes the agent can take to upload unknown files to Cortex XDR before reporting an error.</li><li><code>&#x3C;full path></code>—Path to store the scan report. If no path is specified, Cytool saves the scan report to the local Cytool directory. To save files to this folder, you must first disable service protection using the <code>cytool protect disable</code> command.</li></ul><p></p><p>For example:</p><pre><code><strong>C:\Program Files\Palo Alto Networks\Traps> cytool imageprep scan timeout 4 upload 60 path c:\report 
</strong>Start Time : 17:56:46 
Elapsed Time : 00:04:17 
State : Running 
Scanned Files : 5427 
Suspicious Files : 0 
Failed Files : 9 
Volume Root Path : \\?\C:\ 
Window Usage : 0 236 20000 
Path : ...t\cache2\entries\9B982CE198BF046E6CCF25478920DDFD9E5842E5 

Scan completed successfully 
Complete report can be found at: C:\report\imageprep_2019-03-06_08-59-30.xml
</code></pre></td></tr><tr><td>import</td><td>Import pre-downloaded content or local support exceptions. Used for solving specific problems with a support representative.</td></tr><tr><td>info</td><td><p>Display general Cortex XDR agent information.</p><p>Usage: <code>cytool info [query]</code></p><ul><li>To display the agent version, run the <code>cytool info</code> command without any additional arguments.</li><li>To display additional details about the agent, such as the version of the default policy and the specific build number, add the query argument.</li></ul></td></tr><tr><td>isolate</td><td><p>Release endpoint from network isolation.</p><p>Usage: <code>cytool isolate stop</code></p></td></tr><tr><td>last_checkin</td><td><p>Display the time of the last successful check-in.</p><p>Usage: <code>cytool last_checkin</code></p></td></tr><tr><td>log</td><td><p>Set log level for the desired process/Generate support file archive.</p><p>Usage: <code>cytool log set_level &#x3C;log_level> &#x3C;Components|all></code></p><p>where:</p><p>&#x3C;log_level>—An integer value corresponding to the log level:</p><ul><li>0—Disable logging</li><li>1—Fatal</li><li>2—Critical</li><li>3—Error</li><li>4—Warning</li><li>5—Notice</li><li>6—Information</li><li>7—Debug</li><li>8—Trace</li></ul><p>&#x3C;Components> can be <code>cyserver</code> or <code>all</code> </p><p></p><p>Use <code>cytool log collect</code> to generate a support file archive of all logs in a TGZ file.</p></td></tr><tr><td>payload_execution</td><td><p>Stop or query payload execution status. Relates to Live Terminal and script execution.</p><p>Usage:</p><ul><li><code>cytool payload_execution query</code>—Displays current payload execution status.</li><li><code>cytool payload_execution stop</code>—Stops payload execution.</li></ul></td></tr><tr><td>persist</td><td><p>The Cortex XDR agent stores policy and security event information, such as the list of trusted signers, local verdicts, and one-time actions in local databases on the endpoint. To troubleshoot policy issues and security events, you can use cytool persist operations to import, export, and view information stored in the local database.</p><p>Usage: <code>cytool persist &#x3C;action></code></p><p>Where &#x3C;action> can be:</p><ul><li><code>list</code>—Lists the local databases on the endpoint.</li><li><code>export [&#x3C;database name> | &#x3C;databasepath>]</code>—Exports the database table to a file in the <code>C:\Users\&#x3C;user>\Documents\PaloAltoNetworks\Traps\cytool</code> directory.</li><li><code>import [&#x3C;database name> | &#x3C;databasepath>]</code> &#x3C;file name>—Adds the records in a JSON file to the database.</li><li><code>print &#x3C;database name> | &#x3C;databasepath> [csv]</code>—Prints the records in the database to a CSV file.</li></ul><p>To view a list of all local databases, use the <code>cytool persist list</code> command.</p></td></tr><tr><td>policy</td><td><p>Query or compare the applied policy for a process.</p><p>Usage: <code>cytool policy [query | compare] [process [process]]</code></p><p>where:</p><ul><li><p>Options are:</p><p><code>query</code>—Displays the current applied policy for the process.</p><p><code>compare</code> —Compares the policy against the policy for another process, or against the default policy.</p></li><li><code>&#x3C;process></code>—Either the process name or process ID (PID).</li></ul><div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong>: </p><p>If an image name is specified, a new policy is generated as if the process was created. If a process ID is specified, the system queries the effective policy for the running process.</p></div><p></p><p>For example:</p><p>To query the policy for future executions of notepad.exe:</p><pre><code><strong>C:\Program Files\Palo Alto Networks\Traps> cytool policy query notepad.exe
</strong>Enter supervisor password:

Generic
  Enable         0x00000001
  LongHooks                     0x00000000
  StaticHooks                   0x00000000
  NoCallSplitting               0x00000000
  InitSecurityCookie            0x00000000
  DontInjectThinApp             0x00000001
  LeanInjection                 0x00000000

B01
  Enable                        0x00000000
  BlockAPI                      0x00000000
[...]
</code></pre><p>To compare the policy for future executions of notepad.exe to the default policy:</p><pre><code><strong>C:\Program Files\Palo Alto Networks\Traps> cytool policy compare notepad.exe default
</strong>Enter supervisor password:

Generic
  Enable                            0x00000001                 0x00000001
  LongHooks                         0x00000000                 0x00000000
  StaticHooks                       0x00000000                 0x00000000
  NoCallSplitting                   0x00000000                 0x00000000
  InitSecurityCookie                0x00000000                 0x00000000
  DontInjectThinApp                 0x00000001                 0x00000001
  LeanInjection                     0x00000000                 0x00000000

B01
  Enable                            0x00000000                 0x00000000
  BlockAPI                          0x00000000                 0x00000000
[...]
</code></pre><p><code>cytool policy query 1337</code></p><p>Query the policy of process with ID 1337.</p><p><code>cytool policy compare notepad.exe 1337</code></p><p>Compare notepad's and process ID 1337 policies.</p></td></tr><tr><td>protect</td><td><p>Enable or disable a protection feature.</p><p>Usage: cytool protect <code>&#x3C;Action></code> <code>&#x3C;Feature></code></p><p>where:</p><ul><li><p>&#x3C;Action>—Changes protection for an agent feature. Options are:</p><p><code>enable</code></p><p><code>disable</code></p><p><code>policy</code></p><p><code>query</code></p><p>The query option displays the protection status for each feature.</p></li><li><p>&#x3C;Feature>—Specifies the feature for which you want to change the protection status. Options are:</p><p><code>Process</code>, for agent core processes</p><p><code>Registry</code>, for agent registry keys</p><p><code>File</code>, for agent files</p><p><code>Service</code>, for agent services</p><p><code>Pipe</code>, for protection of agent pipes.</p></li></ul><p></p><p>For example:</p><p>To disable registry protection,</p><p><code>cytool protect disable registry</code></p><p>To enable all protection,</p><p><code>cytool protect enable</code></p><p>To set protection according to policy,</p><p><code>cytool protect policy</code></p><div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>Any protection state change made by Cytool persists until the next reboot and is set according to the policy one hour after reboot.</p></div></td></tr><tr><td>proxy</td><td><p>Set or query cloud-defined proxies for the agent.</p><p>Usage:</p><ul><li><code>cytool proxy query</code>—Displays the current status of cloud-defined proxy settings.</li><li><p><code>cytool proxy set &#x3C;list></code>—Sets cloud-defined proxy settings to the proxies defined in &#x3C;list>.</p><p>For example: <code>cytool proxy set "192.168.50.1:8080,192.168.60.2:808"</code></p></li><li><code>cytool proxy set ""</code>—Disables cloud-defined proxy.</li></ul></td></tr><tr><td>quarantine</td><td><p>View and restore quarantined files.</p><p>Usage:</p><ul><li><code>cytool quarantine list</code>—Lists all quarantined files.</li><li><code>cytool restore &#x3C;ID> [&#x3C;path>]</code>—Restores files to their original location or to a path, if specified, by specifying the file ID.</li></ul></td></tr><tr><td>queryall</td><td>Display a list of imported certificates for troubleshooting purposes.</td></tr><tr><td>reconnect</td><td><p>Try reconnecting to the server if communication has been disabled, or force registration with a new <code>distribution_id</code>.</p><p>Usage:</p><ul><li><code>cytool reconnect</code>—Reconnects the Cortex XDR agent to the management application on the server.</li><li><code>cytool reconnect [force &#x3C;distribution_id]></code></li></ul><div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>The <code>distribution_id</code> must belong to an installation package for the same operating system, and for the same or an earlier agent version than the one currently installed.</p></div></td></tr><tr><td>runtime</td><td><p></p><p>Stop or start product components.</p><p>Usage: <code>cytool runtime &#x3C;Action> &#x3C;Component></code></p><p>where:</p><ul><li><p>&#x3C;Action>—Changes startup runtime action for an agent component.</p><p>Options are: <code>start</code>, <code>stop</code>, and <code>query</code>. The query option displays the startup status for each component.</p></li><li><p>&#x3C;Component>—Specifies the component for which you want to change the runtime action, or you can specify all components by not including any in this command.</p><p>To change the runtime action for a subset of components, list them with spaces separating each component.</p><p>Options are: <code>cyverak</code>, <code>cyvrmtgn</code>, <code>cyvrfsfd</code>, and <code>cyserver</code>.</p></li></ul><p>For example:</p><pre><code><strong>C:\Program Files\Palo Alto Networks\Traps>cytool runtime stop cyserver cyverak
</strong>Enter supervisor password:

Service         State
cyverak         Stopped
cyvrmtgn        Running
cyvrfsfd        Running
cyserver        Stopped
</code></pre></td></tr><tr><td>scan</td><td><p>Scan operations.</p><p>Usage: <code>cytool scan &#x3C;Action></code></p><p>Where &#x3C;action>:</p><ul><li><code>start</code>—Scans the endpoint for malware.</li><li><code>stop</code>—Stops a scan.</li><li><code>query</code>—Displays the progress if a system scan is active.</li><li><code>last_scan_time</code>—Displays the last time a scan was done.</li></ul><p>Example:</p><pre><code><strong>C:\Program Files\Palo Alto Networks\Traps> cytool scan start
</strong>Enter supervisor password:

The operation completed successfully.

<strong>C:\Program Files\Palo Alto Networks\Traps> cytool scan query 
</strong>Enter supervisor password:

Start Time       : 9:09:0648
Elapsed Time     : 00:00:51
State            : Running
Scanned Files    : 3944
Suspicious Files : 0
Failed Files     : 1\?\C:\
Volume Root Path : \\?\C:\                                      8                                            20000
Window Usage     : 0                                           14                                            20000
Path             : ...
</code></pre></td></tr></tbody></table>
