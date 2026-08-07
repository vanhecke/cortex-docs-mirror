# Investigate an asset

Drilldown on an asset on the **Asset View**. On this view you can investigate host assets, view host insights, and see a list of cases related to a host.

{% hint style="info" %}
The Asset view is available for hosts with a Cortex XDR agent installed.
{% endhint %}

### How to investigate an asset

1.  Open the **Asset View**.

    Identify a host with a Cortex XDR agent installed and select **Open Asset View**.
2.  In the left panel, review the overview of the host asset.

    The overview displays the host name and any related cases.

    1. Add an **Alias** or **Comment** to the host name.
    2.  Review the related cases.

        **Recent Open Cases** lists the most recent cases that contain the host as part of the case’s key artifacts, according to the Last Updated timestamp. To dive deeper into a specific case, select the Case ID.
3.  In the right hand view, use the filter criteria to refine the scope of the host information that you want to display.

    In the Type field, select one of the following:

    * **Host Insights:** View a list of the host artifacts.
    * **Network Connections:** Pivot to the **IP view** displaying the IP addresses associated with the host.
    * **Host Risk View:** View insights and profiling information. Available with the the Identity Threat Module.
4.  Review the data.

    Select **Run insights collection** to initiate a new collection. The next time the Cortex XDR agent connects, the insights are collected and displayed.
5. Perform actions on the host.
