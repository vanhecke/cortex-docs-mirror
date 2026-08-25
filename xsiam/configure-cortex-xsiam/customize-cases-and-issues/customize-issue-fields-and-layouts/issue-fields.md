---
description: >-
  Manage Cortex XSIAM system and custom issue fields for mapping, correlation
  rules, issue layouts, and investigations.
---

# Manage Cortex XSIAM issue fields

Use Cortex XSIAM issue fields to support field mapping, correlation rules, custom issue layouts, and investigations. Cortex XSIAM includes system issue fields, content pack fields, and user-defined custom issue fields.

### View custom issue fields in the Issues table

All system and custom issue fields are available in the **Issues** table. New custom fields are hidden by default. To show them, click the three-dot vertical ellipses and select the required columns.

For Grid, HTML, and Markdown fields containing data, the Issues table shows **Data Available** instead of values. Open the issue and click **Investigate** to view the full issue layout. For multi-select fields, the table shows the first value and the number of additional values. For example, if a field holds `x`, `y`, and `z`, it shows `x + 2 More`.

### Review issue field history

Cortex XSIAM stores the original and current values when they differ. It does not store intermediate values. For example, if a value changes from `x` to `m` to `y`, Cortex XSIAM stores only `x` and `y`. To compare field values, hover over the updated issue fields icon <img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABcAAAAaCAMAAABrajdMAAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAABFUExURfn5+e3t7eDg4KKiokxMTDMzMz8/P5aWlqOjo2VlZbu7u319fa6ursfHx1dXV9TU1EtLS3BwcImJiWRkZHFxcVhYWMjIyKzzBG8AAAAJcEhZcwAAFiQAABYkAZsVxhQAAAC2SURBVChTrZDBEoMgDEQTMFCVYBXt/39qF4y23pxp3wGSJbMs0I+ws+KC70RCtAZDjx4MNIZEpLk3mcYcwaQBJo75idOGaNvmBUuJlEprT73UOegqrf3okUTEU8qtPfXUcdvzkUg0Ic9KZasXr3k/rrpTQLxIt8l4yNC1Bo2RWXUwEYgOpTLDZjrCAPi8DHeGBKIRARvxqlsB7s0jxw7f8cneCuCDFUCDuYPw9S68xuzxGf+E6A3bkgf6R9uaLQAAAABJRU5ErkJggg==" alt="alert_fields_history.png" data-size="line"> on the right side of an issue row. To revert all fields to their original values, click **Restore all fields to their original values**. This also restores original values in issue context data. You cannot undo this action.

### Import and export custom issue fields

Import and export custom issue fields. To export one field, right-click it in the fields table and select **Export**. To export all custom fields as one JSON file, click **Export All** above the table. You cannot import or export system issue fields.

After you create a custom issue field, right-click its row to edit, delete, or export it. You cannot change the field name or field type. You cannot edit, delete, or export system fields.

{% hint style="warning" %}
Deleting an issue field or uninstalling a content pack containing an issue field may affect detection and other capabilities based on the deleted field. For example, correlation, layouts, case scoring, starring rules, and playbook triggers.
{% endhint %}

<br>
