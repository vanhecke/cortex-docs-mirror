# Install the XDR Collector installation package for Linux

You can install the XDR Collector using three available packages for a Linux installation: Linux RPM, Linux DEB, and Linux SH. You can install the XDR Collector package on any Linux server, including a physical or virtual machine, and as temporary sessions.

You can install XDR Collectors in any Linux server period, whether its a physical or virtual machine. Temporary sessions can be in either of them.

{% hint style="info" %}
We recommend that you perform a Linux RPM or Linux DEB installation.
{% endhint %}

Before completing this task, ensure that you [create and download a Cortex XDR Collector installation package](create-an-xdr-collector-installation-package), and then upload these installation files to your Linux environment.

To install the XDR Collectors installation package for Linux.

To install the XDR Collectors installation package for Linux.

1.  Log on to the Linux server.

    For example:

    <pre><code>user@local ~
    						$
    <strong>						ssh root@ubuntu.example.com
    </strong>						Welcome to Ubuntu 16.04.3 LTS (GNU/Linux 4.4.0-1041-aws x86_64)

    						* Documentation:  https://help.ubuntu.com
    						* Management:     https://landscape.canonical.com
    						* Support:        https://ubuntu.com/advantage

    						Get cloud support with Ubuntu Advantage Cloud Guest:
    						http://www.ubuntu.com/business/services/cloud

    						0 packages can be updated.
    						0 updates are security updates.


    						Last login: Tue Aug 26 22:14:15 2021 from 192.168.1.100
    					
    </code></pre>
2.  Extract the installation files you uploaded using one of the following commands, which is dependent on the Linux package you downloaded:

    | Linux Package | Extract Command                           |
    | ------------- | ----------------------------------------- |
    | Linux RPM     | `tar xvf <installation_package_name>.rpm` |
    | Linux DEB     | `tar xvf <installation_package_name>.deb` |
    | Linux SH      | `tar xvf <installation_package_name>.sh`  |
3.  Create a directory and copy the `collector.conf` installation file to the `/etc/panw/` directory.

    ```
    sudo mkdir -p /etc/panw
    sudo cp ./collector.conf /etc/panw/
    ```
4.  Install the XDR Collectors software.

    You can install the XDR Collectors on the collector machine manually using the shell installer or using the Linux package manager for `.rpm` and `.deb` installers:

    When performing a XDR Collector installation or upgrade in Linux using a shell installer, the `/tmp` folder cannot be marked as `noexec`. Otherwise, the installation or upgrade fails. As a workaround, before the installation or upgrade, use the following command:

    ```
    mount -o remount,exec /tmp
    ```

#### To deploy using package manager:

1.  Depending on your Linux distribution, install the XDR Collectors using one of the following commands, where the `<file name>` is taken from the files provided in the downloaded Linux installation package:

    | Distribution     | Install Command                                                                                                           |
    | ---------------- | ------------------------------------------------------------------------------------------------------------------------- |
    | RHEL or Oracle   | <ul><li><code>yum install ./&#x3C;file_name>.rpm</code></li><li><code>rpm -i ./&#x3C;file_name>.rpm</code></li></ul>      |
    | Ubuntu or Debian | <ul><li><code>apt-get install ./&#x3C;file_name>.deb</code></li><li><code>dpkg -i ./&#x3C;file_name>.deb</code></li></ul> |
    | SUSE             | <ul><li><code>zypper install ./&#x3C;file_name>.rpm</code></li><li><code>rpm -i ./&#x3C;file_name>.rpm</code></li></ul>   |
2.  Verify the XDR Collectors was installed on the collector machine.

    Enter the following command on the collector machine:

    `dpkg -l | grep xdr-collector` or `rpm -qa | grep xdr-collector`.

#### To deploy the shell installer:

1. Enable execution of the script using the `chmod +x <file_name>.sh` command, where the `<file name>` is taken from the file provided in the downloaded Linux installation package.
2.  Run the install script as root or with root permissions.

    For example:

    <pre><code><strong>root@ubuntu:/home# chmod +x linux.sh								
    </strong><strong>root@ubuntu:/home# ./linux.sh
    </strong>																				Verifying archive integrity... All good.
    Uncompressing XDR-Collector version 1.0.0.467 100%
    Systemd: starting xdr-collector service
    Synchronizing state of xdr-collector.service with SysV service script with /lib/systemd/systemd-sysv-install.
    Executing: /lib/systemd/systemd-sysv-install enable xdr-collector
    Created symlink /etc/systemd/system/multi-user.target.wants/xdr-collector.service→ /lib/systemd/system/xdr-collector.service.
    						
    </code></pre>

{% hint style="info" %}
If the XDR Collector does not connect to Cortex XSIAM, verify your Internet connection on the collector machine. If the XDR Collector still does not connect, verify the installation package has not been removed from the Cortex XSIAM management console.
{% endhint %}

If you are using `rpm` or `deb` installers, you must also add these parameters to the `/etc/panw/collector.conf` file prior to installation.

| Option                                | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| ------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `--proxy-list "<proxyserver>:<port>"` | <p><strong>Proxy communication</strong></p><p>Configure the XDR Collector to communicate through an intermediary such as a proxy.</p><p>To enable the XDR Collector to direct communication to an intermediary, you use this installation option to assign the IP address and port number you want the XDR Collector to use. You can also configure the proxy by entering the FQDN and port number. When you enter the FQDN, you can use both lowercase and uppercase letters. Avoid using special characters or spaces.</p><p>Use double quotes (" ") to enclose the IP address and port number. Use commas to separate multiple addresses. For example:</p><p><code>--proxy-list "My.Network.Name:808, 10.196.20.244:8080"</code></p><p>After the initial installation, you can change the proxy settings from using the configuration XML.</p><p>The XDR Collector does not support proxy communication in environments where proxy authentication is required.</p> |
| `--data-path <directory path>`        | <p><strong>Directory path</strong></p><p>The path for persistence, content, Filebeat application data, and transaction data.</p><p><code>--data–path=/tmp/xdrLog</code></p>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
