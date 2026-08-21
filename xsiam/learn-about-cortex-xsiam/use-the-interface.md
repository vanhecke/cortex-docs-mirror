---
description: >-
  Learn Cortex XSIAM interface navigation, filtering, saved views, result
  exports, system tools, and product areas.
---

# Use the Cortex XSIAM interface

The Cortex XSIAM interface provides a centralized security operations workspace. Use it to view and manage security data across your environment.

Use the navigation menu on the left to move between product areas in the tenant. For a quick overview of each area, see the **Navigation cheat sheet** below.

From the interface, you can:

* Navigate between product areas.
* Chat with an Agentic Assistant agent
* Filter table results to find relevant information.
* Create saved views with commonly used filter configurations.
* Export table data.
* Access in-product help and documentation.

{% hint style="info" %}
- Each SAML login session is valid for 8 hours.
- Some menu items only appear if you have the relevant license.
{% endhint %}

<details>

<summary>Filter Cortex XSIAM page results</summary>

To reduce the number of results, you can filter by any heading and value. When you apply a filter, Cortex XSIAM displays the filter criteria above the results table. You can also filter individual columns for specific values using the icon to the right of the column heading.

Some fields also support additional operators such as =, !=, Contains, not Contains, \*, !\*.Filters are persistent. When you navigate away from the page and return, any filter you added remains active.

To build a filter using one or more fields:

1.  From a Cortex XSIAM page, select filter (<img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-a3eff1c41e4db05b2bd4375bc349b6e526524282%2F3dab14fce079683094a6f5f3328b684c18fb2b68e00d2374edf76b84563d863d.png?alt=media" alt="filter-icon.png" data-size="line">).

    Cortex XSIAM adds the filter criteria above the top of the table.
2. For each field you would like to filter by:
   1. Select or search the field.
   2.  Select the operator that matches the criteria.

       Use **=** to include results that match the value you specify, or **!=** to exclude results that match the value.
   3.  Enter a value to complete the filter criteria.

       <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>CMD fields have a 128-character limit. Shorten longer query strings to 127 characters and add an asterisk (*).</p></div>

       Alternatively, you can select **Include empty values** to create a filter that excludes or includes results when the field has empty values.
3. To add additional filters, click **+AND,** within the filter brackets to display results that must match all specified criteria, or **+OR** to display results that match any of the criteria.
4. To see the results, click out of the filter area.

</details>

<details>

<summary>Save Cortex XSIAM views and filters</summary>

Cortex XSIAM allows you to save filter configurations so you can quickly return to commonly used data selections. Depending on the page you are working on, you can save either views or filters:

* **Saved views** store table configurations, including filters, so you can quickly switch between commonly used table perspectives.
* **Saved filters** store only the filter criteria, allowing you to quickly apply the same filtering logic again.

These options help you quickly focus on the data most relevant to your workflow.

**Saved views**

Saved views store filter configurations for table data, allowing you to quickly return to frequently used filters. You can filter table data by fields such as domain, context, or work queue, configure the columns you want to see, and save the configuration as a reusable view.

Saved views are available on most table-based pages, such as the **Cases** and **Issues** pages. The default view is All (for example, **All Cases**).

Select the arrow next to the view name to see all available views. If you modify filters in an existing view, you can update the view or save the configuration as a new view.

Save a view

1. Apply one or more filters.
2. Select **Save**.
3. Enter a name for the view.
4. Choose whether to share the view.

Manage views

* Use the three-dot **Actions** menu next to the view name to take the following actions:
  * Set the view as the default.
  * Share or unshare the view.
  * Update the view after modifying filters.
  * Delete the view.

{% hint style="info" %}
- Deleting a shared view removes it for all users.
- You can delete your own saved views.
- To delete views created by other users, you must have the Account administrator or Instance administrator role.
{% endhint %}

**Saved filters**

Some pages allow you to save filters instead of views, such as the **IOC** and **BIOC** pages.

Saved filters store filter criteria, allowing you to quickly apply the same filters again. Saved filters help standardize filtering and allow users to quickly apply commonly used search conditions.

Apply a saved filter

1. Open the three-dot **Actions** menu in the table filter row.
2. Select **Saved filters** and choose a filter to apply.
3. Click **Apply**.

Create a filter

1. Remove all filters from the table.
2. Click **Add filter** and define the filter values.
3. Click **Save** and define a filter name.

Share or delete a saved filter

1. Open the three-dot **Actions** menu in the table filter row.
2. Select **Saved filters**.
3. Click the **Actions** menu next to a filter name and select the relevant action.

{% hint style="info" %}
* Deleting a shared filter removes it for all users.
* You can delete your own saved filters.
* To delete filters created by other users, you must have the Account administrator or Instance administrator role.
{% endhint %}

</details>

<details>

<summary>Export Cortex XSIAM results</summary>

You can export the page results for most pages in Cortex XSIAM to a tab-separated values (TSV) file.

1. (**Optional**) Filter page results to reduce the number of results for export.
2.  Select export to file (<img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-2e7796360d71d97770146127e5a5ad1038b20fde%2F6992f55aca13ed26d2bc33ee3b53225ec10150bc0ef4eec957da801fa5c59ece.png?alt=media" alt="export-to-file-icon.png" data-size="line">).

    Cortex XSIAM exports any results matching your applied filters in TSV format. The TSV format requires a tab separator; automatic detection does not work in the case of multi-event exports.

</details>

<details>

<summary>Cortex XSIAM system tools and services</summary>

The following controls appear in the navigation bar and provide access to system tools, help resources, and tenant settings.

**Cortex Agentic Assistant**

Click <img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-fbf527afd3e824d282bea6ff747d08c2e5856a75%2Feb4f93ad10298e4a1a29a18b9b4c1d4415325cda8066af5f7ec57590d0c20cca.png?alt=media" alt="agentic-assistant.png" data-size="line"> in the top-right corner to open the assistant.

The Cortex Agentic Assistant is the autonomous AI capability of Cortex XSIAM. It uses AI agents that plan, reason, and investigate complex threats, such as cloud identity theft or container breaches.

**Notifications**

The Notifications panel displays system alerts and updates generated by Cortex XSIAM.

**Tenant Navigator**

Use **Tenant Navigator** to view and switch between tenants you have access to. Tenants are organized by CSP account. You can also navigate directly to the Cortex Gateway.

**Settings**

From the Settings menu, you can:

* View license information
* Manage audit logs
* Manage exceptions configuration
* Configure data sources and system settings

**Managed Services**

The Managed Threat Hunting service provides 24/7 monitoring by Palo Alto Networks threat researchers and Unit 42 experts.

**Help**

Cortex XSIAM provides in-product help directly within the interface.

Click <img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-ebd100e6504c9bbc9c438b60ecf5c52d421c0c63%2F84045266c4d924c900441db384bb47bc254683014a3042f0b02d60127a09e82c.png?alt=media" alt="in-app-help-center-icon.png" data-size="line"> to open the Help. There are two options:

* Documentation Portal
* Initiate Support Request

If you have the Cortex Agentic Assistant enabled, when you select **Initiate Support Request,** the **Help Center** agent opens to assist with finding relevant documentation, troubleshooting, and creating a support ticket. After your first prompt to the **Help Center** agent, you can click **Submit Support Ticket** above the chat. If you click **Submit Support Ticket**, you are brought directly to the **Submit Support Ticket** wizard.

If you do not have Cortex Agentic Assistant enabled, selecting **Initiate Support Request** brings you directly to the **Submit Support Ticket** wizard.

**User menu**

Click your **username** to access user and tenant options.

From the user menu, you can:

* View tenant information
* See What's New
* Switch between light and dark mode
* Log out

</details>

<details>

<summary>Cortex XSIAM navigation cheat sheet</summary>

**Dashboards & Reports**

| Component         | Description                                                                                                                                                 |
| ----------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Dashboard         | Select a dashboard/command center to view your tenant's activities, enabling you to effectively monitor your cases and overall activity in your environment |
| Reports           | View all the reports that Cortex XSIAM have run.                                                                                                            |
| Dashboard Manager | Manage dashboards, including adding dashboards with customized widgets to surface the statistics that matter to you most.                                   |
| Report Templates  | Build reports using pre-defined templates or customize a report. Reports can be generated on demand or scheduled.                                           |
| Widget library    | Search, view, edit, and create widgets based on predefined widgets and user-created custom widgets.                                                         |

**Cases & Issues**

| Component          | Description                                                                                                                                                                                                                                        |
| ------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Cases              | Investigate cases, manually create new cases, manage case severity and status, assign cases, and merge cases.                                                                                                                                      |
| Issues             | Investigate and manage individual issues. Run a playbook in the **Work Plan** for an individual issue or run the same playbook on multiple issues from the **Issues** table. Run commands in the **War Room**. Navigate to the **Findings** table. |
| Case Configuration | Add case scoring rules, view starred issues, and add featured hosts, users, and IP addresses.                                                                                                                                                      |

**Investigation & Response**

**Search**

| Component         | Description                                                                                                             |
| ----------------- | ----------------------------------------------------------------------------------------------------------------------- |
| Query Builder     | Build complex queries to investigate, identify connections, and expose the root cause of issues from your data sources. |
| Query Center      | View and manage the results of all simple and complex queries created from the Query Builder.                           |
| Scheduled Queries | View and manage all scheduled and recurring queries created from the Query Builder.                                     |

**Automation**

| Component        | Description                                                                                                                     |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| Playbooks        | Manage playbooks, including viewing, creating, and editing.                                                                     |
| Scripts          | Manage scripts. Use **Script Helper** to find relevant commands and scripts for your use case.                                  |
| Jobs             | Create and manage jobs to run a specific playbook, triggered either by time or a delta in a feed.                               |
| Playground       | Safely develop and test scripts, commands, and more, in a non-production environment not connected to a specific issue or case. |
| Automation Rules | Automatically respond to events by defining trigger conditions and desired actions to perform once the condition is met.        |

**Response**

| Component     | Description                                                                                                                                            |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Action Center | Provides a central location from which you can track the progress of all investigation, response, and maintenance actions performed on your endpoints. |
| Live Terminal | Initiate a remote connection to an endpoint, enabling you to remotely manage, investigate, and perform response actions on the endpoint.               |
| EDL           | Add malicious domains and IP addresses to an external dynamic list enforceable on your Palo Alto Networks firewall.                                    |

**Forensics**

| Component | Description                                                                                                                                                                  |
| --------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| N/a       | Streamline your case response, data collection, threat hunting, and analysis of your endpoint data to find the source and scope of an attack. Requires the Forensics add-on. |

**Notebooks**

| Component | Description                                                                                                                                                                                                                                     |
| --------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| N/a       | Use Jupyter tools to build machine learning models to visualize clusters, identify anomalies, and then feed your findings back into the Cortex XSIAM environment to generate security insights. You need a daily minimum of 1000 compute units. |

**Threat Management**

**Detection Rules**

| Component       | Description                                                                                                                                                                        |
| --------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| IOC             | Identify specific hashes, IP addresses, domains, file names, and paths that indicate a threat.                                                                                     |
| BIOC            | Identify a specific network, process, file, or registry activity that indicates a threat.                                                                                          |
| Correlations    | Analyze correlations of multiple events from multiple sources.                                                                                                                     |
| Indicator Rules | Create rules based on filters that are applied as either SHA256 and MD5 prevention rules in specific Agent Prevention Profiles or as file, IP address, and domain detection rules. |

**Threat Intelligence**

| Component           | Description                                                                                                       |
| ------------------- | ----------------------------------------------------------------------------------------------------------------- |
| Threat Intelligence | Requires Cortex XSIAM Premium or any other XSIAM license with the TIM add-on                                      |
| Indicators          | Indicators database. Search, review, and interact with indicators including IPs, domains, URLs, hashes, and more. |

**Posture Management**

Requires Cortex XSIAM Premium or any other XSIAM license with the Cloud Runtime Security add-on.

| Component                | Description                                                                                                                                                                                                             |
| ------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Vulnerability Management | View vulnerability issues, vulnerable assets, vulnerabilities, and vulnerability intelligence.                                                                                                                          |
| Compliance               | Determine asset vulnerabilities and risk by checking whether assets adhere to industry standards or your organization's best practices for compliance. You can select compliance standards from the compliance catalog. |
| Rules & Policies         | Create and edit rules and policies for cloud workload, cloud security, and vulnerability management.                                                                                                                    |

**Inventory**

**Assets**

| Component             | Description                                                                                                         |
| --------------------- | ------------------------------------------------------------------------------------------------------------------- |
| All Assets            | Provides a central location from which you can view and investigate information relating to assets in your network. |
| Groups                | Create and view groups of assets with shared attributes.                                                            |
| Network configuration | Define your internal IP address ranges and domain names to identify and track your network assets.                  |

**Endpoints**

| Component                  | Description                                                                                                                                                                                                                                                             |
| -------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| All Endpoints              | View and manage endpoints that have registered with your Cortex XSIAM instance.                                                                                                                                                                                         |
| Groups                     | Create endpoint groups to which you can perform actions and assign the policy.                                                                                                                                                                                          |
| Installations              | Create packages of the Cortex XSIAM agent software for deployment to your endpoints.                                                                                                                                                                                    |
| Host Insights              | Access comprehensive insights into your system's components, including applications, services, users, and vulnerability assessments, to maintain visibility and security across your environment.                                                                       |
| Policy Management          | Configure your endpoint security profiles and assign them to your endpoints.                                                                                                                                                                                            |
| Host Firewall              | Control communications on your endpoints by applying sets of rules that allow or block internal and external traffic.                                                                                                                                                   |
| Device Control Violations  | Monitor all instances where end users attempted to connect restricted USB-connected devices and Cortex XSIAM blocked them on the endpoint.                                                                                                                              |
| Disk Encryption Visibility | View and manage endpoints that were encrypted using BitLocker.                                                                                                                                                                                                          |
| File Integrity Monitoring  | A security control designed to detect unauthorized or anomalous modifications to files and folders in the file system. Any change, such as, a new file being created or an existing file being modified, will trigger an event that is sent to the Cortex XSIAM tenant. |

**Modules**

| Component            | Description                                                                                                                                                                                                                                                                                                                                                       |
| -------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| AI Security          | <p>Comprehensive overview of the AI assets within an organization. Designed to ensure AI security by offering tools to review and prioritize AI risks effectively.</p><p>This feature is included with a Cloud Runtime Security, Cloud Posture Security, or Cortex XSIAM Premium license.</p>                                                                     |
| Application Security | <p>Secures your applications by identifying and prioritizing them as a single, logical entity encompassing assets across the entire software development lifecycle (SDLC).</p><p>This feature is included with a Cloud Runtime Security, Cloud Posture Security, or Cortex XSIAM Premium license.</p>                                                             |
| Dats Security        | <p>Agentless multi-cloud data security platform that discovers, classifies, protects, and governs sensitive data.</p><p>This feature is included with a Cloud Runtime Security, Cloud Posture Security, or Cortex XSIAM Premium license.</p>                                                                                                                      |
| Identity Security    | <p>Runs a proprietary algorithm to calculate effective permissions and entitlements of the identities across your cloud service providers.</p><p>This feature is included with a Cloud Runtime Security, Cloud Posture Security, or Cortex XSIAM Premium license.</p>                                                                                             |
| Kubernetes Security  | <p>Automatically discovers assets, enforces policies, and scans for vulnerabilities, malware, secrets, and misconfigurations across the environment.</p><p>This feature is included with a Cloud Runtime Security, Cloud Posture Security, or Cortex XSIAM Premium license.</p>                                                                                   |
| Attack Surface       | ASM helps you discover and manage your public attack surface, providing visibility into all of your digital assets, including on-prem and cloud. Identify and remediate vulnerabilities, enforce compliance policies, and reduce the risk of cyberattacks. Included in Cortex XSIAM Premium or any other XSIAM license with the Attack Surface Management add-on. |
| Email Security       | Provides a scalable detection, investigation, and response layer over cloud-hosted email environments. It connects directly to supported email platforms via secure API integrations to ingest rich message-level and identity-related telemetry. Requires the Email Security add-on.                                                                             |
| Exposure Management  | A collection of features, capabilities, integrations, and content designed to help defenders holistically assess, consolidate, prioritize, and proactively respond to exposures in their organization. Requires the Exposure Management add-on.                                                                                                                   |

**Agentic Assistant Hub**

{% hint style="info" %}
This menu item appears if you have enabled the Cortex Agentic Assistant.
{% endhint %}

Manage agentic agents and actions in the Agentic Assistant Hub.

</details>
