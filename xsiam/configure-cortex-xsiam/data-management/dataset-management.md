---
description: >-
  Learn more about managing your datasets and understanding your overall data
  storage, period-based retention.
---

# Dataset management

{% hint style="warning" %}
### Prerequisite

Dataset Management requires **View/Edit** RBAC permissions for **Data Management** (under **Configurations** → **Data Management**), which are the same permissions required for Parsing Rules, Data Model Rules, and Event Forwarding.
{% endhint %}

The **Dataset Management** page enables you to manage your datasets and understand your overall data storage duration for different retention periods and datasets based on your hot and cold storage licenses, and retention add-ons that extend your storage. You can view details about your Cortex XSIAM licenses and retention add-ons by selecting **Settings** → **Cortex XSIAM License**. For more information on license retention and the defaults provided per license, see [Data retention](../../learn-about-cortex-xsiam/cortex-xsiam-product-licenses/data-retention).

{% hint style="warning" %}
Cortex XSIAM enforces retention on all log-type datasets excluding Host Inventory, Vulnerability Assessment, Metrics, and Users.
{% endhint %}

<details>

<summary>Hot and cold storage</summary>

Your current hot and cold storage licenses, including the default license retention and any additional retention add-ons to extend storage, are listed within the **Hot Storage License** and **Cold Storage License** sections of the **Dataset Management** page. Whenever you extend your license retention, depending on your requirements and license add-ons for both hot storage and cold storage, the add-ons are listed.

{% hint style="info" %}
### Note

Cold storage, in addition to a cold storage license, requires compute units (CU) to run cold storage queries. For more information on CU, see [Manage compute units](manage-compute-units).

For information on the CU add-on license, see [Cortex XSIAM product licenses](../../learn-about-cortex-xsiam/cortex-xsiam-product-licenses).
{% endhint %}

</details>

<details>

<summary>Additional hot storage</summary>

You can expand your license retention to include flexible Hot Storage based retention to help accommodate varying storage requirements for different retention periods and datasets. This add-on license is available to purchase based on your storage requirements for a minimum of 1,000 GB. If this license is purchased, an **Additional Storage** subheading in the **Hot Storage License** section is displayed on the **Dataset Management** page with a bar indicating how much of the storage is used.

{% hint style="info" %}
### Note

Only datasets that are already handled as part of the GB license are supported for this license. In addition, the retention configuration is only available in Cortex XSIAM, as opposed to the public APIs.
{% endhint %}

</details>

<details>

<summary>Edit the retention plan</summary>

On any dataset configured to use Additional Hot Storage, you can edit the retention period. This enables you to view the current retention details and configure the retention. This includes setting the amount of flexible hot storage-based retention designated for a dataset and the priority for the dataset's hot storage.

**How to edit the retention plan**

1. Select Settings → Configurations → Data Management → Dataset Management.
2. In the Datasets table, right-click any dataset designated with flexible hot storage, and select Edit Retention Plan.
3. Set the following parameters:
   * Additional hot storage: Set the amount of flexible hot storage-based retention designated for this dataset in months, where a month is calculated as 31 days.
   * Hot Storage Priority: Select the priority designated for this dataset's hot storage as either Low, Medium, or High.
4. Click Save.

</details>

<details>

<summary>Datasets table</summary>

For each dataset listed in the table, the following information is available:

{% hint style="info" %}
### Note

* Certain fields are exposed and hidden by default. An asterisk (\*) is beside every field that is exposed by default.
* Datasets include dataset permission enforcements in the Cortex Query Language(XQL), Query Center, and XQL Widgets. For example, to view or access any of the **`endpoints`** and **`host_inventory`** datasets, you need role-based access control (RBAC) permissions to the **Endpoint Administration** and **Host Inventory** views. Managed Security Services Providers (MSSP) administration permissions are not enforced on child tenants, but only on the MSSP tenant.
{% endhint %}

| Field                    | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| ------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| \*TYPE                   | Displays the type of dataset based on the method used to upload the data. The possible values include: Correlation, Lookup, Raw, Snapshot, System, and User. For more information on each dataset type, see [What are datasets?](dataset-management/what-are-datasets).                                                                                                                                                                                                                                                                                                      |
| \*LOG UPDATE TYPE        | Event logs are updated either continuously (**Logs**) or the current state is updated periodically (**State**) as detailed in the **Last Updated** column.                                                                                                                                                                                                                                                                                                                                                                                                                   |
| \*LAST UPDATED           | <p>Last time the data in the dataset logs were updated.</p><div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Important</strong></p><p>This column is updated once a day. Therefore, if the dataset was created or updated by the target or lookup flows, it's possible that the <strong>Last Updated</strong> value is a day behind when the queries or reports were run as it was before this column was updated.</p></div>                                                                                                     |
| \*ADDITIONAL STORAGE     | Amount of flexible hot storage-based retention designated for this dataset in months, where a month is calculated as 31 days.                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| \*TOTAL DAYS STORED      | Actual number of days that the data is stored in the Cortex XSIAM tenant, which is comprised of the **HOT RANGE** + the **COLD RANGE**.                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| \*HOT RANGE              | Details the exact period of the Hot Storage from the start date to the end date.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| \*COLD RANGE             | Details the exact period of the Cold Storage from the start date to the end date.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| \*TOTAL SIZE STORED      | Actual size of the data that is stored in the Cortex XSIAM tenant. This number is dependent on the events stored in the hot storage. For the **`xdr_data`** dataset, where the first 31 days of storage are included with your license, the first 31 days are not included in the **TOTAL SIZE STORED** number.                                                                                                                                                                                                                                                              |
| \*ADDITIONAL SIZE STORED | Actual size of the additional flexible hot storage data that is stored in the Cortex XSIAM tenant in GB. This number is dependent on the events stored in the hot storage.                                                                                                                                                                                                                                                                                                                                                                                                   |
| \*AVERAGE DAILY SIZE     | Average daily amount stored in the Cortex XSIAM tenant. This number is dependent on the events stored in the hot storage.                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| \*HOT STORAGE PRIORITY   | Indicates the priority set for the dataset's hot storage as either **Low**, **Medium**, or **High**.                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| \*TOTAL EVENTS           | Number of total events/logs that are stored in the Cortex XSIAM tenant. This number is dependent on the events stored in the hot storage.                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| \*AVERAGE EVENT SIZE     | Average size of a single event in the dataset (**TOTAL SIZE STORED** divided by the **TOTAL EVENTS**). This number is dependent on the events stored in the hot storage.                                                                                                                                                                                                                                                                                                                                                                                                     |
| \*TTL                    | <p>For lookup datasets, displays the value of the time to live (TTL) configured for when lookup entries expire and are removed automatically from the dataset. The possible values are:</p><ul><li><strong>Forever</strong>: Lookup entries never expire (default).</li><li><strong>Custom</strong>: Lookup entries expire according to a set number of days, hours, and minutes. The maximum number of days is 99999.</li></ul><p>For more information, see <a href="dataset-management/set-time-to-live-for-lookup-datasets">Set time to live for lookup datasets</a>.</p> |
| DEFAULT QUERY TARGET     | Details whether the dataset is configured to use as your default query target in XQL Search, so when you write your queries you do not need to define a dataset. By default, only the **`xdr_data`** dataset is configured as the **DEFAULT QUERY TARGET** and this field is set to **Yes**. All other datasets have this field set to **No**. When setting multiple default datasets, your query does not need to mention any of the dataset names, and Cortex XSIAM queries the default datasets using a **`join`**.                                                       |
| TOTAL HOT RETENTION      | Total hot storage retention configured for the dataset in months, where a month is calculated as 31 days.                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| TOTAL COLD RETENTION     | Total cold storage retention configured for the dataset in months, where a month is calculated as 31 days.                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |

</details>

<details>

<summary>Dataset views</summary>

Cortex XSIAM supports creating dataset views in the `Dataset Management` page to enhance data efficiency and security. Dataset views provide a virtual representation of data from one or more datasets, based on the Cortex Query Language (XQL) query defined, and provide multiple benefits, such as joining datasets into logical subsets through defined queries, manipulating data without altering underlying datasets, and segregating data for specific user needs or access privileges through the Role-based access control (RBAC) settings.

Once a dataset view is created, you can edit or delete the dataset view by right-clicking the dataset view in the **Dataset Views** table. A dataset view can only be deleted if there are no other dependencies. For example, if a Correlation Rule is based on a dataset view, you wouldn't be able to delete the dataset view until you removed the dataset view from the XQL query of the Correlation Rule.

Cortex XSIAM logs entries for events related to creating, editing, and deleting datasets or dataset views. These monitored activities are available to view in the datasets and dataset views audit logs in the Management Audit Logs. For more information, see [Monitor datasets and dataset views activity](dataset-management/monitor-datasets-and-dataset-views-activity).

**Building XQL dataset view queries**

When building an XQL query to define a dataset view, the query is built in the same way as creating a query through the Query Builder. Yet, it's important to be aware of the following points that are specific for dataset view queries:

* The following features are unsupported in dataset view queries:
  * RT Correlation Rules
  * Cortex Data Model (XDM)
  * Query Library
  * Presets
  * Cold storage queries (`cold_dataset = <dataset name>`)
* Only the following XQL stages are supported when building a dataset view query:
  * `alter`
  * `dedup`
  * `fields`
  * `filter`
  * `join`
  * `replacenull`
  * `union`
* Once the dataset view is created, it is listed as an available `dataset` when building your XQL queries as long as you have the necessary permissions to access the dataset view in the Role-based access control (RBAC) settings.

**How to create a dataset view**

1. Select Settings → Configurations → Data Management → Dataset Management → Dataset Views.
2. Click New Datset View.
3. Enter a Name and Description (optional) for the dataset view.
4. Create your XQL query for the dataset view by typing in the query box.
5.  (Optional) Click Run to view the query results.

    The query must contain no errors, including using only supported commands, to run; otherwise, the Run button remain disabled.
6.  Click Save.

    You'll only be able to save the dataset view if the query contains no errors; otherwise, the Save button is disabled.

    Once the dataset view is created, you can now control user access permissions through Role-based access control (RBAC).

**Dataset views access permissions**

Access permissions for dataset views are configured in the same way that you set dataset access permissions for any dataset through user roles in Cortex XSIAM Access Management. Cortex XSIAM uses role-based access control (RBAC) to manage roles with specific permissions for controlling user access. RBAC helps manage access to Cortex XSIAM components and datasets, so that users, based on their roles, are granted minimal access required to accomplish their tasks. Once the user role is configured to access these dataset views, you can now assign the user role to the designated users or user groups, who you want to access these dataset views.

How to set access permissions for dataset views

1. Select Settings → Configurations → Access Management.
2.  Configure a user role with the dataset views that you want users to access.

    1. Select Roles.
    2. You can perform one of the following:
       * To create a new role to assign the dataset views, click New Role, and set a Role Name and Description (optional).
       * To edit an existing user role with these dataset views, right-click the relevant user role, and select Edit Role.
       * To create a new role based on an existing role, right-click the relevant user role, select Save As New Role, and set a Role Name and Description (optional).
    3. Under Datasets, you have two options for setting the Cortex Query Language (XQL) dataset access permissions for the user role:
       * Set the user role with access to all XQL datasets by disabling the Enable dataset access management toggle.
       * Set the user role with limited access to certain XQL datasets by selecting the Enable dataset access management toggle and selecting the datasets under the different dataset category headings.
    4. Scroll down to Dataset View and select the particular dataset views that you want assigned to this user role.
    5. Click Save.

    For more information on user roles, see [Manage user roles](../../onboard-cortex-xsiam/post-deployment/manage-user-roles-and-access-management/manage-user-roles).
3. Assign the user role with the dataset views configured to the designated users or user groups. For more information, see [Assign user roles and groups](../../onboard-cortex-xsiam/deployment-steps/set-up-users-and-roles/assign-user-roles-and-groups).

**Dataset Views table**

For each dataset view listed in the table, information is available. Here are descriptions on the columns that may require further explanation:

| Field          | Description                                                           |
| -------------- | --------------------------------------------------------------------- |
| SOURCE QUERY   | Displays the query used to create the dataset view.                   |
| IS VALID       | Details whether the query for the dataset view is still valid or not. |
| RELATED TABLES | Details the other datasets that are related to this dataset view.     |

</details>
