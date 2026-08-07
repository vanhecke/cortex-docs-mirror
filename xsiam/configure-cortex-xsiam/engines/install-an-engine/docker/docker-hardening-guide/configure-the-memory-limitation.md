# Configure the memory limitation

We recommend limiting available memory for each container to 1 GB.

If **`swap limit capabilities`** is enabled (see **How to check if your system supports swap limit capabilities** above), in Cortex XSIAM configure the memory limitation using the following advanced parameters.

1. Edit the engine configuration file either by editing the `d1.conf` file, or If you installed via Shell, you can edit the configuration in the UI as well as editing the file directly. For details, see [Configure engines](../../../configure-engines).
2.  Add the following keys.

    **`"limit.docker.memory": true, "docker.memory.limit": "1g"`**

    If you do not want to apply Docker memory limitations, you should explicitly set the advanced parameter: **`limit.docker.memory`** to **`false`**.
3. Save the changes.
4.  Restart the demisto service on the engine machine.

    **`sudo systemctl start d1`**

    (Ubuntu) **`sudo service d1 restart`**
5. Test the memory limit.
   1. Go to Investigation & Response → Automation → Scripts → New Script.
   2. In the Script Name file, type **`TestMemory`**.
   3.  Add the following script:

       ```
       from multiprocessing import Process
       import os


       def big_string(size):
           sys.stdin = os.fdopen(0, "r")
           s = 'a' * 1024
           while len(s) < size:
               s = s * 2
           print('completed creating string of length: {}'.format(len(s)))


       size = 1 * 1024 * 1024 * 1024
       p = Process(target=big_string, args=(size, ))
       p.start()
       p.join()
       if p.exitcode != 0:
           return_error("Return code from sub process indicates failure: {}".format(p.exitcode))
       else:
           print("Success allocating memory of size: {}".format(size))
       ```
   4. In the SCRIPT SETTINGS section, select the script to run on the Single engine and select the engine where you want to run the script.
   5. Save the script.
   6. To test the memory limit, type **`!TestMemory`**. The command returns an error when it fails to allocate 1 GB of memory.
