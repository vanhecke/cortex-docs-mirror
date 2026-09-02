---
description: >-
  Follow the Azure onboarding wizard, and Cortex creates a custom authentication
  template to be executed in Azure.
---

# How to onboard Microsoft Azure

{% hint style="info" %}
This feature is included with a Cortex XSIAM Premium license. It is also included with any other Cortex XSIAM license that has the Cloud Runtime Security or Cloud Posture Security add-ons.

For Cortex XSIAM NG SIEM, Cortex XSIAM Enterprise, and Cortex XSIAM Enterprise+ licenses, see [How to onboard Microsoft Azure with foundational configuration](how-to-onboard-microsoft-azure).
{% endhint %}

After completing the prerequisites, follow these instructions to onboard your Microsoft Azure environment to Cortex XSIAM.

## Access the Azure onboarding wizard in Cortex XSIAM

1. In Cortex XSIAM, select Settings → Data Sources & Integrations.
2. On the Data Sources & Integrations page, click + Add New.
3. On the Add Data Sources or Integrations page, search for Microsoft Azure, then hover over it and click Add.

## Select the Microsoft Azure environment

* In the Microsoft Azure onboarding wizard, select the type of Microsoft Azure environment:
  * **Government:** Microsoft Azure Government environments for compatibility with FedRAMP-certified tenants.
  * **Commercial:** (Default) Standard cloud deployment typically used for private and public sector organizations that do not require isolated government-specific infrastructure.

## Select the scope

1. Select the scope for this cloud instance:
   * **Tenant:** (Default) A specific instance of Azure Active Directory, which can contain several subscriptions.
   * **Management Group:** A collection of Microsoft Azure subscriptions.
   * **Subscription:** A collection of Microsoft Azure resources associated with a specific Microsoft Azure tenant.
2. When you select Tenant, you have the option to select Onboard Microsoft Entra ID only. For more details on this option, see [Onboard Microsoft Entra ID only](../onboard-microsoft-azure#onboard-microsoft-entra-id-only).

## Choose the scan mode

This option is not available when you are onboarding Microsoft Entra ID only.

* Specify the scanning infrastructure for your cloud instance by selecting one of the following scan modes:
  * **Cloud Scan:** (Recommended) Security scanning is performed in the Cortex XSIAM cloud environment.
  *   **Scan with Outpost:** Security scanning is performed on infrastructure deployed to a cloud account owned by you. If you select this option, choose the outpost account to use for this instance or create a new outpost. For more information on outposts, see [Outposts](../outpost-onboarding).

      <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h4>Note</h4><p>Scanning with an outpost may require additional Azure permissions and may incur additional CSP costs.</p></div>

## Verify the service principal in your Azure tenant

Before Cortex XSIAM can proceed with onboarding, the Cortex XSIAM service principal must be present in your Azure tenant. Cortex XSIAM checks the status of the service principal automatically when you enter your tenant ID.

1.  Enter your Azure tenant ID in the **Tenant ID** field.

    Cortex XSIAM checks whether the Cortex XSIAM service principal already exists in your tenant and displays one of the following results:

    * **Service principal found** (green checkmark): The Cortex XSIAM service principal is already registered in your tenant. Click **Next** to continue with the onboarding wizard.
    * **Service principal not found**: The Cortex service principal does not yet exist in your tenant. Cortex XSIAM displays the Azure CLI command you must run to create it.
2.  If the Cortex service principal is not found, copy the Azure CLI command displayed in the wizard and run it in your terminal or in Azure Cloud Shell:

    ```bash
    az ad sp create --id <cortex-tenant-id>
    ```

    The user who runs this command must hold the **Application Administrator** Entra ID role.
3. After the command completes successfully, return to the Cortex XSIAM onboarding wizard and click **Verify** to verify that the Cortex service principal is now present in your tenant.

{% hint style="info" %}
Cortex XSIAM performs a live verification of each tenant's approval status against Azure each time the list is displayed. If a previously approved tenant no longer shows a green checkmark, the Cortex XSIAM service principal may have been removed from the Azure tenant. Run the Azure CLI command again to re-create the service principal, then click **Validate**.
{% endhint %}

## Configure advanced settings (optional)

* Click Show advanced settings to define the following advanced settings:
  * **Instance Name:** Enter a unique instance name or leave it empty to be automatically populated. The automatic naming convention is `Azure-<tenantID>` or `Azure-<subscriptionID>`. Cortex XSIAM does not prevent you from reusing instance names, but it is best practice to use a unique name for every cloud instance.
  * **Deployment Method:** Select whether you want to onboard with a Cortex-generated IaC template or to perform a manual deployment:
    * **Infrastructure as Code:** (Recommended) Automatically provisions all required cloud resources and permissions using an IaC template.
    * **Manual:** Select this option if your organization requires manual provisioning to meet internal security and compliance policies. If you choose to onboard manually, follow the [manual onboarding instructions](https://app.gitbook.com/o/r4DIGbR5VLvkZy3gAYsu/s/EGgPqu5Pm2LdBLfMWLeZ/).
  * **Scope Modifications:** Use these settings to fine-tune your Microsoft Azure scope. You can modify the scope by including or excluding specific regions. If you selected a Government environment, only Microsoft Azure Government regions are displayed. Additionally, if you selected a tenant or management group as the scope, you can modify the scope by including or excluding specific management groups or subscriptions. For more details, see [Apply region or account filters](../..#step-5-apply-region-or-account-filters-optional). Scope modifications are not available when you are onboarding Microsoft Entra ID only.
  * **Additional Security Capabilities:** Choose which security capabilities you want to benefit from. Some security capabilities are enabled by default and can be modified. Adding security capability typically requires additional cloud provider permissions. For detailed information on the permissions required, see [Cloud service provider permissions](../cloud-service-provider-permissions). When you are onboarding Microsoft Entra ID only, only XSIAM analytics is supported as an additional security capability.
    * **Data security posture management:** An agentless data security scanner that discovers, classifies, protects, and governs sensitive data. DSPM is not currently available in Microsoft Azure Government environments.
    * **Registry scanning:** A container registry scanner that scans registry images for vulnerabilities, malware, and secrets. For more details, see [Configure registry scanning for cloud accounts](../../cloud-posture-and-runtime-security-data-sources/container-registry-scanning/configure-registry-scanning-for-cloud-accounts).
    *   **Serverless functions scanning:** Implement serverless scanning to detect and remediate vulnerabilities within serverless functions during the development lifecycle. Seamless integration into CI/CD pipelines enables automated security scans for a continuously secure pre-production environment.

        * **Allow connection to private serverless functions:** (Optional - only available with outpost scan) When serverless scanning runs from the outpost environment, it uses a dynamic IP address. Azure Functions with IP-based network restrictions will block the scanner. Enabling this option assigns a fixed IP address that can be whitelisted.

        <div data-gb-custom-block data-tag="hint" data-style="warning" class="hint hint-warning"><p>Enabling this feature requires additional permissions. Download and run the Terraform template again to apply the permissions required to scan private serverless resources. Private serverless resources are resources that are accessible only through private networks and aren’t publicly accessible.</p></div>
    * **Automation:** Use automation to pre-configure a list of integrations and associated commands to automate security issue responses. Commands can be utilized individually or as part of custom playbooks for issue remediation.
      * **Log Level:** (Optional - for Automation only) Configure the automation integration logging level. Possible values are:
        * Off (Default)
        * Debug
        * Verbose
    * **Agentless disk scanning:** (Recommended) Implement agentless disk scanning to remotely detect and remediate vulnerabilities during the development lifecycle.
  * **Cloud Tags:** Define tags and tag values to be added to any new resource created by Cortex XSIAM in Microsoft Azure. Note: The `managed_by = paloaltonetworks` tag is automatically added to all resources. This tag is mandatory. You cannot edit or remove this tag.
* **Log Collection Configuration:** To maximize security coverage, include the collection of audit logs using Event Hub. Select the collection method:
  * **Automated collection:** Cortex XSIAM provisions the resource group, Event Hub namespace, Event Hub, consumer group, storage account, user-assigned managed identity (UAMI), federated identity credential, diagnostic settings, and role assignment resources in your Azure environment to collect audit logs.
    * **Tenant/management group scope:** A single diagnostic setting is created at the management group scope. Azure natively propagates Activity Logs from all child subscriptions through this management group-level setting and no per-subscription diagnostic setting is created. An Azure policy definition is also deployed to create the Cortex resource group in each child subscription.
    * **Cost considerations:** Event Hub pricing is based on throughput units and ingress/egress. High-volume environments with many subscriptions can generate significant event throughput. We recommend you review your [Azure Event Hubs pricing](https://azure.microsoft.com/en-us/pricing/details/event-hubs/) and expected event volume before enabling.
  *   **Custom** (user defined): Select this option to use an existing Event Hub for storing your audit logs.

      * When you deploy the authentication template in ARM, you will enter the following details: Event Hub name, Event Hub namespace, Event Hub resource group name.
      * Cortex XSIAM creates the user-assigned managed identity (UAMI), federated identity credential, role assignments, and consumer group.
      * After you deploy the stack in ARM, you must ensure that your existing Event Hub has the appropriate diagnostic settings configured to stream Azure Activity Logs.

      #### Important

      It is critical to ensure that your namespace and Event Hub belong to the specific Azure subscription being onboarded. Cross-subscription or centralized logging is not currently supported.
* **Upload unknown files to WildFire:** Use this option to upload unknown files scanned during registry image scans to WildFire for detonation analysis.\
  This option expands malware detection by allowing WildFire to analyze new samples found in your registry images. When a detonation result returns a malicious verdict, the system re-evaluates the relevant registry image and creates a malware finding.

<figure><img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2FbLVVFbhzGA2oRZS73rxU%2Fimage.png?alt=media&#x26;token=cd29d9e4-72d8-401b-8cf0-d66079761890" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
#### Notes

* The file types sent for WildFire analysis depend on the platform type. WildFire accepts files up to 300 MB in size.
* This setting applies only to registry image scans and is enabled by default for new Azure instances. For existing instances, this setting is disabled by default to preserve the current behavior. You can enable it at any time by editing the instance configuration.
* Your cloud provider may charge standard outbound data transfer (egress) fees when scanning with an [Outpost](../outpost-onboarding).
{% endhint %}

## Save the configuration and download the template

1. Click **Save**. Cortex XSIAM generates a Terraform or ARM authentication template based on the settings you configured in the Microsoft Azure onboarding wizard. Cortex XSIAM creates an instance in the pending state. For details on pending instances, see [Pending cloud instances](../pending-cloud-instances).
2.  Download the authentication template:

    * For onboarding Azure tenants and management groups, click one of the following:
      *   **Download Terraform** to download a Terraform file and proceed to [Finalize onboarding by applying the Terraform template's configuration](../finalize-microsoft-azure-onboarding-by-executing-the-authentication-template#finalize-onboarding-by-applying-the-terraform-templates-configuration).

          To onboard all subscriptions within a management group or tenant, our authentication template uses Azure Resource Management (ARM) templates internally. The ARM templates are encoded with base64 and located inside the `template_params.tfvars` file as the `policy_template` variable.
      * **Azure Resource Manager** to download a `tar.gz` file and proceed to [Finalize onboarding of tenants and management groups by deploying the Microsoft Azure Resource Manager (ARM) template](../finalize-microsoft-azure-onboarding-by-executing-the-authentication-template#finalize-onboarding-of-tenants-and-management-groups-by-deploying-the-microsoft-azure-resource-manager-arm-template).
    * For onboarding Azure subscriptions, click one of the following:
      * Download Terraform to download a Terraform file and proceed to [Finalize onboarding by applying the Terraform template's configuration](../finalize-microsoft-azure-onboarding-by-executing-the-authentication-template#finalize-onboarding-by-applying-the-terraform-templates-configuration).
      * Azure Resource Manager to download a JSON file and proceed to [Finalize onboarding of subscriptions by deploying the Microsoft Azure Resource Manager (ARM) template](../finalize-microsoft-azure-onboarding-by-executing-the-authentication-template#finalize-onboarding-of-subscriptions-by-deploying-the-microsoft-azure-resource-manager-arm-template).

    The authentication template is reusable and can be executed as many times as you want to create new cloud instances with the settings you defined in the Microsoft Azure onboarding wizard. The Terraform authentication template is valid for seven days from when it was created.
3. Click **Close**.
