# Deploy and configure the Email Security module

To start using the Cortex Advanced Email Security module, configure the Microsoft O365 integration and then configure the module.

### Integrate Microsoft 365 with the Cortex Advanced Email Security Module

Deploy the Cortex Advanced Email Security module by configuring integration permissions and settings for Microsoft 365.

#### API Permissions and Setup

Deploy the Cortex Advanced Email Security module to collect data from your organization's email network and to generate issues when suspicious activity is detected. To use the Cortex Advanced Email Security module, activate it and then configure the integration permissions and add the email collector as a data source to Cortex XSIAM.

1. From **Settings** → **Cortex XSIAM License**, select **Cortex Advanced Email Security Module**, and click **Enable**.
2. Configure the Microsoft 365 email collector. For more information, see [Ingest logs and data from Microsoft 365](../../configure-cortex-xsiam/cortex-xsiam-data-sources/vendor-specific-data-sources-and-connectors/microsoft/microsoft-office-365-email/ingest-logs-and-data-from-microsoft-365).

### Configure Quick Actions

Define remediation actions to be run for the email security issues.

{% hint style="info" %}
### Notice

To configure a quick action, you must first create an application in Microsoft O365.
{% endhint %}

To configure each set of actions, do the following:

1.  Go to **Marketplace** and select the content pack that corresponds to the action(s) you want to add.

    | Quick action                             | Content pack              | Integration                                        |
    | ---------------------------------------- | ------------------------- | -------------------------------------------------- |
    | <p>Block Sender</p><p>Unblock Sender</p> | Microsoft Exchange Online | EWS Extension Online Powershell v3                 |
    | <p>Delete Email</p><p>Undelete Email</p> | Microsoft Exchange Online | O365 - Security And Compliance - Content Search v2 |
    | Send Email to Recipients - Office 365    | Microsoft Graph Mail      | Microsoft Graph Mail Single User                   |
2. Select the integration.
3. Select **Add Instance**.
4. Configure the connection using the credentials from Microsoft O365.
5. **Test** the connection, and then **Save**.

After you onboard your domains and configure the quick actions, Cortex XSIAM manages your protected domains in **Modules** → **Email Security** → **Email Security Configuration**.

### Configure the Cortex Advanced Email Security module

{% hint style="info" %}
### Notice

Requires the Advanced Email Security module.
{% endhint %}

Use the **Email Security** configuration page to manage your protected domains, allow and block lists, phishing email addresses, URL filtering, and your remediation actions. To access the page, navigate to **Modules** → **Email Security** → **Email Security Configuration**. You have the following options.

#### Protected Domains

View the domains you added to the collector for your organization.

#### Block List

View and manage indicators related to emails, including URLs, attachment file hashes, or sender email addresses that are flagged as malicious.

Right-click a row to edit, delete, disable, and copy each block list rule.

**How to add indicators you want to include in your block list:**

1. Click **Add**.
2. In **Create Block List Rule**, select the type - URL, Hash, or Email Address.
3. Type the indicator, add any comments you want, and click **Done**.

#### Allow List

All the trusted indicators related to emails, including URLs, attachment file hashes, and sender email addresses. These exclusions also appear in the **Issue Exclusions** list under **Exceptions Configuration**.

Right click a row to edit, delete, disable, and copy each allow list rule. In this section, you can add indicators you want to exclude from generating issues.

To add indicators:

1. Click **Add**.
2. In **Create Allow List Rule**, select the type : **URL**, **Email Sender**, or **Email Attachment**.
3. Type the indicator, add any comments you want, and click **Done**.

The new indicator is added to the **Allow List** and to the general **Issue Exclusions** tables.

{% hint style="info" %}
### Note

You can add email indicators to the Allow List also in **Exceptions Configuration** → **Issue Exclusions**. However, if you add multiple indicators in a rule using **Issue Exclusions** under **Exceptions Configuration**, you cannot edit the rule in the Email Security Allow List.
{% endhint %}

#### Phishing Email Address

Configure the email boxes for collecting the emails that users report as phishing. By default, the list includes the email address configured in your email provider for collecting reported phishing emails in your domain.

#### URL Filtering

Enable or disable analysis and identification of malicious URLs in emails.

### Remediation Actions

Configure the following settings for your remediation actions.

#### Warning Email Template

Add the **Sender Email** address, the **Subject**, and the **Body** for the email you want to send to users when a malicious or suspicious email is detected and automatically remediated. An email body template is provided that you can customize to your organization's needs. The template contains the details of the suspicious email, including the sender email address, subject, and the time the email was received.

#### Move to Folder Action

Select a folder to which suspicious emails will be moved. If a folder isn't configured, the email is moved to the default PANW Quarantined folder. If the PANW Quarantined folder doesn't exist, it is automatically created in the mailbox of the user.
