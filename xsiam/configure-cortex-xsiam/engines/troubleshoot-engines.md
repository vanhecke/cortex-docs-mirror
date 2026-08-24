---
description: >-
  Troubleshoot Cortex XSIAM engine issues by reviewing logs, errors, and
  connectivity.
---

# Troubleshoot engines

When troubleshooting engines, access the logs from Settings → Configurations → **Engines** and select the engine from which you want to download the logs.

{% hint style="info" %}
Ensure that pop-ups are not blocked by your browser.
{% endhint %}

### **Debug engines**

The **d1.log** field appears whenever an engine is running. The **d1.log** field contains information necessary for your customer success team to debug any engine-related issue. The field displays any error, as well as noting whether the engine is connected.

![engine-debug.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-4af97017080d0bf0f51b658d5ac171f3232d39f6%2F17428cb11a1fad7a2d109f505c33311e06bd1434fc034033bd7141cd545cb487.png?alt=media)

<details>

<summary>Troubleshoot engine installation</summary>

{% hint style="info" %}
If the installer fails to start due to a permissions issue, even if running as root, add one of the following two arguments when running the installer:

* `--target <path>` - Extracts the installer files into the specified custom path.
* `--keep` - Extracts the installer files into the current working directory (without cleaning at the end).

If using installer options such as `-- -tools=false`, the option should come after the `--target` or `--keep` arguments. For example:

`sudo ./d1-installer.sh --target /some/temp/dir -- -tools=false`

If you set a custom path when you run the installer, you must also set a custom path for upgrading your engine or the upgrade will fail. For more information, see [Upgrade an engine](upgrade-an-engine).
{% endhint %}

After installing the engine, check that the engine is connected to the Cortex XSIAM tenant and that it is running.

1. Go to **Settings** → **Configurations** → **Data Broker** → **Engines** and verify that the engine is connected.
2.  If the engine is not connected, run the following command on the engine server to check if the engine service is running.

    **`sudo systemctl status d1`**

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>If the <strong>Allow running multiple engines on the same machine</strong> option is selected, run the command:</p><p><strong><code>sudo systemctl status d1_&#x3C;Engine _name></code></strong></p></div>
3.  Access the d1 log on the engine server.

    **`sudo tail -f /var/log/demisto/d1.log`**

    * If the engine service is not running, and there’s nothing relevant in the log, run **`journalctl`** on the engine server to understand why the installation failed.
    *   If the engine service is running, review the errors to see if the engine is failing to connect or if there are other issues (ignore all errors related to `\d2ws`, because this is not the same as `d1ws`.) Most often, the server address is incorrect and you will see an error like this:

        `error Cannot connect to [wss://<mainServerIP/HostName>/d1ws]: wss://<mainServerIP/HostName>/d1ws: dial tcp: lookup localhost: no such host. . Waiting 3 seconds. Will try until…`

        In this case, navigate to `/usr/local/demisto/d1.conf` and change the **`EngineURLs`** parameter to an address the engine can reach. Check the addresses at the beginning of the _upgrade\_engine.sh_ file. If the addresses are not correct, set the correct addresses in the `/usr/local/demisto/upgrade.conf` file, as a comma-separated list.

        The configurations that might affect the `upgrade_engine.sh` script are the following variables are located at the beginning of the script:

        * **`SERVER_URLS`**
        * **`TRUST_ANY_CERT`**

        If you make a change to the baseURLs configuration, you must apply the change in `/usr/local/demisto/d1.conf` AND in `/usr/local/demisto/upgrade.conf` under the SERVER\_URLS var. For SERVER\_URLS, specify only the IP/hostname and, optionally, a port. Do not include `https://` or any path at the end.

        If you make a change in the `engine.connection.trust_any_certificate` configuration, you must apply the change in `/usr/local/demisto/upgrade.conf` as follows:

        * If the `engine.connection.trust_any_certificate` configuration was set to true (trust any certificate), set the TRUST\_ANY\_CERT variable to -k.
        * If the `engine.connection.trust_any_certificate` configuration was set to false, the TRUST\_ANY\_CERT variable should be blank (““).

        <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>Any changes made to variables in the <code>upgrade_engine.sh</code> file are reset after each upgrade. We recommend instead using the <code>upgrade.conf</code> file to set variables.</p></div>

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>You can ignore the following error: <strong><code>Cannot create folder '/var/lib/demisto'</code></strong></p></div>
4. To check the connectivity from the engine to the Cortex XSIAM tenant, see _Troubleshoot engine connectivity_ below.
5. If the installation issue remains, open a support case with logs from the engine.
   1. On the engine server, in `/usr/local/demisto/d1.conf`, set "LogLevel": "debug”.
   2.  Restart the d1 service and let it run for a few minutes.

       **`sudo systemctl restart d1`**

       <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>If the <strong>Allow running multiple engines on the same machine</strong> option is selected, run the command:</p><p><strong><code>sudo systemctl status d1_&#x3C;Engine _name></code></strong></p></div>
   3.  Capture a\*\* `journalctl`\*\*:

       **`journalctl --since "1 day ago" > engineTroubleshootingJournalctl.log`**
   4.  On the engine server, tar up the log, conf, **`journalctl`**, and install log on the engine.

       **`tar -cvzf engineLogs.tar.gz /var/log/demisto /usr/local/demisto/d1.conf /tmp/demisto_install.log engineTroubleshootingJournalctl.log`**

</details>

<details>

<summary>Troubleshoot engine upgrades</summary>

During an upgrade, the upgrade file is sent to the engine server. A cron job running on the engine server checks if that file exists. The most common upgrade error is that the job is not running, so the new installer does not run.

{% hint style="info" %}
If the installer fails to start due to a permissions issue, even if running as root, add one of the following two arguments when running the installer:

* `--target <path>` - Extracts the installer files into the specified custom path.
* `--keep` - Extracts the installer files into the current working directory (without cleaning at the end).

If using installer options such as `-- -tools=false`, the option should come after the `--target` or `--keep` arguments. For example:

`sudo ./d1-installer.sh --target /some/temp/dir -- -tools=false`
{% endhint %}

1. SSH to the machine.
2.  Check the d1 service status on the engine server. It is possible that it stopped or doesn't exist.

    **`sudo systemctl status d1`**

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>If the <strong>Allow running multiple engines on the same machine</strong> option is selected, run the command:</p><p><strong><code>sudo systemctl status d1_&#x3C;Engine _name></code></strong></p></div>
3.  Access the installer log on the engine server and review the error.

    **`sudo vi /tmp/demisto_install.log`**
4. Rerun the installer on the engine using one of the following options. You can open a second window and run **`watch df -h`**. If the problem seems to be disk space, you should resolve the disk space issue and then rerun the installer.
5. Do one of the following:
   *   Download the installer from the user interface and copy it to the engine.

       Add the following commands:

       `sudo chmod +x installer.sh`

       `sudo ./installer.sh -- -y`
   * Verify that `/usr/local/demisto/d1_upgrade.sh` exists.
     1.  Run the following commands:

         `sudo chmod +x /usr/local/demisto/d1_upgrade.sh`

         `sudo /usr/local/demisto/d1_upgrade.sh`
     2. If `d1_upgrade.sh` doesn't exist, check if `/usr/local/demisto/archived_d1_upgrade.sh` exists and that it was created at the time of the attempted upgrade.
     3.  If the file exists and was created at the time of the attempted upgrade, run the following commands on the engine server:

         `sudo chmod +x /usr/local/demisto/archived_d1_upgrade.sh`

         `sudo /usr/local/demisto/archived_d1_upgrade.sh`

</details>

<details>

<summary>Troubleshoot engine connectivity</summary>

The following provides instructions for troubleshooting connectivity issues from the engine to the endpoint.

1. Follow the instructions in [network troubleshooting](https://xsoar.pan.dev/docs/reference/articles/troubleshooting-guide#host-based-networking).
2.  Ensure that the engine can reach the endpoint by running the following command on the server engine.

    **`sudo curl -kvv <endpointURL>`**
3.  If the engine could not reach the endpoint, try the IP with curl instruction adding the http(s)//, or try using ping.

    If this works, add the IP to the /etc/hosts file with the hostname and try to reach the endpoint again by running the following command on the engine server

    **`sudo curl -kvv <endpointURL>`**

    If this still fails, then this is an issue of connectivity between the engine and endpoint and you need to resolve this with your networking team.
4. After connectivity has been confirmed via curl:
   *   Try connecting within Docker without passing host networking.

       **`docker run -it --rm demisto/netutils:1.0.0.6138 curl -kvv <endpointURL>`**

       If this succeeds but the integration still fails, it could be an integration credentials issue. In that case, open a [support case](https://support.paloaltonetworks.com/support).
   *   If, without passing the host networking fails, run the following:

       **`docker run -it --rm --network=host demisto/netutils:1.0.0.6138 curl -kvv <endpointURL>`**

       If this succeeds, add \*\*`"python.pass.extra.keys": "--network=host" to /usr/local/demisto/d1.conf` \*\*and retest the integration.

       If you see a Docker or SELinux issue, see [Troubleshoot Docker Issues](install-an-engine/docker/troubleshoot-docker-issues).
5. If the installation issue remains, open a support case with logs from the engine.
   1. On the engine server, in `/usr/local/demisto/d1.conf`, set "LogLevel": "debug”.
   2.  Restart the d1 service and let it run for a few minutes.

       **`sudo systemctl restart d1`**

       <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>If the <strong>Allow running multiple engines on the same machine</strong> option is selected, run the command:</p><p><strong><code>sudo systemctl status d1_&#x3C;Engine _name></code></strong></p></div>
   3.  Capture a journalctl:

       **`journalctl --since "1 day ago" > engineTroubleshootingJournalctl.log`**
   4.  On the engine server, tar up the logs, conf, journalctl, and install log on the engine.

       **`tar -cvzf engineLogs.tar.gz /var/log/demisto /usr/local/demisto/d1.conf /tmp/demisto_install.log engineTroubleshootingJournalctl.log`**

</details>

<details>

<summary>Engine 443 error</summary>

This error might occur when a connection is established between an engine and the Cortex XSIAM tenant, because, by default, Linux does not allow processes to listen on low-level ports.

**Error Message**

**`listen tcp :443: bind: permission denied`**

**Solution**

* In the `d1.conf` file, change the port number to a higher one, for example, 8443.
* Run this command: **`sudo setcap CAP_NET_BIND_SERVICE=+eip /path/to/binary`**. After running this command, the server should be able to bind to low-numbered ports.

</details>

<details>

<summary>Bad handshake error</summary>

This error can occur in the engine logs relating to a bad handshake on the engine when trying to connect to a Cortex XSIAM tenant.

**Error Message**

**`Cannot connect to [wss:/xxx]: [wss://xxx|wss://xxx/]: websocket: bad handshake`**

**Solution**

Verify that time is synchronized on the engine to a reliable NTP source. When timing is off on the engine, this can cause a failure during the SSL/TLS handshake process. When time is resynced, connectivity from the engine to the parent server should be restored.

</details>
