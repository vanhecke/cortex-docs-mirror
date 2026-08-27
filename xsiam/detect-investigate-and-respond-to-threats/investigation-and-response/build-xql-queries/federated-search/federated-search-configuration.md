---
description: Configure Cortex XSIAM Federated Search connections for external data sources.
---

# Federated Search configuration

Before you run federated searches, you must first create an external dataset to run the query.

To define a new external dataset, go to **Settings → Configurations → Data Management → Dataset management → External Datasets** and click Add External Dataset. You can also access the wizard through the Query builder page **Investigation & Response → Search → Query Builder → Federated Search**.

1. Prerequisites: Perform preliminary steps on your remote storage, such as creating a policy and attaching it to a role.
2.  Connection setup and dataset definition:

    Configure the connection and trust relationship with the CSP.

    Define the dataset name, description, path within the storage, region, and format.
3. Schema Validation: Initiate the process to access the remote storage, pull sample data, and deduce the schema. You can view the auto-detected schema and if the fields aren't accurate, add or delete fields as needed.
4. Configuration review and dataset creation: Go over the details and create the dataset.

<details>

<summary>Amazon S3</summary>

#### Prerequisite

* Access to Cortex XSIAM communication. For a list of the authorized IP addresses, see [Enable access to required PANW resources](https://docs-cortex.paloaltonetworks.com/r/5CAbsl8idaK8R43ZLhoTOw/IWU8BPTfKWhw35rIRJGKbQ).
* An AWS bucket that contains your data sources.
* Permissions to modify IAM policies in AWS.

#### How to add an external dataset for an Amazon S3 bucket

1.  In Amazon S3, create an IAM policy to allow access to your bucket.

    1. Navigate to IAM (Access Management) → Policies → Create Policy and select S3.
    2. In Actions Allowed, select Effect → Allow.
    3. In List, select ListBucket.
    4. In Read, select GetObject.
    5. In Resources, click ARN and fill your bucket name for both Bucket and Object. For Object, use an asterisk (\*) and select Any object name.
    6. Check the details and click Next.
    7. Click Create Policy.

    Your policy appears in the Policies table.
2. Create a role for the policy you created.
   1. Navigate to IAM → Roles → Create Role.
   2. In the Trusted entity type page, select Web identity.
   3.  In the Web identity page, under Identity provider, select Google, and under Audience, type 00000, and click Next.

       This will later be replaced by the identity created by Cortex XSIAM.
   4. Select your policy and click Next.
   5. Type a name for your role and select Create Role.
3. Configure the connection.
   1. In the Federated Search wizard, type the Role ARN from AWS.
   2. Specify the bucket region. Supported regions are us-east-1, us-west-2, ap-northeast-2, ap-southeast-2, eu-west-1, eu-central-1.
   3.  Click Generate to create a new Identity for this connection and copy the generated Identity.

       This is the identity provided by Cortex XSIAM to create a trust relationship with AWS.
   4. In the AWS IAM console, add a trust relationship by adding the identity you generated above to the role and set a maximum session duration.
      1. In AWS IAM, select Roles.
      2. Select the role you created.
      3.  Click Edit and set Maximum session duration to 12 hours.

          This configures the length of time the session lasts before requiring re-authentication.
      4. Click Save changes.
      5. Select Trust Relationships and click Edit policy.
      6. Replace the value of `accounts.google.com:aud` with the identity you generated above. You can also replace the policy content with the provided code snippet.
      7. Click Update policy.
4. Configure the dataset.
   1. In the Federated Search wizard, type a meaningful dataset name and add an optional description. External dataset names must always begin with `external_`.
   2.  In S3 URI, enter the Amazon S3 path of the partition directory using the S3 format. To find the path, in the AWS bucket click the directory to display Object overview and copy the S3 URI. The path can only include letters, digits, and the symbols "-","\_","=",".". For example, `s3://bucket-name/table-name/`. Don't use wildcards.

       Your partitioned data must follow the Hive partitioning format, which uses key-value pairs. In your directory, name your partitions in the yyyy-mm-dd format, for example ds=2025-10-07. This creates external datasets based on your partitioned data source paths.

       When you filter a query using the Query Builder Time frame selection, the query uses the dates in the partition.
   3. Specify the format. For correct deduction of the schema, you must provide the correct file format. Federated Search supports CSV, Parquet, and JSONL files. For optimal results, we recommend using Parquet format with explicit schema definition. Federated Search supports certain use cases of gzip compressed files. For additional information, please contact your support agent.
5. Test the connection.
6. If the connection was successful, click Next.
7.  Validate the schema.\
    Cortex XSIAM performs an automated schema discovery process by sampling approximately 500 events, typically from the most recent partitions available in the configured path.\
    The auto-discovery relies on sampling and may not capture less common event types or fields that appear infrequently within the dataset. As a result, some fields visible in broader searches may not be included in the initially detected schema. This process also conducts validations to catch as many field type mismatches as possible, though due to the high volume of data involved, it cannot detect all mismatches.\
    \
    The auto-discovery process is meant to accelerate onboarding by generating a baseline schema, however you can still refine the schema as needed.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>We highly recommend that you don't change the auto-detected schema. However, if the auto-detected schema is incorrect, you can add, edit or delete fields.</p></div>

    * Missing fields: For json files and csv files, even if there are missing fields in the detected schema, your query will run successfully. For parquet files, the full schema is always deduced. If there's a partial schema and you add new fields to the actual data, the query will also run correctly.
    * Field type mismatch: If a type mismatch is detected during onboarding, Cortex XSIAM displays an error message with the specific field name and allows you to change the field type by deleting the field and re-adding it with its proper type. If the type mismatch is found while running a query, the query fails and Cortex XSIAM displays an error message. In this case, you must delete the external dataset, re-onboard it and make the required changes to the field type accordingly.
    * You can't delete the ds field, which is used for Hive partitioning.
    * After you save the schema, you can't delete any fields you added during setup.<br>
8. Review all the details. You can go back to change any details you want, save the query and return to the external datasets table, or save and start a query in the XQL query page. Saving and starting a query can take some time.

{% hint style="info" %}
Note: When you create, delete, or update an external dataset, the action is recorded in the Management Audit Logs under the type External Datasets.
{% endhint %}

</details>

<details>

<summary>Google GCS</summary>

#### Prerequisite

* Access to Cortex XSIAM communication. For a list of the authorized IP addresses, see [Enable access to required PANW resources](../../../../onboard-cortex-xsiam/deployment-steps/activate-cortex-xsiam/enable-access-to-required-panw-resources).
* A GCS bucket that contains your data sources.
* Permissions to modify IAM policies in GCS.

#### How to add an external dataset for a Google Cloud Storage bucket

1. Configure the connection.
   1.  Specify the bucket region. Federated Search supports the following regions:\
       `africa-south1`, `asia-east1`, `asia-east2`, `asia-northeast1`, `asia-northeast2`, `asia-northeast3`, `asia-south1`, `asia-south2`, `asia-southeast1`, `asia-southeast2`, `australia-southeast1`, `australia-southeast2`, `europe-central2`, `europe-north1`, `europe-north2`, `europe-southwest1`, `europe-west1`, `europe-west10`, `europe-west12`, `europe-west2`, `europe-west3`, `europe-west4`, `europe-west6`, `europe-west8`, `europe-west9`, `me-central1`, `me-central2`, `me-west1`, `northamerica-northeast1`, `northamerica-northeast2`, `northamerica-south1`, `southamerica-east1`, `southamerica-west1`, `us-central1`, `us-east1`, `us-east4`, `us-east5`, `us-south1`, `us-west1`, `us-west2`, `us-west3`, `us-west4`

       You can only configure regions that are in the multi-region of your tenant.
   2.  Click Generate to create a new Identity for this connection and copy the generated Identity.

       This is the service account that will allow read access to the GCS bucket.
   3. Grant access to the connection.
      1. In the GCS project, navigate to IAM.
      2. In Allow → View by principals, click Grant access.
      3. Under New principles, paste the Identity you generated in the Federated Search wizard.
      4. Under Assign roles, select the role Storage Object Viewer.
      5. Click Save.
2. Configure the dataset.
   1. In the Federated Search wizard, type a meaningful dataset name and add an optional description. External dataset names must always begin with `external_`.
   2.  In GS URI, specify the partition directory. For example, `s3://bucket-name/table-name/`. Don't use wildcards.

       Your partitioned data must follow the Hive partitioning format, which uses key-value pairs. In your directory, name your partitions in the yyyy-mm-dd format, for example ds=2025-10-07. This creates external datasets based on your partitioned data source paths.

       When you filter a query using the Query Builder Time frame selection, the query uses the dates in the partition.
   3. Specify the format. For correct deduction of the schema, you must provide the correct file format. Federated Search supports CSV, Parquet, and JSONL files. For optimal results, we recommend using Parquet format with explicit schema definition. Federated Search supports certain use cases of gzip compressed files. For additional information, please contact your support agent.
3. Test the connection.
4. If the connection was successful, click Next.
5.  Validate the schema.\
    Cortex XSIAM performs an automated schema discovery process by sampling approximately 500 events, typically from the most recent partitions available in the configured path.\
    The auto-discovery relies on sampling and may not capture less common event types or fields that appear infrequently within the dataset. As a result, some fields visible in broader searches may not be included in the initially detected schema. This process also conducts validations to catch as many field type mismatches as possible, though due to the high volume of data involved, it cannot detect all mismatches.\
    \
    The auto-discovery process is meant to accelerate onboarding by generating a baseline schema, however you can still refine the schema as needed.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>We highly recommend that you don't change the auto-detected schema. However, if the auto-detected schema is incorrect, you can add, edit or delete fields.</p></div>

    * Missing fields: For json files and csv files, even if there are missing fields in the detected schema, your query will run successfully. For parquet files, the full schema is always deduced. If there's a partial schema and you add new fields to the actual data, the query will also run correctly.
    * Field type mismatch: If a type mismatch is detected during onboarding, Cortex XSIAM displays an error message with the specific field name and allows you to change the field type by deleting the field and re-adding it with its proper type. If the type mismatch is found while running a query, the query fails and Cortex XSIAM displays an error message. In this case, you must delete the external dataset, re-onboard it and make the required changes to the field type accordingly.
    * You can't delete the ds field, which is used for Hive partitioning.
    * After you save the schema, you can't delete any fields you added during setup.
6. Review all the details. You can go back to change any details you want, save the query and return to the external datasets table, or save and start a query in the XQL query page. Saving and starting a query may take some time.

{% hint style="info" %}
When you create, delete, or update an external dataset, the action is recorded in the Management Audit Logs under the type External Datasets
{% endhint %}

</details>

<details>

<summary>Azure Blob Storage</summary>

#### Prerequisite

* Access to Cortex XSIAM communication. For a list of the authorized IP addresses, see [Enable access to required PANW resources](../../../../onboard-cortex-xsiam/deployment-steps/activate-cortex-xsiam/enable-access-to-required-panw-resources).
* An Azure Blob Storage blob with your data sources.
* Permissions to modify IAM policies in Azure Blob Storage.

#### How to add an external dataset for an Azure blob

1.  Create a new registration in Azure Blob Storage to be used by Federated Search.

    1. In your Azure tenant, navigate to All Services → App registrations, and click New registration.
    2. Fill the following fields as below:
       * Name: Type a name
       * Supported account types: Accounts in this organizational directory only
       * Redirect URI: Leave blank for now.
    3. Click Register.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note:</strong> Copy the Directory (tenant) ID, the Application (client) ID, and the Object ID. You will use these in the connection step.</p></div>
2. Configure the connection.
   1. In the Federated Search wizard, paste the following values from Azure: Directory ID, Application ID, Object ID.
   2.  Specify the blob region. Federated Search supports only eastus2.

       You can only configure regions that are in the multi-region of your tenant.
   3.  Click Generate to create a new Identity for this connection and copy the generated Identity.

       This is the identity used to establish the trust with Azure Storage.
3. Create credentials for the application.
   1. In your Azure tenant, under All services → App registrations, select your application and click Add a certificate or secret.
   2. Select Federated credentials and click Add credential.
   3. In the Add a credential page, fill in the following values:
      * Federated credential scenario: Other issuer
      * Issuer: https://accounts.google.com
      * Type: Explicit subject identifier
      * Value: Identity you generated above in the Federated Search wizard.
   4. Type a name and description, and click Add.
4. Assign a role to the application.
   1. In Azure → Storage accounts, select your blob.
   2. Select the container and, in the left menu, click Access Control (IAM).
   3. Under Check Access, click Add role assignment.
   4. In Role → Job function roles, select Storage Blob Data Reader and click Next.
   5. For the Assign access to field, select User, group, or service principal.
   6. Click Select members, search for the name of your app registration. Select the app registration and click Select.
   7. Click Review + assign to finalize.
5. Configure the dataset.
   1. In the Federated Search wizard, type a meaningful dataset name and add an optional description. External dataset names must always begin with `external_`.
   2.  In Container URL, specify the partition directory. For example, `s3://bucket-name/table-name/`. Don't use wildcards.

       Your partitioned data must follow the Hive partitioning format, which uses key-value pairs. Name your partitions in the yyyy-mm-dd format, for example ds=2025-10-07. This creates external datasets based on your partitioned data source paths.

       When you filter a query using the Query Builder Time frame selection, the query uses the dates in the partition.
   3. Specify the format. For correct deduction of the schema, you must provide the correct file format. Federated Search supports CSV, Parquet, and JSONL files. For optimal results, we recommend using Parquet format with explicit schema definition. Federated Search supports certain use cases of gzip compressed files. For additional information, please contact your support agent.
6. Test the connection.
7. If the connection was successful, click Next.
8.  Validate the schema.\
    Cortex XSIAM performs an automated schema discovery process by sampling approximately 500 events, typically from the most recent partitions available in the configured path.\
    The auto-discovery relies on sampling and may not capture less common event types or fields that appear infrequently within the dataset. As a result, some fields visible in broader searches may not be included in the initially detected schema. This process also conducts validations to catch as many field type mismatches as possible, though due to the high volume of data involved, it cannot detect all mismatches.\
    \
    The auto-discovery process is meant to accelerate onboarding by generating a baseline schema, however you can still refine the schema as needed.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>We highly recommend that you don't change the auto-detected schema. However, if the auto-detected schema is incorrect, you can add, edit or delete fields.</p></div>

    * Missing fields: For json files and csv files, even if there are missing fields in the detected schema, your query will run successfully. For parquet files, the full schema is always deduced. If there's a partial schema and you add new fields to the actual data, the query will also run correctly.
    * Field type mismatch: If a type mismatch is detected during onboarding, Cortex XSIAM displays an error message with the specific field name and allows you to change the field type by deleting the field and re-adding it with its proper type. If the type mismatch is found while running a query, the query fails and Cortex XSIAM displays an error message. In this case, you must delete the external dataset, re-onboard it and make the required changes to the field type accordingly.
    * You can't delete the ds field, which is used for Hive partitioning.
    * After you save the schema, you can't delete any fields you added during setup.
9. Review all the details. You can go back to change any details you want, save the query and return to the external datasets table, or save and start a query in the XQL query page. Saving and starting a query can take some time.

{% hint style="info" %}
Note: When you create, delete, or update an external dataset, the action is recorded in the Management Audit Logs under the type External Datasets.
{% endhint %}

</details>
