---
description: >-
  View Cortex XSIAM issue exception rules, approval status, affected issues,
  expiration dates, and workflow details.
---

# View issue exception rules

View Cortex XSIAM issue exception rules on the **All Exception Rules** page. Review rule status, affected issues, approvers, expiration dates, and approval workflow details.

To open the **All Exception Rules** page, go to **Settings** → **Exceptions Configuration** → **Exception Rules**.

### All Exception Rules field descriptions

The table below describes each field in the All Exception Rules table.

| Field                  | Description                                                                                                                                                                                                                                                                                                                                                                              |
| ---------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Approver Email         | Email address of the approver.                                                                                                                                                                                                                                                                                                                                                           |
| Approver Name          | Name of the approver.                                                                                                                                                                                                                                                                                                                                                                    |
| Backward Scan Status   | <p>Processing status of the exception rule. It indicates whether or not the exception has taken effect.</p><p>Possible values include:</p><ul><li>Pending: the system has not started excepting issues.</li><li>In progress: the system is actively updating the issues.</li><li>Failed: issue exception failed</li><li>Done: all affected issues have been marked as excepted</li></ul> |
| Decision Justification | Justification provided by the approver for approving or rejection the exception rule request.                                                                                                                                                                                                                                                                                            |
| Exception ID           | Unique ID for the exception rule.                                                                                                                                                                                                                                                                                                                                                        |
| Expiration Date        | Date the exception expires. This is the Exception End Date that was specified when the exception rule was created.                                                                                                                                                                                                                                                                       |
| External Exception ID  | Optional reference provided when the rule was created.                                                                                                                                                                                                                                                                                                                                   |
| Impacted Issues        | Number of issues impacted by the exception request.                                                                                                                                                                                                                                                                                                                                      |
| Justification          | Description of the business justification for this exception.                                                                                                                                                                                                                                                                                                                            |
| Justification Category | High-level category of the business justification.                                                                                                                                                                                                                                                                                                                                       |
| Name                   | Name of the rule.                                                                                                                                                                                                                                                                                                                                                                        |
| Requestor Email        | Email address of the person who created the exception rule.                                                                                                                                                                                                                                                                                                                              |
| Requestor Name         | Name of the person who created the exception rule.                                                                                                                                                                                                                                                                                                                                       |
| Rule                   | The issue ID or other issue identifiers used to define which issues the exception applies to.                                                                                                                                                                                                                                                                                            |
| Status                 | The current workflow status for the rule. Refer to the Exception Rule status descriptions table for a description of each status.                                                                                                                                                                                                                                                        |

### Issue exception rule status descriptions

The following table describes issue exception rule status values.

| Status           | Description                                                                                                                                                  |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Approved         | The rule has been approved and is active.                                                                                                                    |
| Disabled         | The rule has been manually disabled.                                                                                                                         |
| Expired          | The Exception End Date for the rule has passed.                                                                                                              |
| No Decision Made | The approver did not respond to the issue exception rule request within seven days, so the request timed out.                                                |
| Pending Decision | The issue exception rule request was sent to the approver. The approver has not yet responded but the request is still within the seven-day response window. |
| Rejected         | The approver rejected the issue exception rule request.                                                                                                      |
| Self Approved    | The rule was created when the Exceptions Require Approval setting was toggled “off”.                                                                         |

<br>
