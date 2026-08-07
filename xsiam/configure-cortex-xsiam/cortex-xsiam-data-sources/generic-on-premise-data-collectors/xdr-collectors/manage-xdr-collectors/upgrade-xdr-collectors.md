# Upgrade XDR Collectors

After you install the Cortex XDR Collector and the XDR Collector registers with Cortex XSIAM, you can upgrade the XDR Collector software for on-premises Windows or Linux collector machine. You need to create a new installation packages and push the XDR Collector package to up to 500 collector machines from Cortex XSIAM.

1. Create an XDR Collector Installation Package for each operating system version where you want to upgrade the XDR Collector. Note the installation package names.
2. Select Settings → XDR Collectors → Administration. If needed, filter the list of on-premises collector machines. To reduce the number of results, use the collector machine name search and filters at the top of the page.
3. Select the collector machines that you want to upgrade. You can also select collector machines running different operating systems to upgrade the XDR Collectors at the same time.
4. Right-click your selection, and select Upgrade Collector version. For each platform, select the name of the installation package you want to push to the selected on-premises collector machines.\
   Note The XDR Collector keeps the name of the original installation package after every upgrade.
5. Upgrade.\
   Cortex XSIAM distributes the installation package to the selected collector machine at the next heartbeat communication with the XDR Collector. To monitor the status of the upgrades, go to Investigation & Response → Response → Action Center. From the Action Center you can also view additional information about the upgrade (right-click the action and select Additional data) or cancel the upgrade (right-click the action and select Cancel Collector Upgrade).
