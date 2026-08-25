---
description: >-
  Create custom case fields in Cortex XSIAM to capture investigation details,
  standardize case data, and support SOC workflows.
---

# Create custom case fields

Create custom case fields in Cortex XSIAM to add them to custom case layouts.

You can create custom case fields to:

* Map raw JSON fields from incoming issues.
* Display custom fields data in the **Cases** table.
* Create correlation rules that generate issues from XQL queries and map the output of the queries to custom case fields.
* Design custom case layouts that include custom case fields.

### Create a new custom case field in Cortex XSIAM:

1. Select **Settings** → **Configurations** → **Object Setup** → **Cases** → **Fields** → **New Field**.
2.  Choose a field type and enter a field name. You can add an optional tooltip to provide users with information about the field.

    If adding a grid, see [Create a grid field for a case](create-a-grid-field-for-a-case).
3. Save your changes.

Custom case fields can be exported and imported. To export a single custom case field, right-click on the field in the fields table, and select **Export**. To export all custom case fields in a single JSON file, click the **Export All** button above the fields table.

After a custom case field is created, it can be edited, deleted, or exported by right-clicking on the row. The field name and field type cannot be changed after the field is created.
