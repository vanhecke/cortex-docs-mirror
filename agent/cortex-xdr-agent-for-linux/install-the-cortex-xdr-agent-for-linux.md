---
description: Learn how to install the Cortex XDR agent on a Linux endpoint.
---

# Install the Cortex XDR agent for Linux

The Cortex XDR agent for Linux is designed to protect Linux servers and operates transparently in the background as a system process. The agent also extends exploit and malware protection to processes that run in Linux containers. When you install the Cortex XDR agent on a Linux server, running either on Kernel or User Space mode, the agent automatically protects any new and existing containerized processes regardless of the container solution (for example, Docker). Each Linux server receives a single license which includes protection for container processes.

You can also deploy Cortex XDR agents on virtual Linux servers as temporary sessions, to ensure the Cortex XDR agent license returns to the license pool after 90 minutes of session inactivity and to improve your network temporary workloads.

After you install the Cortex XDR agent for Linux, it is typically not necessary to interact with the agent; however, to perform common actions, such as initiating a manual check-in with Cortex XDR, you can use the command-line utility named Cytool. Cytool is available in the `/opt/traps/bin/cytool` directory and must be run as root or with root permissions.

Before installing the agent on a Linux server, verify that the system meets the requirements described in [Cortex XDR Agent for Linux Requirements](cortex-xdr-agent-for-linux-requirements).

{% hint style="info" %}
### Note

If you intend to use SELinux, make sure to enable it before you proceed with the Cortex XDR agent installation. This ensures that the agent disables any injection-based modules that cause compatibility issues.

If you later enable SELinux (change from disabled to enabled - regardless of its mode - permissive to enforcing), you must reinstall the agent to avoid any compatibility issues.

If you later change SELinux operation mode (between permissive and enforcing or vice versa), you must restart the agent to avoid any compatibility issues.
{% endhint %}

To install a Cortex XDR agent:

1. Download the relevant Cortex XDR agent Linux installer for your system from Cortex XDR.
2.  Copy the installer to the Linux server on which you want to install the Cortex XDR agent software.

    For example, to copy the file securely from a local machine to the Linux server:

    ```screen
    user@local ~
                                            scp linux.sh.tar.gz root@centos.example.com:/tmp
                            linux.sh.tar.gz                                100%   52MB   95.2MB/s   00:00
                        
    ```
3.  Log on to the Linux server.

    For example:

    ```screen
    user@local ~
           ssh root@centos.example.com
    root@centos.example.com's password:
    ```
4.  Install the Cortex XDR agent software.

    You can install the Cortex XDR agent on the endpoint manually using the shell installer or using the Linux package manager for **`.rpm`** and **`.deb`** installers.

    *   Unpack the installation archive by running.

        **`tar xf filename.tar.gz`**
    *   Copy the configuration file into `/etc/panw` directory.

        **`sudo mkdir -p /etc/panw`**

        **`sudo cp cortex.conf /etc/panw/`**

    **To deploy using package manager:**

    1. (Optional) For Linux distributions RHEL, CentOS, Oracle, or SUSE that have signature-checking configured or you would like to manually check the integrity of the Cortex XDR package:
       1. Download the [Cortex XDR Public Key](#cortex-xdr-public-key).
       2. Unzip the public key by running **`unzip cortex-xdr-agent.zip`**.
       3. Import the public key by running **`rpm --import cortex-xdr-agent.asc`**.
    2. Depending on your Linux distribution, install the Cortex XDR agent using one of the following commands:

    <table><thead><tr><th width="257.5816650390625">Distribution</th><th>Install Command</th></tr></thead><tbody><tr><td>RHEL, CentOS, or Oracle</td><td><strong><code>yum install ./</code></strong><em><strong><code>filename</code></strong></em><strong><code>.rpm</code></strong> or <strong><code>rpm -i ./</code></strong><em><strong><code>filename</code></strong></em><strong><code>.rpm</code></strong></td></tr><tr><td>Ubuntu or Debian</td><td><strong><code>apt-get install ./</code></strong><em><strong><code>filename</code></strong></em><strong><code>.deb</code></strong> or <strong><code>dpkg -i ./</code></strong><em><strong><code>filename</code></strong></em><strong><code>.deb</code></strong></td></tr><tr><td>SUSE</td><td><strong><code>zypper install ./</code></strong><em><strong><code>filename</code></strong></em><strong><code>.rpm</code></strong> or <strong><code>rpm -i ./</code></strong><em><strong><code>filename</code></strong></em><strong><code>.rpm</code></strong></td></tr></tbody></table>

    3. Verify the agent was installed on the endpoint.

    Enter the following command on the endpoint:

    **`dpkg -l | grep cortex-agent`** or **`rpm -qa | grep cortex-agent`**. **To deploy the shell installer:**

    1. Enable execution of the script using the **` chmod +x`` `` `**_**`filename`**_ command.
    2. Run the install script as root or with root permissions.

    For example on CentOS 7:

    ```screen
    [root@centos]#
     cd /tmp
    [root@centos tmp]#
     ls
    cortex-7.7.0.59559.sh
    cortex.conf
    linux.sh.tar.gz 
    README.md
    [root@centos tmp]#
     chmod +x cortex-7.7.0.59559.sh
    [root@centos tmp]#
     ./cortex-7.7.0.59559.sh
    Verifying archive integrity... All good.
    Uncompressing Cortex XDR 7.7.0.59559 installer  100%
    [!] Path '/bin' is not in PATH
    [!] Path '/sbin' is not in PATH
    [ 1] Checking prerequisites
    Verifying RHEL/CentOS 7 (rpm) packages:
      * openssl ... OK
      * ca-certificates ... OK
      * policycoreutils-python ... OK
      * selinux-policy-devel ... OK
    Done
    [ 2] Installing Cortex XDR [7.7.0.59559] at /opt/traps
    Using packaged compatibility libraries
    Done
    [ 3] Creating runtime directory
    Done
    [ 4] Installing SELinux policies
      Compiling ... OK
      Installing ... OK
      Updating contexts ... OK
    Done
    [ 5] Verifying iptables prerequisite
    Done
    [ 6] Defining Cortex XDR local services (systemd)
    Created symlink from /etc/systemd/system/multi-user.target.wants/traps_pmd.service to /etc/systemd/system/traps_pmd.service.
    Done
    [ 7] Creating/Verifying Cortex XDR auxiliary user
    Done
    [ 8] Configuring connection to server
    Done
    [ 9] Starting Cortex XDR security services
    Redirecting to /bin/systemctl start traps_pmd.service
              Name       PID           User                Status               Command
                   pmd      6072           root               Running               /opt/traps/bin/pmd
             analyzerd       N/A            N/A               STOPPED               N/A
                  dypd      6138           root               Running               /opt/traps/bin/dypd  -s -- 175
                  lted       N/A            N/A               STOPPED               N/A
    Done                            
    ```

    Additional options are available to help you customize your installation if needed. The following table describes common options and parameters that you can use but does not provide an exhaustive list. Use the --help option to print the help for the installer.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>If you are using <code>rpm</code>, <code>deb</code> or <code>sh</code> installers, you must also add these parameters to the <code>/etc/panw/cortex.conf</code> file prior to installation.</p></div>

    Make sure to remove the first couple of leading double dashes. For example, instead of :**`-- --proxy-list ”`**_**`<proxyserver>`**_**`:`**_**`<port>`**_**`”`**, add this: **`--proxy-list="10.196.21.223:808"`**.

    Applies to:

    **`--proxy-list="10.196.21.223:808" --no-km --restrict=live_terminal`**

    <table><thead><tr><th width="244.243896484375">Option</th><th>Description</th></tr></thead><tbody><tr><td><strong><code>--no-km</code></strong></td><td><p><strong>Without Kernel Module Installation</strong></p><p>Use the <strong><code>--no-km</code></strong> option if you do not want to install the Cortex XDR agent kernel module. If you install the agent without the Cortex XDR kernel module or your Linux server runs an unsupported kernel version, the Cortex XDR agent will operate in asynchronous mode.</p></td></tr><tr><td><strong><code>--install-path=</code></strong><em><strong><code>&#x3C;/custom/path></code></strong></em></td><td><p><strong>Custom Agent Installation Directory</strong></p><p>Install the Cortex XDR agent in a custom directory on the endpoint instead of using the default <code>./opt</code> directory. Custom installation directory is a persistent change, and after you install the Cortex XDR to the custom path, all following upgrades and the removal of the agent from the endpoint are executed in the same location.</p><p>Before you start, ensure the custom directory exists on the endpoint and has user and group executable permissions.</p><ul><li><p><strong>SH installer</strong>—Run the following command for example:</p><p><strong><code>root@ubuntu:/tmp# ./linuxshell.sh -- --install-path=</code></strong><em><strong><code>/home/customDir</code></strong></em></p></li><li><p><strong>RPM and DEB installers</strong>—</p><p>1. Create a <code>cortex.conf</code> file on the endpoint, under <code>/ect/panw/</code></p><p>2. Add to the <code>cortex.conf</code> your custom directory parameter, for example:</p><p><strong><code>--install-path=</code></strong><em><strong><code>/home/customDir</code></strong></em></p></li></ul><p>If you are installing Cortex XDR to a custom directory on SELinux enabled systems, ensure:</p><p>1. The custom installation directory must have an SELinux context that allows:</p><ul><li>File execution (execute permission)</li><li>Library loading (execute permission for shared libraries)</li></ul><p>Recommended contexts:</p><ul><li>usr_t - Standard user application files</li><li>bin_t - Executable binaries (for the bin/ subdirectory)</li></ul><p>2. Pre-Installation Steps</p><p><strong>Option A: Set context on the parent directory (Recommended)</strong></p><p>Before installation, configure the SELinux file context for the custom directory.</p><p>Example: If installing to <code>/data/cortex/traps</code>, set the context for the entire directory tree:</p><p><code>sudo semanage fcontext -a -t usr_t "/data/cortex(/.</code><em><code>)?"</code></em></p><p><em><code>sudo mkdir -p /data/cortex</code></em></p><p><em><code>sudo restorecon -Rv /data/cortex</code></em></p><p><em><strong>Option B: Set context after installation</strong></em></p><p><em>If the agent is already installed but failing to start, set <code>bin_t</code> context for executable binaries:</em></p><p><em><code>sudo semanage fcontext -a -t bin_t "/data/cortex/traps/bin(/.</code></em><code>)?"sudo restorecon -Rv /data/cortex/traps/bin</code></p><p>3. Verification - After setting the contexts, verify they are applied correctly.</p><p>Check the context of the installation directory:</p><p><code>ls -laZ /data/cortex/traps/</code></p><p>Check the context of binaries:</p><p><code>ls -laZ /data/cortex/traps/bin/</code></p><p>Expected output should show <code>bin_t</code> or <code>usr_t</code>, NOT default_t</p><p>Example: <code>-rwx------. root root system_u:object_r:bin_t:s0 pmd</code></p><p>4. Verify Cortex XDR agent starts successfully</p><p>Start the agent</p><p><code>sudo systemctl start traps_pmd</code></p><p>Check status</p><p><code>sudo systemctl status traps_pmd</code></p><p>Check for SELinux denials</p><p><code>sudo ausearch -m avc -ts recent</code></p></td></tr><tr><td><strong><code>-- --proxy-list ”</code></strong><em><strong><code>&#x3C;proxyserver></code></strong></em><strong><code>:</code></strong><em><strong><code>&#x3C;port></code></strong></em><strong><code>”</code></strong></td><td><p><strong>Proxy Communication</strong></p><p>Configure the Cortex XDR agent to communicate through an intermediary such as a proxy or the Palo Alto Networks Broker Service.</p><p>To enable the agent to direct communication to an intermediary, you use this installation option to assign the IP address and port number you want the Cortex XDR agent to use. You can also configure the proxy by entering the FQDN and port number. When you enter the FQDN, you can use both lowercase and uppercase letters. Avoid using special characters or spaces.</p><p>Use commas to separate multiple addresses. For example:</p><p><strong><code>-- --proxy-list "My.Network.Name:808, 10.196.20.244:8080"</code></strong></p><p>You can assign up to five different proxies per agent, and the proxy for communication is selected randomly with equal probability.</p><p>To enable the agent to use the Broker Service, you must set up broker VM in your network and use this option to assign the agent the Broker VM IP address with port number 8888.</p><p>After the initial installation, you can change the proxy settings from Cortex XDR.</p><div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>The Cortex XDR agent does not support proxy communication in environments where proxy authentication is required.</p></div></td></tr><tr><td><p>VM Template</p><p><strong><code>--vm-template</code></strong></p><p>Temporary session</p><p><strong><code>--temporary-session</code></strong></p></td><td><p><strong>Virtual Installation</strong></p><p>Deploy Cortex XDR agents on virtual Linux endpoints as temporary instances, ensuring the Cortex XDR agent license returns back to the license pool after 90 minutes of session inactivity and improving your network temporary workloads. Choose your preferred workflow:</p><p><strong>Pre-install</strong>—Install the Cortex XDR agent only on the Linux endpoint you are using to create the VM template. Every instance you create using this template, will include the pre-installed Cortex XDR agent. For example:</p><p><code>$ ./installer.sh -- --vm-template</code></p><p><strong>Fresh install</strong>—Install the Cortex XDR agent on the Linux VM after creating the VM template, as part of provisioning. For example:</p><p><code>$ ./installer.sh -- --temporary-session</code></p></td></tr><tr><td><strong><code>-- --restrict=</code></strong><em><strong><code>&#x3C;flag></code></strong></em></td><td><p><strong>Disable Live Terminal, script execution, and file retrieval on the endpoint</strong></p><p>Use to permanently disable the option for Cortex XDR to perform all, or a combination, of the following actions on endpoints running a Cortex XDR agent: initiate a remote session on the endpoint, (see Run Scripts on an Endpoint), and from the endpoint to the management console.</p><div data-gb-custom-block data-tag="hint" data-style="warning" class="hint hint-warning"><p><strong>Caution</strong></p><p>Disabling any of these actions is an irreversible action, so if you later want to enable the action on the endpoint, you must uninstall the Cortex XDR agent and install a new package without this flag.</p></div><p>To disable all actions, use the corresponding flag: <strong><code>--restrict=all</code></strong></p><p>To disable a specific action, use the corresponding flag:</p><ul><li><strong><code>--restrict=live_terminal</code></strong>—Use to disable Live Terminal.</li><li><strong><code>--restrict=script_execution</code></strong>—Use to disable script execution.</li><li><strong><code>--restrict=file_retrieval</code></strong>—Use to disable file retrieval.</li></ul><p>To disable more than one option, use any combination of these flags.</p></td></tr><tr><td><strong><code>-- --endpoint-tags`` ``</code></strong><em><strong><code>&#x3C;tag></code></strong></em></td><td><p><strong>Add Endpoint Tags</strong></p><p>Add tags to the endpoint tags list.</p><ul><li><p><strong>SH installer</strong>—Run the following command for example:</p><p><strong><code>traps_linux.sh -- --endpoint-tags </code></strong><em><strong><code>tag1,tag2,tag3</code></strong></em></p><p>Spaces in tags are not allowed, if spaces are required, use the configuration file method below.</p><div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>The double dash (--) before the --endpoint-tags argument is mandatory, and the argument and the value must be separated by a space.</p></div></li><li><p><strong>RPM/DEB/Shell installers</strong>—</p><p>1. Create a <code>cortex.conf</code> file on the endpoint, under <code>/ect/panw/</code></p><p>2. Add to the <code>cortex.conf</code> your custom directory parameter, for example:</p><p><strong><code>--endpoint-tags </code></strong><em><strong><code>tag1,tag2,tag3</code></strong></em></p><div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>If one or more tags contains spaces, the entire tags string must be enclosed in quotes ("), for example: <strong><code>--endpoint-tags "tag1,tag multi word2,tag3"</code></strong>.</p></div></li></ul></td></tr></tbody></table>
5.  (For Kernel Mode only) Load SecureBoot Certificates.

    If you enabled the SecureBoot kernel, perform the following to add the Cortex XDR kernel module certificate, available for:

    * RHEL 8, AlmaLinux 8, RockyLinux 8, Oracle 8 and later
    * Ubuntu 18 and later
    * SLES 15 and later

    1. On your server, navigate to `/opt/traps/download/content/km/modules/<os_name>/` and locate key name `xdr_kernel_cert.der` to access the public key.
    2.  Load the key to the MOK by running the command:

        **`mokutil --import xdr_kernel_cert.der`**
    3. Set a password.
    4.  Reboot the system.

        During the machine reboot, the Unified Extensible Firmware Interface (UEFI) will ask you to **Enroll MOK**. When prompted whether to download the key, select **Yes** and enter the password you defined.
    5. Verify the key was loaded by running the command **`mokutil --list-enrolled`** and locating the key with the `Palo Alto Networks` issuer.
6. See the [Use the Cortex XDR agent for Linux](use-the-cortex-xdr-agent-for-linux) section for a list of available options and functions. Enter the **`cytool`** command without any arguments or with **`-h`** or **`--help`** for a full list of available functions.



### Cortex XDR Public key

{% file src="https://517755450-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FuBmMrMEHkk0xAv8axZos%2Fuploads%2FrBgwHcfe1UKQ8LLUxqbG%2Fcortex-xdr-agent-public-key.zip?alt=media&token=8a9fd5db-492d-4a15-a862-92dba55f0462" %}
