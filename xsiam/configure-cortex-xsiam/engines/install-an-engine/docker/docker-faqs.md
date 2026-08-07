# Docker FAQs

<details>

<summary>Does Cortex XSIAM use COPY or ADD for building images?</summary>

Cortex XSIAM uses COPY for building images. The COPY instruction copies files from the local host machine to the container file system. Cortex XSIAM does not use the ADD instruction, which could potentially retrieve files from remote URLs and perform operations such as unpacking, introducing potential security vulnerabilities.

</details>

<details>

<summary>Should the <code>--restart</code> flag be used?</summary>

The `--restart` flag should not be used. Cortex XSIAM manages the lifecycle of Docker images and restarts images as needed.

</details>

<details>

<summary>Can we restrict containers from acquiring additional privileges by setting the no-new-privileges option?</summary>

Cortex XSIAM does not support the no-new-privileges option. Some integrations and scripts may need to change privileges when running as a non-root user (such as Ping).

</details>

<details>

<summary>Can we apply a daemon-wide custom seccomp profile?</summary>

The [default seccomp profile](https://docs.docker.com/engine/security/seccomp/) from Docker is strongly recommended. The default seccomp profile provides protection as well as wide application compatibility. While you can apply a custom seccomp profile, Cortex XSIAM cannot guarantee that it won't block system calls used by an integration or script. If you apply a custom seccomp profile, you need to verify and test the profile with any integrations or scripts you plan to use.

</details>

<details>

<summary>Can we use TLS authentication for Docker daemon configuration?</summary>

TLS authentication is not used, because Cortex XSIAM does not use Docker remote connections. All communication is done via the local Docker IPC socket.

</details>

<details>

<summary>How do we set the logging level to <code>info</code>?</summary>

Set the log level in the [Docker daemon configuration file](https://docs.docker.com/engine/reference/commandline/dockerd/#daemon-configuration-file).

</details>

<details>

<summary>Can we restrict Linux kernel capabilities within containers?</summary>

The default Docker settings (recommended) include 14 kernel capabilities and exclude 23 kernel capabilities. Refer to Docker’s [full list of runtime privileges and Linux capabilities](https://docs.docker.com/engine/reference/run/#runtime-privilege-and-linux-capabilities).

You can further exclude capabilities via advanced configuration, but will first need to verify that you are not using a script that requires the capability. For example, Ping requires **`NET_RAW`** capability.

</details>

<details>

<summary>Is the Docker health check option implemented at runtime?</summary>

The Cortex XSIAM tenant monitors the health of the containers and restarts/terminates containers as needed. The Docker health check option is not needed.

</details>

<details>

<summary>Can we enable live restore?</summary>

Live restore is not used. Cortex XSIAM uses ephemeral Docker containers. Every running container is stateless by design.

</details>

<details>

<summary>Can we restrict network traffic between containers?</summary>

Cortex XSIAM does not disable inter-container communication by default, as there are use cases where this might be needed. For example, a script communicating with a long running integration which listens on a port, may require inter-container communication. If inter-container communication is not required, it can be disabled by modifying the [Docker daemon configuration.](https://docs.docker.com/engine/reference/commandline/dockerd/)

</details>

<details>

<summary>Can we enable user namespace remapping?</summary>

Cortex XSIAM does not support user namespace remapping.

</details>

<details>

<summary>How do we configure auditing for Docker files and directories?</summary>

Auditing is an operating system configuration, and can be enabled in the operating system settings. Cortex XSIAM does not change the audit settings of the operating system.

</details>

<details>

<summary>Can we disable the userland proxy?</summary>

If the kernel supports hairpin NAT, you can disable docker userland proxy settings by modifying the [Docker daemon configuration](https://docs.docker.com/engine/reference/commandline/dockerd/).

</details>

<details>

<summary>Does Cortex XSIAM support the AppArmor profile?</summary>

Cortex XSIAM supports the default AppArmor profile (only relevant for Ubuntu with AppArmor enabled).

</details>

<details>

<summary>Does Cortex XSIAM support the SELinux profile?</summary>

Cortex XSIAM supports the default SELinux profile (only relevant for RedHat with SELinux enabled).

</details>

<details>

<summary>How does Cortex XSIAM handle secrets management?</summary>

For Docker swarm services, a secret is a blob of data, such as password, SSH private keys, SSL certificates, or other piece of data that should not be transmitted over a network or stored unencrypted in a Docker file or in your application’s source code. Cortex XSIAM manages integration credentials internally. It also supports using an [external credentials service](https://xsoar.pan.dev/docs/reference/articles/managing-credentials) such as CyberArk.

</details>
