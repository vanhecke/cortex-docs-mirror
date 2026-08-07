---
description: Learn more about the Graph Search query results.
---

# Understand Graph Search query results

{% hint style="info" %}
### Notice

This feature is included with a Cortex XSIAM Premium license. It is also included with any other Cortex XSIAM license that has the Cloud Posture Security or Cloud Runtime Security add-on.
{% endhint %}

{% hint style="warning" %}
### Prerequisite

Graph Search requires **View** or **View/Edit** RBAC permissions for **Graph Search** under **Investigation & Response** → **Search**.
{% endhint %}

Review the following topics:

* [How to build Graph Search queries?](how-to-build-graph-search-queries)

Once the query is completed, you can search for your query results. The results displayed are dependent on your data.

You can view the Graph Search query results in two formats:

* **Graph** (default): Displays the paths on the graph that matched the node types and conditional attributes in the query. Each result is a full path of the matching query.
* **Table**: Displays the results in a table, where each row in the table represents a different path in the graph that goes through all the matching node types and attributes as they appear in the Graph Search query. Every asset and finding table shows different default columns. For more information, see [Table view columns](#table-view-columns). You can view the full asset information of any cell in the table by clicking the cell.

You can export the Graph Search results as a PNG, SVG, or TSV file. You can always edit the query once the results are displayed, which means that the old results are discarded and the new results are displayed. In addition, you can save the results to the Query Library.

<details>

<summary>Graph output</summary>

The Graph Search resulting graph displays the paths according to the nodes and conditional attributes that you selected in your query. Here are a few things to keep in mind when viewing the graph results:

* There are two different types of nodes, where each node has its own unique shape, icon, and color:
  * **Asset nodes**: Each asset node is depicted as a circle in the resulting graph, where the color and icon displayed is dependent on the asset category and class types selected. There are multiple class types available for each asset node category selected. Once a class type is selected in the node picker dialog box and you hover over it, all the available asset types are listed according to the data collected. For more information, see [All assets](../../detect-investigate-and-respond-to-threats/asset-management/all-assets).
  * **Finding nodes**: Each finding node is depicted as a diamond in the resulting graph, where the color and icon displayed is dependent on the finding type selected. There is only one category type available for each finding selected.
*   In the resulting query, nodes are automatically grouped together to keep the graph looking cleaner and less busy. Nodes are grouped when there are at least five nodes that meet the following conditions:

    * The node isn't a root node.
    * The path is identical.
    * For asset nodes, the nodes have the same class and category type.
    * For finding nodes, the nodes have the same category type.

    A grouped node icon is displayed as a duplicate node. For example, if it's a group node, the icon looks like two shapes, one on top of another. When you select the group node, a dialog box opens displaying all the nodes included in the group.
* When you select each node, or hover on it and select **More Info**, you'll see more information displayed in a dialog box. You can click **View Details** to drill down even further on the node to display more information on the node depending on the data collected for that asset or finding node selected.
* Vulnerability finding nodes automatically display under the node the breakdown of severity.
* Every Graph Search query returns a maximum of 50 paths with an indication displayed at the bottom of the page of the total number of results.
* On the right side of the graph results, different icons can help you drill down into your graph results:
  * **+** and **-** icons: Use the plus and minus icons to zoom in and out of the graph.
  * ![centering\_icon.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-dfca608c922b043f5e977497fe595856666ebf74%2F14286e774c9962e2c1306f36f1bbd233bd0c3b206c18c94b702a09b955bb005d.png?alt=media): Use the diamond icon to center your graph after you've manipulated the output.
  *   ![layers\_icon.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-a2eebf6795e9f96fab51d110903e892d3f78b5ff%2F938180732f9d94ec0f6d846002bce5003100d2e7b49b8f1a3e15fe92786088b8.png?alt=media): Use the layers icon to easily add or remove additional information to the graph without having to define these parameters in your Graph Search query. You can decide when to include these built-in layers, as needed. The following are available:

      * **Public Exposure to the Internet**: Tracks the asset nodes with internet exposure that could be targeted for external surface attacks by displaying the exposure path. A Globe node called **Internet** is added to the graph, which links all exposed asset nodes to this Globe node. You can expand this connection by clicking the **+** icon to reveal the full internet path to include, for example, the NIC, Subnet, and Gateway. In the exposure path, you can select each node or hover on it and select **More Info**; you'll see more information displayed in a dialog box. You can click **View Details** to drill down even further on the asset node to display more information on the node depending on the data collected for that asset node selected. Internet paths are collapsed by default.
      * **Related Cases**: Displays the number of related Cases for each asset node with a breakdown by severity.
      * **Runtime Events**: Adds 100 most recent runtime events to the graph results, which are refreshed every hour. This enables you to investigate real-time activity and identify critical events, such as access to sensitive information typically contained in a storage bucket, which generate issues and cases. All the bucket nodes in the path include a runtime icon ![runtime\_icon.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-aba6e0327e25d7f06ea58c9ee839dc5b81be6f56%2F2bb4d71320a8e52e3d2276bac18d1f85b7842e7e13894b662af33197b275a710.png?alt=media) underneath and run an animation on all the bucket and virtual machine nodes. You can click the runtime icon to reveal more info, such as connection details and runtime events. Click **Show Recent Events** to display the **Runtime Events** table with more details on the last 100 events.

      The results from the different layers are displayed in tabs in the node dialog box, which enables you to quickly switch from one layer to the other.
  * ![Group\_nodes\_icon.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-182dcc4f3b90392c5ea2d092576b9ed6f36c93c3%2Fe7e0492913cbbb6383df541fb280b4494b8d17a32751690d607b1e0415e80fe1.png?alt=media): Use the Group nodes icon to group by the Cloud Provider, Cloud Account, or Cloud Region. Selecting one of these grouping enables you to view the graph results in an aggregated format, providing a clearer and more organized perspective of the data. This feature also helps to identify patterns and trends more easily in your data by grouping similar entities together. In the future, the Group nodes feature will be expanded to enable additional groupings.

</details>

<details>

<summary>Show me an example of Graph Search results with general tips and tricks</summary>

![Understand\_Graph\_Search\_results\_with\_general\_tips\_and\_tricks\_July\_doc.gif](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-2bc05f9be63cb78cefcbdfb0b2962849e10a84b0%2F1883174d7791f52a174db539582c0e22d123cb2e20107959c222f7c111fd364d.gif?alt=media)

</details>

<details>

<summary>Show me how to use the layers and group node icons in the Graph Search results</summary>

This example focuses on using the layers icon to add or remove additional information to the graph and how to group information together using the Group node icon.

![Understand\_Graph\_Search\_query\_results\_July\_Layers\_and\_Group\_Nodes.gif](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-d66b667659acbfc1b85c990ef8eda3ef76153bd4%2Fab9417ecbd5a0e2a856e4bd23cd9f513275823b569158e35becb3fb2b13c6a1e.gif?alt=media)

</details>

<details>

<summary>Table view columns</summary>

Below is a list of the different columns displayed by default in the assets and findings tables.

Asset table

Below is a list of the default columns that are displayed within any asset table, where the names of the columns can change slightly depending on the asset selected. In addition, some assets have additional columns.

* All assets tables:
  * Asset Name
  * Asset Type
  * Asset Category
  * Asset Provider
  * Asset Realm
* All assets additional columns:
  * \<name of asset> ID
* Identity finding additional columns:
  * Identity Account Access
  * Identity Admin Permissions
  * Identity Cloud Region
  * Identity Empty
  * Identity Excessive
  * Identity Guest
  * Identity Has MFA
  * Identity Last Login
  * Identity Last Used

Finding table

Below is a list of the default columns that are displayed with in any finding table, where the names of the columns can change slightly depending on the finding selected. In addition, some findings have additional columns.

* All findings tables:
  * Finding Name
  * Finding Category
* Vulnerability finding additional columns:
  * Vulnerability Finding Package ID
  * Vulnerability Finding CVE ID
  * Vulnerability Finding Severity
  * Vulnerability Finding Fix Versions
  * Vulnerability EPSS Score
  * Vulnerability Package ID
  * Vulnerability Exploitable
  * Vulnerability Affected Versions
  * Vulnerability Status
  * Vulnerability CVE Vendor Link
  * Vulnerability Fix Date
  * Vulnerability Publish Date
  * Vulnerability Derived from Base Image
  * Vulnerability CVSS Score
  * Vulnerability CVSS Vector
  * Vulnerability Has a Fix
  * Vulnerability Fix Versions
  * Vulnerability Severity
  * Vulnerability CVE ID
* Malware finding additional columns:
  * Malware Finding File Path
  * Malware Finding SHA256
  * File Permissions
  * File Name
  * File Size
  * File Path
  * File Last Modified Time
  * Verdict
  * SHA256
* Data finding additional columns:
  * Data Finding Secret Location
  * Data Finding Secret Snippet
  * Secret Snippet
  * Secret Location
  * File Path
  * File Code Line

</details>
