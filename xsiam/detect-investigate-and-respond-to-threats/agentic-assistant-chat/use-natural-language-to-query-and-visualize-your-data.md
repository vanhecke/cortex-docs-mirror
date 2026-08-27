---
description: >-
  Prompt Cortex Agentic Assistant agents to create graphs and charts from its
  findings in Cortex XSIAM.
---

# Use natural language to query and visualize your data

Use natural language prompts to request visual insights by instructing the Agentic Assistant to display its findings as charts or graphs. This makes it easy to visualize data for threat hunting, business intelligence, or investigations without writing XQL queries or manually creating data visualizations.

When you request a visualization, the agent generates an XQL query, executes it, and then presents the results in a graph. Agentic Assistant supports all graph types supported by the Cortex Platform.

This feature is provided as a built-in system hidden action and does not appear in the Agentic Assistant Hub. It is an enhancement of the built-in TextToXQL and Cortex - Run XQL Query actions. For more information, see [Create and run XQL queries with Agentic Assistant chat](create-and-run-xql-queries-with-agentic-assistant-chat).

**Best practices for prompting**

We recommend using clear, specific language to request that the agent create these visualizations. Use terminology such as:

* Create a pie chart showing the distribution of alert severities over the last 7 days.
* Visualize the top 10 targeted assets by malware in a bar chart.
* Generate a line chart tracking the number of failed login attempts per day for the past month.

**Visualization capabilities**

To help you get the most out of your generated graphs and charts, the Agentic Assistant supports the following capabilities:

* **Visualization creation or editing**: You can use natural language to instruct the agent to build a new query from scratch or to modify an existing one.
* **Data filtering**: You can ask the agent to alter the visual representation of your data. The system supports filtering without risking any changes to or breaking the existing underlying XQL query.
*   **Dashboard integration**: Once the graph or chart is created, you can click <img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-11a463bf2b5bf9ecd6322e37719ff9691e5de3f2%2F49fda5fb33e5f524c041a0abe1ea1868806777860768af3c9ef5a3a2716a9c39.png?alt=media" alt="three-dots-dark.png" data-size="line"> to save it to the **Widget Library** and then apply it to your dashboard from the **Widget Library**.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>Once the graph or chart is saved to the <strong>Widget Library</strong>, the link to the chat artifact is severed, and the agent does not track subsequent changes made to the widget or the dashboard.</p></div>
