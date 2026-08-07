# Check Docker hardening configurations

Check your Docker hardening configurations on an engine by running the **`!DockerHardeningCheck`** command in the Case/Issue War Room CLI. The results show the following:

* Non-root User
* Memory
* File descriptors
* CPUs
* PIDs

Before running the command, ensure that your engine is up and running.

1. Update the **`DockerHardeningCheck`** script to run on the engine.
   1. Go to Investigation & Response → Automation → Scripts → DockerHardeningCheck → Settings.
   2. In the Run on field select Single engine and from the list, select the engine you want to run the script.
   3. Save the script.
2. Verify the Docker container has been hardened according to recommended settings. In the Case/Issue War Room CLI, run the **`!DockerHardeningCheck`** command.

<br>
