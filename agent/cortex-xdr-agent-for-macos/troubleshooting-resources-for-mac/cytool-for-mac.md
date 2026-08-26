---
description: >-
  In addition to being available for Windows and Linux endpoints, Cytool is also
  available for Mac endpoints.
---

# Cytool for Mac

Cytool is a command-line interface that is integrated into the Cortex XDR agent that enables you to query and manage both basic and advanced functions of the agent. Unless stated otherwise, changes you make using Cytool take effect when the agent receives the next heartbeat communication (every five minutes) from Cortex XDR.

On Mac endpoints, access Cytool as a super user using a terminal. Cytool is located in the `/Library/Application Support/PaloAltoNetworks/Traps/bin` directory on the endpoint.

The following table displays the Cytool options available on Mac endpoints. For the Cytool admin commands that require a password, the password is the same as is defined as the Uninstall password.

{% hint style="info" %}
### Note

Since Cortex XDR agent 7.6, the `pmd` process includes and replaces the `trapsd` process.
{% endhint %}

<table data-header-hidden><thead><tr><th width="212.9400634765625"></th><th width="535.0599365234375"></th></tr></thead><tbody><tr><td>Command Option</td><td>Description</td></tr><tr><td>cert_enforcement</td><td><p>Perform Certificate enforcement related operations.</p><p>Usage: <code>cytool cert_enforcement &#x3C;operation></code></p><p>Where &#x3C;operation> is one of the following:                                </p><ul><li><code>query</code> —Displays current enforcement status</li><li><code>disable</code> —Forcibly disables enforcement</li><li><code>policy</code>—Sets enforcement by policy</li><li><code>import &#x3C;certificate file path></code>—Imports a proprietary certificate in PEM format as root CA</li><li><code>import clear</code>—Clears all custom root CA certificates.</li></ul></td></tr><tr><td>checkin</td><td><p>Initiate check-in to the server.</p><p>Usage: <code>sudo ./cytool checkin</code></p><p>To verify the checkin, view the check-in time on the Cortex XDR agent console.</p></td></tr><tr><td>connectivity_test</td><td><p>Perform a connectivity test to Cortex XDR servers.</p><p>Usage: <code>cytool connectivity_test [request_count]</code></p></td></tr><tr><td>dump</td><td><p></p><p>Enable or disable dump generation or restore policy settings.</p><pre><code><strong>Traps-Mac:bin Traps$ sudo ./cytool dump enable
</strong><strong>Traps-Mac:bin Traps$ sudo ./cytool dump disable
</strong><strong>Traps-Mac:bin Traps$ sudo ./cytool dump restore
</strong></code></pre></td></tr><tr><td>endpoint_tags</td><td><p>Use Endpoint Tags to identify groups of endpoints.</p><p>Usage: <code>sudo ./cytool endpoint_tags </code><em><code>&#x3C;action></code></em></p><p>where <em><code>&#x3C;action></code></em> can be:</p><ul><li><code>add</code>—Adds tags to the endpoint tags.</li><li><code>remove</code>—Removes the given tags from the list of endpoint tags.</li><li><code>list</code>—Displays the available endpoint tags.</li></ul><div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>Tags should be passed as one string separated by comas.</p></div><p>For example:</p><ul><li><code>Traps-Mac:bin Traps$   sudo ./cytool endpoint_tags add "tag1[,tag2,...,tagN]"</code></li><li><code>Traps-Mac:bin Traps$   sudo ./cytool endpoint_tags remove "tag1[,tag2,...,tagN]"</code></li><li><code>Traps-Mac:bin Traps$   sudo ./cytool endpoint_tags list</code></li></ul></td></tr><tr><td>enum</td><td><p>Enumerate protected processes.</p><p>Usage: <code>sudo ./cytool enum</code></p><p></p><p>For example:</p><pre><code><strong>Traps-Mac:bin Traps$ sudo ./cytool enum
</strong>List of protected processes:
        Process name          Process ID             User
              Photos                2047            User1
                Mail                2099            User2
</code></pre><p><strong>Note</strong></p><div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>If you change the action mode for protected processes in the Exploit Security Profile in Cortex XDR, you must restart the protected processes for the security policy to be enforced on the processes and its forked processes, and only then you will see them on this list.</p></div></td></tr><tr><td>-h --help</td><td><p></p><pre><code>Traps-Mac:bin Traps$ sudo ./cytool

Usage: cytool&#x3C;options>
cytool - Support tool

Options:
-h --help                                           Display help information.
enum                                                List processes protected by Cortex XDR.
startup query                                       List startup status for Cortex XDR agent and daemons.
startup &#x3C;enable | disable> &#x3C;process_name | all>     Enable/Disable Cortex XDR agent and daemons after reboot.
runtime query                                       List runtime status for agent, daemons, and kernel extensions.
runtime &#x3C;start | stop> &#x3C;process_name | all>         Start/Stop Cortex XDR agent, daemons, and kernel extensions immediately.
persist list                                        Display persistent databases.
persist export &#x3C;db_name | db_path>                  Export databases in JSON format.
persist import &#x3C;db_name | db_path> &#x3C;file_name>      Import data into the database from the given JSON file.
persist print &#x3C;db_name | db_path> [csv]             Print database to the command prompt.
log &#x3C;log_level> &#x3C;process_name | all>                Set log level for the desired process.
log collect                                         Generate support file archive.
wakeup                                              Wake up from OS incompatibility state.
dump &#x3C;enable | disable | restore>                   Enable/Disable dump generation or restore policy settings.
checkin                                             Update Cortex XDR from server.
opswat &#x3C;installed | running | protected | version>  Check Cortex XDR Agent status and version. 
</code></pre></td></tr><tr><td>import suex</td><td>Import pre-downloaded content or local support exceptions. Used for solving specific problems with a support representative.</td></tr><tr><td>isolate</td><td><p>Usage: <code>cytool isolate stop</code></p><p>Release endpoint from network isolation.</p></td></tr><tr><td>log</td><td><p><code>Log set_level</code> - Set the log level for the desired process.</p><p>Usage: <code>sudo ./cytool log set_level &#x3C;log_level> &#x3C;components></code></p><p>where:</p><ul><li><p>&#x3C;log_level> is an integer value corresponding to the log level:</p><ul><li>0—Disable logging</li><li>1—Fatal</li><li>2—Critical</li><li>3—Error</li><li>4—Warning</li><li>5—Notice</li><li>6—Information</li><li>7—Debug</li><li>8—Trace</li></ul></li><li>&#x3C;components> is <code>all</code> or one or more of the following agent component: <code>authorized</code>, <code>pmd</code>, <code>cortex xdr</code>, <code>kproc-ctrl</code>.</li></ul><p>For example:</p><pre><code>Traps-Mac:bin Traps$ sudo ./cytool log set_level 2 all
</code></pre><p></p><p><code>log collect</code> </p><p>Use the <code>sudo ./cytool log collect</code> command to generate a support file archive of all logs in a TGZ file. On Mac endpoints running OS X 10.10 and OSX 10.11, Cytool outputs the logs to the <code>/var/log/traps</code> directory. On Mac endpoints running macOS 10.12 and later, you can view logs from the Console application.</p></td></tr><tr><td>opswat</td><td><p>Check the Cortex XDR agent status and version.</p><p>Usage: <code>sudo ./cytool opswat &#x3C;parameter></code></p><p>where &#x3C;parameter> is:</p><ul><li><code>version</code>—Displays the version of the agent.</li><li><p><code>installed</code>—Displays the agent installation status:</p><ul><li><code>true</code> if the com.paloaltonetworks.pkg.cortx xdr package is installed.</li><li><p><code>false</code> if the package is not installed.</p><p>You must also supply the agent supervisor password to view the status.</p></li></ul></li><li><code>running</code>—Displays the running status of agent daemons: true if running or false if not running.</li><li><code>protected</code>—Displays the applied policy status: true if applied or false if not applied.</li></ul><p></p><pre><code><strong>Traps-Mac:bin Traps$ sudo ./cytool opswat version
</strong>8.1.0.1042
<strong>Traps-Mac:bin Traps$ sudo ./cytool opswat installed
</strong>Password:
true
<strong>Traps-Mac:bin Traps$ sudo ./cytool opswat running
</strong>true
<strong>Traps-Mac:bin Traps$ sudo ./cytool opswat protected
</strong>true
</code></pre></td></tr><tr><td>persist</td><td><p>The Cortex XDR agent stores policy and security event information such as the list of trusted signers, local verdicts, and one-time actions in local databases on the endpoint. To troubleshoot policy issues and security events, you can use cytool persist operations to import, export, and view information stored in the local database.<br></p><p>Usage: <code>sudo ./cytool persist &#x3C;</code><em><code>action></code></em></p><p>where <em>&#x3C;action></em>:</p><ul><li><code>list</code>—List the local databases on the endpoint.</li><li><code>export </code><em><code>[&#x3C;database name></code></em><code> | </code><em><code>&#x3C;databasepath>]</code></em>—Export database table to a file in the <code>/Library/Application Support/PaloAltoNetworks/Traps/bin/</code> directory.</li><li><code>import </code><em><code>[&#x3C;database name></code></em><code> | </code><em><code>&#x3C;databasepath></code></em><code>] &#x3C;file name></code>—Add records in a JSON file to the database.</li><li><code>print </code><em><code>&#x3C;database name></code></em><code> | </code><em><code>&#x3C;databasepath></code></em>—Print the database, in comma-separated values (CSV) format, to the command prompt.</li></ul><p>To view a list of all local databases, use the <code>cytool persist list</code> command.</p></td></tr><tr><td>queryall</td><td>The cytool queryall command displays a list of imported certificates, for troubleshooting purposes.</td></tr><tr><td>reconnect</td><td><p>Try reconnecting to the server if communication has been disabled, or force registration with a new <code>distribution_id</code>.</p><p>Usage:</p><ul><li><code>cytool reconnect</code>—Reconnects the Cortex XDR agent to the management application on the server.</li><li><code>cytool reconnect [force &#x3C;distribution_id>]</code></li></ul><div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>The <code>distribution_id</code> must belong to an installation package for the same operating system, and for the same or an earlier agent version than the one currently installed.</p></div></td></tr><tr><td>runtime</td><td><p>Stop or start product components.</p><p>Usage: <code>sudo ./cytool runtime </code><em><code>&#x3C;action></code></em> <em><code>&#x3C;component></code></em></p><p>where:</p><ul><li><p><em>&#x3C;action></em>—Change startup runtime action for an agent component.</p><p>Options are: <code>start</code>, <code>stop</code>, <code>query</code>. The query option displays the startup status for each component.</p></li><li><p><em>&#x3C;component></em>—Target component for which to set the runtime action, or all components if no components are specified.</p><p>To change the runtime action for multiple components, list them with spaces separating each component.</p><p>Options are: <code>cortex xdr</code>, <code>authorized</code>, <code>pmd</code>, <code>kproc-ctrl</code> </p></li></ul><p></p><p>For example:</p><pre><code><strong>Traps-Mac:bin Traps$ sudo ./cytool runtime query
</strong>         Name    PID         User              Status		Command
  cortex xdr   1055        User1             Running		/Library/Application Support/PaloAltoNetworks/Traps/bin/cortex xdr.app/Contents/MacOS/cortex xdr
   authorized    927  _traps_panw             Running		/Library/Application Support/PaloAltoNetworks/Traps/bin/authorized
          pmd    909         root             Running		/Library/Application Support/PaloAltoNetworks/Traps/bin/pmd
   kproc-ctrl    159         root              Loaded		com.paloaltonetworks.driver.kproc-ctrl
<strong>Traps-Mac:bin Traps$ sudo ./cytool runtime stop all
</strong>         Name    PID         User              Status		Command
   authorized    N/A          N/A             STOPPED		N/A
          pmd    N/A          N/A             STOPPED		N/A
  cortex xdr    N/A          N/A             STOPPED		N/A
   kproc-ctrl    N/A          N/A            Unloaded		N/A
<strong>Traps-Mac:bin Traps$ sudo ./cytool runtime start all
</strong>         Name    PID         User              Status		Command
system call failed for command='/usr/bin/su -l Traps -c "/bin/launchctl start cortex xdr.plist"', returned status code=768
   authorized   1883  _traps_panw             Running		/Library/Application Support/PaloAltoNetworks/Traps/bin/authorized
          pmd   1889         root             Running		/Library/Application Support/PaloAltoNetworks/Traps/bin/pmd
  cortex xdr    N/A          N/A     FAILED TO START		N/A
   kproc-ctrl    160         root              Loaded		com.paloaltonetworks.driver.kproc-ctrl
</code></pre></td></tr><tr><td>security_modules</td><td><p>Query, enable, disable or return to policy the Cortex XDR agent anti-tampering protection.</p><p>Usage: <code>cytool security_modules operation module</code></p><p>Where:</p><ul><li><p>Operation is one of the following:</p><ul><li><code>query</code> — Queries Security Module activity status</li><li><code>enable</code>— Enables Security Module</li><li><code>disable</code>— Disables Security Module</li><li><code>policy</code>— Syncs the Security Module according to cloud-defined policy</li></ul></li><li>Module options <code>self_prot</code> | <code>proc_ctrl</code> | <code>event_collection</code> | <code>dlprot</code> | <code>kpep</code> | <code>dlp</code> | <code>all</code></li></ul><p>Example: To disable the Cortex XDR agent anti-tampering protection:</p><p><code>cytool security_modules disable self_prot</code></p></td></tr><tr><td>startup</td><td><p>Enable, disable, or query the startup state of Cortex XDR agent components.</p><p>Usage: <code>sudo ./cytool startup </code><em><code>&#x3C;action></code></em> <em><code>&#x3C;component></code></em></p><p>where:</p><ul><li><p><em>&#x3C;action></em>—Change startup action for an agent component.</p><p>Options are: <code>enable</code>, <code>disable</code>, <code>query</code>.</p><p>The query option displays the startup status for each component.</p></li><li><em>&#x3C;component></em>—Target component for which to set the startup action. To change the startup action for multiple components, list them with spaces separating each component. Options are: <code>cortex xdr</code>, <code>authorized</code>, <code>pmd</code>, <code>kproc-ctrl</code></li></ul><p>For example:</p><pre><code><strong>Traps-Mac:bin Traps$ sudo ./cytool startup disable cortex xdr pmd
</strong>                  Process name                Startup status
                    cortex xdr                      Disabled
                    authorized                      Enabled
                           pmd                      Disabled
                    kproc-ctrl                      Loaded
<strong>Traps-Mac:bin Traps$ sudo ./cytool startup enable all
</strong>                  Process name                Startup status
                    cortex xdr                      Enabled
                    authorized                      Enabled
                           pmd                      Enabled
                    kproc-ctrl                      Loaded
</code></pre></td></tr><tr><td>wakeup</td><td><p>Wake up the endpoint from an OS incompatibility state.</p><p><code>Traps-Mac:bin Traps$  sudo ./cytool wakeup SIGTERM caught</code></p></td></tr></tbody></table>
