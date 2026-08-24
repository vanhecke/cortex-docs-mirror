---
description: Troubleshoot integrations that run on Cortex XSIAM engines.
---

# Troubleshoot integrations running on engines

The following are common errors that occur when integrations are running on an engine.

<details>

<summary>Troubleshoot engine import error or invalid syntax error</summary>

When running an integration on an engine, the most common errors are:

* **`Broken Pipe`**
* **`"ImportError: No module named...`**
* **`Invalid syntax`**
* **`Script failed to run: exec: “python”: executable file not found in $PATH (2603)`**

These errors could indicate that the engine is not using Docker.

1. Use SSH to access the engine server.
2. Make sure Docker is healthy.
   1.  Ensure that Docker is installed and is running.

       **`sudo systemctl status docker`**

       If the Docker status is not good, restart your Docker.

       **`sudo systemctl restart docker`**
   2.  Ensure Docker can run a container.

       **`sudo docker run hello-world`**

       If this fails, reinstall your Docker.
3.  Access the d1.conf file on the engine server.

    **`sudo vi /usr/local/demisto/d1.conf`**
4. Add the **`"python.engine.docker": true`** configuration to the d1.conf file and remove any other configurations related to python and Docker, such as **`“python.executable.no.docker”`**.
5.  Restart the system on the engine server.

    **`sudo systemctl restart d1`**

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>If the <strong>Allow running multiple engines on the same machine</strong> option is selected, run the command:</p><p><strong><code>sudo systemctl restart d1_&#x3C;Engine _name></code></strong></p></div>
6. Retest the integration from the user interface. This may take a few minutes because it may need to pull the relevant Docker image.

</details>

<details>

<summary>Troubleshoot permission denied</summary>

A common error message you may see when running integrations on engines is something like: **`Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get http://%2Fvar%2Frun%2Fdocker.sock/v1.35/images/json?t.`**

1.  Determine if you are using a Docker group or Dockerroot group by running one of the following on the server engine:

    *   **`ls -la /var/run/docker.sock`**

        The output from this command will show what user/group is running docker.sock. For example:

        ```programlisting
        srw-rw----. 1 root docker 0 Apr 12 20:32 /var/run/docker.sock
        ```

        shows that it’s a Docker group and not Dockerroot.
    *   **`cat /etc/group | grep docker`**

        This command shows if you are running Docker or Dockerroot.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>Docker CE installations typically run Docker, while Docker EE installations typically run dockerroot.</p></div>
2. To fix a Docker user, run the following commands on the server engine:
   1. **`sudo groupadd docker`**
   2. **`sudo usermod -aG docker demisto`**
   3. **`sudo systemctl restart docker`**
   4.  **`sudo systemctl restart d1`**

       <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>If the <strong>Allow running multiple engines on the same machine</strong> option is selected, run the command:</p><p><strong><code>sudo systemctl restart d1_&#x3C;Engine _name></code></strong></p></div>
3. To fix a `dockerroot` user, run the following commands on the server engine:
   1. **`sudo groupadd dockerroot`**
   2. Set the dockerroot group in `/etc/docker/daemon.json`. For example: { "group": "dockerroot" }.
   3. **`sudo usermod -aG dockerroot demisto`**
   4. **`sudo chcon -Rt svirt_sandbox_file_t /var/lib/demisto/temp`**
   5. **`sudo systemctl restart docker`**
   6.  **`sudo systemctl restart d1`**

       <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>If the <strong>Allow running multiple engines on the same machine</strong> option is selected, run the command:</p><p><strong><code>sudo systemctl restart d1_&#x3C;Engine _name></code></strong></p></div>

</details>
