---
description: >-
  Investigate IP address activity, threat intelligence, and related cases in
  Cortex XSIAM.
---

# Investigate an IP address

Drill down on an IP address on the **IP View**. On this view, you can investigate and take actions on IP addresses, and see detailed information about an IP address over a defined 24-hour or 7-day time frame. In addition, to help you determine whether an IP address is malicious, the **IP View** displays an interactive visual representation of the collected activity for a specific IP address.

### How to investigate an IP address

1.  Open the **IP View**.

    Right-click the IP address that you want to investigate and select **Open IP View**.
2.  In the left panel, review the overview of the IP address.

    The overview displays network operations, cases, actions, and threat intelligence information relating to the selected IP address, and provides a summary of the network operations and processes related to the IP address.

    The displayed information and available actions are context-specific.

    1. Add an **Alias** or **Comment** to the IP address.
    2. Review the location of the IP address. By default, Cortex XSIAM displays information on whether the IP address is an internal or external IP address.
       * **External**—**Connection Type: Incoming** displaying IP address is located outside of your organization. Displays the country flag if the location information is available.
       * **Internal**—**Connection Type: Outgoing** displaying IP address is from within your organization. The XDR Agent icon is displayed if the endpoint identified by the IP address had an agent installed at that point in time.
    3.  Identify the IOC severity.

        The color of the IP address value is color-coded to indicate the IOC severity.
    4.  Review threat intelligence for the IP address.

        Depending on the threat intelligence sources that are integrated with Cortex XSIAM, the following threat intelligence might be available:

        *   **Virus Total** score and report

            <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>Requires a license key. Select Settings → Configurations → Integrations → <strong>Threat Intelligence</strong>.</p></div>
        * **Whois** identification data for the specific IP address.
        * **IOC** Rule, if applicable, includes the IOC **Severity**, **Number of hits**, and **Source**.
        * **EDL** IP address if the IP address was added to an EDL.
    5.  Review the related cases.

        **Recent Open Cases** lists the most recent cases that contain the IP address as part of the case’s key artifacts, according to the Last Updated timestamp. If the IP address belongs to an endpoint with a Cortex XDR agent installed, the cases are displayed according to the hostname rather than the IP address. To dive deeper into a specific case, select the case ID.
3.  In the right-hand view, use the filter criteria to refine the scope of the IP address information that you want to visualize in the map.

    In the Type field, select **Host Insights** to pivot to the **Asset View** of the host associated with the IP address, or select **Network Connections** to display the **IP View** of the network connections made with the IP address.
4. Review the selected data.
   * Select each node for additional information.
   * Select **Recent Outgoing Connections** to view the most recent connections made by the IP address. **Search all Outgoing Connections** to run a Network Connections query on all the connections made by the IP address.
5.  Perform actions on IOC or EDL.

    Depending on the current IOC and EDL status, the **Actions** button is displayed.
