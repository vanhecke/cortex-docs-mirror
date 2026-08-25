---
description: >-
  Create Cortex XSIAM case timers and custom SLAs to track KPIs, response-time
  goals, case milestones, and SLA compliance.
---

# Create additional case timers and SLAs

Create Cortex XSIAM case timers and custom SLAs to monitor key performance indicators (KPIs). Case SLAs track response-time goals, provide operational insights, and support established objectives.

{% hint style="info" %}
**Tip**

You don't need to build a resolution SLAs and timers from scratch. The following built-in fields are available in the **Cases** table:

* **Resolution Timer:** Works automatically out-of-the-box to measure elapsed case duration.
* **Resolution SLA:** Pre-positioned in the system, but requires you to configure your specific time goals to begin tracking compliance.

For more information, see [](<> "mention").
{% endhint %}

In addition to the default **Resolution Timer** and **Resolution SLA** fields, create timer and SLA fields for separate milestones. For example, track initial response times or enforce targets for specific customer tiers.

All active case SLAs are displayed in the case header.

Case SLAs are based on case timer fields. When a case matches defined criteria, the timer starts. When linked to an SLA, the timer tracks case progress against the SLA goal. The timer field counts up, and the SLA field counts down.

{% hint style="warning" %}
### Prerequisite

Before you can create a case SLA, you must first create a timer field. A timer field can be associated with a single case SLA.
{% endhint %}

<details>

<summary>Create a Cortex XSIAM case timer</summary>

Take the following steps to create a case timer field:

1. Go to **Settings** → **Configurations** → **Object Setup** → **Case** and open the **Fields** tab.
2. Click **New Field**.
3. Under **Field Type**, select **Timer**.
4. Type a field name.
5. Under **Tooltip**, enter a description to pop-up when you hover over the field.
6.  Under **Case Filter**, click **Set Filter** and define the subset of cases for which the timer will be activated. For example, you can define timers for specific domains or case source types.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>If you edit this filter after creation, the timer and associated SLA will be removed from any case that no longer qualifies, even if the timer is already running.</p></div>
7. Under **Conditions**, add filters that define when the timer will start and end. To add a pause condition to the timer, click **Pause** and define the pause criteria.
8. Under **When case is reopened**, select the action that you want Cortex XSIAM to take.
9. Click **Save**.

The following timer measures the amount of time a security case is waiting in **New** status before an analyst starts investigating.

| Field                 | Value                                               |
| --------------------- | --------------------------------------------------- |
| Field Type            | Timer                                               |
| Field Name            | Security case response                              |
| Tooltip               | Measure time from case opening to analyst response. |
| Cases Filter          | Case Domain = Security                              |
| Start when            | Status = New                                        |
| End when              | Status = Under Investigation                        |
| When case is reopened | Reset timer                                         |

</details>

<details>

<summary>Create a custom case SLA field</summary>

Take the following steps to create a case SLA. You can set up multiple goals for an SLA.

1. Go to **Settings** → **Configurations** → **Object Setup** → **Cases** and open the **Fields** tab.
2. Click **New Field**.
3. Under **Field Type**, select **SLA**.
4. Type a name to identify the SLA.
5. Under **Tooltip**, enter a description to pop-up when you hover over the field.
6. Under **Timer**, select the timer field with which to associate the SLA.
7.  Under **Goals**, click **Add SLA Goal**.

    The default goal applies to all cases that meet the filter criteria specified in the timer field. You can set up addition goals that apply to subsets of the defined cases.
8. In the SLA goal, type a goal name and set filter criteria.
9. In the **Days**, **Hours**, or **Minutes** fields, define the time conditions for to the SLA goal.
10. Arrange the SLA goals by dragging them in order of goal priority.
11. Click **Save**.

The following SLA field sets goals for analyst response times for security cases with Critical and High severity. This SLA is based on the timer field created in the previous example. Because the timer field is set up with the filter **Case Domain = Security**, this SLA will apply to security cases only.

The first SLA goal applies to security cases with a severity level of **Critical**. The SLA specifies that an analyst must respond to critical severity cases within one hour.

The second SLA goal applies to security cases with a severity level of **High**. The SLA specifies that an analyst must respond to high severity cases within two hours.

| Field      | Value                                                                                                   |
| ---------- | ------------------------------------------------------------------------------------------------------- |
| Field Type | SLA                                                                                                     |
| Field Name | Security case response SLA                                                                              |
| Tooltip    | Measure time from case opening to analyst response.                                                     |
| Timer      | Security case response                                                                                  |
| Goals      | <ul><li>Name: Critical severity cases</li><li>Minutes: 60</li><li>Filter: severity = Critical</li></ul> |
|            | <ul><li>Name: High severity cases</li><li>Minutes: 120</li><li>Filter: severity = High</li></ul>        |

</details>

<details>

<summary>Display case timer and SLA fields</summary>

After creating new timer and SLA fields, you can add them to the **Cases** table layout and view them in the **Cases** detailed view:

* In the **Cases** table view, add the timer and SLA fields to the **Layout** tab in the **Table Setting Menu**.
*   In the **Cases** detailed view, use the **Sort By** field to filter the cases list by the SLA field. Details of the SLA are shown in the list.

    In addition, create a custom case layout with a tab displaying SLA fields. For more information, see [case-layouts](../customize-case-fields-and-layouts/case-layouts "mention").

</details>

<details>

<summary>Example case timer and SLA fields</summary>

This example is based on the fields created in the previous procedures:

* The **Security case response** timer field displays the number of minutes since case creation. When the case status moves from **New** to **Under Investigation**, the timer stops.
* The **Security case response SLA** field starts counting backwards to show the remaining time to meet the SLA. If the field is shown in red with a minus time, the SLA is breached.
  * For case 001, the critical severity case has been in **New** status for 5 minutes. An analyst must respond within the remaining 55 minutes.
  * For case 002, the high severity case has been in **New** status for 20 minutes. An analyst must respond within the remaining 1 hour and 40 minutes.
  * For case 003, an analyst did not respond within 60 minutes and therefore the SLA was breached. The **Security case response SLA** field displays a minus value and a red icon.

| Case ID | Severity | Security case response | Security case response SLA                                                                                                                                                                                                                                                               |
| ------- | -------- | ---------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 001     | Critical | 5m                     | 55m 25s ![SLA\_timer.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-ad96902e8b99e8d7af95d5aee4162c48d3b403a3%2F034523c0d885528820fb1054168bcf8a7473a8d766543c0686c582c2aa8a6885.png?alt=media)    |
| 002     | High     | 20m                    | 1h 40m 30s ![SLA\_timer.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-ad96902e8b99e8d7af95d5aee4162c48d3b403a3%2F034523c0d885528820fb1054168bcf8a7473a8d766543c0686c582c2aa8a6885.png?alt=media) |
| 003     | Critical | 65m                    | - 5m 23s ![SLA\_breach.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-6320e10f587f889d23c82cd7f35ab57d02503a87%2F38bfa9547a4b3d99cabafa1aec2a175182764972c8d5e8fa2e6f00319816ac60.png?alt=media)  |

</details>

<details>

<summary>Case timer and SLA considerations</summary>

Consider the following information when working with timer and SLA fields:

* When a case is resolved, the timer calculation stops.
* Updating timer logic affects open and new cases. Therefore, the timer and associated SLA will be removed from any case that no longer qualifies, even if the timer is already running.
* If you delete a timer field, the SLA associated to the timer is also deleted.

</details>
