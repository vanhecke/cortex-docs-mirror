# Transform a list into an array

Create a transformer to split a list into an array, add or edit a task in a playbook, or map an instance.

1. Go to Investigation & Response → Automation → Playbooks and create or edit a playbook.
2. Select Create Task.
3. In the Choose script field, select the Set automation.
4. In the Key field, enter the key name.
5. In the value field, click {}
6. Add a transformer.
   1. Click Filters And Transformers.
   2. In the Get field, click {}.
   3. Expand the Lists node and select a list to transform.
   4. In Apply transformers on the field, click Add transformer.
   5. Search for and select Split.
   6. (Optional) In the delimiter field, type the delimiter used to separate the items in the string (default is ",").
   7. Click Save.
7. Save the task and playbook.

For an example of using a transformer in a list, see [Apply transformers to extracted data](../playbooks/build-your-playbook/customize-your-playbook/filter-and-transform-data).
