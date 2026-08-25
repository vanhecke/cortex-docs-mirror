---
description: >-
  Create Cortex XSIAM issue exception rules with approvers, expiration dates,
  SLA timer pauses, and issue filter criteria.
---

# Create issue exception rules

You create an issue exception by creating an exception rule. The following steps describe how to create an exception rule on the All Exceptions Rules page.

{% hint style="info" %}
You can create a maximum of 10 issue exceptions per day.
{% endhint %}

1. Navigate to Settings → Exceptions Configuration and click on the Exception Rules tab to display the All Exception Rules page.
2. Click + Add Exception, select Create new exception, and then click Next.
3. Complete the following fields, and then click Next:
   1. Rule Name
   2. Approver: Select an approver from the dropdown list.
   3. Exception End Date: The exception will expire on this date and the SLA timer will start to count down.
   4. Justification: Describe the business justification for creating this rule.
   5. Reason Category: Select a reason category from the dropdown list.
   6. External Exception ID: (Optional) Enter a ticket number or other tracking record.
4.  Click Add filters, and then use the dropdown lists to create a filter that identifies the issues you want the exception rule to apply to.

    The query must return fewer than 100,000 issues.

    Click Next.
5.  Review the summary of the proposed rule. If it is correct, click Create.

    The proposed exception rule will now appear in the All Exception Rules list with the status Pending Decision, and, if the Exception Rule Approval workflow is enabled, an Exception Rule Request email will be sent to the approver. The exception rule will not take effect until the request has been approved.
