# Troubleshoot Integrations

The **Troubleshooting Instances** dashboard provides you with insight into command execution errors. When troubleshooting integrations, we recommend the following steps:

* Use the **Test** button in the integration instance.
* Verify the integration settings. Check settings such as usernames, URLs, and passwords.
*   Download the debug log file and review its contents.

    In the following example, you receive a 401 unauthorized error code after testing the integration.

    ![integration-error.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-5ac4ef4721e7db1423f8d542a8a6746e3a39c3b5%2F30564624f5c0f4c137d8e31b79e9695974386a681e906c9e8f46a2c26097ee56.png?alt=media)

    Click **Run Test & Download Debug Log**, to download the debug file locally. You can verify what server the URL request is being forwarded to and any other reasons as to why you received this error code. The 401 unauthorized error code usually relates to invalid error credentials, expired tokens, or incorrect API settings.
* Enable verbose or debug-level logging on the integration.

{% hint style="info" %}
### Note

If an integration instance consistently encounters API rate limits when running on the tenant, consider configuring the instance to run on an engine to change the source of the outbound traffic.
{% endhint %}

If you are unable to fix the integration, contact Customer Support for further assistance.
