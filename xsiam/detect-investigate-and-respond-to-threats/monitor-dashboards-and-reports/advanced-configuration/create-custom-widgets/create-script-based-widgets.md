---
description: >-
  Create Cortex XSIAM script-based widgets to display custom dashboard data and
  insights.
---

# Create script-based widgets

You can use scripts in custom widgets to create dynamic widgets for more complex calculations and to present data from third-party systems. For examples of creating widgets using scripts, see [Script-based widget examples](#script-based-widget-examples).

Before creating a script-based widget in the **Widgets Library**, you need to create or upload the script to the **Scripts** page. In the **Widgets Library**, you can change elements of the visual presentation. Because these widgets can contain unique logic or sensitive data queries, they are now managed as individual items with specific access rules.

{% hint style="info" %}
To create a script-based widget, your user role must allow you to create scripts and build dashboards. These permissions are set by your administrator. For more information, see [Manage access to custom dashboards](../../../../onboard-cortex-xsiam/post-deployment/manage-user-roles-and-access-management/manage-access-to-objects/manage-access-to-custom-dashboards).
{% endhint %}

### How to create a script-based widget

1. **Create the script**: Select **Investigation & Response** → **Automation** → **Scripts**. You can upload an existing script or create a new one. Cortex XSIAM supports JavaScript, Python and PowerShell. You can create a script for one of the following chart types:
   * Pie
   * Column
   * Line
   * Single Value
2. **Configure for the Widget Library**: In the **Script Settings**, add the **widget** tag to the script. This tag ensures the script is recognized as a visualization tool and becomes available in the **Widget Library**.
3. **Create the Custom Script Widget**: Select **Dashboards & Reports** → **Widget Library**, click **Create custom widget**, and select **Script**.
4. **Define the widget properties**:
   * **Name** and **Description**: Give your widget a clear name so you can identify it later in the **Widget Library**.
   *   **Script**: Select the script you created in step 1 from the list.

       <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>If you have added arguments to the script, these appear when creating a widget.</p></div>
5. **Set visibility**: Use the **Public widget** toggle to determine how the widget appears in the **Widget Library**. Leave it unselected (default) to keep the widget **Restricted** (visible only to you) or select it to make the widget **Public** (visible to all users with **Widget Library** access).
6. **Preview and save**: Run a preview to ensure the script executes correctly and displays the data as intended, then click **Save**.
7.  **Configure the display (Chart Editor)**: Use the **Chart Editor** to choose the graph type and the subtype, and to enable or disable the graph legend.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>Available options are <strong>Pie</strong>, <strong>Column</strong>, <strong>Line</strong>, and <strong>Single Value</strong>.</p><p>To display the result of the script as a time duration, choose the graph type <strong>Single Value</strong> and enable <strong>Show as Time</strong>. You can then select the <strong>Time Unit</strong> (millisecond, second, minute, or hour) and the <strong>Display format</strong>.</p></div>
8. **Add to reports or dashboards**: Once saved to the **Widget Library**, you can add this script-based widget to any custom dashboard or include it when building a report template.

### Script-based widget examples

You can use script-based widgets to perform calculations on and visualize third-party data.

{% hint style="info" %}
Add the **widget** tag in the script settings to make the script available for use in script-based widgets. For more information, see [Create a script](../../../../configure-cortex-xsiam/automations/scripts/create-a-script).
{% endhint %}

The following are sample Python scripts for the graph types **Single Value**, **Pie**, **Line**, and **Column**.

<details>

<summary>Single value</summary>

This example shows how to use a script with an API call to return a single value in a widget. Use this example to build your own script that pulls in third-party data to display a single value.

{% hint style="info" %}
If your script returns a time duration, configure the widget with the graph type **Single Value** and enable **Show as Time**..
{% endhint %}

**Example:**

```programlisting
import requests

def main():
    api_key = 'PUTYOURKEYHERE'
    symbol = 'PANW'
    api_url = f'https://www.alphavantage.co/query?function=GLOBAL_QUOTE&symbol={symbol}&apikey={api_key}'

    response = requests.get(api_url)
    data = response.json()

    price_str = data['Global Quote']['05. price']
    price_int = int(float(price_str))

    return_results(price_int)

if __name__ in ('__main__', '__builtin__', 'builtins'):
    main()
```

</details>

<details>

<summary>Pie, Line, or Column Chart</summary>

**Example 1**

The following example script creates random, mock data to simulate a stock price fluctuating over a short period of time. Use this example to build your own script that brings in third-party data and display trends using a pie, line, or column chart.

```programlisting
import random
import json
from datetime import datetime, timedelta

def main():
    chart_data = []
    start_time = datetime.strptime("13:00", "%H:%M")

    # Start the price at a realistic value
    current_price = 202.0

    # Simulate 50 data points
    for i in range(50):
        # Generate a time label in 1-minute jumps
        time_label = (start_time + timedelta(minutes=i)).strftime("%H:%M")

        # Create the data point for the chart
        data_point = {
            "name": time_label,
            "data": [int(current_price)],
            "groups": []
        }
        chart_data.append(data_point)

        # Simulate the next price by adding a small change to the current price
        price_change = random.uniform(-1.5, 1.5) # A small drift up or down
        current_price += price_change

    # Return the data formatted exactly as in your working script
    return_results({
        "Type": 1,
        "ContentsFormat": "json",
        "Contents": json.dumps(chart_data)
    })


if __name__ in ('__main__', '__builtin__', 'builtins'):
    main()
```

**When used in a widget:**

![stockgraph-examplescript.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-3274f61faa1690b19ef667dc394f109c22c44117%2F21c6d31413551eace10a95e9948eceab88b6752c5ef8d024e291296445c84731.png?alt=media)

**Example 2**

The following example script generates simulated data representing the count of security incidents (or other events) broken down by severity level for each day of the week (Monday to Friday). Use this example to build your own script to create a stacked column chart. Configure the widget with graph type **Column** subtype **Stacked**.

```programlisting
import json
import random

def main():
    chart_data = []
    days = ["Monday", "Tuesday", "Wednesday", "Thursday", "Friday"]
    severities = ["Critical", "High", "Medium", "Low", "Info"]

    for day in days:
        groups_list = []
        daily_total = 0

        for severity in severities:
            count = 0
            if severity == "Critical":
                count = random.randint(0, 5)
            elif severity == "High":
                count = random.randint(5, 15)
            elif severity == "Medium":
                count = random.randint(10, 25)
            elif severity == "Low":
                count = random.randint(20, 50)
            else:
                count = random.randint(5, 30)

            daily_total += count
            groups_list.append({"name": severity, "data": [count]})

        chart_data.append({
            "name": day,
            "data": [daily_total],
            "groups": groups_list
        })

    return_results({
        "Type": 1,
        "ContentsFormat": "json",
        "Contents": json.dumps(chart_data)
    })
```

**When used in a widget:**

![severitybyday-examplescript.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-2847042adb821b020094a611e1a2245953dccddc%2Fb726a42673f09843c1cb092b96b188e0d211adada0397122fe0e27cbb54f9f88.png?alt=media)

</details>
