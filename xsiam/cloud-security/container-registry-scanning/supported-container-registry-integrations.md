---
description: Learn about supported container registry integrations in Cortex XSIAM
---

# Supported container registry integrations

Container Registry scanning supports both managed cloud registries and third-party registry integrations, allowing you to monitor container images across various environments.

**Managed Cloud Registries**

The container registry scanner automatically detects and scans container registries and images within your onboarded cloud accounts. Supported registries include:

* Amazon Elastic Container Registry (ECR)
* Azure Container Registry (ACR)
* Google Artifact Registry (GAR)
* Oracle Cloud Infrastructure (OCI) Artifact Registry

For more details, see [configure registry scanning for cloud accounts](configure-registry-scanning-for-cloud-accounts).

**Third-Party Integrations**

The container registry scanner supports agentless scanning of container images by direct integration with various third-party registries, independent of the cloud account onboarding process. These integrations include a streamlined, user-friendly connector configuration experience for the following:

* [Docker Hub](../../configure-cortex-xsiam/cortex-xsiam-data-sources/vendor-specific-data-sources-and-connectors/docker/connect-docker-hub-registry)
* [Docker V2 compliant registries](../../configure-cortex-xsiam/cortex-xsiam-data-sources/vendor-specific-data-sources-and-connectors/docker/connect-docker-v2-compliant-container-registry)
* [GitLab Container Registry](../../configure-cortex-xsiam/cortex-xsiam-data-sources/vendor-specific-data-sources-and-connectors/gitlab/connect-gitlab-container-registry)
* [Harbor Registry](../../configure-cortex-xsiam/cortex-xsiam-data-sources/vendor-specific-data-sources-and-connectors/harbor/connect-harbor-registry)
* [JFrog Container Registry](../../configure-cortex-xsiam/cortex-xsiam-data-sources/vendor-specific-data-sources-and-connectors/jfrog/connect-jfrog-container-registry)
* [Sonatype Nexus Repository Manager](../../configure-cortex-xsiam/cortex-xsiam-data-sources/vendor-specific-data-sources-and-connectors/sonatype-nexus/connect-sonatype-nexus-registry)

Cortex XSIAM also scans images in the Red Hat OpenShift integrated container registry. Because this registry runs inside your cluster, scans are performed in-cluster through the Kubernetes connector. For more details, see [OpenShift container registry](https://app.gitbook.com/s/SqNMu2K0VWh4WXps5pCW/onboard-the-kubernetes-connector/openshift-container-registry).
