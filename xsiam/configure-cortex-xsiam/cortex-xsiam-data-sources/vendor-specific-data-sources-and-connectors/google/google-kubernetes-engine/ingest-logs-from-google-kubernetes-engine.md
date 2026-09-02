---
description: Collect Google Kubernetes Engine data with Cortex XSIAM.
---

# Ingest logs from Google Kubernetes Engine

Instead of forwarding Google Kubernetes Engine (GKE) logs directly to Google StackDrive, Cortex XSIAM can ingest container logs from GKE using Elasticsearch Filebeat. To receive logs, you must install Filebeat on your containers and enable Data Collection settings for Filebeat.

When Cortex XSIAM begins receiving logs, the app automatically creates an Cortex Query Language (XQL) dataset using the vendor and product name that you specify during Filebeat setup. It is recommended to specify a descriptive name. For example, if you specify `google` as the vendor and `kubernetes` as the product, the dataset name will be `google_kubernetes_raw`. If you leave the product and vendor blank, Cortex XSIAM assigns the dataset a name of `container_container_raw`.

After Cortex XSIAM creates the dataset, you can search your GKE logs using XQL Search.

1. Install Filebeat on your containers. For more information, see [https://www.elastic.co/guide/en/beats/filebeat/current/running-on-kubernetes.html](https://www.elastic.co/guide/en/beats/filebeat/current/running-on-kubernetes.html).
2.  [Ingest logs from Elasticsearch Filebeat](../../elastic/elasticsearch-filebeat/ingest-logs-from-elasticsearch-filebeat).

    Record your token key and API URL for the Filebeat Collector instance as you will need these later in this workflow.
3.  Deploy a Filebeat as a DaemonSet on Kubernetes.

    This ensures there is a running instance of Filebeat on each node of the cluster.

    a. Download the manifest file to a location where you can edit it.

    ```
    curl -L -O https://raw.githubusercontent.com/elastic/beats/7.10/deploy/kubernetes/filebeat-kubernetes.yaml
    ```

    b. Open the YAML file in your preferred text editor.

    c. Remove the `cloud.id` and `cloud.auth` lines.\
    <img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2FwIGGANV6Pb9U7EXVbTOk%2Fimage.png?alt=media&#x26;token=31da9c6a-8e43-4d72-9b20-52a3baf535da" alt="" data-size="original">

    d. For the **`output.elasticsearch`** configuration, replace the **`hosts`**, **`username`**, and **`password`** with environment variable references for **`hosts`** and **`api_key`**, and add a field and value for **`compression_level`** and **`bulk_max_size`**.\
    <img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2F4tquZyD0sVykLFtxQbDK%2Fimage.png?alt=media&#x26;token=57c38048-87c3-4c47-afc8-2066c838953d" alt="" data-size="original">

    e. In the **`DaemonSet`** configuration, locate the **`env`** configuration and replace **`ELASTIC_CLOUD_AUTH`**, **`ELASTIC_CLOUD_ID`**, **`ELASTICSEARCH_USERNAME`**, **`ELASTICSEARCH_PASSWORD`**, **`ELASTICSEARCH_HOST`**, **`ELASTICSEARCH_PORT`** and their relative values with the following.

    * **`ELASTICSEARCH_ENDPOINT`:** Specify the API URL for your Cortex XSIAM tenant. You can copy the URL from the Filebeat Collector instance you set up for GKE in the Cortex XSIAM management console (Settings → (ConfigurationsData CollectionCustom CollectorsCopy API URL`https://api-tenant external URL:443/logs/v1/filebeat)`
    * **`ELASTICSEARCH_API_KEY`:** Specify the token key you recorded earlier during the configuration of your Filebeat Collector instance.

After you configure these settings your configuration should look like the following image.![](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2FGZ3AvBTdzCe4R6amg4u1%2Fimage.png?alt=media\&token=b814f421-a517-4ee6-82d1-9bf82731b099)

f. Save your changes.

4. If you use RedHat OpenShift, you must also specify additional settings. See [https://www.elastic.co/guide/en/beats/filebeat/7.10/running-on-kubernetes.html](https://www.elastic.co/guide/en/beats/filebeat/7.10/running-on-kubernetes.html#_red_hat_openshift_configuration).
5. Deploy Filebeat on your Kubernetes.

```
kubectl create -f filebeat-kubernetes.yaml
```

This deploys Filebeat in the kube-system namespace. If you want to deploy the Filebeat configuration in other namespaces, change the namespace values in the YAML file (in any YAML inside this file) and add `-n <your_namespace>`.\
\
After you deploy your configuration, the Filebeat DameonSet runs throughout your containers to forward logs to Cortex XSIAM. You can review the configuration from the Kubernetes Engine console: **Workloads → Filebeat → YAML**.

{% hint style="info" %}
**Note**

Cortex XSIAM supports logs in single line format or multiline format. For more information on handling messages that span multiple lines of text in Elasticsearch Filebeat, see [Manage Multiline Messages](https://www.elastic.co/guide/en/beats/filebeat/current/multiline-examples.html).
{% endhint %}

6. After Cortex XSIAM begins receiving logs from GKE, you can use the XQL Search to search for logs in the new dataset.
