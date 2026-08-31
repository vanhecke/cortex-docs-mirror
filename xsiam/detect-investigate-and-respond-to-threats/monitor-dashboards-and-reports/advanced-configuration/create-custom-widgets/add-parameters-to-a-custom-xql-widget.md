---
description: >-
  Add parameters to Cortex XSIAM custom XQL widgets for interactive dashboard
  filtering.
---

# Add parameters to a custom XQL widget

If you want to use filters and drilldowns on your dashboard, one or more widgets on the dashboard must contain parameters. For more information about filters and drilldowns, see [Configure global filters](../configure-global-filters) and [Configure drilldowns](../configure-drilldowns).

Parameters can be static or dynamic, and support single or multi-select values.

{% stepper %}
{% step %}
**Create an XQL widget.**
{% endstep %}

{% step %}
**Define an XQL query and click Preview.**

You can base your filters on fields and values in the query results.
{% endstep %}

{% step %}
**Add parameters to the query using the filter stage, define parameters prefixed with `$`.**

*   **For single select filters:** `filter <field> = &<parameter>`

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Example:</strong><br>This filter enables dashboard users to filter the dashboard by a single predefined severity value.</p><p><code>filter xdm.issue.severity = &#x26;severity)</code></p></div>
*   **For multi select filters:** `filter <field> in(&<parameter>)`

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Example:</strong><br>This filter enables dashboard users to filter the dashboard by one or more domain values (predefined or dynamically generated).</p><p><code>filter domain in(&#x26;domain)</code></p></div>
{% endstep %}

{% step %}
**(Optional) Under Parameters, define default values for your query parameters.**

This makes the widget populate automatically on load. You can also define default values when configuring filters in the dashboard or report builder, or leave this blank.
{% endstep %}
{% endstepper %}
