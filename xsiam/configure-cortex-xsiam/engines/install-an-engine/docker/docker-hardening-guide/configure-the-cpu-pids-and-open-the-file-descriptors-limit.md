# Configure the CPU, PIDs, and open the file descriptors limit

Set the advanced parameters to configure the CPU limit, PIDs limit, and the open file descriptor limit.

1. Edit the engine configuration file either by editing the `d1.conf` file, or if you installed via Shell, you can edit the configuration in the UI as well as edit the file directly. For details, see [Configure engines](../../../configure-engines).
2.  Add the following keys:

    | Parameter                   | Key                                                                                                                                                                      |
    | --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
    | Available CPU limit         | **`"limit.docker.cpu": true, "docker.cpu.limit": "`**_**`<CPU Limit>`**_**`"`** We recommend to limit each container to 1 CPU. (For example, **`1.0`**. Default is 1.0). |
    | PIDs limit                  | **`"python.pass.extra.keys": "--pids-limit=256"`**                                                                                                                       |
    | Open file descriptors limit | **`"python.pass.extra.keys": "--ulimit=nofile=1024:8192"`**                                                                                                              |
3. Save the changes.
4.  Restart the demisto service on the engine machine.

    **`sudo systemctl start d1`**

    (Ubuntu) **`sudo service d1 restart`**
