---
description: >-
  The integration description file includes use case and integration instance
  configuration information.
---

# Integration description file

The integration description file provides the supported integration use cases, and helps Cortex XSIAM users to easily configure an integration instance.

{% hint style="info" %}
### Tip

* Give as much information as you think the user needs to succeed, including permission levels, credentials, and keys.
* If there are permissions required on the integration level, list them.
* If commands have separate permissions, mention that, but document the required permission on the command level.
* [Images](../../documentation/images-in-documentation) can be added to integration description files.
{% endhint %}

**Common use cases**

* How to get credentials
* How to get API Key/secret
* How to get Application ID

**Integration description file location**

The description file should be placed with the rest of the integration's files.

For example, if the pack name is **HelloWorld** and the integration name is also **HelloWorld**, the description file path is:

`~/.../content/Packs/HelloWorld/Integrations/HelloWorld/HelloWorld_description.md`

**Integration description file data**

The description file contains details on how to configure an integration instance, together with the relevant details needed from the product that are important for configuration. The file content can include troubleshooting tips and advanced details for different configuration cases.

{% hint style="info" %}
### Note

This file should not be confused with the integration [README file](../../documentation/readme-files-for-content-entities).
{% endhint %}

**Example**

This is the content of the HelloWorld\_description.md file:

```programlisting
## Hello World
- This section explains how to configure the instance of HelloWorld in Cortex XSIAM.
- You can use the following API Key: `43ea9b2d-4998-43a6-ae91-aba62a26868c`
```

**Integration description file content in the UI**

The content of the description file is displayed in the **Help** tab next to the integration instance settings configurations:

![](https://4088726609-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FurXrv6qkJRLbdhMdvPIU%2Fuploads%2Fgit-blob-c6dc8377f3edd4fbfcf73898bf3b4f0c372ca5de%2F0cf9fa4aeb344ff16c1140a822d883c210e5e01608de246e158d169278d8fce9.png?alt=media)

**Support level header YML metadata key**

The `supportlevelheader` key can be set to one of the following values to set the support level header in the content description:

* `xsoar` - The description specifies that Palo Alto Networks supports this integration.
* `partner` - The description specifies that this integration is partner supported and list the partner's contact information.
* `community` - The description specifies that this integration is community supported or lists the pack's author.

**Set the support level header YML metadata key**

To set the key, open the YAML file for the integration in the same folder where the description file is located and add the `supportlevelheader` key with of the supported values listed above.

If the key is not set in the integration YAML, the support level header is set to the `support` key in the `pack_metadata.json` file.
