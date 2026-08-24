---
description: Uninstall an XDR Collector from Cortex XSIAM.
---

# Uninstall the XDR Collector

If you want to uninstall the XDR Collector from the on-premise collector machine, you can do so from the XDR Collectors console at any time. You can uninstall the XDR Collector from an unlimited number of collector machines in a single bulk action. Uninstalling a collector machine triggers the following lifespan flow:

* Once you uninstall the XDR Collector from the on-premise collector machine, Cortex XSIAM distributes the uninstall to the selected collector machine at the next heartbeat communication with the XDR Collector. All XDR Collector files are removed from the collector machine.
* The collector machine status changes to `Uninstalled`. After a retention period of 7 days, the XDR Collector is deleted from the database and is displayed in XDR as Collector Machine Name - `N/A (Uninstalled)`.
* Data associated with the deleted on-premise collector machine is displayed in the Action Center tables for the standard 90 days retention period.

The following workflow describes how to uninstall the XDR Collector from one or more Windows or Linux on-premise collector machines.

1. Select Settings → Configurations → XDR Collectors → Administration.
2. Select the collector machines you want to uninstall. You can also select collector machines running different operating systems to uninstall the XDR Collectors at the same time.
3. Right-click your selection and select Uninstall Collector.
4. To proceed, select I agree to confirm that you understand this action uninstalls the XDR Collector on all selected collector machines.
5. Click OK.\
   To monitor the status of the uninstall process, go to Investigation & Response → Response → Action Center.
