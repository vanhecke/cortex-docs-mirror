---
description: Onboard Oracle Cloud Infrastructure to Cortex XSIAM.
---

# How to onboard Oracle Cloud Infrastructure with foundational configuration

{% hint style="info" %}
Onboarding Oracle Cloud Infrastructure (OCI) using the foundational configuration is included with Cortex XSIAM NG SIEM, Cortex XSIAM Enterprise, and Cortex XSIAM Enterprise+ licenses. For more details on the CSP onboarding tiers and licensing, see [Understand CSP onboarding tiers and licensing](../understand-csp-onboarding-tiers-and-licensing).

This procedure describes foundational onboarding, which includes support of asset discovery and audit log collection. For the procedure describing comprehensive onboarding, see [How to onboard Oracle Cloud Infrastructure](onboard-oracle-cloud-infrastructure).
{% endhint %}

After completing the [prerequisites](prerequisites-for-onboarding-oci), follow these instructions to onboard your Oracle Cloud Infrastructure (OCI) environment to Cortex XSIAM.

### Access the OCI onboarding wizard in Cortex XSIAM

1. In Cortex XSIAM, select Settings → Data Sources & Integrations.
2. On the Data Sources & Integrations page, click + Add New.
3. On the Add Data Sources or Integrations page, search for Oracle Cloud Infrastructure, then hover over it and click Add.

### Set the instance name (optional)

*   In Instance Name, enter a unique instance name.

    If you don't enter a name, Cortex XSIAM applies the default name, `OCI-<TENANCY_OCID>`. Cortex XSIAM does not prevent you from reusing instance names, but it is best practice to use a unique name for every cloud instance.

### Configure advanced settings (optional)

* Click Show advanced settings to define the following advanced settings:
  *   **Scope Modifications:** You can modify the scope by including or excluding specific Compartments. If you choose to include specific compartments, only the specified compartments and their sub-compartments will be included. This setting will affect future sub-compartments added to your OCI environment after onboarding. If you choose to exclude specific compartments, this setting will also affect their sub-compartments.

      **Note**: The root compartment is always onboarded, and only the sub-compartment scope can be modified.

      Excluded compartments are not visible in Cortex XSIAM.
  * **Cloud Tags:** Define tags and tag values to be added to any new resource created by Cortex XSIAM in OCI. Note: The `managed_by = paloaltonetworks` tag is automatically added to all resources. This tag is mandatory. You cannot edit or remove this tag.
  * **Log Collection Configuration:** To maximize security coverage, enable the collection of audit logs. This may require additional cloud service provider permissions. For detailed information on the permissions required, see [Cloud service provider permissions](../../../../reference-and-developer-docs/reference/cloud-service-provider-permissions). Enter the following details for each preexisting OCI storage bucket that you intend to use for log collection:
    * Region: The geographic OCI region where the bucket is located. For example, "us-phoenix-1".
    * Bucket Name: The name of the OCI storage bucket.
    * Compartment OCID: The Oracle Cloud Identifier (OCID) of the compartment that contains the bucket.

### Save the configuration and download the authentication template

1. Click **Save**. Cortex XSIAM generates a Terraform authentication template based on the settings you configured in the OCI onboarding wizard. Cortex XSIAM creates an instance in the pending state. For details on pending instances, see [Pending cloud instances](../pending-cloud-instances).
2.  Download the OCI authentication template by clicking **Download Terraform**.

    The Terraform authentication template is reusable and can be executed as many times as you want to create new instances with the settings you defined in the wizard. The Terraform authentication template is valid for seven days from when it was created.
3. Click **Close**.
