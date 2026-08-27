---
description: Define integration settings for a sample integration in Cortex XSIAM.
---

# Define sample integration settings

When you click on the **BYOI** button, you enter the Cortex XSIAM IDE. By default, the HelloWorld integration template is loaded. You will replace it with the integration you create. This includes replacing the existing HelloWorld integration settings with new settings, and deleting unused parameters or arguments.

Behind the scenes, the settings you enter are saved in a YAML file which you can export and import. To learn more about Cortex XSIAM integration YAML files, see [Integration metadata YAML file](../components/integration-metadata-yaml-file).

As an example, we are going to create an English to Yoda translator, which translates normal English into the way Yoda, the Star Wars character, speaks. This is a simple integration that lets us explore important aspects of integration development. With our integration, we can try calling an API, parsing data, and posting it to the War Room. We will use the Yoda-Speak translate API available at [FunTranslations](https://funtranslations.com/api/yoda).

### Configure basic sample integration settings

In the **Basic** section, name the integration, add a description, choose a category, and set several additional options.

1. Under **Integration Name**, replace the `HelloWorld` integration name with `Yoda Speak`.
2. Under **Description**, include basic information about the integration, common troubleshooting steps, and any required setup instructions. For the purposes of this tutorial, enter `Creating an Integration, we are`.
3. Under **Category**, select `Utilities`. See the full list of available [categories](../../readme/design/design-best-practices).
4.  Add a **Logo**. You can drag and drop the logo or click the box to open a file browser to select a file for upload.

    Logo requirements:

    * No larger than 10KB
    * Transparent background
    * PNG format

![xsiam-yoda-speak-basic-settings.png](https://4088726609-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FurXrv6qkJRLbdhMdvPIU%2Fuploads%2Fgit-blob-c389d979719c59d723c822190f75a4042f0b64f4%2Fee2c97eb8f35a28e98e7460aac8dce2c761f3822fb8fe9105824c9976ebdbbdc.png?alt=media)

{% hint style="info" %}
**Note**

The **Fetches alerts** checkbox tells Cortex XSIAM that the integration runs periodically to ingest events and create alerts in Cortex XSIAM. Our Yoda Speak integration does not need to fetch incidents, so make sure this checkbox is empty. While we don’t need this feature for our Yoda Speak integration, fetching alerts is an essential part of many integrations. There are additional options available here including external schema support and long running integration, but these are less commonly used.
{% endhint %}

### Configure sample integration parameters

This section lets you set parameters that can be used across all commands in the integration. Some common parameters include the API key used for communicating with the product, your username, whether to use proxy, etc.

For the Yoda Speak integration, we want to include the API key and proxy settings, and to allow for insecure requests. We also include a URL parameter, which tells the integration where to send requests. For each parameter, we include a display name that tells the user what the value is used for.

#### Add the API key parameter

Enter the following values for the **apikey** parameter.

* **Parameter name**: apikey
* **Type**: Authentication
* **Mandatory**: unselected
* **Display password**: API Key

For the Yoda Speak integration, the free service does not require an API key and allows up to 60 API calls a day with up to 5 calls an hour. If you require more API calls, FunTranslations offers a paid service that you can access with an API key. In this case, we provide the option for users with a paid subscription to enter their API key, but we don’t make it mandatory. The Authentication parameter type enables using Cortex XSIAM's built-in credential management system to save and use the API key, and ensures that the API key is not displayed to the user and is not stored in logs.

{% hint style="info" %}
**Note**

Many integrations that connect to third-party services require an API key for authentication, which is sent with every request to the third party service. Since it’s used by every command that performs an API call, we add it as a global parameter and not an argument.
{% endhint %}

![xsiam-yoda-speak-apikey.png](https://4088726609-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FurXrv6qkJRLbdhMdvPIU%2Fuploads%2Fgit-blob-603c15db9e73c8c5a2927c9f6e5af5467ecbec2c%2F614cacfd1a6c403018fd6f120ef9a8cce59b66124e6cd368d8aca0d11d1b7f5d.png?alt=media)

#### Add the API URL parameter

Enter the following values for the **url** parameter.

* **Parameter name**: url
* **Type**: Short Text
* **Mandatory**: selected
* **Initial value**: https://api.funtranslations.com/translate/
* **Display name**: API URL

{% hint style="info" %}
**Note**

In some cases, the URL parameter may be used for third-party services that enable connecting to more than one server, such as servers in different geographic regions (https://login.example.de or https://login.example.com).
{% endhint %}

![xsiam-yoda-speak-url.png](https://4088726609-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FurXrv6qkJRLbdhMdvPIU%2Fuploads%2Fgit-blob-08bdbae194f851bb4f8158ea865fe08675bf7a65%2Ff2f38e1e23de0736f3145ef28ae8cc641a5dc2b02abf9e39ee3c687167917292.png?alt=media)

#### Add the insecure connection parameter

Enter the following values for the **insecure** parameter.

* **Parameter name**: insecure
* **Type**: Boolean
* **Initial value**: false
* **Display name**: Trust any certificate (not secure)

When Trust any certificate is set to true, the integration ignores TLS/SSL certificate validation errors. Use this to test connection issues or connect to a service while ignoring SSL certificate validity. We do not recommend setting this option to true in a production environment.

![xsiam-yoda-speak-insecure.png](https://4088726609-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FurXrv6qkJRLbdhMdvPIU%2Fuploads%2Fgit-blob-a9b466a0ea6d98ae4c6780fa778b2c931c88a2ec%2F081ebfe068b3d7c26cf61684c6778dd0bf60303350e39a1b3bfdec0c675c8683.png?alt=media)

#### Add the proxy parameter

Enter the following values for the **proxy** parameter:

* **Parameter name**: proxy
* **Type**: Boolean
* **Initial value**: false
* **Display name**: Use system proxy settings

When Use system proxy settings is set to true, the integration runs using the proxy server (HTTP or HTTPS) defined in the server configuration. In most cases, a proxy is not required.

![xsiam-yoda-speak-proxy.png](https://4088726609-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FurXrv6qkJRLbdhMdvPIU%2Fuploads%2Fgit-blob-1d105c1c79d562a6ea9ee37400b3dfe1c180d92e%2F92fcd03628ca4338911db26478fef9aeb4b6a14c08209d16b3bfa23a43a1244b.png?alt=media)

### Configure the sample integration command

Create commands to be used in the integration code.

1. Click **+Add command**.
2. Enter the following values.
   * **Command name**: yoda-speak-translate
   * **Description**: Translates a text from English to Yoda

![xsiam-yoda-speak-command.png](https://4088726609-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FurXrv6qkJRLbdhMdvPIU%2Fuploads%2Fgit-blob-0621b68c8c25cef71ea9103e2df88fa02dd4e087%2F7f4e6a0a2ced34c6b5c1e851e6be285b8d822e648a951a1097289d4b8b0a2f87.png?alt=media)

{% hint style="info" %}
**Note**

Command names should follow “brand-function” name formatting convention. For example, VirusTotal has a command named `vt-comments-add` that adds a comment to a scan. An exception to this rule is when creating commands that enrich indicators, the commands should be named according to the indicator, for example `!ip` and `!domain`. This naming convention allows commands from multiple integrations to be run together to enrich an indicator. For example, running `!ip ip=8.8.8.8` can trigger multiple integrations that gather information about the IP address. For more information, see [Generic reputation commands](../../developing/generic-commands#UUID-67e7ba5f-4f74-45fc-8f2f-1aab4ef77100).
{% endhint %}

#### Add the translation command argument

Arguments are parameters specific to a command.

In this example, we want to translate English text to Yoda-style text, so we add an argument called `text`. Users can provide a different text string on every call. The argument is mandatory, since the command can’t run if there’s nothing to translate.

![xsiam-yoda-speak-argument.png](https://4088726609-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FurXrv6qkJRLbdhMdvPIU%2Fuploads%2Fgit-blob-6ac4a74f8ff7a4e367a90d467f736257aef889df%2F1c04bd5ea7adaa0860804ac5a6bac0725fdea6d2493f68d9772903556daea6da.png?alt=media)

#### Configure translation command outputs

In Cortex XSIAM, the context is a JSON object that is created for each incident and stores results from integration commands and automation scripts. Context is important because it enables you to add information to an incident and run playbooks and integrations utilizing that information.

To write the translation to context, add an output to the `yoda-speak-translate` command.

1. Click **+Add output**.
2. Enter the following values.
   *   **Context Path**: YodaSpeak.TheForce.Translation

       The naming convention for the context path is `Brandname.Object.Property`.
   * **Description**: Translation this is
   * **Type**: String

![xsiam-yoda-speak-outputs.png](https://4088726609-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FurXrv6qkJRLbdhMdvPIU%2Fuploads%2Fgit-blob-74f525527c249b7e1ec0c2f7a290e32c978284e1%2Fe947f9db6862c01452e9fc3e21db72256d623e486a127c92b6b1dcdec88abc47.png?alt=media)
