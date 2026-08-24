---
description: >-
  Install and configure a Cortex XSIAM engine for integration and automation
  workloads.
---

# Install an engine

When you install the engine, the `d1.conf` is installed on the engine machine, which contains engine properties such as proxy, log level, and log files. If Docker/Podman is already installed, the **`python.engine.docker`** and **`powershell.engine.docker`** keys are set to **`true`**. If Docker or Podman is not available when the engine is installed, the key is set to **`false`**. If so, you need to set the key to **`true`** after installing Docker and Podman. Verify that **`python.engine.docker`** and **`powershell.engine.docker`** configuration keys are present in the **`d1.conf`** file.

{% hint style="info" %}
If you are using DEB, RPM, or Zip installation, install Docker or Podman.

Natively running Python or PowerShell integrations/scripts on Windows or Linux is not supported on Cortex XSIAM engines.
{% endhint %}

<details>

<summary>Installation types</summary>

Cortex XSIAM supports the following file types for installation on the engine machine:

*   **Shell:** For all Linux deployments, including Ubuntu and SUSE. Automatically installs Docker/Podman, downloads Docker/Podman images, enables remote engine upgrade, and allows installation of multiple engines on the same machine.

    The installation file is selected for you. Shell installation supports the purge flag, which by default is false. To uninstall an engine, run the installer with the purge flag enabled.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>When upgrading an engine that was installed using the Shell installation, you can use the <strong>Upgrade Engine</strong> feature in the <strong>Engines</strong> page. For Amazon Linux 2-type engines, you need to upgrade these engine types using a zip-type engine and not use the <strong>Upgrade Engine</strong> feature.</p><p>If you use the shell installer, Docker/Podman is automatically installed. We recommend using Linux and not Windows to be able to use the shell installer, which installs all dependencies.</p></div>
* **DEB:** For Ubuntu operating systems.
*   **RPM:** RHEL operating systems.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>Use DEB and RPM installation when the shell installation is not available. You need to manually install <a href="install-an-engine/docker/install-docker">Docker</a> or <a href="install-an-engine/podman/install-podman">Podman</a> and any dependencies.</p></div>
* **Zip:** Used for Amazon Linux 2 machines.
* **Configuration:** Configuration file for download. When you install one of the other options, this configuration file (`d1.conf` ) is installed on the engine machine.

{% hint style="info" %}
For DEB/RPM engines, Python (including 3.x) and the containerization platform (Docker/Podman) must be installed and configured. For Docker or Podman to work correctly on an engine, [IPv4 forwarding](https://docs.docker.com/network/bridge/#enable-forwarding-from-docker-containers-to-the-outside-world) must be enabled.
{% endhint %}

</details>

<details>

<summary>How to install an engine</summary>

1. Create an engine.
   1. Select **Settings** → **Configurations** → **Data Broker** → **Engines** → **Create New Engine**.
   2. In the **Engine Name** field, add a meaningful name for the engine.
   3. Select one of the installer types from the list.
   4.  (Optional) (Shell only) Select the checkbox to enable multiple engines to run on the same machine.

       If you have an existing engine, and you did not select the checkbox, and now you want to install another engine on the same machine, you need to delete the existing engine.
   5. (Optional) Add any required configuration in JSON format.
   6. Click **OK** to create the engine.
2.  For shell installation, do the following:

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Tip</h3><p>For Linux systems, we recommend using the shell installer. If using Amazon Linux 2, use the zip installer (see step 4).</p></div>

    1. Move the `.sh` file to the engine machine using a tool such as SSH or PuTTY.
    2.  On the engine machine, grant execution permission by running the following command:

        **`chmod +x /<engine-file-path>`**
    3.  Install the engine by typing one of the following commands:

        With tools: **` sudo`` `` `**_**`<engine-file-path>`**_

        Without tools: **` sudo`` `` `**_**`<engine-file-path> -- -tools=false`**_

        <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>If you receive a <strong><code>permissions denied</code></strong> error, it is likely that you do not have permission to access the <strong><code>/tmp</code></strong> directory.</p><p>If the installer fails to start due to a permissions issue, even if running as root, add one of the following two arguments when running the installer:</p><ul><li><code>--target &#x3C;path></code> - Extracts the installer files into the specified custom path.</li><li><code>--keep</code> - Extracts the installer files into the current working directory (without cleaning at the end).</li></ul><p>If using installer options such as <code>-- -tools=false</code>, the option should come after the <code>--target</code> or <code>--keep</code> arguments. For example:</p><p><code>sudo ./d1-installer.sh --target /some/temp/dir -- -tools=false</code></p><p>If you set a custom path when you run the installer, you must also set a custom path for upgrading your engine or the upgrade will fail. For more information, see <a href="upgrade-an-engine">Upgrade an engine</a>.</p></div>
3. For RPM/DEB installation, do the following:
   1. Move the file to the required machine using a tool such as SSH or PuTTY.
   2.  Type one of the following installation commands:

       | Machine Type | Install Command                               |
       | ------------ | --------------------------------------------- |
       | RHEL (RPM)   | **`sudo rpm -Uvh d1-2.5_15418-1.x86_64.rpm`** |
       | Ubuntu (DEB) | **`sudo dpkg --install d1_xxx_amd64.deb`**    |
   3.  Start the engine by running one of the following commands:

       | Machine Type | Start Command                 |
       | ------------ | ----------------------------- |
       | RHEL (RPM)   | **`sudo systemctl start d1`** |
       | Ubuntu (DEB) | **`sudo service d1 restart`** |
4. For Zip installation on Amazon Linux 2, run the following commands:
   1.  Create the engine folder.

       **`mkdir /usr/local/demisto`**
   2.  Unzip the engine files to the folder created in the previous step.

       **`unzip ./d1.zip -d /usr/local/demisto`**
   3.  Allow the process to bind to low-numbered ports.

       **`setcap CAP_NET_BIND_SERVICE=+eip /usr/local/demisto/d1_linux_amd64`**
   4.  Change the owner of `/usr/local/demisto` to the demisto user.

       **`chown -R demisto:demisto /usr/local/demisto`**
   5.  In `/etc/systemd/system` edit the `d1.service` file as follows (adjust the directory and the name of the binary file if needed).

       ```programlisting
        [Unit]
       Description=Demisto Engine Service
       After=network.target
       [Service]
       Type=simple
       User=demisto
       WorkingDirectory=/usr/local/demisto
       ExecStart=/usr/local/demisto/d1_linux_amd64
       EnvironmentFile=/etc/environment
       Restart=always
       [Install]
       WantedBy=multi-user.target
       ```
   6.  Run the following commands:

       `chown root:root /etc/systemd/system/d1.service`

       `chmod 644 /etc/systemd/system/d1.service`
   7.  Run the engine process.

       **`systemctl start d1`**
   8.  Verify that the engine is running.

       **`systemctl status d1`**
5. Verify that the engine you created is connected.
   1. Select **Settings** → **Configurations** → **Data Broker** → **Engines**.
   2. Locate your engine on the **Engines** page and check that it is connected.
6.  When the engine is connected, you can add the engine to a load-balancing group by clicking **Load-Balancing Group** on the Engines page.

    If you want to add the engine to a new group, click **Add to new group** from the list.

    When the engine is in the load-balancing group, it cannot be used as an individual engine and does not appear when configuring an engine from the list.
7. (Optional) After installing the engine, you may want to set up a proxy, set up Docker hardening, configure the number of workers for the engine, or perform other related engine configurations. For more information, see [Configure Engines](configure-engines). You can also configure an integration instance to run on the engine you created.

</details>
