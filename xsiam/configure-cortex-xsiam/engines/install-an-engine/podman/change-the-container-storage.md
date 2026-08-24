---
description: Configure Podman container storage for Cortex XSIAM engines.
---

# Change the Container storage

By default, Podman uses the **`$HOME/.local/share/containers/storage`** directory. To use a different directory for container storage, edit the [Podman config file](https://github.com/containers/podman/blob/main/vendor/github.com/containers/storage/storage.conf#L33) located at **`/home/demisto/.config/containers/storage.conf`**. If the Podman config file does not exist, you need to create it and change the ownership.

The new storage directory needs to be owned by the **demisto** user, otherwise, they will be denied access to it.

{% hint style="warning" %}
Do not use NAS storage or a temporary (tmpfs) directory for the **`graphroot`** setting. The **`graphroot`** needs to be a local, non-temporary directory for Podman to work. For more information, see [https://en.wikipedia.org/wiki/Network-attached\_storage](https://en.wikipedia.org/wiki/Network-attached_storage).
{% endhint %}

{% hint style="info" %}
We recommend reserving 150 GB for container storage, either in the /home partition or a different storage directory that you have set using the **`graphroot`** key.
{% endhint %}

1. If the Podman config file does not exist:
   1.  Create the Podman config file.

       **`sudo mkdir -p /home/demisto/.config/containers`**

       **`cp /etc/containers/storage.conf /home/demisto/.config/containers`**
   2.  Change the ownership of the Podman config file.

       **`sudo chown -R demisto:demisto /home/demisto`**
2.  To set a different directory for container storage, change the key: **`graphroot`** in the **`storage.conf`** file. For example:

    **`graphroot = "/var/lib/containers/cortex-storage"`**
3.  Some additional changes are required in the storage.conf file. Comment out the **`runroot`** setting by adding a **`#`** (hash) before it. For example:

    **`#runroot = "/run/containers/storage"`**

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>Alternatively, the <strong><code>runroot</code></strong> setting may be set to some temporary directory that is accessible by the user demisto. If you choose to set the <strong><code>runroot</code></strong>, it must be a directory that is mounted as tmpfs (temporary filesystem), unlike the graphroot.</p></div>
4.  Under \[storage.options.overlay], uncomment the following line (remove the # from the start):

    **`mount_program = "/usr/bin/fuse-overlayfs"`**
5.  If the engine has already been installed, apply your changes to any existing containers:

    **`sudo -u demisto podman system migrate`**
6.  Verify the change (once the engine is installed):

    **`sudo -u demisto podman info | grep graph`**
