---
description: Create custom Cortex XSIAM filters and transformers for playbook data.
---

# Create custom filters and transformers

If you require a filter or transformer that is not provided out-of-the-box, you can create your own by creating a script and then adding to the operators window.

1. Select **Investigation & Response** → **Automation** → **Scripts** → **New Script**.
2. Type a meaningful name for the script, and click **Save**.
3. To create a filter operator script, do the following:
   1.  In the **Tags** field, add the `filter` tag.

       If you want a custom transformer that operates on an entire array rather than on each individual item, you need to add the `entirelist` tag.
   2.  In the **Arguments** section, add the following arguments:

       | Argument | Description                                                                                                                                                                                                 |
       | -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
       | left     | Mark as mandatory. This argument defines the left-side value of the transformer operation. In this example, this is the value being checked if it falls within the range specified in the right-side value. |
       | right    | Mark as mandatory. This argument defines the right-side value of the transformer operation. In this example, this is the range to check if the left-side value is in.                                       |
   3. Add the script syntax and save.
4. To create a transformer operator script, do the following:
   1. In the **Tags** field, add the `transformer` tag.
   2.  In the **Arguments** section, add the following arguments:

       | Argument | Description                                                                                                            |
       | -------- | ---------------------------------------------------------------------------------------------------------------------- |
       | value    | Mark as mandatory. The value to transform. In this example, this is the UNIX epoch timestamp to convert to ISO format. |
   3. Add the script syntax and save.
5. Go to the filters and transformers window and select the operator.
