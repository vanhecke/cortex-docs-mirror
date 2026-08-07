---
description: Install, configure, secure, and troubleshoot Docker for Cortex XSIAM engines.
---

# Docker

Docker is a software framework for building, running, and managing containers.

{% hint style="info" %}
This section is relevant when installing an engine.
{% endhint %}

Cortex XSIAM maintains Docker images in the [Cortex Docker Hub organization](https://hub.docker.com/u/demisto/).

Each Python or PowerShell integration specifies its Docker image in its YAML file. If the image is not local, the engine downloads it from Docker Hub or the Cortex Container Registry. The integration then runs inside that container. For background information, see the [Docker documentation](https://docs.docker.com/) and [Using Docker](https://xsoar.pan.dev/docs/integrations/docker).

{% hint style="info" %}
You can [download Docker images](https://xsoar.pan.dev/docs/reference/articles/download-packs-offline) with their content packs for offline installation.
{% endhint %}
