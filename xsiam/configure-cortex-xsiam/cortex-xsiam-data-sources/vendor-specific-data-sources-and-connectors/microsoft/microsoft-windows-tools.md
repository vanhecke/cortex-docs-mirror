# Microsoft Windows Tools

{% hint style="warning" %}
**Important**

This connector is only available for tenants that onboarded after July 26, 2026. For tenants that onboarded before this date, use Marketplace to access the standalone integration. For more information, see Marketplace.
{% endhint %}

This sub-capability is available with any active Cortex XSIAM or Cortex AgentiX license.

Connect to Windows hosts to run scripts and commands remotely for tasks such as acquiring forensic data, gathering information, and remediating hosts. Uses PowerShell Remoting (built on the Windows Management Framework and Windows Remote Management) and the pywinrm library to create remote sessions and execute processes or PowerShell scripts.

This connector includes the following sub-capabilities (Marketplace integrations link to PAN DEV for more information):

* [PowerShell Remoting](https://xsoar.pan.dev/docs/reference/integrations/power-shell-remoting): PowerShell Remoting is a comprehensive built-in remoting subsystem that is a part of Microsoft's native Windows management framework (WMF) and Windows remote management (WinRM).\
  This feature allows you to handle most remoting tasks in any configuration you might encounter by creating a remote PowerShell session to Windows hosts and executing commands in the created session.\
  The integration includes out-of-the-box commands which supports agentless forensics for remote hosts.
* [Windows Remote Management](https://xsoar.pan.dev/docs/reference/integrations/windows-remote-management): Uses the Python pywinrm library and commands to execute either a process or using Powershell scripts.

To configure this connector, follow the steps outlined in the configuration wizard.
