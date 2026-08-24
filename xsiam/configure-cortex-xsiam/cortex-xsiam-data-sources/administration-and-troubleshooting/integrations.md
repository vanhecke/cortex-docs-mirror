---
description: Manage and configure integrations in Cortex XSIAM.
---

# Integrations

Integrations are mechanisms through which Cortex XSIAM connects and communicates with other products. These integrations can be executed through REST APIs, webhooks, and other techniques. Integrations enable you to orchestrate and automate SOC operations.

### **Integrations installed from a content pack**

Integrations are included in content packs, which you download and install from Marketplace (go to Settings → **Configurations** → **Marketplace**). After you download and install a content pack that includes an integration, you need to configure the integration by adding an instance. You can have multiple instances of an integration, for example, to connect to different environments. Additionally, if you are an MSSP and have multiple tenants, you could configure a separate instance for each tenant.

{% hint style="info" %}
* Some integrations can be downloaded directly without having to initially download a content pack from Marketplace. For more information, see Define data sources.
* In addition to content packs that you install from Marketplace, related content packs are automatically downloaded when you adopt playbooks or edit tasks that require content items such as scripts or integrations.
{% endhint %}

Cortex XSIAM comes out-of-the-box with integrations to help you onboard, such as:

*   Mail Sender

    Sends email notifications to users.
*   Generic Export Indicators Service

    Provides an endpoint with a list of indicators as a service for the system indicators. For more information about how to set up the integration, see [Export indicators](../../../detect-investigate-and-respond-to-threats/threat-management/threat-intel-management/indicator-configuration/export-indicators).
*   Palo Alto Networks WildFire Reports

    Generates a Palo Alto Networks WildFire PDF report. For more information, see [Palo Alto Networks WildFire Reports](https://xsoar.pan.dev/docs/reference/integrations/wild-fire-reports).
*   Rasterize

    Converts URLs, PDF files, and emails to an image file or PDF file. For more information, see [Rasterize](https://xsoar.pan.dev/docs/reference/integrations/rasterize).

### **Create an integration in Cortex XSIAM**

You can create an integration by adding parameters, commands, arguments, and outputs as well as writing the necessary integration code. You should have a working Cortex XSIAM tenant and programming experience with Python.

1. Navigate to the Settings → **Data Sources & Integrations** page and click **+ Add New**.
2. In the **Add Data Source or Integrations** page, click **Create Integration** and select either **Import File** or **Create from Template**.
3. If you select **Import File** drag and drop or browse to and select the relevant integration file. If you select **Create from Template**, provide the integration code and settings.

For more information about how to create an integration, including an example, see [Create an Integration](https://xsoar.pan.dev/docs/tutorials/tut-integration-ui).

### **Configure an integration in Cortex XSIAM**

From the **Data Sources & Integrations** page, you can perform actions on an integration such as:

| Action                                                                                    | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| ----------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Add an instance                                                                           | <p>Configure an integration instance to connect and communicate with other products. For more information, see <a href="integrations/add-an-integration-instance">Add an integration instance</a>.</p><p>After configuring the instance, you can also enable/disable the integration instance, copy the instance, and view the integration fetch history.</p>                                                                                                                                                        |
| View the integration's source                                                             | <p>View the integration settings and source code.</p><p>To access this functionality, select an integration from the table and click <img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-11a463bf2b5bf9ecd6322e37719ff9691e5de3f2%2F49fda5fb33e5f524c041a0abe1ea1868806777860768af3c9ef5a3a2716a9c39.png?alt=media" alt="three-dots-dark.png">.</p>                                                                           |
| Edit the integration's source code                                                        | <p>Edit the integration settings and source code. For more information about editing the integration's source code, see <a href="https://xsoar.pan.dev/docs/tutorials/tut-integration-ui">Create an Integration</a>.</p><div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>If the integration was installed from a content pack, you need to duplicate the integration before editing.</p></div>                                                      |
| Duplicate the integration                                                                 | <p>If you want to change the source code, and settings, or download the integration, you need to duplicate the integration.</p><p>To access this functionality, select an integration from the table and click <img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-11a463bf2b5bf9ecd6322e37719ff9691e5de3f2%2F49fda5fb33e5f524c041a0abe1ea1868806777860768af3c9ef5a3a2716a9c39.png?alt=media" alt="three-dots-dark.png">.</p> |
| Show integration commands                                                                 | <p>Show the commands the integration contains.</p><p>To access this functionality, select an integration from the table and click <img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-11a463bf2b5bf9ecd6322e37719ff9691e5de3f2%2F49fda5fb33e5f524c041a0abe1ea1868806777860768af3c9ef5a3a2716a9c39.png?alt=media" alt="three-dots-dark.png">.</p>                                                                              |
| Delete an integration instance                                                            | Although you cannot delete an integration installed from a content pack (unless a duplicate), you can delete an integration instance by either right-clicking an instance and either selecting **Delete** or by right-clicking an instance and selecting **Settings** and then deleting from the settings configuration pane.                                                                                                                                                                                        |
| Set an integration instance to run always whenever the integration is called or on demand | For each integration instance, you have the option of setting the instance to be used only **On Demand**, when it is specified with the `using` argument in a playbook or the CLI. By default, the settings is **Always** and the integration instance is used whenever the integration is called.                                                                                                                                                                                                                   |

### **Use integration commands in Cortex XSIAM**

The command line interface (CLI) enables you to run system commands, integration commands, scripts, etc from the Cases War Room, Issues War Room, or Playground CLI. The CLI auto-complete feature allows you to find relevant commands, scripts, and arguments.

Cortex XSIAM uses the "`!`" such as `!ad-create-user username=[name of user]`

Under each integration, you can view a list of commands.

{% hint style="info" %}
### Note

Integration commands are only available when the integration instance is enabled. Some commands depend on a successful connection between Cortex XSIAM and third-party integrations.
{% endhint %}

You can run the CLI commands in the Playground or in a case/issue War Room. The Playground is a non-production environment where you can safely develop and test automation scripts, APIs, commands, etc. It is an investigation area that is not connected to a live (active) investigation.

When running the command, the results are returned in the War Room or Playground and also in a JSON format in Context Data.

{% hint style="info" %}
### Tip

In the Playground, you can clear the context data, if needed, which deletes everything in the Playground context data, but does not affect the actual issue or case. To clear the context, run `!DeleteContext all=yes'` from the CLI or click **Clear Context Data** while viewing the context data.
{% endhint %}
