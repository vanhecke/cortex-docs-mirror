---
description: "Create a content pack for\_Cortex XSIAM with custom content for issues."
---

# Issues

When you create a content pack for Cortex XSIAM, you can include custom issue layouts, fields, and rules, as well as classifiers and mappers. Develop these items in the UI.

* Issue fields - Issue fields support mapping, correlation rules, custom issue layouts, and display in the Issues table.
* Issue layouts - Custom issue layouts let you choose fields and buttons for issues that meet specific rules. You can include custom and out-of-the-box issue fields.
* Issue layout rules - Issue layouts are applied according to layout rules. You can assign a custom layout based on the issue source, including issues from your integration.
* Classifiers - Classification determines the issue type created for events from a specific integration. Create and define the classifier in the integration.
* Mappers - Map fields from your third-party integration to issue fields.

After these items have been created and finalized, we can add them to the content pack by downloading them using `demisto-sdk download -i "Resource Name" -o Packs/MyPack`. The SDK will put the content item in the correct subfolder per the type of resource it is.
