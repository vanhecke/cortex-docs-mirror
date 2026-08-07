# Create widgets using AI

Use natural language prompts to request visual insights by instructing the **Agentic Assistant** to display its findings as charts or graphs. This makes it easy to visualize data for threat hunting, business intelligence, or investigations without writing XQL queries or manually creating data visualization.

When you request a visualization, the agent generates an XQL query, executes it, and then presents the results in a graph. **Agentic Assistant** supports all graph types supported by the Cortex Platform.

{% stepper %}
{% step %}
**From the Widget Library, select Create widget > Generate with AI.**
{% endstep %}

{% step %}
**Input a natural language prompt describing the security metrics you want to evaluate.**

For example: _"Show me a bar chart of failed user logins sorted by country over the last week"_.

The **Agentic Assistant** parses your request and creates a widget visualization.
{% endstep %}

{% step %}
**(Optional) Provide additional prompts to refine the widget using the Agentic Assistant.**
{% endstep %}

{% step %}
**(Optional) Refine the widget manually in XQL.**

Click the three dots icon on the widget and **Edit in XQL** to open the query in the **Query Builder**. You can edit the query or use the **Chart Editor** to change the visualization. See [Create XQL widgets](create-xql-widgets) for instructions.
{% endstep %}

{% step %}
**Save to the Widget Library.**

Click the three dots icon on the widget and **Save as Widget**. You can define the widget name, description, and visibility level (Public or Restricted).
{% endstep %}
{% endstepper %}

**Best practices for prompting**\
We recommend using clear specific language to request that the agent create these visualizations. Use terminology such as:

* Create a pie chart showing the distribution of issue severities over the last 7 days.
* Visualize the top 10 targeted assets by malware in a bar chart.
* Generate a line chart tracking the number of failed login attempts per day for the past month.
