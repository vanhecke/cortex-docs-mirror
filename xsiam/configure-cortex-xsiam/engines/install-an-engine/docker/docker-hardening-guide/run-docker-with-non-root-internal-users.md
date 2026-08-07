# Run Docker with non-root internal users

For additional security isolation, we recommend to run Docker containers as non-root internal users. This follows the principle of least privilege.

1. Edit the engine configuration file either by editing the `d1.conf` file, or If you installed via Shell, you can edit the configuration in the UI as well as edit the file directly. For details, see [Configure engines](../../../configure-engines).
2.  Add the following key:

    **`"docker.run.internal.asuser": true`**
3.  For containers that do not support non-root internal users, add the following key:

    **`"docker.run.internal.asuser.ignore" : "`**_**`A comma separated list of container names. The engine matches the container names according to the prefixes of the key values>`**_**`"`**

    For example, **`"docker.run.internal.asuser.ignore"="demisto/python3:","demisto/python:"`**

    The engine matches the key values for the following containers:

    ```
    demisto/python:1.3-alpine
    demisto/python:2.7.16.373
    demisto/python3:3.7.3.928
    demisto/python3:3.7.4.977
    ```

    The **`:`** character should be used to limit the match to the full name of the container. For example, using the **`:`** character does not find **`demisto/python-ubuntu:2.7.16.373`**.
4. Save the changes.
5.  Restart the demisto service on the engine machine.

    **`sudo systemctl start d1`**

    (Ubuntu) **`sudo service d1 restart`**
