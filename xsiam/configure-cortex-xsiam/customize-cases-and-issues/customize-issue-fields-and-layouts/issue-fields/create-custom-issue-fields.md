---
description: >-
  Create and manage custom Cortex XSIAM issue fields for JSON mapping, XQL
  correlation rules, issue layouts, and automation.
---

# Create custom issue fields

Create custom Cortex XSIAM issue fields to map incoming data, support correlation rules, and tailor issue layouts. You can use custom fields to:

* Map raw JSON fields from incoming issues.
* Display custom field data in the **Issues** table.
* Create correlation rules that generate issues from XQL queries.
* Map XQL query output to custom issue fields.
* Design custom issue layouts that include custom fields.

### Create a custom Cortex XSIAM issue field

1. Select Settings → Configurations → Object Setup → Issues → Fields → New Field.
2.  Choose a field type and enter a field name. For available field types, see [issue-field-types](issue-field-types "mention"). You can add an optional tooltip for users.

    If you add a grid, see [create-a-grid-field-for-an-issue](create-a-grid-field-for-an-issue "mention").
3. Click Save.

### Import, export, and update custom issue fields

Import and export custom issue fields. To export one field, right-click it in the fields table and select **Export**. To export all custom fields as one JSON file, click **Export All** above the table.

After you create a custom issue field, right-click its row to edit, delete, or export it. You cannot change the field name or field type.

Update custom field values with the **Set** command in the CLI, a script, or a playbook. For more information, see [update-issue-fields](../../../../detect-investigate-and-respond-to-threats/investigation-and-response/investigate-issues/issue-investigation-actions/update-issue-fields "mention").
