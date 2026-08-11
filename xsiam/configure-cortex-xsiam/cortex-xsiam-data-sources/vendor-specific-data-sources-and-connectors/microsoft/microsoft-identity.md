# Microsoft Identity

{% hint style="warning" %}
**Important**

This connector is only available for tenants that onboarded after July 26, 2026. For tenants that onboarded before this date, use Marketplace to access the standalone integration. For more information, see [Marketplace](../../../marketplace).
{% endhint %}

Manage Microsoft Entra ID (formerly Azure Active Directory) identity resources — users, groups, applications and service principals, directory roles, conditional access, and risky users — and ingest Azure public IP address and endpoint indicator feeds. Fetches Microsoft Entra ID Protection risk detections as issues and enables automation and remediation across the Microsoft Graph and Azure APIs.

This connector includes the following sub-capabilities (Marketplace integrations link to PAN DEV for more information):

* [Azure AD Connect Health Feed](https://xsoar.pan.dev/docs/reference/integrations/azure-ad-connect-health-feed): Use the Microsoft Azure AD Connect Health Feed integration to get indicators from the feed. This sub-capability is available with any active Cortex XSIAM or Cortex AgentiX license.
* [AzureFeed](https://xsoar.pan.dev/docs/reference/integrations/azure-feed): This sub-capability is available with any active Cortex XSIAM or Cortex AgentiX license.
* [AzureRiskyUsers](https://xsoar.pan.dev/docs/reference/integrations/azure-risky-users): Azure Risky Users provides access to all at-risk users and risk detections in the Azure AD environment. This sub-capability is available with any active Cortex XSIAM, Cortex Cloud Posture Security, Cortex Cloud, Cortex Cloud Runtime Security, Cortex XDR, or Cortex AgentiX license.
* [Microsoft Graph Groups](https://xsoar.pan.dev/docs/reference/integrations/microsoft-graph-groups): Entra ID Groups integration (formely Azure Active Directory Groups) enables you to create and manage different types of groups and group functionality according to your requirements. This sub-capability is available with any active Cortex XSIAM, Cortex Cloud Posture Security, Cortex Cloud, Cortex Cloud Runtime Security, Cortex XDR, or Cortex AgentiX license.
* [Microsoft Graph User](https://xsoar.pan.dev/docs/reference/integrations/microsoft-graph-user): The Entra ID Users integration (formerly Azure Active Directory Users) is a Unified gateway to security insights - all from a unified Microsoft Graph User API. This sub-capability is available with any active Cortex XSIAM, Cortex Cloud Posture Security, Cortex Cloud, Cortex Cloud Runtime Security, Cortex XDR, or Cortex AgentiX license.
* [MicrosoftGraphApplications](https://xsoar.pan.dev/docs/reference/integrations/microsoft-graph-applications): Use the Entra ID Applications integration (formerly Azure Active Directory Applications) to manage authorized applications. This sub-capability is available with any active Cortex XSIAM, Cortex Cloud Posture Security, Cortex Cloud, Cortex Cloud Runtime Security, Cortex XDR, or Cortex AgentiX license.
* [MicrosoftGraphIdentityandAccess](https://xsoar.pan.dev/docs/reference/integrations/microsoft-graph-identityand-access): Use the Entra ID Identity And Access integration to manage roles and members (formerly Azure Active Directory Identity And Access). This sub-capability is available with any active Cortex XSIAM, Cortex Cloud Posture Security, Cortex Cloud, Cortex Cloud Runtime Security, Cortex XDR, or Cortex AgentiX license.

To configure this connector, follow the steps outlined in the configuration wizard.
