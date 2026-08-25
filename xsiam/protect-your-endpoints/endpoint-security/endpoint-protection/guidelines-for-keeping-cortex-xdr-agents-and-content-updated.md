---
description: >-
  Plan phased Cortex XDR agent and content updates to maintain endpoint
  protection in Cortex XSIAM.
---

# Guidelines for keeping Cortex XDR agents and content updated

Cortex XSIAM helps you manage Cortex XDR agent upgrades and security content updates across endpoints. Use a phased rollout to reduce production risk while delivering current endpoint protection capabilities.

### Why keep agents and content updated

Keeping Cortex XDR agents up-to-date is essential for protecting against evolving threats and vulnerabilities. Regular updates ensure the latest security features for malware and exploit prevention, and compatibility with the latest software environments, which helps reduce the risk of attacks. This can also help organizations meet regulatory standards while maintaining strong overall protection.

Content updates, such as new threat intelligence or detection logic, are critical for defending against newly discovered cyber threats and malware and are designed to ensure that systems remain protected against the latest attacks. Content updates, released on a weekly basis, address compatibility issues as well, helping to achieve smooth operations alongside the Cortex XDR agent. Without regular content updates, security solutions may fail to detect new or evolving threats, leaving systems vulnerable to attacks.

The Cortex XDR agent can retrieve content updates immediately as they become available, or after a pre-configured delay period of up to 30 days. In addition, to expedite testing and evaluation, the staging content provides a preview of the content update a week before it is published to GA.

{% hint style="info" %}
### Important

When planning Cortex XDR agent upgrades and content updates, consult with the appropriate stakeholders and teams and follow the change management strategy in your organization.
{% endhint %}

Cortex XSIAM can be configured to manage the deployment of agent and content updates by adjusting the following settings:

**Agent settings per endpoint:**

* **Agent Auto-Upgrade** is disabled by default. Before enabling agent auto-upgrade for Cortex XDR agents, make sure to consult with all relevant stakeholders in your organization. Enabling this option allows you to define the scope of the automatic updates, such as upgrading to the latest agent release, one release prior, only maintenance releases, or maintenance releases within a specific version.
* **Upgrade Rollout** includes two options: Immediate, where the Cortex XDR agent automatically receives new releases, including maintenance updates and features, and Delayed, which lets you set a delay of 7 to 45 days after a version is released before upgrading endpoints.
* **Agent Upgrade Scheduler** allows the upgrade task to be scheduled for specific days of the week and a specific time range.

**Global agent settings:** Configure the number of parallel upgrades to apply to all endpoints in your organization.

**Content updates per endpoint:**

* **Content Auto-Update** is enabled by default and automatically retrieves the latest content before deploying it on the endpoint. If you disable content updates, the agent will stop fetching updates from the Cortex XSIAM tenant and will continue to operate with the existing content on the endpoint.
* **Content Rollout:** The Cortex XDR agent can retrieve content updates immediately as they become available, after a pre-configured delay period of up to 30 days. Utilize the staging content for early evaluation on test environments before the content is released to production.

**Global content updates:** Configure the content update cadence and bandwidth allocation within your organization. To enforce immediate protection against the latest threats, enable minor content updates. Otherwise, the content updates in your network occur only on major releases.

### Plan Cortex XDR agent upgrades

Use a phased rollout plan by creating batches for deploying updates. The specifics may vary based on your organization and its structure. Start with a control group, then deploy to 10% of your organization. Subsequently, allocate the remaining upgrades in batches that best suit your organization until achieving a full 100% rollout.

The following is an example of a rollout plan for deploying a Cortex XDR agent upgrade:

**Phase 1: Control group rollout:** Start by selecting a control group of endpoints as early adopters. This group should consist of a diverse range of operating systems, devices, applications, and servers, with a focus on low-risk endpoints. After a defined testing period, such as one week, assess for any issues. If no problems are found, move to the next phase.

**Phase 2: 10% rollout:** Expand the rollout to 10% of the organization’s endpoints. This group should maintain the same variety as the control group but include low- to medium-risk endpoints. Monitor performance during the set period. If the rollout is successful with no issues, proceed to the next phase.

**Phase 3: 40% rollout:** After confirming the success of the 10% rollout, extend the deployment to 40% of the organization. Continue including a variety of endpoints while gradually incorporating some medium-risk endpoints. Ensure thorough testing during this phase before moving forward.

**Phase 4: 80% rollout:** Extend the deployment to 80% of the organization's endpoints. This batch should include a wide variety of endpoints, incorporating both medium and high-risk systems. After a careful monitoring period and confirmation that everything is stable, move to the final phase.

**Phase 5: Full rollout:** Complete the rollout by updating the remaining 20% of the organization’s endpoints. By this point, the majority of systems should have been thoroughly tested, reducing the risk of issues in the final stage. Once complete, 100% of the organization will be updated.

![agentupgradeflow.gif](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-db1880af14014aac99b0130e185b562a2745b368%2F149b07ab6d178c7c5eac9210dd75d5adf1e8d7556ada05764b0531b2bac38d1d.gif?alt=media)

### Plan content updates

Content updates consist of detection rules and operational logic, and are typically released on a weekly basis. Staging content provides a preview of the content update a week before the published GA.

Use a phased rollout plan by creating batches for deploying updates. Start with a control group, then deploy to 10% of your organization. Subsequently, allocate the remaining upgrades in batches that best suit your organization until achieving a full 100% rollout.

For early evaluation, select a small test group or a lab environment for enabling the staging content preview.

The following is an example of a rollout plan over a period of one week for deploying content updates:

**Phase 1: Control group rollout:** Keep the default configuration set to deploy content updates immediately.

**Phase 2: 10% rollout:** Content is automatically deployed on day 2 following a delay period defined in the profile.

**Phase 3: 60% rollout:** Content is automatically deployed on day 3 following a delay period defined in the profile.

**Phase 4: Full rollout:** Increase the deployment to include medium- and high-risk systems, until the entire organization is updated.

![contentupgradeflow.gif](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-7ba7a069cba51c07cbe6466cb27aa090b896d4c1%2F67824809ef70f95f08baa45e4e42948389ca28749b299a365b94c52be0e1d1b8.gif?alt=media)

### Configure agent and content updates

The following information will help you select and configure the update settings.

#### Cortex XDR agent upgrades

Configure one or more of the settings described in this section to keep your Cortex XDR agents up-to-date.

<details>

<summary>Distribute agent upgrades to selected endpoints</summary>

1.  Create an agent installation package for each operating system version for which you want to upgrade the Cortex XDR agent.

    Note the installation package names.
2.  Select **Inventory** → **Endpoints** → **All Endpoints**.

    If needed, filter the list of endpoints. To reduce the number of results, use the endpoint name search and filters at the top of the page.
3.  Select the endpoints you want to upgrade.

    You can also select endpoints running different operating systems to upgrade the agents at the same time.
4.  Right-click your selection and select **Endpoint Control** → **Upgrade Agent Version**.

    For each platform, select the name of the installation package you want to push to the selected endpoints.

    You can install the Cortex XDR agent on Linux endpoints using a package manager. If you do not want to use the package manager, clear the option **Upgrade to installation by package manager**.

    When you upgrade an agent on a Linux endpoint that is not using a package manager, Cortex XSIAM upgrades the installation process by default according to the endpoint Linux distribution.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>The Cortex XDR agent keeps the name of the original installation package after every upgrade.</p></div>
5.  **Upgrade**.

    Cortex XSIAM distributes the installation package to the selected endpoints at the next heartbeat communication with the agent. To monitor the status of the upgrades, go to **Investigation and Response** → **Response** → **Action Center**.

    From the **Action Center** you can also view additional information about the upgrade (right-click the action and select **Additional data**) or cancel the upgrade (right-click the action and select **Cancel Agent Upgrade**).

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><ul><li>Custom dashboards that include upgrade status widgets, and the <strong>All Endpoints</strong> page display upgrade status.</li><li>During the upgrade process, the endpoint operating system might request a reboot. However, you do not have to perform the reboot for the Cortex XDR agent upgrade process to complete it successfully.</li><li>After you upgrade on an endpoint with Cortex XSIAM Device Control rules, you need to reboot the endpoint for the rules to take effect.</li></ul></div>

</details>

<details>

<summary>Agent settings per endpoint</summary>

{% hint style="info" %}
### Note

These profiles can be configured on one or more endpoints, static/dynamic groups, tags, IP ranges, endpoint names, or other parameters that allow the creation of logical endpoint groups. See [how to define endpoint group](https://app.gitbook.com/s/AEIjuYE3RXcIfmuQnBbm/deployment-steps/install-cortex-xdr-agents/define-endpoint-groups).
{% endhint %}

1. Go to **Inventory** → **Endpoints** → **Policy Management** → **Profiles**, and then edit an existing profile, add a new profile, or import from a file.
2.  If you're adding a new profile, select the operating system and **Agent Settings**. Then click **Next**.

    If you want to edit an existing profile, hover over **Agent Settings** for the operating system and click **View Profile**.
3.  Select **Agent Upgrade**. By default, this option is disabled.

    <div data-gb-custom-block data-tag="hint" data-style="warning" class="hint hint-warning"><h3>Caution</h3><p>Before enabling Auto-Update for Cortex XDR agents, make sure to consult with all relevant stakeholders in your organization.</p></div>

The following table describes the available **Agent Auto-Upgrade** options:

| Item                    | Options                                                                                                                                                                              | Description                                                                                                                                                                                                                                                                                                                                                                                                              |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Automatic Upgrade Scope | <ul><li>Latest agent release (Default)</li><li>One release before the latest one</li><li>Only maintenance releases</li><li>Only maintenance releases in a specific version</li></ul> | <p>For <strong>One release before the latest one</strong>, Cortex XSIAM upgrades the agent to the previous release before the latest, including maintenance releases. Major releases are numbered X.X, such as release 8.0, or 8.2. Maintenance releases are numbered X.X.X, such as release 8.2.2.</p><p>For <strong>Only maintenance releases in a specific version</strong>, select the required release version.</p> |
| Upgrade Rollout         | <ul><li>Immediate (Default)</li><li>Delayed</li></ul>                                                                                                                                | <p>The Cortex XDR agent automatically fetches any new agent release, maintenance and new features.</p><p>For <strong>Delayed</strong>, set the delay period (number of days) to wait after the version release before upgrading endpoints. Choose a value between 7 and 45.</p>                                                                                                                                          |
| Scheduling              | <ul><li>Hours</li><li>Days of the week</li></ul>                                                                                                                                     | Schedule the upgrade task for specific time and days of the week.                                                                                                                                                                                                                                                                                                                                                        |

</details>

<details>

<summary>Global agent settings</summary>

Configure the Cortex XDR agent upgrade scheduler and the number of parallel upgrades to apply to all endpoints in your organization.

1. Go to **Settings** → **Configurations** → **Agent Configurations**, and scroll to **Agent upgrade**.
2.  Configure the Cortex XDR agent upgrade scheduler and the number of parallel upgrades.

    | Item                        | Description                                                                                                                                                                                                                                                                                                                    |
    | --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
    | Amount of parallel upgrades | <p>During the first week of a new Cortex XDR agent release rollout, only a single batch of agents is upgraded. After that, auto-upgrades continue to be deployed across your network with the number of parallel upgrades as configured.</p><p>Set the number of parallel agent upgrades, where the maximum is 500 agents.</p> |

</details>

#### Content updates

When a new content update is available, Cortex XSIAM notifies the Cortex XDR agent. The Cortex XDR agent then randomly chooses a time within a six-hour window during which it will retrieve the content update from Cortex XSIAM. By staggering the distribution of content updates, Cortex XSIAM reduces the bandwidth load and prevents bandwidth saturation due to the high volume and size of the content updates across many endpoints. You can view the distribution of endpoints by content update version from the dashboard.

You can configure whether to update content per endpoint or use the global settings.

![content\_version\_breakdown.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-0bb437fe7f56ad67eac2287409d55d4b37a4ffcd%2Fd5a860ad21cbf825cd931a211d3a6b2956d37b60e3f1d4499324faefd31431af.png?alt=media)

<details>

<summary>Content update settings per endpoint</summary>

Configure content update options for agents within the organization to ensure it is always protected with the latest security measures.

{% hint style="info" %}
### Note

These profiles can be configured on one or more endpoints, static/dynamic groups, tags, IP ranges, endpoint names, or other parameters that allow the creation of logical endpoint groups.
{% endhint %}

The following table describes the available **Content Configuration** options:

1. Go to **Inventory** → **Endpoints** → **Policy Management** → **Profiles**, and then edit an existing profile, add a new profile, or import from a file.
2.  If you're adding a new profile, select the operating system and **Agent Settings**. Then click **Next**.

    If you want to edit an existing profile, hover over **Agent Settings** for the operating system and click **View Profile**.
3. Select **Content Configuration**. By default, this option is Enabled.

| Item                | Options                                                                | More details                                                                                                                                                                                                                                                                                                                                                                                                                                |
| ------------------- | ---------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Content Auto-Update | <ul><li>Enabled (Default)</li><li>Disabled</li></ul>                   | <p>When Content Auto-Update is enabled, the Cortex XDR agent retrieves the most updated content and deploys it on the endpoint.</p><p>If you disable content updates, the agent stops retrieving them from the Cortex XSIAM tenant, and keeps working with the current content on the endpoint.</p>                                                                                                                                         |
| Staging Content     | <ul><li>Enabled</li><li>Disabled (Default)</li></ul>                   | Enable users to deploy agent staging content on selected test environments. Staging content is released before production content, allowing for early evaluation of the latest content update.                                                                                                                                                                                                                                              |
| Content Rollout     | <ul><li>Immediate (Default)</li><li>Delayed</li><li>Specific</li></ul> | <p>The Cortex XDR agent can retrieve content updates immediately as they are available, after a pre-configured delay period of up to 30 days, or you can select a specific version.</p><p>When you delay content updates, the Cortex XDR agent will retrieve the content according to the configured delay. For example, if you configure a delay period of two days, the agent will not use any content released in the last 48 hours.</p> |

</details>

<details>

<summary>Global content update settings</summary>

1. Go to **Settings** → **Configurations** → **Agent Configurations**, and scroll to **Content Management**.
2.  Configure the content update cadence and bandwidth allocation within your organization.

    | Item                                     | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
    | ---------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | Enable bandwidth control                 | Based on the number of agents you want to update with content and upgrade packages, active or future agents, the Cortex XSIAM calculator configures the recommended amount of Mbps (Megabits per second) required for a connected agent to retrieve a content update over a 24 hour period or a week. Cortex XSIAM supports between 20 - 10000 Mbps, you can enter one of the recommended values or enter one of your own. For optimized performance and reduced bandwidth consumption, it is recommended that you install and update new agents with Cortex XDR agents 7.3 and later include the content package built in using SCCM. |
    | XDR Calculator for Recommended Bandwidth | <p>Based on the number of agents you want to update with content and upgrade packages, active or future agents, the Cortex XSIAM calculator configures the recommended amount of Mbps (Megabits per second) required for a connected agent to retrieve a content update over 24 hours or a week. This calculation is based on connected agents and includes an overhead for large content update.</p><p>Cortex XSIAM supports between 20 - 10000 Mbps.</p><p>It is recommended to allocate a minimum of 20 Mbps, or you can enter a value.</p>                                                                                         |
    | Enable minor content version updates     | To enforce immediate protection against the latest threats, enable minor content updates. Otherwise, the content updates in your network occur only on major releases.                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |

</details>
