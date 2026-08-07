---
description: Secure, harden, and troubleshoot Docker images and containers.
---

# Docker image security

The project that contains the source Dockerfiles used to build the images and the accompanying files is fully open source and [available for review](https://github.com/demisto/dockerfiles). Cortex XSIAM uses the secure Docker Hub registry for its [Docker images](https://hub.docker.com/u/demisto). However, in an Engine environment, you can also use the [PANW registry](https://docs-cortex.paloaltonetworks.com/access?ft:baseId=UUID-4e9bb025-5de8-f83f-befc-b2e46a4a2dee) . You can view the Docker trust information for each image at the [image info branch](https://github.com/demisto/dockerfiles-info/blob/master/README.md).

| [![docker-trust.png](https://docs-cortex.paloaltonetworks.com/api/khub/maps/5CAbsl8idaK8R43ZLhoTOw/resources/xsgsgRQm7Uzm207TYqHECg-5CAbsl8idaK8R43ZLhoTOw/content?v=4621cc5b747355d0\&Ft-Calling-App=ft/turnkey-portal)](https://docs-cortex.paloaltonetworks.com/viewer/attachment/5CAbsl8idaK8R43ZLhoTOw/xsgsgRQm7Uzm207TYqHECg-5CAbsl8idaK8R43ZLhoTOw) |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

We automatically update our open-source Docker images and their accompanying dependencies (OS and Python). Examples of automatic updates can be viewed on [GitHub](https://github.com/demisto/dockerfiles/pull/700).

We maintain Docker image information, which includes information on Python packages, OS packages, and image metadata for all our Docker images. [Data image information](https://github.com/demisto/dockerfiles-info/blob/master/README.md) is updated nightly.

All of our images are continuously scanned using Cortex XSIAM for known and newly published vulnerabilities, in two scenarios:

* Every new image, and every new version of an image, are scanned before publishing to our public registries, as part of our CI/CD process.
* All existing images are continuously scanned to check whether new vulnerabilities have been published and now exist in those images.

We evaluate all critical/high findings and actively work to prevent and mitigate security vulnerabilities.

Cortex XSIAM ensures container images are fully patched and do not contain unnecessary packages. Patches and dependencies are applied automatically via our open-source Docker file build project.

**Response Prioritization**

We remediate any critical and high level vulnerabilities, irrespective of who found them. Issues may be discovered by external researchers, found during internal testing, encountered by customers or reported by other organizations and vendors.

Any vulnerability with a possible exploitation against our images would be responded to with utmost urgency. If we conclude that there is a risk for our customers we will issue an advisory with recommended actions and mitigations. Advisories are published at: [https://security.paloaltonetworks.com/](https://security.paloaltonetworks.com/).

In each version release (every 3 months,) we publish a new version of our content, which will use the latest and secure versions of our images.

**Troubleshooting**

* Purge old and unused images periodically.
* If you scanned the Docker images locally, and found some critical CVE’s - Make sure you use the latest version of the pack, as it should have the latest version of the image. In addition, purge the old and unused images with vulnerabilities.
