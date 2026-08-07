---
description: Configuration information for enabling inactive human identity logs on Azure.
---

# Enable inactive human identity logs on Azure in Cloud Identity Security

{% hint style="info" %}
This feature is included with a Cortex XSIAM Premium license. It is also included with any other Cortex XSIAM license that has the Cloud Posture Security or Cloud Runtime Security add-on.
{% endhint %}

To enable inactive human identity logs on the Microsoft Azure platform in Cloud Identity Security, you must first configure diagnostic settings for the **SignInLog** log types. These log types provide information regarding how long human identities have been signed in.

To configure the **SignInLog** log types, do the following:

1. Open the Azure console.
2. Navigate to the **Diagnostic settings** screen.
3. In the **Logs** area, under **Categories**, select the following categories that are related to sign-in logs:
   * **SigninLogs**
   * **NonInteractiveUserSigninLogs**
   * **ServicePrincipalSigninLogs**
   * **ManagedIdentitySigninLogs**
   * **ADFSSigninLogs**
4. Click **Save**.

{% hint style="info" %}
### Note

For more information, see [Ingest logs from Microsoft Azure Event Hub](../../configure-cortex-xsiam/cortex-xsiam-data-sources/vendor-specific-data-sources-and-connectors/microsoft/azure-event-hub/ingest-logs-from-microsoft-azure-event-hub).
{% endhint %}
