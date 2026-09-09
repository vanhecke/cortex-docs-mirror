---
description: >-
  Learn how to configure Cortex XSIAM to scan container registries in
  third-party integrations
---

# Configure registry scanning for third party integrations

The container registry scanner supports agentless scanning of container images through direct integration with third-party registries. This integration is independent of the cloud account onboarding process.

{% hint style="warning" %}
**Limitation:** Registry scanning supports container images up to **80 GB** in size. Successful scanning of images larger than 80 GB is not guaranteed.
{% endhint %}

To add a container registry connector:

1. Go to **Settings > Data Sources & Integrations**.
2. Click **+ Add New**. The **Add Data Sources or Integrations** page opens.
3. In the search bar, enter the name of the data source, or click **Show More** and select **Container Registries**.
4. Select the connector you want to add.

For information about creating and managing container registry connectors, see

* [Docker Hub](../../configure-cortex-xsiam/cortex-xsiam-data-sources/vendor-specific-data-sources-and-connectors/docker/connect-docker-hub-registry)
* [Docker V2 compliant registries](../../configure-cortex-xsiam/cortex-xsiam-data-sources/vendor-specific-data-sources-and-connectors/docker/connect-docker-v2-compliant-container-registry)
* [GitLab Container Registry](../../configure-cortex-xsiam/cortex-xsiam-data-sources/vendor-specific-data-sources-and-connectors/gitlab/connect-gitlab-container-registry)
* [Harbor Registry](../../configure-cortex-xsiam/cortex-xsiam-data-sources/vendor-specific-data-sources-and-connectors/harbor/connect-harbor-registry)
* [JFrog Container Registry](../../configure-cortex-xsiam/cortex-xsiam-data-sources/vendor-specific-data-sources-and-connectors/jfrog/connect-jfrog-container-registry)
* [OpenShift container registry](https://app.gitbook.com/s/SqNMu2K0VWh4WXps5pCW/onboard-the-kubernetes-connector/openshift-container-registry)
* [Sonatype Nexus Repository Manager](../../configure-cortex-xsiam/cortex-xsiam-data-sources/vendor-specific-data-sources-and-connectors/sonatype-nexus/connect-sonatype-nexus-registry)
