---
description: Answer some frequently asked questions relating to Graph Search.
---

# FAQ on Graph Search

{% hint style="info" %}
### Notice

This feature is included with a Cortex XSIAM Premium license. It is also included with any other Cortex XSIAM license that has the Cloud Posture Security or Cloud Runtime Security add-on.
{% endhint %}

{% hint style="warning" %}
### Prerequisite

Graph Search requires **View** or **View/Edit** RBAC permissions for **Graph Search** under **Investigation & Response** → **Search**.
{% endhint %}

Here are several Frequently Asked Questions (FAQ) about Graph Search:

<details>

<summary>What data is currently searchable in Graph Search?</summary>

For this release, several assets and findings are supported. For the upcoming releases, we will roll out more assets and provide the ability to model new services. For more information on the supported assets and findings, see [Supported assets and findings](supported-assets-and-findings).

</details>

<details>

<summary>Can the Graph Search results be exported and in what formats?</summary>

For this release, you can export the Graph Search results to a PNG, SVG, and TSV file.

</details>

<details>

<summary>Can the Graph Search results be grouped in the output?</summary>

Yes, there are two types of groupings possible - automatic groupings and manual groupings that you can apply to the graph results displayed.

</details>

<details>

<summary>How are the Graph Search query results displayed?</summary>

The query results are displayed in a graph (default) or table format. In a graph format the paths on the graph that matched the node types and conditional attributes in the query are displayed. Each result is a full path of the matching query. Yet, in a table format the results are displayed in a table, where each row in the table represents a different path in the graph that goes through all the matching node types and attributes as they appear in the Graph Search query. You can view the full asset information of any cell in the table by clicking the cell. Every asset and finding table shows different default columns.

</details>

<details>

<summary>Are there any built-in manipulations to the query results that I can apply or are they automatically displayed without having to update and rerun the Graph Search query?</summary>

Yes, the following are available:

* On the right side of the graph results, there are different icons that can help you drilldown into your graph results. These two icons provide built-in manipulations without having to make any changes to your Graph Search query:
  * ![layers\_icon.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-a2eebf6795e9f96fab51d110903e892d3f78b5ff%2F938180732f9d94ec0f6d846002bce5003100d2e7b49b8f1a3e15fe92786088b8.png?alt=media): Use the layers icon to easily add or remove additional information to the graph without having to define these parameters in your Graph Search query. You can decide when to include these built-in layers, as needed. The following are available:
    * **Public Exposure to the Internet**: Tracks the asset nodes with internet exposure that could be targeted for external surface attacks by displaying the exposure path. A Globe node called **Internet** is added to the graph, which links all exposed asset nodes to this Globe node. You can expand this connection by clicking the **+** icon to reveal the full internet path to include, for example, the NIC, Subnet, and Gateway. In the exposure path, you can select each node, or hover on it and select **More Info**, you'll see more information displayed in a dialog box. You can click **View Details** to drill down even further on the asset node to display more information on the node depending on the data collected for that asset node selected. Internet paths are collapsed by default.
    * **Related Cases**: Displays the number of related Cases for each asset node with a breakdown by severity.
    * **Runtime Events**: Adds 100 most recent runtime events to the graph results, which are refreshed every hour. This enables you to investigate real-time activity and identify critical events, such as access to sensitive information typically contained in a storage bucket, which generate issues and cases. All the bucket nodes in the path include a runtime icon ![runtime\_icon.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-aba6e0327e25d7f06ea58c9ee839dc5b81be6f56%2F2bb4d71320a8e52e3d2276bac18d1f85b7842e7e13894b662af33197b275a710.png?alt=media) underneath and run an animation on all the bucket and virtual machine nodes. You can click the runtime icon to reveal more info, such as connection details and runtime events. Click **Show Recent Events** to display the **Runtime Events** table with more details on the last 100 events.
  * ![Group\_nodes\_icon.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-182dcc4f3b90392c5ea2d092576b9ed6f36c93c3%2Fe7e0492913cbbb6383df541fb280b4494b8d17a32751690d607b1e0415e80fe1.png?alt=media): Use the Group nodes icon to group by the Cloud Provider, Cloud Account, or Cloud Region. Selecting one of these grouping enables you to view the graph results in an aggregated format, providing a clearer and more organized perspective of the data. This feature also helps to Identify patterns and trends more easily in your data by grouping similar entities together. In the future, the Group nodes feature will be expanded to enable additional groupings.
* Vulnerability finding nodes automatically display under the node a breakdown of severity.

</details>

<details>

<summary>Are Graph Search queries accessible from the Query Library and are there any built-in queries that come out-of-the-box to view?</summary>

Cortex XSIAM provides, as part of Graph Search, a Query Library for saving and managing your own queries, queries shared with you, and built-in Graph Search queries provided by Palo Alto Networks to help illustrate how to build meaningful Graph Search queries on your data.

</details>
