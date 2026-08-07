# Change the Docker Installation folder

The **`/var/lib/docker/`** folder is the default Docker folder for Ubuntu, Fedora, and Deblan in a standard engine installation, used to store container images and logs.

To change the Docker folder:

1.  Stop the Docker daemon.

    **`sudo service docker stop`**
2.  Create a file called **`daemon.json`** under the **`/etc/docker`** directory with the following content:

    ```
    {
            "data-root": "<path to your Docker folder>"
      }
    ```
3.  Copy the current data directory to the new one.

    **`sudo rsync -aP /var/lib/docker/ <path to your Docker folder>`**
4.  Rename the old docker directory.

    **`sudo mv /var/lib/docker /var/lib/docker.bkp`**
5.  After confirming that the change was successful, you can remove the backup file.

    **`sudo rm -rf /var/lib/docker.bkp`**
6.  Start the Docker daemon.

    **`sudo service docker start`**
