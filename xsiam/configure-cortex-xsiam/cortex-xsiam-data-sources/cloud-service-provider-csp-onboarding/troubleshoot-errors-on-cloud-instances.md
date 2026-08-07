---
description: >-
  You can troubleshoot errors on cloud instances by drilling down on an instance
  from the Data Sources & Integrations page.
---

# Troubleshoot errors on cloud instances

To help you to troubleshoot errors on a cloud instance, Cortex Cloud provides the following visibility and drilldown options:

* Overall status of an instance that indicates the health of your instance.
* A breakdown of the security capabilities enabled on an instance, detailing the status of each capability along with any open errors or issues.
* Additional XQL drill down options to query the history of error and recovery events for each security capability.

### How to troubleshoot errors on a cloud instance

1.  Navigate to **Settings → Data Sources & Integrations**.

    Under **Cloud Service Provider**, review the status of the instances that were onboarded for the service provider. If the status shows **Warning** or **Error**, hover over the service provider and click **View Details**.
2. On the **Cloud Instances** page review the list of instances that were onboarded and their overall status. The status is displayed as follows:
   * **Connected**: The connector is enabled and has no issues.
   * **Warning**: The connector is enabled and has minor issues. For example, some accounts or capabilities are in warning or error status.
   * **Error**: The connector is enabled and has substantial errors. For example, an authentication failure, an outpost failure, major permissions issues, or (for organization level accounts) the majority of the accounts in the instance are in error status.
   * **Disabled**: The connector is disabled.
3.  To understand why an instance is showing a Warning or Error status, click on the instance name.

    The cloud instance panel provides a breakdown of the security capabilities and the accounts onboarded on the instance. Review the information in the following sections:

    <table><thead><tr><th width="188.08984375">Section</th><th>Context</th></tr></thead><tbody><tr><td>Header</td><td><p>Displays the overall status of the instance and the following information about the account, as specified during onboarding:</p><p><strong>Scope of the instance</strong>: The number of accounts onboarded on the instance and their status. See the Accounts section for more information about the individual accounts and the type of account (single account or organization).</p><p><strong>Scan mode</strong>: Cloud Scan or Outpost. For accounts using Outpost, information is displayed about the status of the Outpost account and the account ID.</p><p><strong>Resource Tags</strong>: Tags defined during onboarding.</p></td></tr><tr><td>Security Capabilities</td><td><p>Displays a breakdown of the security capabilities enabled on the instance and their individual statuses. Click on any item that shows a warning or error status to see the open errors and issues that contributed to the status:</p><p><strong>Errors</strong> are factual objects that are automatically created when problems occur, and provide insight into the current status of the capability. For example, if a permission is missing, an error is displayed. Browse and filter the errors to better understand and resolve the problem.</p><p><strong>Issues</strong> are actionable objects that are triggered when detected problems exceed defined thresholds. Issues are manageable, trackable, and provide remediation suggestions and automations.</p><p>The issues displayed in the panel are open issues that are specifically related to the selected connector with the selected capability in the observed scope (single account or organization). Click an issue to start investigating it.</p></td></tr><tr><td>Accounts</td><td><p>Lists the accounts that are onboarded on the instance and their individual status.</p><p>If multiple accounts are onboarded on the instance, click on each account to filter the page information by account, and drill-down to the security capability statuses for each account.</p></td></tr></tbody></table>
4. If the instance shows an Outpost error, go to the **All Outposts** page and find the outpost account that is being used by this instance. Right click the Outpost account to view the open errors and issues for the account.
5. If the account shows **Permission** errors, use the side panel to check which permissions are missing. You can also **Edit** the instance to redeploy the cloud setup template, which should normally resolve the error.
6.  Further investigate errors by running XQL queries on the `cloud_health_auditing` dataset.

    This dataset records error and recovery events for the security capabilities in cloud instances. By querying this dataset you can see information about when the error started, the prevalence of the error, and whether there is a recurrency pattern. See the specific fields descriptions and query examples for each security capability.

{% hint style="info" %}
Note: Errors related to collection of audit logs in the cloud instance are recorded in the `collection_auditing` dataset. For more information, see [Audit logs fields and query examples](#audit-logs-fields-and-query-example).
{% endhint %}

7. Set up correlation rules to trigger issues when errors occur in cloud security capabilities. See the following examples.

<details>

<summary>Outpost fields and query examples</summary>

You can review Outpost entries in the `cloud_health_auditing` dataset to see Outpost activity over time, or to search for errors on specific accounts. Outpost entries are added to the dataset as follows:

* An error occurred on an Outpost account that disabled or prevented an operation. This is audited as Error.
* An exceptional condition occurred on an Outpost account that might cause problems if not resolved. This is audited as Warning.
* The Outpost account returns to normal function. This is audited as Informational.

The following table describes the fields for Outpost entries:

<table data-header-hidden><thead><tr><th width="152.05078125"></th><th></th></tr></thead><tbody><tr><td>Field</td><td>Description</td></tr><tr><td>Account</td><td>Cloud account ID of the Outpost</td></tr><tr><td>Name</td><td>Category of the error, or a brief description of the event</td></tr><tr><td>Resource ID</td><td>Outpost ID</td></tr><tr><td>Capability</td><td>Outpost</td></tr><tr><td>Region</td><td>Region where the event occurred, or <strong>All regions</strong>.</td></tr><tr><td>Classification</td><td>Type of entry (Error, Warning, or Informational)</td></tr><tr><td>Message</td><td>Description of the error or <strong>Connected</strong> for informational entries.</td></tr><tr><td>Error</td><td>Details about the error. For informational entries this is blank.</td></tr></tbody></table>

#### Example

*   Identify Outpost errors on all Outpost accounts in the eu-west-3 region:

    ```
    dataset = cloud_health_auditing | filter capability = "Outpost" and classification = "Error" and region = "eu-west-3"
    ```
*   See all entries (error, warning, and recovery) for Outpost\_1 on cloud account Account\_A:

    ```
    dataset = cloud_health_auditing | filter capability = "Outpost" and resource_id = “Outpost_1” and
    ```

</details>

<details>

<summary>Permissions fields and query examples</summary>

You can review Permissions entries in the `cloud_health_auditing` dataset to see Permissions activity over time, or to search for errors on specific accounts. Permissions entries are added to the dataset as follows:

* A permission problem was found. This is audited as **Error**.
* An exceptional condition occurred that might cause problems if not resolved. This is audited as **Warning**.
* A permission problem is resolved. This is audited as **Informational**.

The following table describes the fields for Permissions entries:

<table data-header-hidden><thead><tr><th width="146.91015625"></th><th></th></tr></thead><tbody><tr><td>Field</td><td>Description</td></tr><tr><td>Account</td><td>Name of the account where the event occurred, or <strong>All accounts</strong>.</td></tr><tr><td>Connector</td><td>Name of the connector where the event occurred</td></tr><tr><td>Name</td><td>Permission name</td></tr><tr><td>Capability</td><td>Permissions</td></tr><tr><td>Classification</td><td>Type of entry (Error, Warning, or Informational)</td></tr><tr><td>Message</td><td>Description of the error or <strong>Granted</strong> for informational entries.</td></tr></tbody></table>

</details>

<details>

<summary>Discovery engine fields and query examples</summary>

You can review Discovery engine entries in the `cloud_health_auditing` dataset to see Discovery activity over time, or to search for errors on specific accounts. Discovery entries are added to the dataset as follows:

* An API exec problem is found. This is audited as **Error**.
* An exceptional condition occurred that might cause problems if not resolved. This is audited as **Warning**.
* An API exec problem is resolved. This is audited as **Informational**.

The following table describes the fields for Discovery engine entries:

<table data-header-hidden><thead><tr><th width="141.53515625"></th><th></th></tr></thead><tbody><tr><td>Field</td><td>Description</td></tr><tr><td>Account</td><td>Name of the account where the event occurred, or <strong>All accounts</strong></td></tr><tr><td>Connector</td><td>Name of the connector where the event occurred</td></tr><tr><td>Name</td><td>Asset name</td></tr><tr><td>Capability</td><td>Discovery</td></tr><tr><td>Region</td><td>Region where the event occurred, or <strong>All regions</strong>.</td></tr><tr><td>Classification</td><td>Type of entry (Error, Warning, or Informational)</td></tr><tr><td>Message</td><td>Description of the error or <strong>Connected</strong> for informational entries.</td></tr></tbody></table>

#### Example

*   Identify API exec errors on the Discovery engine for all accounts on the AWS\_1 connector:

    ```
    dataset = cloud_health_auditing | filter capability = "Discovery" and connector = "AWS_1" and classification = “Error”
    ```
*   See all Discovery engine activity on connector AWS\_1 for Account\_ A in the af-south-1 region:

    ```
    dataset = cloud_health_auditing | filter capability = "Discovery" and connector = "AWS_1" and account = "accountA" and region = "af-south-1
    ```

</details>

<details>

<summary>Agentless Disk Scanning (ADS) fields and query examples</summary>

You can review ADS entries in the `cloud_health_auditing` dataset to see ADS activity over time, or to search for errors on specific accounts. ADS entries are added to the dataset as follows:

* ADS failed to scan an asset. This is audited as **Failed**.
* ADS successfully scanned an asset. This is audited as **Scanned**.
* The asset or host is not supported by ADS. This is audited as **Unsupported**.
* The asset or Host was excluded from the scan. This is audited as **Excluded**.

<table data-header-hidden><thead><tr><th width="137.03125"></th><th></th></tr></thead><tbody><tr><td>Field</td><td>Description</td></tr><tr><td>Account</td><td>Name of the account to which the asset belongs</td></tr><tr><td>Connector</td><td>ID of the connector</td></tr><tr><td>Name</td><td>Name of the asset</td></tr><tr><td>Resource ID</td><td>Asset ID</td></tr><tr><td>Capability</td><td>ADS</td></tr><tr><td>Region</td><td>Region where the asset is located</td></tr><tr><td>Classification</td><td>Type of entry (Failed, Unsupported, Excluded, Scanned)</td></tr><tr><td>Message</td><td>Description of the error, or Connected for informational entries.</td></tr><tr><td>Error</td><td>Details about the error. For informational entries this is blank.</td></tr><tr><td>Type</td><td>Type of asset that was scanned</td></tr><tr><td>Scope</td><td>Scope of the asset (Asset, Region, or Account)</td></tr></tbody></table>

#### Example

*   Identify failed ADS scans on connector "a8df43e848dd42778ae7efd5a706a0fc" for EC2 assets at the asset scope level, filtered by region (northamerica-northeast2-a):

    ```
    dataset = cloud_health_auditing | filter capability = "ADS" and classification = "failed" and connector = “a8df43e848dd42778ae7efd5a706a0fc” and type = "EC2_INSTANCE" and scope = "Asset" and region = "northamerica-northeast2-a" 
    ```
*   See all ADS scans (failed and successful) on connector "a8df43e848dd42778ae7efd5a706a0fc" for EC2 assets belonging to Account\_A:

    ```
    dataset = cloud_health_auditing | filter capability = "ADS" and connector = “a8df43e848dd42778ae7efd5a706a0fc” and type = "EC2" and account = “Account_
    ```

</details>

<details>

<summary>Data Security Scanning (DSPM) fields and query examples</summary>

You can review DSPM entries in the `cloud_health_auditing` dataset to see DSPM activity over time, or to search for errors on specific accounts. DSPM entries are added to the dataset as follows:

* DSPM failed to scan an asset. This is audited as **Failed**.
* DSPM successfully scanned an asset. This is audited as **Success**.

The following table describes the fields for DSPM entries:

| Field          | Description                                                       |
| -------------- | ----------------------------------------------------------------- |
| Account        | Name of the account to which the asset belongs                    |
| Connector      | Name of the connector where the event occurred                    |
| Name           | Name of the asset                                                 |
| Resource ID    | Asset ID                                                          |
| Capability     | DSPM                                                              |
| Region         | Region where the asset is located                                 |
| Classification | Type of entry (Failed or Success)                                 |
| Message        | Description of the error, or Connected for informational entries. |
| Error          | Details about the error. For informational entries this is blank. |
| Type           | Type of asset that was scanned                                    |
| Scope          | Scope of the asset (Asset, Region, or Account)                    |

#### Example

*   Identify failed DSPM scans on the AWS\_1 connector for S3 asset types, filtered by region (ap-east-1):

    ```
    dataset = cloud_health_auditing | filter capability = "DSPM" and classification = “Error” and connector = “AWS_1” and type = "S3_BUCKET" and region = "ap-east-1"
    ```
*   See all DSPM scans (failed and successful) on the AWS\_1 connector, for all scanned assets on Account\_A:

    ```
    dataset = cloud_health_auditing | filter capability = "DSPM" and account = "Account_A" and connector = “AWS_1”
    ```

</details>

<details>

<summary>Registry scanning fields and query examples</summary>

You can review Registry scanning entries in the `cloud_health_auditing` dataset to see Registry scanning activity over time, or to search for errors on specific accounts. Registry scanning entries are added to the dataset as follows:

* The Registry scanner failed to scan an asset. This is audited as **Failed**.
* The Registry scanner successfully scanned an asset. This is audited as **Scanned**.

The following table describes the fields for Registry scanning entries:

<table data-header-hidden><thead><tr><th width="143.5234375"></th><th></th></tr></thead><tbody><tr><td>Field</td><td>Description</td></tr><tr><td>Account</td><td>Name of the account to which the asset belongs</td></tr><tr><td>Connector</td><td>Name of the connector where the event occurred</td></tr><tr><td>Resource ID</td><td>Asset ID</td></tr><tr><td>Capability</td><td>Registry</td></tr><tr><td>Classification</td><td>Type of entry (Scanned or Failed)</td></tr><tr><td>Error</td><td>Details about the error. For informational entries this is blank</td></tr><tr><td>Scope</td><td>Scope of the asset (Asset or Account)</td></tr></tbody></table>

#### Example

*   Identify failed scans on connector GCP\_1:

    ```
    dataset = cloud_health_auditing | filter capability = "Registry" and classification = “error” and connector = “GCP_1”
    ```
*   Review all registry scans (failed and successful) on connector GCP\_1 for asset Asset\_A:

    ```
    dataset = cloud_health_auditing | filter capability = "Registry" and connector = “GCP_1” and ressource_id = "Asset_A"
    ```

</details>

<details>

<summary>Audit logs fields and query example</summary>

You can review Audit logs entries in the `collection_auditing` dataset. Querying this dataset can help you see the connectivity changes of an instance over time, the escalation or recovery of the connectivity status, and the error, warning, and informational messages related to status changes. For more information about this dataset, see [Verify collector connectivity](https://app.gitbook.com/s/mxWuY3s7AUvWfzCV9p1A/administration-and-troubleshooting/verify-collector-connectivity).

The following table describes the fields for Audit logs entries:

<table data-header-hidden><thead><tr><th width="168.3359375"></th><th></th></tr></thead><tbody><tr><td>Field</td><td>Description</td></tr><tr><td>Instance</td><td>Instance name</td></tr><tr><td>Log type</td><td>Type of logs affected</td></tr><tr><td>Classification</td><td>Type of entry (Error, Warning, or Informational)</td></tr><tr><td>Collector type</td><td>Type of the collector</td></tr><tr><td>Description</td><td>Description of the error, or <strong>Connected</strong> for informational entries.</td></tr></tbody></table>

#### Example

Identify disruptions (errors) in audit log collection on connector AWS\_1:

```
dataset = collection_auditing | filter instance = “AWS_1” and log_type = "Audit Logs" and classification = “Error”
```

<br>

</details>

<details>

<summary>Correlation rule examples</summary>

The following examples show how to set up correlation rules to trigger Health Collection issues when errors occur on a specific security capability.

#### Example rule for DSPM errors

In this example, a correlation rule will trigger a Health Collection issue if a DSPM scan fails on an AWS\_S3 asset on the AWS\_1 connector.

Example XQL:

```
dataset = cloud_health_auditing | filter capability = "DSPM" and classification = “Error” and type = "AWS_S3" and scope = "Asset" and connector = “AWS_1”
```

Additional fields to specify in the correlation rule:

<table data-header-hidden><thead><tr><th width="192.66796875"></th><th></th></tr></thead><tbody><tr><td>Field</td><td>Value</td></tr><tr><td>Time Schedule</td><td>Hourly</td></tr><tr><td>Query time frame</td><td>1 Hour</td></tr><tr><td>Issue Suppression</td><td>Select <strong>Enable issue suppression</strong>.</td></tr><tr><td>Action</td><td>Select <strong>Generate Issue</strong>.</td></tr><tr><td>Issue Domain</td><td>Health</td></tr><tr><td>Severity</td><td>Medium</td></tr><tr><td>Category</td><td>Collection</td></tr></tbody></table>

#### Example rule for Outpost errors

In this example, a correlation rule will trigger a Health Collection issue if an error is recorded on account Outpost\_A in the us-east-1 region.

Example XQL:

```
dataset = cloud_health_auditing | filter capability = "Outpost" and account = "Outpost_A" and region = "eu-west-3" and classification = "Error"
```

Additional fields to specify in the correlation rule:

<table data-header-hidden><thead><tr><th width="197.37109375"></th><th></th></tr></thead><tbody><tr><td>Field</td><td>Value</td></tr><tr><td>Time Schedule</td><td>Hourly</td></tr><tr><td>Query time frame</td><td>1 Hour</td></tr><tr><td>Issue Suppression</td><td>Select <strong>Enable issue suppression</strong>.</td></tr><tr><td>Action</td><td>Select <strong>Generate Issue</strong>.</td></tr><tr><td>Issue Domain</td><td>Health</td></tr><tr><td>Severity</td><td>Medium</td></tr><tr><td>Category</td><td>Collection</td></tr></tbody></table>

</details>
