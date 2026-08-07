---
description: Grant the correct cloud service provider permissions for Cortex XSIAM.
---

# Cloud service provider permissions

When you set up Cortex XSIAM to collect data from your cloud environments, the onboarding wizard will ensure that the correct permissions are granted for Cortex XSIAM. The following tables list the permissions required for each of the options available in the onboarding wizards.

Review the permissions required for each cloud service provider:

* [Amazon Web Services (AWS)](cloud-service-provider-permissions/amazon-web-services-aws-provider-permissions)
* [Microsoft Azure](cloud-service-provider-permissions/microsoft-azure-provider-permissions)
* [Google Cloud Platform (GCP)](cloud-service-provider-permissions/google-cloud-platform-gcp-provider-permissions)
* [Oracle Cloud Infrastructure (OCI)](cloud-service-provider-permissions/oracle-cloud-infrastructure-oci-provider-permissions)

## About automation permission scopes for unified Cortex platform cloud content packs

The unified Cortex platform cloud content packs (AWS, Azure, and GCP) require a defined set of automation permissions to enable full integration with your cloud environment. Review the following before configuring access:

* **Forward compatibility**: The permission set declared by each pack covers both currently available commands and commands planned for future releases. This eliminates the need to re-authorize permissions with each pack update.
* **Granular review**: To see the permissions required for a specific command, refer to the Command Details section in the pack documentation.
* **Custom scoping**: If your security policy requires permissions more restrictive than the recommended defaults, use a custom deployment template to define your access levels manually.

{% hint style="warning" %}
**Caution**

Reducing permissions below the recommended level may cause specific commands to fail or limit functionality in future pack updates.
{% endhint %}
