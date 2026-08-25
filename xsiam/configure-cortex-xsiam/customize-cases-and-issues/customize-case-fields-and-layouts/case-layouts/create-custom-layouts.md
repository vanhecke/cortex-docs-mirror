---
description: >-
  Create custom Cortex XSIAM case layouts with case fields, tabs, sections, and
  action buttons for different case types.
---

# Create custom layouts

Create custom Cortex XSIAM case layouts to control the fields, tabs, sections, and action buttons shown for different case types. Layouts can include custom and out-of-the-box case fields.

Custom tabs can be renamed, hidden, duplicated, or deleted. Hover over a tab name, click the settings button, and select an option. Drag and drop tabs to change their order. Empty fields are hidden by default. To show them, select **Show empty fields** from the tab settings.

You cannot edit the **Overview**, **Key Assets & Artifacts**, **Issues & Insights**, **Timeline**, **War Room**, and **Executions** system tabs. Select **Hide Tab** to hide a system tab without deleting it.

Export custom case layouts and duplicated system layouts. To export one case layout, right-click it in the layouts table and select **Export**. To export all custom layouts and duplicated system layouts as one JSON file, click **Export All** above the table.

Import a custom case layout by clicking **Import** and uploading its JSON file.

### Create a custom Cortex XSIAM case layout

1. Select **Settings** → **Configurations** → **Object Setup** → **Cases** → **Layouts** → **New Layout**.
2. Enter a name for the layout.
3.  To add a section, click on **New** or from the **Library** , under the **Sections** tab, drag and drop **New Section** into the new custom tab. You can also add a **Notes** section to the tab.

    By clicking on the pencil icon for a section, you can configure how a section appears, by hiding or showing the section header, as well as configuring the section fields to appear in rows or as cards.
4.  To add custom or out-of-the-box case fields to the layout, drag the fields from the **Fields** tab into existing sections or new sections that you added to the layout.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>Limit the number of case fields to 50 in each section. You can create additional sections as needed.</p></div>
5.  Add buttons to the layout.

    Buttons allow you to add tasks to your layout, which can assist an analyst. For example, you can add a button to scan a host or kill a process.

    1. From the **Fields and Buttons** tab of the **Library**, drag a buttons into a section of the layout.
    2. **Click to configure**.
    3.  Enter a descriptive name for the button, select a color, and select the script that you want to run when the button is clicked.

        For fields (script arguments) that are optional, you can define whether to show them to analysts when they click on buttons. To expose an optional field, select the **Ask User** checkbox next to the script argument(s) in the button settings page.

        <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>The script that runs when an action button is clicked accepts only mandatory arguments through the pop up window and does not provide an option for any non-mandatory arguments to be filled in when the button is clicked. We recommend using a wrapper script to collect and validate arguments in scenarios where there can be a combination of mandatory and non-mandatory arguments for a button.</p></div>

    For information on **Filters and Transformers**, refer to [Filter and transform data](../../../automations/playbooks/build-your-playbook/customize-your-playbook/filter-and-transform-data).
6. Save the layout.
7. (Optional) To modify an existing layout, right-click the layout in the layout table and select **Edit**, **Duplicate**, **Delete**, or **Export**.
