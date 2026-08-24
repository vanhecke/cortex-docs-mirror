---
description: Deploy a Cortex XSIAM Broker VM on Amazon Web Services.
---

# Set up Broker VM on Amazon Web Services

Learn how to set up your Cortex XSIAM Broker virtual machine (VM) on AWS.

After you download your Cortex XSIAM Broker VMDK image, you can convert the image to an Amazon Web Services (AWS) Amazon Machine Image (AMI) using the AWS CLI. The task below explains how to do this on Linux.

{% hint style="info" %}
#### Prerequisite

* Download a Cortex XSIAM Broker VM VMDK image. For more information, see the virtual machine compatibility requirements in [Set up and configure Broker VM](..).
* You need to set up an AWS VM Import role (`vmimport`) before running the `import-snapshot` CLI command. If the role `vmimport` does not exist or does not have the required permissions, you can create it using the steps below or use a different role with the necessary permissions. You'll need an Administrator role or the required permissions to create or modify this role. For more information on setting up an AWS VM Import role and the permissions required, see [Required service role](https://docs.aws.amazon.com/vm-import/latest/userguide/vmie_prereqs.html#vmimport-role).
{% endhint %}

To convert the image to AWS, perform the following procedures in the order listed below.

#### Task 1. Create an IAM User with Proper Permissions

You need to log in using an AWS Identity and Access Management (IAM) user, where the permissions are defined in the IAM policy to use the virtual machine Import and export.

1. Log in to the [AWS IAM Console](https://console.aws.amazon.com/iam/home), and in the navigation pane, select Access Management → Users, and click Create user.
2. Under User name, specify a username, and click Next.
3. In the Permissions options section, select Attach Existing Policies directly, and then in the Permissions policies section, click Create policy.
4. In the JSON tab, copy and paste the following syntax to define the policy:

```json
{ "Version": "2012-10-17", "Statement": [ { "Effect": "Allow", "Action": [ "s3:GetBucketLocation", "s3:GetObject", "s3:PutObject" ], "Resource": ["arn:aws:s3:::mys3bucket","arn:aws:s3:::mys3bucket/_"] }, { "Effect": "Allow", "Action": [ "ec2:CancelConversionTask", "ec2:CancelExportTask", "ec2:CreateImage", "ec2:CreateInstanceExportTask", "ec2:CreateTags", "ec2:DescribeConversionTasks", "ec2:DescribeExportTasks", "ec2:DescribeExportImageTasks", "ec2:DescribeImages", "ec2:DescribeInstanceStatus", "ec2:DescribeInstances", "ec2:DescribeSnapshots", "ec2:DescribeTags", "ec2:ExportImage", "ec2:ImportInstance", "ec2:ImportVolume", "ec2:StartInstances", "ec2:StopInstances", "ec2:TerminateInstances", "ec2:ImportImage", "ec2:ImportSnapshot", "ec2:DescribeImportImageTasks", "ec2:CancelImportTask" ], "Resource": "_" } ] }
```

5. Click Next.
6. In the Policy details section, under Policy name, specify a name for the policy, and click Create policy.
7. Select the policy that you created above based on the syntax you added, and click Next.
8. Complete the user creation process by clicking Create user.

#### Task 2. Create access credentials

1. After confirmation that the user is created, select the user that you created.
2. Open the Security credentials tab, scroll down to the Access key section, and click Create access key.
3. In Step 1 Access key best practices & alternatives perform the following:
4. Select the Command Line Interface (CLI) option.
5. Select the Confirmation checkbox.
6. Click Next.
7. (Optional) In Step 2 Set description tag, you can enter a description for the access key, or leave it empty, and then click Create access key.
8. In Step 3 Retrieve access keys, copy the following user information, which you will need later:
   * User name
   * Access key ID
   * Secret access key

#### Task 3. Setup AWS CLI

You can run the AWS CLI commands using one of the two options below.

**Option 1: AWS CloudShell (Recommended - No Installation)**

AWS CloudShell is a browser-based shell that is pre-authenticated with your Console credentials.

1. Log in to the AWS Management Console.
2. Select the Region where your S3 bucket is located.
3. Click the CloudShell icon (

**Option 2: External Terminal**

Install the AWS CLI and configure it with the IAM user that you created.

1. Login to the server with admin privilege and install the AWS CLI.

```shell
# sudo bash
# apt update
# apt install awscli
```

2. Run the following command to configure the AWS CLI:

```shell
# aws configure
```

You need to specify the proper configurations for the following:

* AWS Access Key ID: The Access key ID for the IAM user you created.
* AWS Secret Access Key: The Secret access key for the IAM user you created.
* Default region name: The Region where you've defined the IAM user you created. You are now ready to implement commands in the AWS CLI.

#### Task 4. Create an AMI Image

To create an AMI image, you need to download Broker VM VMDK file from the Cortex XSIAM Web Console, import this file to your S3 bucket, and then convert the VMDK file to an AMI Image.

1. In the Cortex XSIAM Web Console , select Settings → Configurations → Data Broker → Broker VMs → Add Broker → VMDK.
2. Download the VMDK file, such as **`broker-vm-<broker-vm-version>.vmdk`**, to your computer.
3. Navigate and log in to your AWS account.
4. In the AWS Console, select All services → Storage → S3.
5. On the Buckets page, click Create bucket to upload your Broker VM image to this bucket. Specify a unique name for the S3 bucket and use the default configurations.
6. Upload the Broker VM VMDK you downloaded from Cortex XSIAM to the AWS S3 bucket using one of the following methods:
   * Using the AWS Management Console: On the Buckets page, select your bucket, and click Upload to upload the VMDK file.
   *   Using an external terminal: Run

       ```shell
       # aws s3 cp \~/\<path/to/broker-vm-version.vmdk> s3://\<your\_bucket/broker-vm-version.vmdk>
       ```
7. Prepare the following configurations files on your hard drive.

<details>

<summary>Create configuration.json</summary>

1. In a terminal, create the file:

```shell
# vi configuration.json
```

2. Copy the following content into the file. Replace `<your_bucket>` with the bucket name. Replace `<broker-vm-version.vmdk>` with the VMDK filename.

```json
{ "Description":"Cortex XSIAM Broker VM ", "Format":"vmdk", "UserBucket":{ "S3Bucket":"\<your\_bucket>", "S3Key":"\<broker-vm-version.vmdk>" } }
```

</details>

<details>

<summary>Create trust-policy.json</summary>

1. In a terminal, create the file:

```shell
# vi trust-policy.json
```

2. Copy the following content into the file.

```json
{ "Version": "2012-10-17", "Statement": [ { "Effect": "Allow", "Principal": { "Service": "vmie.amazonaws.com" }, "Action": "sts:AssumeRole", "Condition": { "StringEquals":{ "sts:Externalid": "vmimport" } } } ] }
```

</details>

<details>

<summary>Create role-policy.json</summary>

1. In a terminal, create the file:

```shell
# vi role-policy.json
```

2. Copy the following content into the file. Replace the bucket placeholders with your bucket name. Use `*` to allow access to all S3 buckets.

```json
{ "Version":"2012-10-17", "Statement":[ { "Effect": "Allow", "Action": [ "s3:GetBucketLocation", "s3:GetObject", "s3:ListBucket" ], "Resource": [ "arn:aws:s3:::", "arn:aws:s3:::/_" ] }, { "Effect": "Allow", "Action": [ "s3:GetBucketLocation", "s3:GetObject", "s3:ListBucket", "s3:PutObject", "s3:GetBucketAcl" ], "Resource": [ "arn:aws:s3:::", "arn:aws:s3:::/_" ] }, { "Effect": "Allow", "Action": [ "ec2:ModifySnapshotAttribute", "ec2:CopySnapshot", "ec2:RegisterImage", "ec2:Describe*", "ec2:ImportSnapshot", "ec2:DescribeImportSnapshotTasks" ], "Resource": "*" } ] }
```

</details>

8. Use the **`create-role`** command to create a role named **`vmimport`** and grant VM import and export permissions using the **`trust-policy.json`** file.

```shell
# aws iam create-role --role-name vmimport --assume-role-policy-document "file://trust-policy.json"
```

9. Use the **`put-role-policy`** command to attach the policy to the **`vmimport`** role created above.

```shell
# aws iam put-role-policy --role-name vmimport --policy-name vmimport --policy-document "file:// role-policy.json"
```

10. Create a snapshot from the VMDK file. Run the following command to start the import process:

```shell
# aws ec2 import-snapshot --description "\<Cortex XSIAM Broker VM " --disk-container "file://configuration.json"
```

To track the progress, use the task `id` value from the output and run:

```shell
# aws ec2 describe-import-snapshot-tasks --import-task-ids import-snap-
```

Completed status output:

```json
{ "ImportSnapshotTasks": [ { "Description": "Broker VM snapshot import", "ImportTaskId": "import-snap-12346b69617c1395t", "SnapshotTaskDetail": { ... "DiskImageSize": 2976817664.0, "Format": "vmdk", "SnapshotId": "snap-1234567890", "Status": "completed", "UserBucket": { "S3Bucket": "broker-vm", "S3Key": "broker-vm-.vmdk" } }, "Tags": [] } ] }
```

11. Register the AMI from the snapshot. Once the `describe-import-snapshot-tasks` command shows a status of `completed`, a new Snapshot has been created in your account. You must now register this snapshot as an AMI.
    1. Locate the snapshot ID. In the output of your completed task, find the `SnapshotId`, for example `snap-0123456789abcdef0`. Alternatively, you can find it in the AWS Console:
    2. Select All services → EC2.
    3. In the left sidebar, under Elastic Block Store, select Snapshots.
    4. Locate the snapshot with the description you provided during the import.
    5. Create the image from the snapshot.
    6. Select the checkbox next to your snapshot.
    7. Select Actions → Create image from snapshot.
    8. Specify mandatory settings in the Create image from snapshot section. To ensure the Broker VM functions correctly, configure these settings in the following sections:
       * Image settings
         * Architecture: x86\_64
         * Root device name: `/dev/sda1`
         * Virtualization type: Hardware-assisted virtualization
         * Boot mode: Legacy BIOS
       * Block device mappings - optional
         * Size (GIB): `480GB`
         * Volume type: General Purpose SSD (gp3)
         * IOPS: `3000`
         * Throughput (MB/s): 125 Once the task is complete, the AMI Image is ready for use.
12. (Optional) After the AMI image has been created, you can define a new name for the image. Select All services → EC2 → IMAGES → AMIs and locate your AMI image using the task ID. Select the pencil icon to specify a new name.

#### Task 5. Launch a Broker VM Instance in AWS EC2

You can launch the a Broker VM instance in AWS EC2 using the AMI Image created.

{% hint style="warning" %}
#### Important

A t3.xlarge (16 GB RAM) is the lowest machine type that can be used as an instance type to meet the mandatory 4 vCPU requirement.
{% endhint %}

1. To view the AMI image that you added, select All services → EC2 → Images → AMIs.
2. Select EC2 → Instances, and click Launch instances to create an instance of the AMI image.
3. In the Launch Instance Wizard define the instance according to your company requirements and Launch.
4. (Optional) In the Instances page, locate your instance and use the pencil icon to rename the instance Name.
5. Define HTTPS and SSH access (optional) to your instance. Select your instance and then choose Actions → Security → Change security groups. Attach a security group that allows HTTPS to access the Broker VM Web UI and SSH for remote access when troubleshooting. Make sure to allow these connections to the Broker VM from secure networks only.

{% hint style="info" %}
#### Note

Assigning security groups can take up to 15 minutes.
{% endhint %}

6\. Verify the Broker VM has started correctly. On the Instances page, select your instance, and the choose Actions → Monitor and troubleshoot → Troubleshoot → Get instance screenshot. You are directed to your Broker VM console listing your Broker details.
