---
description: >-
  Create and monitor synced remediation tickets for Cortex XSIAM SaaS Security
  issues.
---

# Create and monitor tickets

Integrate SaaS Security with Jira or ServiceNow to streamline misconfiguration remediation. This integration allows security teams to delegate manual remediation tasks directly to SaaS application administrators using your organization's existing issue tracking system.

***

### Prerequisites

Before managing tickets from the SSPM console, ensure:

* An active Jira or ServiceNow instance is connected and authenticated within your tenant settings. Follow these steps to activate [Issue Syncing](../../../detect-investigate-and-respond-to-threats/investigation-and-response/investigate-issues/issue-syncing).

***

### Ticket Management Workflows

#### 1. Create a Ticket

When a SaaS Security issue requires manual intervention within a target SaaS application:

1. Open the target Issue in the Cortex console.
2. On the **Overview** page, select Jira under the issue properties. This takes you to the ticket’s sync settings.
3. Under **Sync Configuration**, select Bi-directional.
4. Assign the ticket to the appropriate team member or administrator for investigation and resolution.

Once created, SaaS Security automatically establishes a bi-directional reference linking the specific issue to the new ticket ID.

#### 2. View Linked Tickets

You can track remediation progress directly from the SaaS interface:

* Select the highlighted ticket reference within any issue view to open the issue directly in Jira or ServiceNow.
