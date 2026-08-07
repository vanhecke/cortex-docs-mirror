# Grouping graph

The **Grouping Graph** is a visual representation of the logic used to group issues in a case. It provides transparency into why specific issues are linked, illustrating the relationships between data points and the underlying decision-making process of the analysis engine.

By revealing these connections, the graph offers key insights into the case narrative, visualizes the overall scope, and identifies common artifacts for investigation.

### Understanding case grouping

Issues and artifacts are automatically matched into a unified case based on a specific grouping logic. This allows you to resolve the entire scope of a case rather than treating detections in isolation. The logic is driven by the following factors:

* **Artifact association:** Issues sharing core artifacts, for example the same file hash or IP.
* **Similarity clustering:** Issues with similar detection patterns on the same entities.
* **Related entities:** Detections on related assets occurring within a close timeframe or context.
* **Linked and merged issues:** Issues that were manually linked to the case and merged issues.

Related issues are added to the case until a specific **grouping threshold** is met. In the **Grouping Graph** you can see whether case grouping is active or inactive. For more information about case grouping and case thresholds, see [Case grouping](../../case-concepts/case-grouping).

### Core components of the Grouping Graph

The graph uses a structured hierarchy of edges and nodes to represent the primary elements of a case:

<table><thead><tr><th width="167">Component</th><th>Description</th></tr></thead><tbody><tr><td>Edges</td><td><p>Represent the relationship between graph entities to show why they were linked. Edges display as lines that link nodes and entities together. Each full line represents a direct relationship.</p><p>The system defines three edge types:</p><ul><li><strong>Case > Issue:</strong> Links the case to the issue that initiated its creation.</li><li><strong>Issue > Artifact:</strong> Links an issue to an associated artifact. This indicates that the issue is the source of the artifact in the case.</li><li><strong>Artifact > Issue:</strong> Links an artifact to an issue or issue cluster. This indicates that the artifact is the source of the issues in the case.</li></ul><p>Edges display as:</p><ul><li><strong>Solid line:</strong> Connects the case node to its originating issue, as well as to related artifacts and additional issues later grouped into the case.</li><li><p><strong>Broken line:</strong> Connects similar, manually linked, or merged issues to the case. The connection type is indicated by a label:</p><ul><li><strong>linked:</strong> Issues manually linked to the case</li><li><strong>similar:</strong> Issues grouped by similarity clustering</li><li><strong>merged:</strong> Issues merged into the case</li></ul></li></ul></td></tr><tr><td>Case node</td><td>The central anchor node to which all other elements are connected.</td></tr><tr><td>Issue nodes</td><td>Visualized with parent/child relationships to show how primary threats spawned secondary activities.</td></tr><tr><td>Clusters</td><td><p>Groups of issues that are automatically clustered to keep the visual workspace organized, with details of the total issue count in the cluster and severity breakdown. Issues are clustered if they:</p><ul><li>Share a common artifact.</li><li>Are manually linked to the case.</li><li>Have been merged.</li><li><p>Are identified as similar through similarity clustering.</p><div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>Similar issues are displayed as individual entities rather than in a parent/child hierarchy.</p></div></li></ul></td></tr><tr><td>Artifacts</td><td>Represent artifacts that are linked to the issues in the case. Artifacts include user names, IPs, and causality chains. Causality chains link issues in the same causality chain to the case.</td></tr></tbody></table>

### Explore the graph

You can interact with the graph to uncover deeper layers of data without leaving the case view:

* **Expand and break down:** Click elements within the graph to expand clusters and view additional node details, such as severity, domains, and current status. You can also click the expand icon to view the grouping graph in a full page view.
* **Review issues and artifacts:** Hover over any entity in the graph to open a quick-view panel containing high-level details such as severity, domain, and current status. Hover over a cluster to see a breakdown of the severities contained within it.
* **Deep dive into issues:** Click an issue node and select **Open Issue** to view a detailed issue card with granular details about the issue.

#### **Example of the grouping graph**

![Grouping\_graph\_example.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-afcf83666f2854cafb8e15e847e46b8eb9a62b67%2Fbe3ca9a6b3a18bef2b2104275fa2bf6012c060a6ecbca6a06484996495ccf3dd.png?alt=media)

The following table breaks down the components in this example:

<table><thead><tr><th width="91.00006103515625">Label</th><th>Explanation</th></tr></thead><tbody><tr><td>1</td><td>Solid edge linking the case node to the issue that initiated case creation.</td></tr><tr><td>2</td><td>The issue that initiated case creation.</td></tr><tr><td>3</td><td>Casualty chain related to the initial issue.</td></tr><tr><td>4</td><td>Cluster of issues. These issues are part of the same causality chain as the initial issue. You can see that there are 13 issues in the cluster, and their severity breakdown.</td></tr><tr><td>5</td><td>Broken edge linking to a cluster of issues that were manually linked to the case. This is indicated by the <strong>linked</strong> label.</td></tr><tr><td>6</td><td>User name related to one or more issues in the linked issues cluster.</td></tr><tr><td>7</td><td>Issue related to the user name.</td></tr><tr><td>8</td><td><strong>Case grouping is inactive</strong> label. This indicates that the case is no longer accepting new matching issues, which happens when a case grouping threshold is met. For more information, see <a href="../../overview-of-cases/case-thresholds">Case thresholds</a>.</td></tr></tbody></table>
