# Update issue fields with playbook tasks

During the investigation, you can set and update issue fields using the **setIssue** script in a playbook task.

You initially define issue fields after the planning stage, with mapping and classification for how the issues will be ingested from third-party integrations into Cortex XSIAM.

{% hint style="info" %}
* The **setIssue** script includes all available fields; use the scroll bar to see all the fields.
* The `name` field has a limit of 600 characters. If there are more than 600 characters, you can shorten the `name` field to under 600 characters and then include the full information in a long text field such as the `description` field.
* There are many ﬁelds already available as part of the Common Type content pack. Before creating a new issue field, check if there is an existing ﬁeld that matches your needs.
{% endhint %}

For more information, see Update issue fields
