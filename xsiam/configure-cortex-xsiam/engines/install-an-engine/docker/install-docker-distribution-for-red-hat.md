---
description: >-
  Install Docker and configure SELinux on Red Hat servers for Cortex XSIAM
  engines.
---

# Install Docker distribution for Red Hat

Red Hat maintains its own package of Docker, which is the version used in OpenShift Container Platform environments, and is available in the RHEL Extras repository.

If running RHEL v8 or higher, the engine installs [Podman](../podman/install-podman) packages and configures the operating system to enable Podman in rootless mode.

For more information about the different packages available to install on Red Hat, see the [Red Hat Knowledge Base Article](https://access.redhat.com/solutions/3092401) (requires a Red Hat subscription to access).

1. Install [Red Hat’s Docker package](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux_atomic_host/7/html-single/getting_started_with_containers/index#using_the_docker_command_and_service).
2.  Run the following commands.

    **`systemctl enable docker.service`**

    **`systemctl restart docker.service`**
3. Change ownership of the Docker daemon socket so members of the **`dockerroot`** user group have access.
   1. Edit or create the file `/etc/docker/daemon.json`.
   2.  Enable OS group **`dockerroot`** access to Docker by adding the following entry to the `/etc/docker/daemon.json: "group": "dockerroot"`file. For example:

       **`{ "group": "dockerroot" }`**
   3.  Restart the Docker service by running the following command.

       **`systemctl restart docker.service`**
   4. [Install the engine](..)
   5.  After the engine is installed, run the following command to add the **`demisto`** os user to the **`dockerroot`** os group (Red Hat uses dockerroot group instead of docker).

       **`usermod -aG dockerroot demisto`**
   6. Restart the engine.
4.  Set the required SELinux permissions.

    The Cortex XSIAM engine uses the `/var/lib/demisto/temp` directory (with subdirs) to copy files and receive files from running Docker containers. By default, when SELinux is in **enforcing** mode, directories under **`/var/lib/`** it cannot be accessed by Docker containers.

    1.  To allow containers access to the `/var/lib/demisto/temp` directory, you need to set the correct SELinux policy type, by typing the following command.

        **`chcon -Rt svirt_sandbox_file_t /var/lib/demisto/temp`**
    2.  ( Optional) Verify that the directory has the **`container_file_t`** SELinux type attached by running the following command.

        **`ls -d -Z /var/lib/demisto/temp`**
    3.  Configure label confinement to allow Python and PowerShell containers to access other script folders.

        In the d1.conf file, set the following parameters:

        |                           | Key                        | Value                                   |
        | ------------------------- | -------------------------- | --------------------------------------- |
        | For Python containers     | python.pass.extra.keys     | --security-opt=label=level:s0:c100,c200 |
        | For PowerShell containers | powershell.pass.extra.keys | --security-opt=label=level:s0:c100,c200 |
    4. Open any issue and in the issue War Room CLI, run the **`/reset_containers`** command.
