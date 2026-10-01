---
description: >-
  Manage permission updates for your cloud instances following new feature
  releases or bug fixes in Cortex XSIAM.
---

# Update cloud permissions after Cortex XSIAM release updates

This topic provides guidance on how to manage permission updates for your cloud instances following new feature releases or bug fixes. It outlines how users are notified of required permission changes and provides step-by-step instructions for granting necessary permissions to ensure continued functionality and security.

{% hint style="info" %}
#### Prerequisites

* Ensure that the user account used to modify permissions has the necessary privileges within both the Cortex platform and your cloud environment, for example, AWS or Azure.
* You received a notification regarding a new version available that requires permission updates, or viewed an **Update Available** status in the **Data Sources & Integrations** page.
{% endhint %}

1. Navigate to the **Data Sources & Integrations** page.
2.  To identify instances requiring updates:

    1. For the relevant instance, locate the **Update Status** column.
    2. Filter or sort by this column to quickly identify instances marked as **Update Available**. The message on the page indicates the number of instances that need updating.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h4>Note</h4><p>Instances requiring updates will not change their connection status, for example, <strong>Connected</strong>, <strong>Warning</strong>, <strong>Error</strong>, <strong>Disabled</strong>, due to the pending permission update.</p></div>
3. Click the name of the instance that shows **Update Available**. The instance detail panel opens.
4. In the **Security Capabilities** section, an action button appears at the top. The button label depends on the state of the instance:
   * **Update Available**: the instance needs a new template deployed to add permissions, but has no current permission errors.
   * **Resolve Permission Issues**: the instance has permission errors but no pending update.
   * **Update and Resolve**: the instance both needs a new template and has current permission errors.
5. Click the button. In the **This instance should be updated** dialog box, follow the process appropriate for your deployment environment:
   * **Infrastructure as Code (IaC)**: Click **Download Template** to download the template. Execute the template in your cloud environment at the appropriate scope. See [Edit your onboarded CSP configuration](edit-your-onboarded-csp-configuration) for details on executing the template to update your cloud instance.
   * **Manual**: To resolve permission errors and update the cloud instance, manually make the required changes in your cloud environment at the appropriate scope. After applying the changes, confirm that the changes have been made by selecting **I've applied the change. Don't show this message again.**
6. Return to the **Data Sources & Integrations** page and verify that the updated status of the instance shows as up-to-date, or the update is in progress.
7.  Monitor the instance's health and functionality to confirm the changes have taken effect and the connector is operating as expected.

    If you encounter issues during the permission update process, check the generated health alerts for more specific details.
