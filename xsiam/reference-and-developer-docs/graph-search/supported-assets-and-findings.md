# Supported assets and findings

{% hint style="info" %}
### Notice

This feature is included with a Cortex XSIAM Premium license. It is also included with any other Cortex XSIAM license that has the Cloud Posture Security or Cloud Runtime Security add-on.
{% endhint %}

{% hint style="warning" %}
### Prerequisite

Graph Search requires **View** or **View/Edit** RBAC permissions for **Graph Search** under **Investigation & Response** → **Search**.
{% endhint %}

The following tables list the supported assets and findings that can be used in Graph Search.

<details>

<summary>Supported assets table</summary>

Below are the asset classes and asset categories that are supported. When clicking on any asset category, the applicable asset types are displayed in the entity picker of the Graph Search user interface for building query based on the available data.

| Asset Class Name | Asset Category                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| ---------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| AI               | <ul><li>AI Model</li><li>AI Workspace</li><li>Dataset</li><li>Model Endpoint</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| API              | <ul><li>API Endpoint</li><li>API Gateway</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| Code             | <ul><li>CI/CD Pipeline</li><li>Repository</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| Compute          | <ul><li>Container Cluster</li><li>Container Image</li><li>Container Image Repository</li><li>Container Instance</li><li>Container Registry</li><li>Container Service</li><li>Container Specification</li><li>Container Workload</li><li>Kubernetes Cluster</li><li>Kubernetes ConfigMap</li><li>Kubernetes Endpoint</li><li>Kubernetes Gateway API</li><li>Kubernetes Ingress</li><li>Kubernetes Namespace</li><li>Kubernetes Network Policy</li><li>Kubernetes Node</li><li>Kubernetes Secret</li><li>Kubernetes Service</li><li>Kubernetes Workload</li><li>Registry Image</li><li>Runtime Image</li><li>Serverless Function</li><li>Virtual Machine</li><li>Virtual Machine Image</li></ul> |
| Data             | <ul><li>Backup</li><li>Bucket</li><li>Database</li><li>Disk</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| External Surface | <ul><li>Services</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| Identity         | <ul><li>Group</li><li>Identity</li><li>Policy</li><li>Service Account</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| Network          | <ul><li>Gateway</li><li>Load Balancer</li><li>Network Interface</li><li>Public internet</li><li>Subnet</li><li>VPC</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| Organization     | <ul><li>Account</li><li>Organization</li><li>Organization Unit</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |

</details>

<details>

<summary>Supported findings table</summary>

Below are the findings categories that are supported, along with the name of the category that you select in the entity picker of the Graph Search user interface.

| Finding Category Name | Finding Category to Select in Graph Search |
| --------------------- | ------------------------------------------ |
| Configuration         | Configuration Finding                      |
| Data                  | Data Finding                               |
| Identity              | Identity Finding                           |
| Malware               | Malware Finding                            |
| Posture               | Posture Finding                            |
| Vulnerability         | Vulnerability Finding                      |

</details>
