---
description: List of Oracle Cloud Infrastructure provider permissions for Cortex XSIAM.
---

# Oracle Cloud Infrastructure (OCI) provider permissions

The following reference tables are organized by security module and then the list of the CSP permissions being requested.

* [Discovery engine](#discovery-engine)
* [ADS](#ads)
* [Registry scan](#registry-scan)

### Discovery engine

"Discovery Engine" read only access. Grants read-only access to OCI tenancy and resources.

### ADS

| Permission                                                                                                                                                                                 | Module | Scope                                                                        | Purpose                                                                       |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------ | ---------------------------------------------------------------------------- | ----------------------------------------------------------------------------- |
| Admit group CortexOutpostGroup of tenancy CortexOutpost to use volumes in tenancy                                                                                                          | ADS    | In tenancy                                                                   | Allow creation of backups from volumes                                        |
| Admit group CortexOutpostGroup of tenancy CortexOutpost to use key-delegate in tenancy                                                                                                     | ADS    | In tenancy                                                                   | Re-encrypt backups during copy/restore operations                             |
| Admit group CortexOutpostGroup of tenancy CortexOutpost to associate keys in tenancy with volumes in tenancy CortexOutpost                                                                 | ADS    | Volumes in tenancy                                                           | Associate encryption keys with volumes during backup/restore                  |
| Admit group CortexOutpostGroup of tenancy CortexOutpost to use tag-namespaces in tenancy                                                                                                   | ADS    | In tenancy                                                                   | Enable tagging for permission scoping, resource tracking, and cost visibility |
| Admit group CortexOutpostGroup of tenancy CortexOutpost to manage boot-volume-backups in tenancy where request.operation != 'DeleteBootVolumeBackup'                                       | ADS    | Excludes delete                                                              | Allow full management of boot volume backups except deletion                  |
| Admit group CortexOutpostGroup of tenancy CortexOutpost to manage boot-volume-backups in tenancy where target.resource.tag.cortex\_m-o-lcaas\_id.panw\_capability = 'cortex-scan-platform' | ADS    | Only boot-volume-backups tagged with panw\_capability = cortex-scan-platform | Restrict deletion to Cortex scan-related resources only                       |
| Admit group CortexOutpostGroup of tenancy CortexOutpost to read all-resources in tenancy                                                                                                   | ADS    | In tenancy                                                                   | Read-only access to all resources                                             |

### Registry scan

#### Dynamic group permissions

| Permission                                                          | Scope                    | Purpose                                                  |
| ------------------------------------------------------------------- | ------------------------ | -------------------------------------------------------- |
| Allow dynamic-group registry-scan to manage buckets in tenancy      | Tag-scoped (project\_id) | Manage Object Storage buckets for scan artifacts/results |
| Allow dynamic-group registry-scan to manage objects in tenancy      | Tag-scoped (project\_id) | Upload/download image layers, manifests, and reports     |
| Allow dynamic-group registry-scan to read secret-bundles in tenancy | Tag-scoped (project\_id) | Retrieve registry credentials from OCI Vault             |
| Endorse dynamic-group registry-scan to read repos in any-tenancy    | Cross-tenancy            | Allow cross-tenancy image pulls for scans                |

#### Inherited base permissions for registry scanning

| Permission                                                                   | Scope                    | Purpose                                             |
| ---------------------------------------------------------------------------- | ------------------------ | --------------------------------------------------- |
| Allow any-user to manage buckets in tenancy                                  | Tag-scoped (project\_id) | Create/manage buckets for scan data                 |
| Allow any-user to manage objects in tenancy                                  | Tag-scoped (project\_id) | Read/write objects (artifacts, logs, results)       |
| Allow any-user to use keys in tenancy                                        | Tag-scoped (project\_id) | Decrypt secrets for registry access                 |
| Allow any-user to manage secret-versions in tenancy                          | Tag-scoped (project\_id) | Rotate credentials and manage secret versions       |
| Allow any-user to manage secrets in tenancy                                  | Tag-scoped (project\_id) | Create/update secrets for scanners                  |
| Allow any-user to manage secret-family in tenancy                            | Tag-scoped (project\_id) | Broader secret-management rights                    |
| Allow any-user to manage vaults in tenancy                                   | Tag-scoped (project\_id) | Create/administer Vaults for key and secret storage |
| Allow any-user to inspect tag-family in tenancy                              | Global                   | Discover tag namespaces/definitions                 |
| Allow any-user to use tag-family (namespace=cortex\_cloud, managed\_by=PANW) | Restricted               | Restrict tag usage to Palo Alto-managed groups      |
| Endorse any-group to use tag-namespaces in any-tenancy                       | Cross-tenancy            | Allow tag namespace usage across tenancies          |

***
