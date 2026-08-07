# Cortex Command Center

The Cortex Command Center is a unified view for complete asset visibility, providing full organizational visibility across your cloud and enterprise environments. By combining cloud security data with SOC insights, the Cortex Command Center offers a detailed view of cloud and enterprise assets, including asset risk levels and active threats to assets.

Because this is a system-provided dashboard, it is **Public** by default and visible to all authorized users. It cannot be edited, deleted, or have its ownership transferred.

This dashboard helps you gain key insights into your environment, including:

* **A complete overview of your assets:** Understand asset distribution across your organization, with a comprehensive breakdown of assets by class, provider, and region.
*   **Assets at risk due to posture issues:** Identify assets with open posture issues that require attention to prevent threats from occurring in your environment.

    Posture issues are associated with risk management activities to detect and mitigate risks to assets in the environment before they occur in runtime, and improve resilience. For example, misconfigurations in cloud instances, over-permissive users, or the detection of secrets or shadow data.
*   **Assets with active runtime threats:** Identify assets with open security issues that require immediate attention.

    Security issues are associated with case response activities for detecting, preventing, and blocking threats as they occur in runtime. For example, identification of malware in a file, a compromised endpoint, or a phishing attempt.
* **Assets with active threats and posture issues:** Highlight assets with open security and posture issues. These are assets with active threats that might have already been exploited, and require immediate attention.
* **Data Ingestion in your environment:** See the total amount of ingested data in your environment over the last 24 hours, with a breakdown by data source. Click the widget to see a full breakdown on the **Data Ingestion** dashboard.

<details>

<summary>Show me more</summary>

![Cortex\_Command\_Center.gif](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-933ddbb76e10b476f6a9cb94ada747c47f89a5cd%2Fa602e38cc8705d693ba514d9cede3bb4861435c148fd16d647ee93ca400d81a8.gif?alt=media)

</details>

When you access the **Cortex Command Center**, the dashboard displays a view of all monitored assets. On the left side of the dashboard, you can see the total number of monitored assets, and a breakdown by status. On the right side, the radar provides a visual representation of your assets. The data on this dashboard shows the current status of your environment and is updated every 20 minutes. You can take the following actions to investigate your assets:

*   **Refine the displayed data:** Use the severity filters in the top-right corner. By default, assets with High and Critical issues are displayed. You can also change the radar view to display data by asset class, provider, or region, and drill down on assets by status: assets with active threats, assets at risk from posture issues, and assets with both active threats and posture issues.

    Drill down further on an asset class, provider, or region by clicking on the radar to open a side view with a breakdown of the selected option.
* **Identify unprotected assets:** Filter by asset class **Compute** to see the number of Compute assets that are being protected by the Cortex Agent. This information can help you to identify unprotected assets, and ensure complete coverage in your environment. Click on the number of agents to see more information on the **Agent Management** dashboard.
* **Investigate open issues for an asset type:** Click a group (such as Identity) to see the number of open issues for each asset status. Click on the number of issues to open the Issues page, filtered for the asset type and status.
* **See asset details:** On the radar, each dot represents a group of assets, color-coded by their collective status. Click a dot to view details about the assets in the group. Use the arrows to click through the assets, click See details to open the asset card for a specific asset or click **See All** to open the **Asset Inventory**, filtered to display all assets in the group.

### Limitations

The **Cortex Command Center** currently has the following limitations:

* Only assets that are included in the **Asset Inventory** are displayed on the dashboard.
* In the region view, the location is based on cloud provider region and its data center location and therefore the map view shows only cloud assets.
* When you click **See All** assets in the **Asset Inventory**, the listed assets are limited to 1,000.
