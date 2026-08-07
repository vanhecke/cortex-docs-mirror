---
description: >-
  Scenarios that occur when managing content with a remote repository in Cortex
  XSIAM.
---

# Remote repository troubleshooting

**Pointing to a non-empty branch when enabling a tenant**

If you configure a tenant to use a remote repository, you have two options:

* Overwrite all content in the tenant with content from the repository.
*   Overwrite all content in the remote repository with content from the tenant.&#x20;

    To overwrite the remote repository with content from the tenant, you must use an empty branch. If the branch is not empty, you will get an error message prompting you to select an empty branch. Alternatively, you can select the first option and overwrite all content in the tenant with the content from the remote repository.

**Switching between remote repository types**

If you switch between built-in and private remote repository types, you get a warning that switching between repository types may result in the loss of all version history.

To keep your content history, select Existing content on your tenant to overwrite all content in the remote repository with content from your tenant.
