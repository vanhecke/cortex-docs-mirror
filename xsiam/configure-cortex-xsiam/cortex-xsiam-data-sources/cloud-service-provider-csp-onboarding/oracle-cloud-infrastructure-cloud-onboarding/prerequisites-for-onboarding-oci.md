---
description: >-
  Before you begin onboarding Oracle Cloud Infrastructure, you must review the
  following prerequisites.
---

# Prerequisites for onboarding OCI

## Permissions

Before you begin to onboard Oracle Cloud Infrastructure (OCI) to Cortex XSIAM, ensure that you have the necessary permissions:

* In Cortex XSIAM, you must have a Cortex XSIAM role with Data Sources - View & Edit permissions (to add/configure cloud accounts in Cortex XSIAM). This role is included in the following built-in roles: Instance Administrator, Security Admin, and IT Admin.
* In OCI, your credentials must include permissions for the following:
  * Creation of identity groups (for more information, refer to [Managing Groups](https://docs.oracle.com/en-us/iaas/Content/Identity/Tasks/managinggroups.htm))
  * Policies (for more information, refer to [How Policies Work](https://docs.oracle.com/en-us/iaas/Content/Identity/Concepts/policies.htm#How_Policies_Work))
  * Tag namespaces in the root compartment (for more information, refer to [Tags and Tag Namespace Concepts](https://docs.oracle.com/en-us/iaas/Content/Tagging/Tasks/managingtagsandtagnamespaces.htm))

### Additional prerequisites

Before you begin onboarding OCI, ensure that:

* You have access to the Oracle Cloud Infrastructure console.
* If you plan to enable audit log collection, you must first [configure the OCI connector for log collection](#configure-the-oci-connector-for-log-collection).
* If you want to use bucket replication, see [Object Storage Replication](https://docs.oracle.com/en-us/iaas/Content/Object/Tasks/usingreplication.htm)

### Configure the OCI connector for log collection

In order to enable audit log collection in Cortex XSIAM, you must first create an OCI service connector. For more details, see [Creating a Connector with a Logging Source](https://docs.oracle.com/en-us/iaas/Content/connector-hub/create-service-connector-logging-source.htm). After you have created the OCI service connector, you can proceed to [Onboard Oracle Cloud Infrastructure](onboard-oracle-cloud-infrastructure) and enable collection of audit logs.

1. Log in to the [OCI Console](https://cloud.oracle.com/). Open the navigation menu and go to **Analytics and AI → Connector Hub**.
2. On the **Connectors** page, click **Create connector**.
3. On the **Create Connector** page, enter a descriptive name for the new connector (for example, `CortexCloud_Log_Exporter`). Click **Create connector**.
4. Select the Compartment where you want to store the new connector resource.
5. Set the **Source** service to **Logging**.
6. Set the **Target** service to **Object Storage**. This is the storage bucket that Cortex XSIAM will read from.
7. Under **Configure target**, configure the storage bucket to send the log data to:
   * **Compartment**: Select the compartment that contains the bucket that you want to use.
   * **Bucket**: Select the name of the bucket that you want to send the data to.
   * **Object Name Prefix**: (Optional) Enter a prefix value.
   * **Show additional options**: (Optional) Click this link to enter values for batch size (in MBs) and batch time (in milliseconds).
8. (Optional) Add one or more tags to the connector. Select **Show Advanced Options** to show the **Add Tags** section.
9. Click **Create**. When the connector is ready, the connector's details page opens.
