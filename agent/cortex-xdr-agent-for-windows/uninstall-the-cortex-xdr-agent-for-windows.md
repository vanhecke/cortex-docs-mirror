# Uninstall the Cortex XDR agent for Windows

You can uninstall the Cortex XDR agent using any of the following methods on a Windows endpoint:

* Uninstall an agent or multiple agents from the management console. Refer to Uninstall the Cortex XDR Agent in the Administrator’s Guide for instructions.
* Manually uninstall the Cortex XDR agent for Windows. [How to manually uninstall Cortex XDR agent for Windows](#how-to-manually-uninstall-cortex-xdr-agent-for-windows)
* Use [Msiexec to uninstall the Cortex XDR Agent for Windows.](#how-to-uninstall-cortex-xdr-agent-for-windows-using-msiexec)

After you uninstall the agent, the endpoint is no longer protected by the Security policy of your company and the license returns to the pool of available licenses.

<details>

<summary>How to manually uninstall Cortex XDR agent for Windows</summary>

Use the following workflow to manually uninstall the Cortex XDR agent. If you intend to use Cytool in Step 1, make sure that you know the uninstall password before performing this procedure.

1. Use one of the following methods to disable the Cortex XDR agent security protection on the endpoint:
   * Run the **`Cytool protect disable`** command.
   * Apply an Agent Settings profile that disables XDR **Agent Tampering Protection** on the endpoint.
2. Select **Start** → **Control Panel** → (**Programs**) → **Programs and Features**.
3. Select **Cortex XDR** from the list and then **Uninstall**.
4. When prompted to continue uninstalling, click **Yes** and acknowledge any notifications.

</details>

<details>

<summary>How to uninstall Cortex XDR agent for Windows using Msiexec</summary>

Use the following workflow to uninstall the Cortex XDR agent using Msiexec. If you intend to use Cytool in Step 1, ensure that you know the uninstall password before performing this procedure.

1. If you are uninstalling XDR Agent using the MSI file via SCCM or another software management system, use one of the following methods to disable the Cortex XDR agent security protection on the endpoint:
   * Run the **`Cytool protect disable`** command.
   * Apply an Agent Settings profile that disables XDR **Agent Tampering Protection** on the endpoint.
2. Use one of the following options to open a command prompt as an administrator:
   * Select **Start** → **All** **Programs** → **Accessories**. Then right-click **Command prompt** and **Run as administrator**.
   * Select **Start**. In the **Start Search** box, type **cmd**. Then, to open the command prompt as an administrator, press **CTRL**+ **SHIFT**+ **ENTER**.
3.  Run the **`msiexec`** command followed by one or more of the following options or properties:

    *   Uninstall and logging options:

        * **`/x<installpath>\<installerfilename>.msi`**—Uninstall a package.
        * **`/l*v <logpath>\<logfilename>.txt`**—Log verbose output to a file.

        For a full list of Msiexec parameters, see [https://docs.microsoft.com/en-us/windows/desktop/Msi/command-line-options](https://docs.microsoft.com/en-us/windows/desktop/Msi/command-line-options)

    For example, to uninstall the Cortex XDR agent using the cortexxdr.msi installer with the specified password and log verbose output to a file called uninstallLogFile.txt, enter the following command:

    ```screen
    C:\Users\username>msiexec /x c:\install\cortexxdr.msi /l*v c:\install\uninstallLogFile.txt 
                      
    ```

</details>
