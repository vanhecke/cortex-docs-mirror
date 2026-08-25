---
description: Deploy the Cortex XSIAM container-embedded agent to protect CaaS workloads.
---

# CaaS Workloads

Deploy the Cortex XDR container-embedded agent on Container as a Service (CaaS) environments to extend runtime security and vulnerability scanning to containerized workloads. The container-embedded Cortex XDR agent provides malware prevention, exploit protection, vulnerability assessment, and altered binary execution restriction for containers running on managed container services.

The Cortex XDR container-embedded agent is a purpose-built agent designed for containerized environments. The agent embeds directly into your existing workflows.

The container-embedded agent is embedded directly into your container image during the Docker build process. The agent runs as an entry point within your application container, providing runtime security and vulnerability scanning without requiring a separate container.

This topic explains the process of how to embed the Cortex XDR agent in your dockerfile.

{% hint style="info" %}
### Notice

This feature requires a Cloud Runtime Security or Cortex XSIAM Premium license. Every 10 container-embedded agents will consume a single Cortex Runtime Security license.
{% endhint %}

### **CaaS container-embedded agent installer**

The following managed container services are supported. See the prerequisites tables below for the requirements for each container service.

* AWS ECS Fargate; containers using x86\_64 and AArch64 architecture
* Azure Container Instances (ACI); containers using x86\_64 architecture
* Google Cloud Run (GCR); containers using x86\_64 architecture

**Prerequisites**

Before you deploy the container-embedded agent, verify the following:

<table><thead><tr><th width="250.25">Prerequisite</th><th>Details</th></tr></thead><tbody><tr><td>Supported Environment</td><td>AWS ECS Fargate; containers using x86_64 and aarch64 architecture</td></tr><tr><td>Requirements</td><td><p>Cortex XDR agent version 9.2.0 or later</p><p>Required resources per container:</p><ul><li>Disk space: 1.5 GB</li><li>1 CPU</li><li>Memory: 512 MB</li></ul><p>Dockerfile requirements:</p><ul><li>SYS_PTRACE must be enabled</li></ul><p>Assets discovery: Onboard the relevant AWS environments</p><p>Drift detection: Container registry image scanning</p></td></tr><tr><td>Limitations</td><td><ul><li>ENTRYPOINT/CMD must not be added to the task_definition.</li><li>ENTRYPOINT cannot be run in exec format with the CMD shell command.</li><li>AArch64-based architecture does not support exploit protection mechanisms.</li></ul></td></tr></tbody></table>

<table><thead><tr><th width="250.25">Prerequisite</th><th>Details</th></tr></thead><tbody><tr><td>Supported Environment</td><td>Azure Container Instances (ACI) containers using x86_64 architecture</td></tr><tr><td>Requirements</td><td><p>Cortex XDR agent version 9.3.0 or later</p><p>In your YAML deployment file, define the following:</p><p>a) Required resources per container:</p><ul><li>1 CPU</li><li>Memory: 1.5 GB</li></ul><p>b) Azure container registry credentials imageRegistryCredentials:</p><p>Server: Full ACR</p><p>Username: Access Key Admin Username</p><p>Password: Access Key Admin User Password</p><p>c) There are two valid identity options, one of these identities must be defined:</p><ul><li>System Identity</li><li>User Identity</li></ul><p>d) The relevant identity must have Reader and AcrPull permissions</p><p><br>e) securityContext: privileged: true</p><p>f) For the User Identity option, assign the following Environment Variables:</p><ul><li>UAMI_CLIENT_ID_XDR: User assigned Client ID</li><li>SUB_ID_XDR: Azure subscription ID</li><li>RG_XDR: Resource Group</li><li>ACI_NAME_XDR: Container name</li></ul></td></tr><tr><td>Supported deployments</td><td><ul><li>System Identity: System-Assigned Managed Identity</li><li>Identity Permissions: Identity has Reader access to the Container Instance resource</li><li>Image Resolution: Image referenced by digest</li><li><p>User Identity: User-Assigned Managed Identity<br>For User Identity deployment, user must also define the following environment variables:</p><ul><li>SUBSCRIPTION_ID_FOR_CORTEX</li><li>RESOURCE_GROUP_FOR_CORTEX</li><li>CONTAINER_INSTANCE_NAME_FOR_CORTEX</li></ul></li></ul></td></tr></tbody></table>

<table><thead><tr><th width="250.25">Prerequisite</th><th>Details</th></tr></thead><tbody><tr><td>Supported Environment</td><td>Google Cloud Run (GCR) containers using x86_64 architecture</td></tr><tr><td>Requirements</td><td><p>Cortex XDR agent version 9.3.0 or later</p><p>a) Required resources per container:</p><ul><li>1 CPU</li><li>Memory: 1.5 GB</li></ul><p>b) Dockerfile requirement:</p><p>For log retention, set the environment variable path:</p><p>XDR_LOG_DIR = &#x3C;/opt/traps/log></p><p>Note: Do not use /var/log or any subdirectories from it.</p></td></tr><tr><td>Supported deployments</td><td><ul><li>Service Account Permissions: Service account has roles/run.viewer (Cloud Run Viewer)</li><li>Cloud Run Service: Container Count (Up to 2 containers per Service)</li><li>Cloud Run Job: Container Count (Up to 1 container per Job)</li></ul></td></tr><tr><td>Limitations</td><td><ul><li>Instance-based billing only</li><li>Execution environment: Second Generation and above</li></ul></td></tr></tbody></table>

**To create the Cortex XDR container-embedded agent Dockerfile via API.**

See the API reference guide: [Create distributions](broken-reference)

**To create the Cortex XDR container-embedded agent Dockerfile via user interface:**

1. In your Cortex management console, navigate to **Inventory** → **Endpoints** → **Installations**, click Create.
2. Select **CaaS** as the Package Type and in Metadata, select **Container Embedded** as the Deployment Type.
   1. Define the configuration settings for version and proxy (optional).
   2. Upload your Dockerfile. Cortex XSIAM validates your Dockerfile against the prerequisites.
3. A new Agent Installation instance will be created- right-click it and download the newly generated Dockerfile.

Embed the Cortex XDR container-embedded agent Dockerfile into your container image:

1. Select the newly generated Dockerfile.
2. Re-build your container image using the newly generated Dockerfile.
3. During the build process, the agent binary will be fetched from the Cortex repository and baked into the image.
4. Once the build process is successfully finished, you are ready to use the new container image in your CaaS environments, based on the prerequisites above.
