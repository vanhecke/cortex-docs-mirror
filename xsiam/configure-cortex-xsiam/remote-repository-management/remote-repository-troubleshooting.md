---
description: >-
  Troubleshoot Cortex XSIAM remote repository issues, including non-empty
  branches and switching between built-in and private repositories.
---

# Remote repository troubleshooting

Use this guide to resolve common Cortex XSIAM remote repository configuration issues. These issues include non-empty Git branches and repository type changes.

### Resolve non-empty branch errors when enabling a tenant

When you configure a Cortex XSIAM tenant to use a remote repository, choose one of these options:

* Overwrite all content in the tenant with content from the repository.
* Overwrite all content in the remote repository with content from the tenant.

To overwrite the remote repository with tenant content, use an empty branch. A non-empty branch produces an error that prompts you to select an empty branch. Alternatively, overwrite tenant content with content from the remote repository.

### Switch between built-in and private remote repositories

Switching between built-in and private remote repository types can remove version history. Cortex XSIAM displays a warning before you make the change.

To retain content history, select **Existing content on your tenant**. This overwrites remote repository content with tenant content.
