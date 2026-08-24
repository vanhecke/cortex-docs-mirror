---
description: Deploy a Cortex XSIAM Broker VM on Google Cloud Platform.
---

# Set up Broker VM on Google Cloud Platform (GCP)

Learn more about how to set up your Cortex XSIAM Broker VM on Google Cloud Platform.

You can deploy the Broker VM on Google Cloud Platform. The Broker VM allows communication with external services through the installation and setup of applets such as the Syslog collector applet.

To set up the Broker VM on the Google Cloud Platform, install the VMDK image provided in Cortex XSIAM.

{% hint style="info" %}
#### Prerequisite

* Download a Cortex XSIAM Broker VM VMDK image. For more information, see the virtual machine compatibility requirements in [Set up and configure Broker VM](..).
* To complete the set up, you must have G Cloud installed and have an authenticated user account.
{% endhint %}

Perform the following procedures in the order listed below.

<details>

<summary>Create a Google Cloud Storage bucket in G Cloud</summary>

From G Cloud, create a Google Cloud Storage bucket to store the Broker VM image.

1. [Create a project in GCP](https://cloud.google.com/resource-manager/docs/creating-managing-projects). Enable Google Cloud Storage, for example, `brokers-project`. Define a default network.
2. [Create a bucket](https://cloud.google.com/storage/docs/creating-buckets), such as `broker-vms`.

</details>

<details>

<summary>Set up the GCP project</summary>

Open a command prompt and run the following:

```shell
gcloud config set project <project-id>
```

</details>

<details>

<summary>Upload the VMDK image to the Google Cloud Storage bucket</summary>

Upload the VMDK image to the bucket, run the following:

```shell
gsutil cp </path/to/broker.vmdk> gs://<bucket-name>
```

</details>

<details>

<summary>Import the GCP image</summary>

You can import the GCP image using either G Cloud CLI or Google Cloud console.

{% hint style="info" %}
#### Note

The import tool uses Cloud Build API, which must be enabled in your project. For the import to work, Cloud Build service account must have **`compute.admin`** and **`iam.serviceAccountUser`** roles. When using the Google Cloud console to import the image, you will be prompted to add these permissions automatically.
{% endhint %}

{% hint style="danger" %}
#### Danger

Before importing a GCP image using the gcloud CLI, ensure that you update the Google Cloud components to version 371.0.0 and above using the following command:

```shell
gcloud components update
```
{% endhint %}

The following command uses the minimum required parameters. For more information on permissions and available parameters, refer to the [Google Cloud SDK](https://cloud.google.com/sdk/gcloud/reference/beta/compute/images/import).

Open a command prompt and run the following:

```shell
gcloud compute images import <VMDK image> --data-disk --source-file="gs://<image path>" --network=<network_name> --subnet=<subnet_name> --zone=<region> --async
```

</details>

<details>

<summary>Create a new instance of the image</summary>

When the Google Compute completes the image creation, create a new instance.

1. In Google Cloud Platform, select **Compute Engine** → **VM instances**.
2. Select **Create instance**.
3. Under **Boot disk**, choose **Custom images**. Select the image you created.
4. Configure the instance for your workload:
   * Use `e2-standard-2` for Agent Proxy only.
   * Use `e2-standard-4` for multiple applets.

</details>

<details>

<summary>Allow the 4443 port in your firewall configuration</summary>

1. In the Google Cloud menu, select **VPC network** → **Firewall**. Select **Create firewall rule**.
2. Set the rule parameters:
   * **Name:** Enter a name for the rule.
   * **Network:** Select the Broker VM network.
   * **Direction of traffic:** Select **Ingress**.
   * **Targets:** Select **All instances in the network**.
   * **Source IPv4 ranges:** Enter the allowed client IP range. Use `0.0.0.0/0` to allow all addresses.
   * **TCP:** Enter `4443`.
3. Select **Create**. The rule appears under **VPC firewall rules**.

</details>

<details>

<summary>Verify that the firewall rule is assigned to the Broker VM</summary>

1. In the Google Cloud menu, select **Compute Engine** → **VM instances**.
2. For the Broker VM, select **More actions** (⋮) → **View network details**.
3. Under **Firewall and routes details**, select **Firewalls**.
4. Verify that the firewall rule appears.

You can now connect to the Broker VM web console using the Broker VM IP address. Connect with https over port 4443 using the format `https://<ip address>:4443`.

</details>
