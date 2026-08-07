---
description: Upgrade an engine on Cortex XSIAM or directly on the remote machine.
---

# Upgrade an engine

Whenever there is a Cortex XSIAM major version change or a change in tenant-engine protocol version, your engines require an upgrade. On the **Engines** page, the **Status** column shows those engines that require upgrades. You can upgrade an engine by doing the following:

* If you installed the engine using the Shell installer, you can upgrade the engine on the **Engines** page.
* If you didn't install the engine using the Shell installer, you need to remove the engine and do a fresh install.

**Upgrade an engine (shell installations)**

You can upgrade the engine on the **Engines** page if you have installed the engine using the shell installer. The engine must be connected during the upgrade.

**Customize upgrade variables**

Before upgrading, we recommend you review the upgrade variables and verify if any need to be set in the `/usr/local/demisto/upgrade.conf` file on the engine. For environments with multiple engines, the file is located at `/usr/local/demisto/<engine-name>/upgrade.conf`. In some cases, usually related to a web proxy server or a custom directory, if you do not configure the `upgrade.conf` file, the upgrade will fail.

The option to set custom upgrade variables is only available for shell installation.

{% hint style="info" %}
The `upgrade.conf` file is available on the engine after it has been upgraded to Cortex XSIAM 3.1. Any custom variables you add to the file are applied when you upgrade from Cortex XSIAM 3.1 to Cortex XSIAM 3.2 or later.
{% endhint %}

| Variable                               | Description                                                                                                                                                                                                                                                                                                                                                          | Default                                                         |
| -------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------- |
| https\_proxy                           | The URL of a web proxy server to use when connecting with the server. The variable name is case sensitive. Other common proxy variables, such as `http_proxy` or `HTTPS_PROXY` are ignored. Use `https_proxy` even if your proxy address begins with `http://`.                                                                                                      | Not set                                                         |
| SERVER\_URLS                           | The URL to connect to for hash validation. Set this variable if your tenant's address has changed. Use your tenant's API address, with the `api-` prefix added, instead of the UI address. For example: `SERVER_URLS="api-example.us.paloaltonetworks.com"`. Include only the IP/hostname and, optionally, a port. Do not include `https://` or any path at the end. | Public tenant URL                                               |
| TRUST\_ANY\_CERTIFICATE                | Determines whether the connection's SSL certificate must be trusted. This variable must be empty `""` to require certificate trust. When set to `-k`, trusts any certificate. We recommend enabling this setting. Verify first that the engine host has the required CA root certificate, especially if using a proxy.                                               | -k                                                              |
| XSOAR\_ENGINE\_AUTO\_UPGRADE\_TMP\_DIR | Specifies a directory to use for extracting upgrade files and executing the upgrade. For example, `XSOAR_ENGINE_AUTO_UPGRADE_TMP_DIR="/root/tmp/engine1"` For environments with multiple engines, each engine must use a different temporary directory. This variable must be set if you used the `--target` option in the shell installer.                          | By default, a random directory under the `/tmp` folder is used. |

**Test upgrade connectivity**

1.  Test the upgrade connectivity by creating a mock `d1_upgrade.sh` file :

    ```programlisting
    cd /usr/local/demisto
    echo test > d1_upgrade.sh
    ```

    After you create the file, the upgrade cron job removes the file within one minute.
2. Check the upgrade log file `/var/log/demisto/demisto_install.log` for connection-related errors. For hosts with multiple engines, the log file can be found at `/tmp/<engine name>/demisto_install.log`.
3. If the test is successful, the following message appears at the end of the log file, with a recent timestamp: `Validation HTTPS request returned: false`.
4. If you find errors in the log, you may need to change the variables in the `upgrade.conf` file or to change your network configuration.

How to upgrade

1. On the **Engines** page, select the checkbox for the engine that requires an upgrade.
2.  Click **Upgrade Engine**.

    When the upgrade finishes, the version appears in the **Cortex XSIAM Version** column. The upgrade procedure can take several minutes.

**Upgrade an engine (non-shell installations)**

If you didn't use the Shell installer, you need to remove the engine and do a fresh install.

1. On the **Engines** page, locate the engine that requires an update.
2. In the Download link, click the relevant Download files.
3.  On the remote machine, do the following:

    * Remove the existing engine. For more information, see [Remove an engine](remove-an-engine).
    * Install the engine you downloaded in step 2. For more information, see [Install an engine](install-an-engine).

    When the upgrade finishes, the version appears in the **Cortex XSIAM Version** column. The upgrade procedure can take several minutes.

**Related information**

[Troubleshoot engines](troubleshoot-engines)
