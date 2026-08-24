---
description: Configure Docker images securely for Cortex XSIAM engine deployments.
---

# Configure Docker images

You can apply more specific, fine-tunedimage-specific settings to Docker images, according to the Docker image name or the Docker image name including the image tag. To apply settings to a Docker image name, add the advanced configuration key to the engine configuration file. If you apply Docker image specific settings, they will be used instead of the general **`python.pass.extra.keys`** setting. This overrides the general memory and CPU settings, as needed.

1. Edit the engine configuration file either by editing the `d1.conf` file, or if you installed via Shell, you can edit the configuration in the UI as well as edit the file directly. For details, see [Configure engines](../../../configure-engines).
2.  Add the following key to apply settings to a Docker image name.

    **`"python.pass.extra.keys.<image_name>"`**

    For example, **`"python.pass.extra.keys.demisto/dl"`**.

    *   To apply settings to a Docker image name, including the image tag, use **`"python.pass.extra.keys.<image_name>": "<image_tag>"`**.

        For example, **`"python.pass.extra.keys.demisto/dl": "1.4"`**.
    * To set the Docker images **`demisto/dl`** (all tags) to use a higher max memory value of 2g and to remain with the recommended PIDs and ulimit, add the following to the configuration file:**`"python.pass.extra.keys.demisto/dl": "--memory=2g##--ulimit=no- file=1024:8192##--pids-limit=256"`**
3. Save the changes.
4.  Restart the demisto service on the engine machine.

    **`sudo systemctl start d1`**

    (Ubuntu) **`sudo service d1 restart`**
