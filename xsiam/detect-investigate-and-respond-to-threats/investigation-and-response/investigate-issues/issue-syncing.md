---
description: Sync Cortex XSIAM issues with external tickets to coordinate remediation.
---

# Issue syncing

You can set up integrations that mirror Cortex XSIAM issues with external applications, such as Atlassian Jira or ServiceNow. When mirroring issues (also referred to as issue syncing), you can make changes in an external application that will be reflected in the platform, and vice versa. If an issue is mirrored with an external application, you have the following options:

* **Link the ticket to the issue:** If an issue is linked to a ticket, the ticket number is displayed in the **Overview** section of the issue card. You see details about the status of the ticket by clicking on the ticket number.
* **Sync changes between the issue and the ticket:** If an issue is synced to a ticket, changes are synchronized in an outbound, inbound, or bi-directional flow.

{% hint style="info" %}
Multiple tickets can be linked to an issue with outbound syncing. Issues with inbound syncing can be linked to a single ticket only.
{% endhint %}

### Set up an external integration to sync with issues

Before you can sync issues with external applications, you must set up and configure your integration instance. Complete the following steps:

{% stepper %}
{% step %}
**Install the content pack.**

1. Install the relevant content pack, for example **Atlassian Jira** or **ServiceNow:**
   * To install from the **Data Sources & Integrations** page: Navigate to **Settings** → **Data Sources & Integrations**, click **+ Add New**, and search for the relevant content pack.
   * To install from **Marketplace**: Navigate to Settings → **Configurations** → **Marketplace**. and browse for the relevant content pack.
{% endstep %}

{% step %}
**Connect an integration instance.**

1. Navigate to **Settings** → **Data Sources & Integrations**.
2. Search for the relevant data source (for example **Atlassian Jira**) select it, and click **Add Instance**.
3. Enter instance details in the required fields and click **Connect**.
{% endstep %}
{% endstepper %}

### Manually create a synced ticket

{% hint style="info" %}
**Prerequisite**

You must set up the following before you can sync issues:

* An external integration. For more information, see [Set up an external integration to sync with issues](#set-up-an-external-integration-to-sync-with-issues).
* A sync profile. For more information, see [Create a sync profile](../../../configure-cortex-xsiam/customize-cases-and-issues/create-a-sync-profile).
{% endhint %}

You can manually sync existing issues with external applications.

1. From the **Issues** page, right-click an issue and select **Run Automation** → **Select Automation**.
2. Under **Quick Actions**, select the action you want to configure, such as **Create Jira Ticket** or **Create ServiceNow Ticket**.
3.  Define the required ticket parameters.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>Using issue fields as variables is not currently supported.</p></div>
4.  Under **Using**, select the name of the instance to execute the command.

    <div data-gb-custom-block data-tag="hint" data-style="warning" class="hint hint-warning"><h3>Warning</h3><p>If you leave this field blank, all configured instances will be used.</p></div>
5. Under **Sync Configuration**, the following options are displayed, depending on your selection:
   * **Link to issue:** select this option if you want the issue to be linked to the created ticket. You must check this option if you want to sync the issue with the ticket.
   * **Sync Direction:** select the syncing configuration:
     * **Inbound:** Sync changes from the external ticket with the Cortex XSIAM issue.
     * **Outbound:** Sync changes from the Cortex XSIAM issue with the external ticket.
     * **Bi-directional:** Sync changes in both directions.
     * **None:** Do not sync changes between the Cortex XSIAM issue with the external ticket. If you select this option, the tickets are still linked, but changes are not synced. You can update this option at any time to start syncing.
6.  Define the inbound and/or outbound sync profiles.

    Depending on the selected option, select sync profiles that define field mapping between the issue and the external ticket. You can use the default sync profiles or you can create custom profiles. For more information about sync profiles, see [Create a sync profile](../../../configure-cortex-xsiam/customize-cases-and-issues/create-a-sync-profile).

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>You can only define a single inbound profile. If you change the inbound sync profile the current profile is overwritten.</p><p>You can define multiple outbound profiles; one issue can update multiple tickets.</p></div>
7.  Click **OK**.

    After ticket creation, the ticket number is shown in the Issue card. Click on the ticket number to see details about the created ticket and syncing configuration. In addition, the execution is recorded in the **War Room** tab. If there is a error in the requested action, you can see details in the audit.
8. View or edit the syncing configuration. For more information, see **View, update, or resolve a ticket** below.

#### Example

The following example shows an automation run on an issue to create a ServiceNow ticket that is synced in an outbound flow with the ticket.

![Outbound\_SNOW\_sync\_example.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-90168a95212d19d43da2c09e433db653f24a324e%2F035920bfaf9907d48b6df51c3e797e6cd0c85e9b663ef1b21da97c49e48caf6a.png?alt=media)

### Create an automation rule for syncing issues with external tickets

{% hint style="warning" %}
### Prerequisite

You must set up an integration before you can sync issues.
{% endhint %}

You can set up automation rules that create external tickets when certain issues occur and define the syncing configuration for transferring data between the issues and tickets.

1. Go to **Investigation & Response** → **Automation** → **Automation Rules**.
2. Click **Add Automation Rule**.
3. Enter a name and description for the rule.
4. Select whether to enable the rule after creation.
5. Under Rule Conditions, define the WHEN, and IF conditions. For more information about rule conditions, see [Create an automation rule](../../../configure-cortex-xsiam/automations/create-an-automation-rule).
6. Under THEN select the desired automation, such as **Create Jira Ticket** and complete the following fields:
   1.  Define the required ticket parameters.

       <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>Using issue fields as variables is not currently supported.</p></div>
   2.  Under **Using**, select the name of the instance to execute the command.

       <div data-gb-custom-block data-tag="hint" data-style="warning" class="hint hint-warning"><h3>Warning</h3><p>If you leave this field blank, all configured instances will be used.</p></div>
   3. Under **Sync Configuration**, the following options are displayed, depending on your selection:
      * **Link to issue:** select this option if you want the issue to be linked to the created ticket. You must check this option if you want to sync the issue with the ticket.
      * **Sync Direction:** select the syncing configuration:
        * **Inbound:** Sync changes from the external ticket with the Cortex XSIAM issue.
        * **Outbound:** Sync changes from the Cortex XSIAM issue with the external ticket.
        * **Bi-directional:** Sync changes in both directions.
        * **None:** Do not sync changes between the Cortex XSIAM issue with the external ticket. If you select this option, the tickets are still linked, but changes are not synced. You can update this option at any time to start syncing.
      *   Define the inbound and/or outbound sync profiles.

          Depending on the selected option, select sync profiles that define field mapping between the issue and the external ticket. You can use the default sync profiles or you can create custom profiles. For more information about sync profiles, see [Create a sync profile](../../../configure-cortex-xsiam/customize-cases-and-issues/create-a-sync-profile).

          <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>You can only define a single inbound profile. If you change the inbound sync profile the current profile is overwritten.</p><p>You can define multiple outbound profiles; one issue can update multiple tickets.</p></div>
   4.  Click **OK**.

       If a ticket is created, the ticket number is shown in the Issue card. You can click on the ticket number to see details about the created ticket and syncing configuration. In addition, the execution is recorded in the **War Room** tab. If there is a error in the requested action, you can see details in the audit.
7.  Click **Create**.

    The rule is added to the **Automation Rules** page. If required, drag to reorder the rules.

#### Example

The following example shows an automation rule that creates a Jira ticket with bi-directional syncing when a Critical Posture issue is triggered.

![issue\_sync\_automation\_rule.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-ab3b53f00a7a427eba42053ab50649351d9827f1%2Fd04f2e1b404cf393f108881c193d2174b737320070ba626d17641a987ef595b4.png?alt=media)

### View, update, or resolve a ticket

Once you have set up ticket syncing, you can view, update and resolve the issue and external ticket as required The changes are reflected according to the defined syncing configuration.

1.  To open the ticket details, in the **Overview** section of the issue card, click on the external ticket number.

    A panel opens with details of the external ticket. You can see the external ticket number, the sync configuration, and details of the ticket.
2. Open the linked ticket by clicking on the external ticket number in the panel.
3.  Update the fields as required.

    The updates are logged in the ticket history.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><ul><li>The inbound syncing flow runs every two minutes, and the outbound syncing flow runs every five minutes.</li><li>In a bi-directional set-up, if the same field is updated in both tickets, the most recently updated value is used.</li><li>In the external ticket, the logged history shows updates to the ticket. The user name that is logged with the history reflects the user token of the user who configured the data source.</li></ul></div>
4.  Resolve the ticket.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>After an issue is resolved, ticket syncing remains active for up-to seven days. Therefore, you still update, change, or reopen the issue or external ticket and the tickets will continue to sync.</p></div>

### Edit or disable ticket syncing

You can change the syncing configuration between a ticket and an issue from the issue card.

1.  In the **Overview** section of the issue card, click on the external ticket number.

    A panel opens with details of the ticket.
2. Click on the settings icon.
3.  Under **Sync Configuration**, change the syncing configuration as required.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>If you change the selected inbound sync profile, the original sync profile is immediately overwritten.</p></div>
4. To disable ticket syncing, take one of the following actions:
   *   To pause ticket syncing, set the **Sync Direction** value to **None**.

       This temporarily stops the tickets from syncing, but the tickets are still linked. You can update the syncing configuration at any time to resume ticket syncing.
   *   To unlink the tickets, uncheck **Link to issue**.

       This action is not reversable.
5. Click **Save**.

### Limitations of issue mirroring

Consider the following limitations of issue mirroring:

* Issue syncing requires the latest version of Atlassian Jira (V3) and ServiceNow (V2).
* Issue syncing is currently supported in Atlassian Jira (V3) and ServiceNow (V2) only.
* You can sync up to 50K objects.
* You can create a maximum of 200 sync profiles.
* Up to 100 inbound syncs are supported across all synced tickets over a two-minute period. Any additional changes beyond this limit will not be synced.
* If a connector instance is deleted or disabled, tickets are no longer synced and external ticket information is not available.
* Custom statuses are not supported.
* Currently, a specific set of fields is supported.
