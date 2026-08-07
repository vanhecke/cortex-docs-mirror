# Create custom layouts

Custom case layouts let you choose the specific fields and buttons that are displayed for different types of cases. You can create custom case layouts that include both custom and out-of-the-box case fields.

Tabs that were created can be renamed, hid, duplicated, or deleted. To make these changes, hover over the tab name, click the settings button, and select the relevant option. You can drag and drop tabs to change the order they appear. By default, empty fields within the tab are hidden in the case layout. To show empty fields, hover over the tab name, click the settings button, and select **Show empty fields**.

You cannot edit the **Overview**, **Key Assets & Artifacts**, **Issues & Insights**, **Timeline**, **War Room**, and **Executions** tabs in the case layout. Select **Hide Tab** to hide the tab, rather than deleting the tab as you may want to use the tab again for future use.

Custom case layouts and duplicates of system case layouts, can be exported. To export a single case layout, right-click on the layout in the layouts table, and select **Export**. To export all custom case layouts and duplicates of system case layouts in a single JSON file, click the **Export All** button above the layouts table.

You can import a custom case layout by clicking **Import** and uploading the JSON file.

#### How to create a custom case layout

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
