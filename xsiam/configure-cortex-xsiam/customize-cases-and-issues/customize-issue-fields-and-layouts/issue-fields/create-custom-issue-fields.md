---
description: >-
  Create and manage custom issue fields for incoming data, layouts, and
  correlation rules.
---

# Create custom issue fields

You can create custom issue fields to:

* Map raw JSON fields from incoming issues.
* Display custom fields data in the Issues table.
* Create correlation rules that generate issues from XQL queries and map the output of the queries to custom issue fields.
* Design custom issue layouts that include custom issue fields.

### How to create a custom issue field:

1. Select Settings → Configurations → Object Setup → Issues → Fields → New Field.
2.  Choose a field type and enter a field name. For a description of available field types, see [Issue field types](issue-field-types). You can add an optional tooltip to provide users with information about the field.

    If adding a grid, see [Create a grid field for an issue](create-a-grid-field-for-an-issue).
3. Click Save.

Custom issue fields can be exported and imported. To export a single custom issue field, right-click on the field in the fields table, and select Export. To export all custom issue fields in a single JSON file, click the Export All button above the fields table.

After a custom issue field is created, it can be edited, deleted, or exported by right-clicking on the row. The field name and field type cannot be changed after the field is created.

You can also update the custom field values by running the Set command in the CLI, a script, or a playbook. For more information, see [Update issue fields](../../../../detect-investigate-and-respond-to-threats/investigation-and-response/investigate-issues/issue-investigation-actions/update-issue-fields).
