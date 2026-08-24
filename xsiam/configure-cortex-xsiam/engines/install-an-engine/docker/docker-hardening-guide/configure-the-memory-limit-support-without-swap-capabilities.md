---
description: Configure Docker memory limits without swap support for Cortex XSIAM engines.
---

# Configure the memory limit support without swap capabilities

When a container exceeds the specified amount of memory, the container starts to swap. Not all Linux distributions have the swap limit support enabled by default.

* Red Hat distributions usually have swap limit support enabled by default.
* Ubuntu distributions usually have swap limit support disabled by default.

To protect the host from a container using too many system resources (either because of a software bug or a DoS attack), limit the resources available for each container. In the engine configuration file, some of these settings are set using the advanced parameter: **`python.pass.extra.keys`**. This key receives as a parameter full **`docker run`** options, separated with the **`##`** string.

How to check if your system supports swap limit capabilities

1.  On the engine machine, run the following command:

    **`sudo docker run --rm -it --memory=1g demisto/python:1.3-alpine true`**
2. If **`swap limit capabilities`** is enabled, configure the memory limitation. (To test the memory, see step 5 of [configure the memory limitation](configure-the-memory-limitation).)
3.  If you see the following message in the output (the message may vary between Docker versions):

    **`WARNING: Your kernel does not support swap limit capabilities or the cgroup is not mounted. Memory limited without swap.`**

    You have 2 options:

    * Configure **`swap limit capabilities`** by following the [Docker documentation](https://docs.docker.com/config/containers/resource_constraints/).
    * See [Docker hardening guide]().

    If you see the **`WARNING: No swap limit support`** you can configure memory support without swap limit capabilities.

How to configure the memory limit support without swap limit capabilities

1. Edit the engine configuration file either by editing the `d1.conf` file, or If you installed via Shell, you can edit the configuration in the UI as well as editing the file directly. For details, see [Configure engines](../../../configure-engines).
2.  Add the following key to disable swap memory enforcement:

    **`"python.pass.extra.keys": "--memory=1g##--memory-swap=-1"`**

    If you have the **`python.pass.extra.keys`** already set up with a value, add the value after the **`##`** separator.
3. Save the changes.
4.  Restart the demisto service on the engine machine.

    **`sudo systemctl start d1`**

    (Ubuntu) **`sudo service d1 restart`**
