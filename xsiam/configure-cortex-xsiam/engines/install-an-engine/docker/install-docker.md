---
description: Install Docker and verify required user permissions for Cortex XSIAM engines.
---

# Install Docker

Docker lets engines run Python and PowerShell integrations in a controlled environment. The Shell installer installs Docker automatically. For DEB and RPM installations, install Docker or Podman before installing the engine.

Cortex XSIAM supports the latest Docker Engine release and these corresponding Linux distributions:

* 5.3.15 and later
* 5.4.2 and later
* 5.5 and later

Older Docker Engine releases from the past 12 months are also supported. Known compatibility issues may require an upgrade before Support can assist.

#### Docker installation by operating system

* [Red Hat](#install-docker-distribution-for-red-hat-on-an-engine-server)
* [Ubuntu](https://docs.docker.com/engine/install/ubuntu/)
* [Amazon Linux](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/docker-basics.html#install_docker)
* [Oracle Linux](https://docs.oracle.com/en/operating-systems/oracle-linux/docker/)

{% hint style="info" %}
Red Hat Docker deployments need Mirantis Container Runtime (formerly Docker Engine- Enterprise). For Red Hat's Docker distribution, you need Mirantis Container Runtime (formerly Docker Engine - Enterprise) to run specific Docker-dependent integrations and scripts. For more information, see [Install Docker distribution for Red Hat on an engine server](install-docker-distribution-for-red-hat).

To use the Mirantis Container Runtime (formerly Docker Engine - Enterprise) follow the [deployment guide](https://docs.mirantis.com/welcome/mcr) for your operating system distribution.
{% endhint %}

#### Verify Docker user and permissions

Verify Docker user

If you installed an engine before installing Docker, verify the `demisto` operating system user is part of the Docker operating system group.

1.  Run **`id demisto`** verify. For example:

    ```
    id demisto
    uid=997(demisto) gid=997(demisto) groups=997(demisto),998(docker)
    ```

    If needed, add the demisto user to the operating system group:

    ```
    sudo groupadd docker
    sudo usermod -aG docker demisto
    ```

    Remove these keys from the engine configuration file.

    ```
    python.executable
    python.executable.no.docker
    ```

Verify user permissions

To verify that the operating system user (demisto) has the necessary permissions and can run Docker containers, run the following command from the OS command line.

**`sudo -u demisto docker run --rm -it demisto/python:1.3-alpine python --version`**

If everything is configured properly, you will receive the following output. `Python 2.7.14`.
