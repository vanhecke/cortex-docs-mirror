---
description: >-
  Learn how to onboard and manage registry scanning programatically with APIs
  for Cortex XSIAM.
---

# Manage registry scanning with APIs

### 1. Onboarding and managing connectors

#### Third-party integrations

Use the [registry onboarding API](https://cortex-docs.paloaltonetworks.com/xsiam-api/cloud-workload-protection/registry-onboarding) endpoints to onboard or manage third-party integrations such as JFrog Artifactory, Docker Hub, Harbor, Sonatype Nexus, GitLab Container Registry, Docker V2, and OpenShift.

Cortex provides dedicated, schema-validated Public API endpoints:

<table><thead><tr><th width="188.8876953125">Action</th><th>Endpoint</th></tr></thead><tbody><tr><td>Create connector</td><td><code>POST /public_api/v1/cwp/registry_onboarding/instances</code></td></tr><tr><td>Get connector details</td><td><code>GET /public_api/v1/cwp/registry_onboarding/instances/{connectorID}</code></td></tr><tr><td>Update connector</td><td><code>PUT /public_api/v1/cwp/registry_onboarding/instances/{connectorID}</code></td></tr><tr><td>Delete connector</td><td><code>DELETE /public_api/v1/cwp/registry_onboarding/instances/{connectorID}</code></td></tr></tbody></table>

#### Managed cloud registries

(AWS ECR, GCP Artifact Registry/GCR, Azure ACR, OCI)

No individual registry-creation endpoints. These are onboarded at the cloud account level through [Cloud Account Onboarding APIs](https://cortex-docs.paloaltonetworks.com/xsiam-api/cloud-onboarding/cloud-onboarding-overview).

### 2. Triggering scans

There is no public API to trigger on-demand registry scans. Registry scanning is automated and event-driven.

### 3. Retrieving scan results

There's no single dedicated `/public_api/.../registry/scan-results` endpoint. Because results are normalized into the Unified Asset Inventory, findings, and issues, you retrieve them as follows:

a. [Asset SBOM API](https://cortex-docs.paloaltonetworks.com/xsiam-api/cloud-workload-protection/sbom)

* `GET /public_api/v1/assets/{assetId}/sbom` — returns the SBOM (packages, versions, licenses) for a scanned container image asset.

b. [XQL Query API](https://cortex-docs.paloaltonetworks.com/xsiam-api/cortex-platform/xql-query)

* `POST /public_api/v1/xql/start_xql_query` and `POST /public_api/v1/xql/get_query_results`
  * Image assets & metadata: query the `asset_inventory` dataset filtered on the container image asset type to inspect tags, digests, repositories, registries, and scan timestamps.
  * Vulnerabilities, secrets, malware: query the `findings` dataset by asset ID, for finding types such as `VULNERABILITY`, `MALWARE`, `SECRET`, or compliance checks.

c. [Platform Issues API](https://cortex-docs.paloaltonetworks.com/xsiam-api/issues-apis/issues-apis-overview)

* `POST /public_api/v1/issue/search/` and `GET /public_api/v1/issue/<issue_id>/` — retrieves security issues generated when scanned images trigger CWP security policies.
