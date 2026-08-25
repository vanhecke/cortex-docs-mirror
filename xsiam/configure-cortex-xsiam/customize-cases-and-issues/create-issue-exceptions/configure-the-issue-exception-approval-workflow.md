---
description: >-
  Configure Cortex XSIAM issue exception approvals by managing approvers and
  enabling or disabling approval requirements.
---

# Configure the issue exception approval workflow

The following sections describe how to add or delete issue exception approvers and how to disable the issue exception approval workflow entirely, so that exception rules can be created without approvals.

## Add issue exception rule approvers in Cortex XSIAM

An exception rule approver must be added to the list of approvers in the system before an exception rule request can be sent to them. Exception approvers are not required to be Cortex XSIAM users. When you add a new approver to the list, that approver is sent an email notification indicating that they have been added to the approver list.

You can not be the approver of your own issue exception rule request.

{% hint style="warning" %}
### Prerequisite

You must have Exception Approver Admin permission to add or delete approvers.
{% endhint %}

1. Navigate to Settings>Configurations>Server Settings and scroll down to the Exception Management section.
2. Enter the approver’s name and email address, and then click Add New Approver.

The system will send the approver an email indicating that they have been added as an exception rule approver.

## Delete an issue exception rule approver in Cortex XSIAM

Consider the following restrictions when deleting issue exception rule approvers from the approver list:

* When the approval workflow is enabled, you cannot delete an approver if they are the only approver in the list. You must add a second approver before you can delete an approver.
* If an approver is linked to active or pending issue exception rules, you must disable those rules before you can delete the approver.

{% hint style="warning" %}
### Prerequisite

You must have Exception Approver Admin permission to add or delete approvers.
{% endhint %}

How to delete an issue exception rule approver

1. Navigate to **Settings** → **Configurations** → **Server Settings** and scroll to the **Exception Management** section.
2. Under **List of Approvers**, click the **X** next to the approvers name to delete them from the list.
3. **Save** the update.

## Disable the issue exception approval workflow in Cortex XSIAM

Disable the issue exception approval workflow to allow issue exceptions to be created without an approval.

{% hint style="warning" %}
### Prerequisite

You must have the Exception Approver Admin permission to disable or re-enable the issue exception approval workflow.
{% endhint %}

1. Navigate to **Settings** → **Configuration** → **General** → **Server Settings** and scroll to the **Exception Management** section.
2. Toggle Off **Approval Required**.

You can re-enable the issue exception approval workflow by toggling on Approval Required.
