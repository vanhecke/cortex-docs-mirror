---
description: "Create a content pack for\_Cortex XSIAM with custom content for alerts."
---

# Alerts

When you create a content pack for Cortex XSIAM, you can include custom alert layouts, fields, and rules, as well as a classifiers and mappers. These should all be developed in the UI.

* Alert fields - Alert fields can be used for mapping, correlation rules, custom alert layouts, and for display in the Alerts table.
* Alert layouts - Custom alert layouts let you choose the fields and buttons that are displayed for alerts that meet specific rules. You can create custom alert layouts that include both custom and out-of-the-box alert fields.
* Alert layout rules - Alert layouts are applied to alerts according to layout rules. You can assign a custom alert layout based on the alert source, such as a specific layout for alerts generated from your integration.
* Classifiers - Classification determines the type of alert that is created for events ingested from a specific integration. You create a classifier and define that classifier in an integration.
* Mappers - You can map the fields from your third party integration to the alert fields.

After these items have been created and finalized, we can add them to the content pack by downloading them using `demisto-sdk download -i "Resource Name" -o Packs/MyPack`. The SDK will put the content item in the correct subfolder per the type of resource it is.
