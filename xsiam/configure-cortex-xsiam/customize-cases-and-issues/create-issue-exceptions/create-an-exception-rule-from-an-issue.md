# Create an exception rule from an issue

You can create an issue exception directly from an issue on the Issues page. This will result in an issue exception rule for a specific issue ID.

{% hint style="info" %}
You can create a maximum of 10 issue exception rules per day.
{% endhint %}

1. Navigate to Cases & Issues>Issues.
2. Right-click on the issue that you want to create an exception for, select Manage Issue>Except Issue.
3. Complete the following fields, and then click Next:
   1. Rule Name
   2. Approver: Select an approver from the dropdown list.
   3. Exception End Date: The exception will expire on this date and the SLA timer will start to count down.
   4. Justification: Describe the business justification for creating this rule.
   5. Reason Category: Select a reason category from the dropdown list.
   6. External Exception ID: (Optional) Enter a ticket number or other tracking record.
4. Verify that the correct issue appears in the table, and click Next.
5.  Review the summary of the proposed rule. If it is correct, click Create.

    The proposed exception rule will now appear in the All Exception Rules list with the status Pending Decision, and, if the Exception Rule Approval workflow is enabled, an Exception Rule Request email will be sent to the approver. The exception rule will not take effect until the request has been approved.
