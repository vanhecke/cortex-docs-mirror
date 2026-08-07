# Manually connect a cloud instance

When onboarding your cloud instance using the onboarding wizard, after you download the authentication template and execute it in your cloud environment, notification is sent to Cortex Cloud and a cloud instance is created. This connection between your cloud environment and the Cortex Cloud cloud instance typically occurs automatically.

There are several scenarios when the instance should be connected manually:

* You executed the template in your cloud environment and your environment is an air-gapped network. In this case, the notification to create the instance in Cortex Cloud does not happen.
* You have executed the template, but the instance has not appeared in **Cloud Instances**. This is often due to connectivity or firewall issues.
* You have a specific need to connect the instance manually.

To manually connect a cloud instance, you need to identify the pending instance you want to connect. In **Cloud Instances**, remove the default filter that excludes pending instances. Right-click on a pending instance and select **View Details** to see the configuration details of that specific pending instance. After you have identified the pending instance you want to connect manually, right-click and select **Manually connect an instance**. For more information on pending instances, see [Pending cloud instances](https://app.gitbook.com/s/mxWuY3s7AUvWfzCV9p1A/administration-and-troubleshooting/manage-instances/pending-cloud-instances).

{% tabs %}
{% tab title="AWS" %}
In AWS Management Console, navigate to [CloudFormation](https://console.aws.amazon.com/cloudformation/). Use the following table to guide you on where to obtain the necessary input for the manual onboarding. Not every field appears in every manual onboarding instance.

| Connect Instance input field | Value                                                         |
| ---------------------------- | ------------------------------------------------------------- |
| Organization ID              | Onboarded organization ID.                                    |
| Organizational Unit ID       | Onboarded organizational unit ID.                             |
| Account ID                   | Onboarded account ID.                                         |
| Role ARN                     | The value of **Outputs → CORTEXXDRARN**.                      |
| External ID                  | The value of **Parameters → ExternalID**.                     |
| Audit Logs SQS URL           | The value of **Resources → CloudTrailLogsQueue**.             |
| Audit Logs Role ARN          | The value of **Resources → CloudTrailReadRole → ARN**.        |
| Audit Logs Audience          | Automatically populated.                                      |
| Outpost Scanner Role ARN     | The value of **Resources → CortexPlatformScannerRole → ARN.** |
{% endtab %}

{% tab title="GCP" %}
1. Open your local terminal (Command prompt, PowerShell, or Terminal).
2.  Log in to your GCP account using the gcloud CLI:

    ```
    gcloud auth login
    ```
3.  Display the values of all defined output variables in your Terraform configuration, formatted as a JSON object:

    ```
    terraform output -json
    ```

Use the following table to guide you on which values in the output map to the necessary input for the manual onboarding. Not every field appears in every manual onboarding instance.

| Connect Instance input field            | Value                                                                            |
| --------------------------------------- | -------------------------------------------------------------------------------- |
| Organization ID                         | organization\_id.value                                                           |
| Project ID                              | project\_id.value                                                                |
| Folder ID                               | folder\_id.value                                                                 |
| Service Account Email                   | service\_account\_email.value                                                    |
| Audit Logs Audit Pubsub Subscription ID | resources\_data.value.AUDIT\_LOGS.audit\_pubsub\_subscription\_id                |
| Audit Logs Service Account Email        | resources\_data.value.AUDIT\_LOGS.audit\_service\_account\_email                 |
| Outpost Scanner Service Account Email   | resources\_data.value.OUTPOST\_SCANNER.outpost\_scanner\_service\_account\_email |
{% endtab %}

{% tab title="Azure with Terraform" %}
1. Open your local terminal (Command prompt, PowerShell, or Terminal).
2.  Log in to your Azure account using the Azure CLI:

    ```
    az login
    ```
3.  Display the values of all defined output variables in your Terraform configuration, formatted as a JSON object:

    ```
    terraform output -json
    ```

Use the following table to guide you on which values in the output map to the necessary input for the manual onboarding. Not every field appears in every manual onboarding instance.

| Connect Instance input field                          | Value                                                                           |
| ----------------------------------------------------- | ------------------------------------------------------------------------------- |
| Resource Group Location (only for subscription scope) | Onboarded resource group location                                               |
| Resource Group Name                                   | Automatically populated                                                         |
| Audit Logs Audience                                   | Automatically populated                                                         |
| Audit Logs Storage Account Name                       | resources\_data.value.AUDIT\_LOGS.storage\_account\_name                        |
| Audit Logs Tenant ID                                  | Automatically populated                                                         |
| Audit Logs Client ID                                  | resources\_data.value.AUDIT\_LOGS.client\_id                                    |
| Audit Logs Namespace                                  | resources\_data.value.AUDIT\_LOGS.namespace                                     |
| Audit Logs Eventhub Name                              | resources\_data.value.AUDIT\_LOGS.eventhub\_name                                |
| Audit Logs Azure Audit Eventhub Consumer Group Name   | resources\_data.value.AUDIT\_LOGS.azure\_audit\_eventhub\_consumer\_group\_name |

<br>
{% endtab %}

{% tab title="Azure Portal" %}
Navigate to the [Microsoft Azure Portal](http://portal.azure.com/) and log in.

Use the following table to guide you on which values in the output map to the necessary input for the manual onboarding. Not every field appears in every manual onboarding instance.

| Connect Instance input field                          | Value                                                                                                                                                                      |
| ----------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Resource Group Location (only for subscription scope) | Onboarded resource group location                                                                                                                                          |
| Resource Group Name                                   | Automatically populated                                                                                                                                                    |
| Audit Logs Audience                                   | Automatically populated                                                                                                                                                    |
| Audit Logs Storage Account Name                       | Navigate to **Storage accounts** and filter by resource group.                                                                                                             |
| Audit Logs Tenant ID                                  | Automatically populated                                                                                                                                                    |
| Audit Logs Client ID                                  | Navigate to **App registrations** and sort by time. The default name starts with "auditlogsapp".                                                                           |
| Audit Logs Namespace                                  | Navigate to **Event Hubs** and filter by resource group.                                                                                                                   |
| Audit Logs Eventhub Name                              | Navigate to **Event Hubs** and select the Event Hub Namespace. Under **Event Hubs**, take the value in the **Name** column.                                                |
| Audit Logs Azure Audit Eventhub Consumer Group Name   | Navigate to **Event Hubs** and select the Event Hub Namespace and then the Event Hub. Under **Consumer Groups**, use the value in the **Name** column, but not ‘$Default’. |
{% endtab %}

{% tab title="OCI" %}
1. Open your local terminal (Command prompt, PowerShell, or Terminal).
2.  Log in to your OCI account using the OCI CLI:

    ```
    oci session authenticate
    ```
3.  Display the values of all defined output variables in your Terraform configuration, formatted as a JSON object:

    ```
    terraform output -json
    ```
4.  Use the following table to guide you on which values in the output map to the necessary input for the manual onboarding. Not every field appears in every manual onboarding instance.

    | Connect instance input field | Value                                |
    | ---------------------------- | ------------------------------------ |
    | Tenancy OCID                 | tenancy\_ocid.value                  |
    | Home Region                  | home\_region.value                   |
    | Cortex Policy                | cortex\_policy.value                 |
    | Cortex Group                 | cortex\_group.value                  |
    | Authentication Method        | The authentication method being used |
{% endtab %}

{% tab title="Alibaba Cloud" %}
1. Open your local terminal (Command prompt, PowerShell, or Terminal).
2.  Log in to your Alibaba Cloud account using the aliyun CLI:

    ```
    aliyun auth login
    ```
3.  Display the values of all defined output variables in your Terraform configuration, formatted as a JSON object:

    ```
    terraform output -json
    ```
4.  Use the following table to guide you on which values in the output map to the necessary input for the manual onboarding. Not every field appears in every manual onboarding instance.

    | Connect instance input field | Value                                |
    | ---------------------------- | ------------------------------------ |
    | Alibaba Cloud Account ID     | alibaba\_cloud\_account\_id.value    |
    | Alibaba Cloud Region         | alibaba\_cloud\_region.value         |
    | RAM Role ARN                 | ram\_role\_arn.value                 |
    | OIDC Provider ARN            | oidc\_provider\_arn.value            |
    | authentication method        | The authentication method being used |
{% endtab %}
{% endtabs %}
