---
description: Development environments and tools to help develop various content items.
---

# Content development environments

Cortex XSIAM offers several tools for development including an IDE in the UI, a Visual Studio Code extension, and the Demisto SDK Python library.

When creating complex integrations and scripts, we recommend using a full development environment. Options include:

* [Local development environment](content-development-environments/set-up-a-local-development-environment)
* [GitHub Codespace environment](content-development-environments/set-up-a-github-codespace-environment)
* [Containerized development environment](content-development-environments/set-up-a-containerized-development-environment)

#### Content developed in the UI

The following content items should be developed from within the Cortex XSIAM UI:

* Playbooks
* Alert fields, layouts, and rules
* Indicator fields, types and layouts
* Classifiers and Mappers
* Widgets
* Dashboards

Once the resource is developed in the Cortex XSIAM UI, you can download it using `demisto-sdk download -i "$NAME_OF_RESOURCE"` or export it from the UI.

#### Content developed in Visual Studio Code

For integrations and scripts, when creating content to use within your instance of Cortex XSIAM or for contribution as a community supported content pack, the UI may be sufficient. For more complex development needs, or if you plan on contributing content as a partner supported content pack or a modification to partner supported content, we recommend Visual Studio Code. The [Visual Studio Code extension](content-development-environments/visual-studio-code-extension) should be installed locally, and can be used with a regular local development environment or GitHub Codespace. It is included by default with the containerized development environment. We also recommend installing [Demisto SDK](https://github.com/iKettles/palo-alto-networks-gitbook/tree/iain/import/document/preview/860019/README.md#UUID-94ba506f-b779-272f-c04a-9d5d83e0e1ea) to upload, download, and run code on Cortex XSIAM directly from your operating system shell. Demisto SDK is included by default with the containerized development environment.

{% hint style="info" %}
### Note

To develop content for contribution as a partner-supported content pack, or to submit modifications to partner-supported content packs, you are required to set up a full development environment.
{% endhint %}
