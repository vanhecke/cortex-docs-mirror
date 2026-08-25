---
description: >-
  Create a grid case field in Cortex XSIAM to capture and organize structured,
  tabular investigation data.
---

# Create a grid field for a case

In Cortex XSIAM, grid case fields enable you to view and edit tables in a custom case layout.

1. Select **Settings** → **Configurations** → **Object Setup** → **Cases** → **Fields** → **New Field**.
2. In the **New Case Field** window **Field Type** field drop down list, select **Grid (table)**.
3.  Complete the following parameters:

    | Parameter         | Description                                                                               |
    | ----------------- | ----------------------------------------------------------------------------------------- |
    | Field Name        | A meaningful name for the grid field.                                                     |
    | Tooltip           | (Optional) A brief descriptive message that explains what the field is and how to use it. |
    | User can add rows | (Optional) Enables users to add/remove rows in the grid.                                  |
4.  In the **Grid** tab, add or remove the required rows and columns.

    How you design the grid determines how it appears to users. If the **user can add rows** field is selected, the user can add rows but not columns.
5.  Configure each column by selecting the required field types, such as short text, Boolean, URL, etc. You can move the columns, rename, add values, etc.

    If you select the **Lock** check box, the value for that field is static (not editable). If you do not select the **Lock** check box (default), users can perform inline editing.
6. Click **Save**.
