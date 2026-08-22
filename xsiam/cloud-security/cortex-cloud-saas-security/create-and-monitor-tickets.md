---
description: Learn more about creating a synced ticket to remediate an issue.
---

# Create and monitor tickets

Integrate SaaS Security with Jira or ServiceNow to streamline misconfiguration remediation. This integration allows security teams to delegate manual remediation tasks directly to SaaS application administrators using your organization's existing issue tracking system.

***

**Prerequisites**

Before managing tickets from the Cortex console, ensure:

* An active Jira or ServiceNow instance is connected and authenticated within your tenant settings. Follow these steps to activate [Issue Syncing](../../detect-investigate-and-respond-to-threats/investigation-and-response/investigate-issues/issue-syncing).

***

### Ticket Management Workflows

#### 1. Create a Ticket

When a SaaS Security issue requires manual intervention within a target SaaS application:

1. Navigate to **Cases and Issues** and locate the target SaaS Posture or AI Agent Issue.
2. Right-click on the Issue you wish to create a ticket for and select **Run Automation**. Integrations are available for Jira and Service Now. The workflow below uses Jira as an example:
   1. Select **Create a Jira ticket** from the available automations. If the Jira integration is not already present, you will be directed to provide the URL for you Jira instance and the associated secrets to initiate the integration.
   2. On the **Create a Jira Ticket** side-panel, enter your data for the Description, Issue Type, Project Key, and Summary fields.
   3. Under **Sync Configuration**, select Bi-directional, and click OK.
   4. Assign the ticket to the appropriate team member or administrator for investigation and resolution.

Once created, SaaS Security establishes a bi-directional reference linking the specific issue to the new ticket ID.

#### 2. View Linked Tickets

You can track remediation progress directly from the SaaS interface:

* Navigate to the targeted Issue and choose War Room to view the highlighted ticket reference. To track remediation progress, click on the ticket to open the issue directly in Jira, and Service Now.

***

### Send issues to Slack for remediation

Streamline issue remediation by routing SaaS Posture and AI Agent alerts directly to a dedicated Slack channel.

**Prerequisites**

* Set up [outbound Slack issue notifications](https://cortex-docs.paloaltonetworks.com/cortex-xsiam/onboard-cortex-xsiam/post-deployment/data-and-log-forwarding/forward-logs-and-data-from-cortex-xsiam-to-external-services/configure-external-applications-for-forwarding/integrate-slack-for-outbound-notifications) to link your channel.

**Procedure**

1. Navigate to **Cases & Issues**.
2. Locate and right-click the target issue.
3. Select **Create a case**.

A notification for the new case posts to the linked Slack channel.
