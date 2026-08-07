---
description: Install and configure Podman for Cortex XSIAM engines.
---

# Install Podman

When installing a new engine on RHEL 8 or later, the shell installer configures Podman automatically. There are some cases, however, where you might need to install Podman manually:

* When using an installation method other than the shell installer (e.g., an RPM package) on RHEL 8 or later.
* When the shell installer did not successfully install Podman.
* When you want to migrate from Docker to Podman for an existing Cortex XSIAM engine.

{% hint style="info" %}
This procedure is intended for RHEL 8 or later. It may not work for other operating system types.

Do not use [NAS storage](https://en.wikipedia.org/wiki/Network-attached_storage) for the $HOME directory. The directory needs to be a local directory for Podman to work.
{% endhint %}

1.  For RHEL 8, install Podman by typing the following commands:

    * **`sudo yum -y install slirp4netns fuse-overlayfs`**
    * **`sudo yum -y module install container-tools`**

    For RHEL 9 or later, install Podman by typing the following command:

    * **`sudo yum -y install slirp4netns fuse-overlayfs podman`**
2. Run the following commands:
   * **`sudo touch /etc/subuid /etc/subgid`**
   * **`sudo mkdir -p /home/demisto`**
   * **`sudo chown demisto:demisto /home/demisto`**
3.  Configure the **`unqualified-search-registries`** used by Podman.

    Podman by default uses the fedoraproject.org, redhat.com, and docker.io unqualified search registries. SinceCortex XSIAM images use only the docker.io registry, you can speed up download times for container images by setting **`unqualified-search-registries`** to just docker.io.

    1. Create or edit the **`/home/demisto/.config/containers/registries.conf`** config file.
    2.  In the file, set **`unqualified-search-registries = ["docker.io"]`**

        <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>If you edit the file with the <strong><code>root</code></strong> user, make sure to set the <strong><code>demisto</code></strong> user as file owner by running <strong><code>chown demisto:demisto /home/demisto/.config/containers/registries.conf</code></strong></p></div>
4.  Change the **`subuids`** and **`subgids`** by running the following command:

    **`sudo usermod --add-subuids 200000-265535 --add-subgids 200000-265535 demisto`**
5.  Migrate existing containers to Podman:

    **`sudo sh -c "cd /; runuser -u demisto -- podman system migrate"`**
6. Set the **`net.ipv4.ping-group-range`**, by typing the following commands:
   * **`sudo sh -c "echo 'net.ipv4.ping_group_range=0 2000000' > /etc/sysctl.d/demisto-ping.conf"`**
   * **`sudo sysctl -w "net.ipv4.ping_group_range=0 2000000"`**
7.  As root user, edit the following **`config`** file:

    **`/usr/local/demisto/d1.conf`**
8.  Change the **`"container.engine.type": "docker"`** to **`“podman"`**.

    If this line does not exist, add the following line to the file:

    **`"container.engine.type": "podman"`**

    ```
    "Server": {
                    "HttpsPort": "443",
                    "ProxyMode": true
            },
            "container": {
                                    "engine": {
                                            "type": "podman"
                                    }
            },
            "db": {
                    "index": {
                            "entry": {
                                    "disable": true
    ```
9.  If the engine is running, restart the service.

    **`sudo systemctl restart d1`**

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>If the Allow running multiple engines on the same machine option is selected, run the command:</p><p><strong><code>sudo systemctl restart d1_&#x3C;Engine _name></code></strong></p></div>
