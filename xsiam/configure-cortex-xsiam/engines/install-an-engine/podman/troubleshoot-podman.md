---
description: Resolve common Podman issues on Cortex XSIAM engines.
---

# Troubleshoot Podman

<details>

<summary>dbus-daemon process leak</summary>

Podman version 3.4.1 and lower has a [known issue](https://github.com/containers/podman/issues/9727) that dbus-daemon processes may leak when running in an environment containing the dbus-x11 OS package. The issue occurs when the dbus-x11 OS package is installed, for example, when installing an X11 desktop environment like GNOME desktop on the host machine. If you experience this issue, you see a large number of dbus-daemon processes owned by the demisto OS user. To check if you are affected by the issue, run the following command:

**`ps -fe | grep demisto | grep dbus-daemon`**

To fix this issue:

1.  Remove the dbus-x11 OS package and dependent packages by running the following command:

    **`sudo yum remove dbus-x11`**
2.  After removal you can kill the leaked dbus-daemon processes by running the following OS command:

    **`pgrep -u demisto dbus-daemon | xargs sudo kill`**

</details>

<details>

<summary>Invalid argument error</summary>

When Podman fails to run with an “Invalid argument” error, such as:

```
ERRO[0000] running `/usr/bin/newuidmap 15936 0 1029 1 1 165536 65536 65537 200000 65536`: newuidmap: write to uid_map failed: Invalid argument
Error: cannot set up namespace using "/usr/bin/newuidmap": exit status 1
```

This can be caused by duplicate lines for Cortex XSIAM in `/etc/subuid` and `/etc/subgid`.

To fix this issue:

1.  Check if the `/etc/subuid` file contains multiple lines that start with the Cortex XSIAM username (usually demisto). For example:

    ```
    alice:100000:65536
    demisto:165536:65536
    demisto:200000:65536
    splunk:331072:65536
    ```
2.  If this is the case, edit the file as root, and remove the extra line(s) for Cortex XSIAM. The line you should keep is the one that ends with 200000:65536. Continuing with the above example, here is the end result:

    ```
    alice:100000:65536
    demisto:200000:65536
    splunk:331072:65536
    ```
3. Repeat the above steps for the `/etc/subgid` file.

</details>

<details>

<summary>Verify Podman installation</summary>

When encountering errors in Cortex XSIAM that are Podman related, such as:

* **`failed to run "docker ps". stderr: [], err: [Timeout. Process killed (1400)`**
* **`Timeout while waiting for pong response [error 'Read timed out (15s)`**
* **`Error: error joining network namespace of container 06b8aec6eabe2e735128e3a72cb06c8ae2d97ade60a56ab555034442ea4e2a84: error retrieving network namespace at /tmp/podman-run-989/netns/cni-86dca01c-bd84-1aaf-85fb-72b659a8e42a: unknown FS magic on "/tmp/podman-run-993/netns/cni-86dca01c-bd84-1aaf-85fb-72b659a8e42a": 58465342`**

1.  Verify that Podman is running properly with the **`demisto`** OS user by performing the following steps:

    *   Change the OS user to **`demisto`** by running the following command:

        **`sudo su - -s /bin/bash demisto`**
    *   Check that your system complies with the minimum requirements, and view general system information such as host architecture, CPU, OS, registries, container storage path, etc., by running the following command:

        **`podman info`**
    *   Check all active running containers, container names, and IDs by running the following command:

        **`podman ps`**
    *   Check that Podman can run a container by running the following command:

        **`podman run --rm -t demisto/python3:3.10.4.29342 echo "podman is working"`**

    If any of the Podman commands are not working, try running with the **`--log-level=debug`** to receive additional details as to why it is failing. For example:

    `podman --log-level=debug ps`

    `podman --log-level=debug ps podman --log-level=debug run --rm -t demisto/python3:3.10.4.29342 echo "podman is working"`
2.  Reset the Podman Data Directories.

    If the Podman commands in step 1 are failing, you should clean the Podman working directories. Sometimes Podman's data directories get corrupted (for example, as a result of insufficient disk space).

    <div data-gb-custom-block data-tag="hint" data-style="warning" class="hint hint-warning"><p>This step removes all Podman images, including any custom images you may have created.</p></div>

    1.  Stop the engine by running the following command:

        **`sudo systemctl stop d1`**
    2.  Ensure that all Podman containers of the **`demisto`** user are stopped by running the following command:

        **`ps -fe | grep demisto | grep 'podman run'`**

        If required, kill the running containers.
    3.  Delete the following directories (assuming the **`demisto`** OS user's home directory is at: /home/demisto)

        * **`sudo rm -rf /home/demisto/.cache/containers/`**
        * **`sudo rm -rf /home/demisto/.local/share/containers/`**
        * **`sudo rm -rf /tmp/podman-run-$(id -u demisto)`**
        * **`sudo rm -rf /tmp/containers-user-$(id -u demisto)`**
        * **`sudo rm -rf /tmp/tmp/run-$(id -u demisto)`**

        <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong><code>$(id -u demisto)</code></strong> is used to get the <strong><code>demisto</code></strong> user ID, which is part of the directory name. For example, <strong><code>/tmp/podman-run-993</code></strong></p><p>Not all the directories above may be present.</p></div>
    4.  Start the engine by running the following command:

        **`sudo systemctl start d1`**
    5. Verify that Podman is working properly with the **`demisto`** OS user by following step 1.

</details>

<details>

<summary>Unused containers consume resources</summary>

In some cases, if the Podman process crashes or is killed abruptly, it can leave containers on disk. You might see errors such as `error allocating lock for new container: allocation failed; exceeded num_lock` when the maximum number of locks used to manage containers is exhausted due to the unused containers that remain.

1. Change to the demisto operating system user `sudo su - -s /bin/bash demisto`.
2. Run `podman ps -a -f status=exited` to check for unused containers.
3.  Clean up the unused containers `podman container cleanup --rm -a`.

    When you run `podman container cleanup --rm -a`, you might see a message such as `running or paused containers cannot be moved without force`. The message can be safely ignored, as it only pertains to current running containers, which are not removed.
4. After cleanup, verify there are no remaining unused containers `podman ps -a -f status=exited`.

</details>

<details>

<summary>Keyring quota exceeded</summary>

`Script failed to run: Docker code runner got container error: [Docker code script is in inconsistent state, ... error: [exit status 126] stderr: [Error: OCI runtime error: crun: create keyring ...: Disk quota exceeded]`

By default, Podman creates a `keyring` that is used by each container. The limit per user on the machine might be low, and Podman can reach the limit when running more containers than the `keyring` limit. To check the `keyring` usage, run the **`sudo cat /proc/key-users`** operating system command.

The command returns the usage for each UID (to retrieve the demisto user UID, run **`id demisto`** ). The fourth column shows the number of keys used out of the total number available. For more information about keys, see [Kernel Key Retention Service](https://www.kernel.org/doc/Documentation/security/keys.txt).

You can either increase the limit of max keyrings (increasing to 1000 is safe and reasonable) per user, as specified by your Linux vendor documentation or you can disable keyring creation by Podman. We recommend disabling keyring creation unless keyrings are used by Podman in other applications on the machine. To disable keyring creation by Podman, modify the `containers.conf` file and add the option `keyring = false` under the `"[containers]"` section. For more information, see the [Containers Engine Configuration File](https://github.com/containers/common/blob/main/docs/containers.conf.5.md).

</details>

<details>

<summary>error "exit status 125" and output "Error: chown...operation not permitted"</summary>

If the container storage directory is not owned AND exclusively used by the demisto user, scripts will fail to run. See the Podman section for more information about assigning ownership of the storage directory.

</details>

<details>

<summary>Report a support case for installation issues</summary>

If the procedure set out in the Verify Podman installation section above does not solve the Podman issue and you require assistance from Support, do the following:

1. Include the following files as part of the support case:
   * **`/etc/containers/storage.conf`**
   *   **`/home/demisto/.config/containers/storage.conf`**

       If the file does not exist, indicate that there is no such file.
   *   **`/home/demisto/.config/containers/registries.conf`**

       If the file does not exist, indicate that there is no such file.
2.  Include the output of the following commands as the **`demisto`** user.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>To change to the <strong><code>demisto</code></strong> OS user, run the following command:</p><p><strong><code>sudo su - -s /bin/bash demisto</code></strong></p><ul><li><strong><code>podman info</code></strong></li><li><strong><code>podman images</code></strong></li><li><strong><code>podman --log-level=debug ps</code></strong></li><li><strong><code>podman --log-level=debug run --rm -t demisto/python3:3.10.4.29342 echo "podman is working</code></strong></li></ul></div>

</details>

<details>

<summary>Permission issues with directories under the /run path</summary>

When installing a Cortex XSIAM engine on a RHEL system (version 8 or later), or when running an integration on such an engine, you get a permission error for a path under `/run` (for example `/run/user/0` or `/run/libpod`).

1.  In RHEL 9 only: Make sure the `container-tools` meta-package is installed by running:

    `yum -y install container-tools`
2. Run the following commands:
   * `cp /etc/containers/storage.conf /home/demisto/.config/containers/storage.conf`
   * `chown demisto:demisto /home/demisto/.config/containers/storage.conf`
   * `chmod 600 /home/demisto/.config/containers/storage.conf`
3. Edit `/home/demisto/.config/containers/storage.conf`.
   *   Under `[storage]`, change `runroot` to some temporary directory that is accessible by user `demisto`.

       For example: `runroot = "/tmp/podman-run-xsiam"`

       <div data-gb-custom-block data-tag="hint" data-style="warning" class="hint hint-warning"><p>The <code>runroot</code> must be located under the <code>tmpfs</code> file system type. This is required to clean Podman's run state on reboot and for performance reasons.</p></div>
   *   Also under `[storage]`, change `graphroot` (where container images are stored) to any location that is owned and accessible by user `demisto`. We recommend using this standard path:

       `graphroot = "/home/demisto/.local/share/containers/storage"`

       <div data-gb-custom-block data-tag="hint" data-style="warning" class="hint hint-warning"><p>Unlike the <code>runroot</code>, the <code>graphroot</code> must NOT be located under the <code>tmpfs</code> file system type. Using <code>tmpfs</code> for the <code>graphroot</code> might corrupt container images, causing command executions to fail. It also degrades performance by forcing Podman to needlessly re-pull images.</p></div>
   *   Under `[storage.options.overlay]`, uncomment the following line (remove the # from the start):

       `mount_program = "/usr/bin/fuse-overlayfs"`
4.  Save the file and run the following.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>You must switch to user <code>demisto</code> before running the "system migrate" (running it as root will have no effect).</p></div>

    * `su - demisto`
    * `podman system migrate`
5.  Also as user `demisto`, run the following to ensure the path changes were applied:

    `podman info | grep Root`

    You should see the correct runRoot and graphRoot settings.
6.  As user `demisto`, verify the issue is resolved by running:

    `podman run hello-world`
7.  If the issue persists, purge Podman's database by running the following:

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>The "system migrate" must be done by the user demisto.</p></div>

    * `rm -rf /home/demisto/.local/share/containers/*`
    * `podman system migrate`

</details>
