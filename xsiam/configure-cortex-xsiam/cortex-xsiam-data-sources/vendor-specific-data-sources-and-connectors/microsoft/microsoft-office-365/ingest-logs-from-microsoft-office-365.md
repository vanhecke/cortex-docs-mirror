# Ingest logs from Microsoft Office 365

{% hint style="warning" %}
**Important**

**Migration Advisory: Microsoft Graph Security API v1 to v2**

Microsoft will retire the [Legacy Alerts (v1)](https://learn.microsoft.com/en-us/graph/api/resources/security-api-overview?view=graph-rest-1.0\&preserve-view=true#legacy-alerts) API endpoint in **April 2026**. To avoid service interruption, instances currently using the legacy Alerts (v1) option must manually transition to the [v2 GA](https://learn.microsoft.com/en-us/graph/api/resources/security-alert?view=graph-rest-1.0) endpoint by selecting the Alerts → Security Alerts V2 option.

* **Schema impact**: Moving from v1 to v2 involves schema changes. While all out-of-the-box content is compatible, you must manually review and adjust custom correlation rules, parsing rules, and dashboards to align with the v2 schema.
{% endhint %}

{% hint style="info" %}
**Note**

* Ingesting Microsoft Entra ID (formerly known as Azure AD) authentication and audit events from Microsoft Graph API requires a Microsoft Azure Premium 1 or Premium 2 license. Alternatively, if the directory type is Azure AD B2C, the sign-in reports are accessible through the API without any additional license requirement.
* To ingest **email** logs and data from Microsoft Office 365, use the dedicated data collector. For more information, see [Ingest logs and data from Microsoft 365](../microsoft-office-365-email/ingest-logs-and-data-from-microsoft-365).
{% endhint %}

Cortex XSIAM can ingest the following logs and data from Microsoft Office 365 Management Activity API and Microsoft Graph API using the Office 365 data collector. Alerts are collected with a delay of 5 minutes. If your organization requires collection that is closer to real-time collection, we recommend using the Microsoft Azure Event Hub integration instead. For more information, see [Ingest logs from Microsoft Azure Event Hub](../azure-event-hub/ingest-logs-from-microsoft-azure-event-hub).

To ingest email logs and data from Microsoft Office 365, use the dedicated data collector. For more information, see [Ingest logs and data from Microsoft 365](../microsoft-office-365-email/ingest-logs-and-data-from-microsoft-365).

*   Microsoft Office 365 audit events from Management Activity API, which provides information about various user, administrator, system, and policy actions and events from Office 365, Microsoft Entra ID (formerly known as Azure AD) and MDO activity logs.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>When auditing is turned off from the default setting, you need to first <a href="https://learn.microsoft.com/en-us/microsoft-365/compliance/turn-audit-log-search-on-or-off?view=o365-worldwide#verify-the-auditing-status-for-your-organization">turn on auditing</a> for your organization to collect Microsoft Office 365 audit events from the Management Activity API. Log duplication of up to 5% in Microsoft products is considered normal. In some cases, such as login to a portal using MFA, two log entries are recorded by design.</p></div>
*   Microsoft Entra ID (Azure AD) authentication and audit events from Microsoft Graph API.

    When collecting Azure AD Authentication Logs, Cortex XSIAM also collects by default all sign-in event types from a beta version of Microsoft Graph API, which is still subject to change. In addition to classic interactive user sign-ins, selecting this option allows you to collect.

    * Non-interactive user sign-ins.
    * Service principal sign-ins.
    * Managed Identities for Azure resource sign-ins.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>To address <a href="https://docs.microsoft.com/en-us/azure/active-directory/reports-monitoring/reference-reports-latencies">Azure reporting latency</a>, there is a 10-minute latency period for Cortex XSIAM to receive Azure AD logs.</p></div>
* Microsoft 365 alerts from Microsoft Graph Security API are available for different products.
  *   Microsoft Graph Security API v1: Alerts from various products (including Microsoft Defender for Cloud and Microsoft Entra ID Protection) are available via this endpoint.

      <div data-gb-custom-block data-tag="hint" data-style="warning" class="hint hint-warning"><p><strong>Important</strong></p><p>Microsoft has deprecated the <a href="https://learn.microsoft.com/en-us/graph/api/resources/security-api-overview?view=graph-rest-1.0&#x26;preserve-view=true#legacy-alerts">Legacy Alerts (v1)</a> API in <strong>April 2026</strong>. To avoid service interruption, you must migrate to the <a href="https://learn.microsoft.com/en-us/graph/api/resources/security-alert?view=graph-rest-1.0">v2 endpoint</a> before this date.</p></div>

      * Microsoft Defender for Cloud, Azure Active Directory Identity Protection, Microsoft Defender for Cloud Apps, Microsoft Defender for Endpoint, Microsoft Defender for Identity, Microsoft 365, Azure Information Protection, and Azure Sentinel.
  *   Microsoft Graph Security API v2 (GA): This endpoint provides a unified alerts API for Microsoft 365 Defender, Microsoft Defender for Identity, and Microsoft Purview Data Loss Prevention.

      * Microsoft 365 Defender unified alerts API, which serves alerts from Microsoft 365 Defender, Microsoft Defender for Endpoint, Microsoft Defender for Office 365, Microsoft Defender for Identity, Microsoft Defender for Cloud Apps, and Microsoft Purview Data Loss Prevention (including any future new signals integrated into M365D).

      To view alerts from the various products via the Microsoft Graph Security API versions, you need to ensure that you've set up the applicable licenses in Office 365. The table below lists the various licenses required for the different Microsoft Defender products. For more information on other Microsoft product licenses, see the Microsoft documentation.

      | Product                                  | Standalone license | E3 license | E3 + Security add-on license | E5 license | E5 Security license | E5 Compliance license |
      | ---------------------------------------- | ------------------ | ---------- | ---------------------------- | ---------- | ------------------- | --------------------- |
      | Microsoft Defender for Endpoint Plan 1   | ✓                  | ✓          | ✓                            | —          | —                   | —                     |
      | Microsoft Defender for Endpoint Plan 2   | —                  | —          | ✓                            | ✓          | ✓                   | —                     |
      | Microsoft Defender for Identity          | —                  | —          | ✓                            | ✓          | ✓                   | —                     |
      | Microsoft Defender for Office 365 Plan 1 | ✓                  | —          | —                            | —          | —                   | —                     |
      | Microsoft Defender for Office 365 Plan 2 | ✓                  | —          | ✓                            | ✓          | ✓                   | —                     |
      | Microsoft Defender for Cloud Apps        | —                  | —          | ✓                            | ✓          | ✓                   | ✓                     |

{% hint style="info" %}
**Note**

For more information, see the [Office 365 Management Activity API schema](https://docs.microsoft.com/en-us/office/office-365-management-api/office-365-management-activity-api-schema).
{% endhint %}

To receive logs from Microsoft Office 365, you must first configure the Data Sources & Integrations settings in Cortex XSIAM. After you set up data collection, Cortex XSIAM begins receiving new logs and data from the source.

When Cortex XSIAM begins receiving logs, the app creates a new dataset for the different types of logs and data that you are collecting, which you can use to initiate XQL Search queries. For example queries, refer to the in-app XQL Library. For all Microsoft Office 365 logs, Cortex XSIAM can also generate Cortex XSIAM issues (Analytics, IOC, BIOC, and Correlation Rules), when relevant, from Office 365 logs. While Correlation Rules issues are generated on non-normalized and normalized logs, Analytics, IOC, and BIOC issues are only generated on normalized logs.

For the different types of data you can collect using the Office 365 data collector, the following table lists the different datasets, vendors, and products automatically configured, and whether the data is normalized.

| Data type                                                                    | Dataset                           | Vendor | Product                  | Normalized data                                                                                                                          |
| ---------------------------------------------------------------------------- | --------------------------------- | ------ | ------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------- |
| Microsoft Office 365 audit events from Management Activity API               |                                   |        |                          |                                                                                                                                          |
| <ul><li>Microsoft Entra ID (Azure AD)</li></ul>                              | `msft_o365_azure_ad_raw`          | `msft` | `O365 Azure AD`          | —                                                                                                                                        |
| <ul><li>Exchange Online</li></ul>                                            | `msft_o365_exchange_online_raw`   | `msft` | `O365 Exchange Online`   | Cortex XSIAM supports normalizing Exchange Online audit logs into stories, which are collected in a dataset called `saas_audit_logs*`.   |
| <ul><li>SharePoint Online</li></ul>                                          | `msft_o365_sharepoint_online_raw` | `msft` | `O365 Sharepoint Online` | Cortex XSIAM supports normalizing SharePoint Online audit logs into stories, which are collected in a dataset called `saas_audit_logs*`. |
| <ul><li>DLP</li></ul>                                                        | `msft_o365_dlp_raw`               | `msft` | `O365 DLP`               | —                                                                                                                                        |
| <ul><li>General</li></ul>                                                    | `msft_o365_general_raw`           | `msft` | `O365 General`           | Cortex XSIAM supports normalizing General audit logs into stories, which are collected in a dataset called `saas_audit_logs*`.           |
| Microsoft Entra ID (Azure AD) authentication events from Microsoft Graph API | `msft_azure_ad_raw`               | `msft` | `Azure AD`               | When relevant, Cortex XSIAM normalizes Azure AD authentication logs and Azure AD Sign-in logs to authentication stories.                 |
| Microsoft Entra ID (Azure AD) audit events from Microsoft Graph API          | `msft_azure_ad_audit_raw`         | `msft` | `Azure AD Audit`         | When relevant, Cortex XSIAM normalizes Azure AD audit logs to cloud audit logs stories.                                                  |
| Alerts from Microsoft Graph Security API v1 and v2                           | `msft_graph_security_alerts_raw`  | `msft` | `Security Alerts`        | —                                                                                                                                        |

{% hint style="info" %}
**\*Note**

For the `saas_audit_logs` dataset, the Vendor is saas and Product is Audit Logs.
{% endhint %}

{% hint style="info" %}
**Note**

In FedRAMP environments, Azure sign-in logs are not supported, due to vendor technical constraints.
{% endhint %}

How to set up the Office 365 integration

1.  From the Microsoft Entra ID console (formerly Azure AD console), create an app for Cortex XSIAM with the applicable API permissions for the logs and data you want to collect as detailed in the following table:\
    **Required Azure AD / Entra ID API permissions**\
    \
    When registering the app for Cortex XSIAM in the Microsoft Entra ID console, you must assign the permissions listed below.

    <div data-gb-custom-block data-tag="hint" data-style="warning" class="hint hint-warning"><p><strong>Important</strong></p><p>All permissions listed below must be granted as Application Permissions, not Delegated permissions.</p></div>

| Log type and data                                                 | API/Permission name                                                                                          |
| ----------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------ |
| Microsoft Office 365 audit events from Management Activity API    |                                                                                                              |
| Azure AD                                                          | Office 365 Management APIs → ActivityFeed.Read                                                               |
| Exchange Online                                                   | Office 365 Management APIs → ActivityFeed.Read                                                               |
| Sharepoint Online                                                 | Office 365 Management APIs → ActivityFeed.Read                                                               |
| DLP                                                               | Office 365 Management APIs → ActivityFeed.ReadDlp                                                            |
| General                                                           | Office 365 Management APIs → ActivityFeed.Read                                                               |
| Azure AD authentication and audit events from Microsoft Graph API | <ul><li>Microsoft Graph → AuditLog.Read.All</li><li>Microsoft Graph → Directory.Read.All</li></ul>           |
| Alerts from Microsoft Graph Security API v1 and v2                | <ul><li>Microsoft Graph → SecurityAlert.Read.All</li><li>Microsoft Graph → SecurityEvents.Read.All</li></ul> |

For more information on Microsoft Azure, see the following instructions in the Microsoft documentation portal.

* [Register an app](https://docs.microsoft.com/en-us/azure/active-directory/develop/quickstart-register-app).
* [Add API permissions with type Application](https://docs.microsoft.com/en-us/azure/active-directory/develop/quickstart-configure-app-access-web-apis#add-permissions-to-access-web-apis).
* [Create an application secret](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#create-a-new-application-secret).

2. Navigate to Settings → Data Sources & Integrations.
3. On the Data Sources & Integrations page, click + Add New, search for Office 365, then hover over it and click Add.
4.  Integrate the applicable Microsoft Entra ID (Azure AD) service with Cortex XSIAM.

    a. Specify the Tenant Domain of your Microsoft Entra ID tenant.

    b. Obtain the Application Client ID and Secret for your Microsoft Entra ID (Azure AD) service from the Microsoft Entra ID console, and specify the values in Cortex XSIAM. These values enable Cortex XSIAM to authenticate with your Microsoft Entra ID (Azure AD) service.

    c. Select the types of logs that you want to receive from Office 365.\
    The following options are available.

    * Office 365 Management Activity API
      * Cloud Environment: select the cloud environment used by your organization:
        * Enterprise: Default option for non-US Government tenants
        * GCC: US Government Compliant Cloud tenants
        * GCC High: US Government Compliant Cloud High tenants
        * DoD: US Department of Defense tenants
      * Azure AD: Includes subset of Azure AD audit events and Azure AD authentication events. There can be significant overlap between these and the Azure AD Authentication Logs originating from Microsoft Graph API. ### Note Use this option when you don’t want to grant permissions for Azure AD Authentication and Azure AD Audit.
      * Exchange Online: Includes audit logs on [Azure Exchange mailboxes](https://docs.microsoft.com/en-us/office/office-365-management-api/office-365-management-activity-api-schema#exchange-mailbox-schema) and [Exchange admin activities](https://docs.microsoft.com/en-us/office/office-365-management-api/office-365-management-activity-api-schema#exchange-admin-schema) on the Office 365 Exchange.
      * Sharepoint Online: Includes audit events on Sharepoint and OneDrive activities.
      * DLP: Includes Microsoft 365 DLP events for Exchange, Sharepoint, and OneDrive.
      * General: Includes audit logs for [various Microsoft 365 applications](https://docs.microsoft.com/en-us/office/office-365-management-api/office-365-management-activity-api-schema), such as Power BI and Microsoft Forms.
    * Microsoft Graph API
      * Cloud Environment: select the cloud environment used by your organization:
        * Global Service: Default option for non-US Government tenants
        * Government L4: US Government Layer 4 tenants
        * Government L5 (DOD): US Government Layer 5 tenants
      * Azure AD Authentication Logs: Collects interactive sign-in events using the Microsoft Graph API. These logs are part of Microsoft Entra ID (formerly Azure AD) and are found under [Microsoft Entra sign-in logs](https://docs.microsoft.com/en-us/azure/active-directory/reports-monitoring/concept-sign-ins).Collect all sign-in event types: When enabled, this option switches the collection to a beta version of the Microsoft Graph API.**This beta API may experience instability, collection lags, and temporary data gaps.** For production environments, we recommend using the [Azure Event Hub collector](../azure-event-hub/ingest-logs-from-microsoft-azure-event-hub) instead of this nested option to ensure consistent data delivery. This setting should be used for non-production or evaluation purposes only. In addition to classic interactive user sign-ins, this option expands Azure AD Sign-in logs to include: -Non-interactive user sign-ins. -Service principal sign-ins. -Managed Identities for Azure resource sign-ins.
      * Azure AD Audit Logs: [Azure AD Audit logs](https://docs.microsoft.com/en-us/azure/active-directory/reports-monitoring/concept-audit-logs) includes different categories, such as User Management, Group Management and Application Management.
      * Alerts: When this checkbox is selected, define how alerts are collected by selecting one of the following options:
        * Security Alerts V2 (Default): Alerts are collected via the [v2 GA](https://learn.microsoft.com/en-us/graph/api/resources/security-alert?view=graph-rest-1.0) endpoint.
          * Microsoft 365 Defender unified alerts API, which serves alerts from Microsoft 365 Defender, Microsoft Defender for Endpoint, Microsoft Defender for Office 365, Microsoft Defender for Identity, Microsoft Defender for Cloud Apps, and Microsoft Purview Data Loss Prevention (including any future new signals integrated into M365D).
        * Legacy Alerts (Deprecated): Alerts are collected via the **deprecated** Legacy Microsoft Graph Security API [v1](https://learn.microsoft.com/en-us/graph/api/resources/security-api-overview?view=graph-rest-1.0\&preserve-view=true#legacy-alerts).
          * Microsoft Defender for Cloud, Azure Active Directory Identity Protection, Microsoft Defender for Cloud Apps, Microsoft Defender for Endpoint, Microsoft Defender for Identity, Microsoft 365, Azure Information Protection, and Azure Sentinel.
      * Emails: Deprecated. Use the dedicated email collector instead. For more information, see [Ingest logs and data from Microsoft 365](../microsoft-office-365-email/ingest-logs-and-data-from-microsoft-365).

    d. Click Test to test the connection settings. To test the connection, you must select one or more log types. Cortex XSIAM then tests the connection settings for the selected log types.

    e. If successful, click Enable to enable Office 365 log collection.
