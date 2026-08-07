# Issue fields

Cortex XSIAM includes out-of-the-box issue fields, issue fields from installed content packs, and user defined custom issue fields. You can use issue fields for mapping, correlation rules, and custom issue layouts.

All system and custom issue fields are available in the Issues table. New custom fields are hidden by default. To show custom issue fields in the Issues table, click the three dot vertical ellipses and select the column(s) from the list.

For Grid fields, HTML fields, and Markdown fields, if the field contains data the Issues table shows Data Available instead of the values. To view the data, open the issue and click Investigate to see the full issue layout. For multi-select fields, the first value is shown in the Issues table and the number of additional values is stated, but the additional values are not shown. For example, if a multi-select field holds the values x, y, and z, the Issues table shows x + 2 More.

Cortex XSIAM stores both the original value of the field and the current value of the field, if different. Any changes made between the original value and the current value are not stored. For example, if the original value of the field was x, the value was then changed to m, and then changed to y, only the x and y values are stored. To view the original value and the current value of changed fields, hover over the updated issue fields icon [![alert\_fields\_history.png](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABcAAAAaCAMAAABrajdMAAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAABFUExURfn5+e3t7eDg4KKiokxMTDMzMz8/P5aWlqOjo2VlZbu7u319fa6ursfHx1dXV9TU1EtLS3BwcImJiWRkZHFxcVhYWMjIyKzzBG8AAAAJcEhZcwAAFiQAABYkAZsVxhQAAAC2SURBVChTrZDBEoMgDEQTMFCVYBXt/39qF4y23pxp3wGSJbMs0I+ws+KC70RCtAZDjx4MNIZEpLk3mcYcwaQBJo75idOGaNvmBUuJlEprT73UOegqrf3okUTEU8qtPfXUcdvzkUg0Ic9KZasXr3k/rrpTQLxIt8l4yNC1Bo2RWXUwEYgOpTLDZjrCAPi8DHeGBKIRARvxqlsB7s0jxw7f8cneCuCDFUCDuYPw9S68xuzxGf+E6A3bkgf6R9uaLQAAAABJRU5ErkJggg==)](https://docs-cortex.paloaltonetworks.com/viewer/attachment/5CAbsl8idaK8R43ZLhoTOw/YWcHWCzd1u_y4BZz71i__w-5CAbsl8idaK8R43ZLhoTOw) on the right side of the row in the Issues table. To revert all of the fields in an issue to their original values, click Restore all fields to their original values in the updated issue fields box. Restoring all fields to their original values also restores the original values in the issue context data. Once you restore fields to their original values, this action can not be undone.

Custom issue fields can be exported and imported. To export a single custom issue field, right-click on the field in the fields table, and select Export. To export all custom issue fields in a single JSON file, click the Export All button above the fields table. System issue fields cannot be exported or imported.

After a custom issue field is created, it can be edited, deleted, or exported by right-clicking on the row. The field name and field type cannot be changed after the field is created. System fields cannot be edited, deleted, or exported.

{% hint style="warning" %}
Deleting an issue field or uninstalling a content pack containing an issue field may affect detection and other capabilities based on the deleted field. For example, correlation, layouts, case scoring, starring rules, and playbook triggers.
{% endhint %}

<br>
