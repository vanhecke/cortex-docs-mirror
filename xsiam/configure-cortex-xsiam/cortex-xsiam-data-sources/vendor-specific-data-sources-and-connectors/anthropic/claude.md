---
description: Use Claude with Cortex XSIAM.
---

# Claude

The capabilities and sub-capabilities listed for this connector are available with any active Cortex XSIAM, Cortex Cloud Posture Security, Cortex Cloud Runtime Security, or Cortex Data Security license.

Scan sensitive content and monitor data security risks for Anthropic Claude AI.

This connector includes the following capabilities and sub-capabilities (if applicable):

* **Data Security:** Scan and protect data across the Claude service
* **Identity Posture:** Maintain visibility and control over Claude identities, including users, groups, roles, and granular permissions.

To configure this connector, follow these steps:

### Prerequisite

Sign in to your Anthropic Claude organization as a **Primary Owner** and generate a Compliance API key.

#### 1. Enable Compliance API access

1. Sign in to the Claude.ai console using an account with **Primary Owner** privileges.
2. Click **Settings** in the left navigation menu, and select **Organization Settings**.
3. In **Organization Settings**, select the **API** tab.
4. Verify that the **Compliance API** option is enabled.

#### 2. Generate a Compliance API key and assign scopes

1. On the **API** tab, locate the **Keys** section and click **+ Create Key**.
2. Enter a name for the API key.
3. Under **Scopes**, select the required scopes:
   * `read:compliance_activities` — Read compliance activity logs and audit trails.
   * `read:compliance_org_data` — Read organization-level workspace metadata and asset definitions.
   * `read:compliance_user_data` — Read user identities, group memberships, and role assignments.
   * `delete:compliance_user_data` — Allow programmatic purging or remediation of non-compliant sensitive data.
4. Click **Create**.
5.  Copy the generated API key and store it securely.

    **Note:** You cannot retrieve the API key after you close the dialog.

### How to configure the Claude connector

#### Task 1. Select services

1. In Cortex Cloud, navigate to **Settings** → **Data Sources & Integrations**.
2. Click **+ Add new**.
3. On the **Add Data Source** page, search for **Claude**, hover over it, and click **Add**.

In the Configuration Wizard, configure the following settings.

#### Capabilities tab

1. Enter a unique name for the new connector instance.
2.  Under **Select Capabilities**, select the capabilities that you want to enable.

    * **Data Security** to enable scanning and inventory collection across the selected repositories.
    * **Identity Posture** to maintain visibility and control over SaaS-based identities, including users, groups, roles, and granular permissions.

    **Note:** **Identity Posture** is automatically enabled when **Data Security** is selected and cannot be disabled during setup. Identity Posture is required for user and group validation and cross-tenant exposure analysis.
3. Click **Next**.

#### Connection tab

1. On the **Connection** tab, select your preferred authentication method:
   * **Recommended:** Paste your Anthropic Claude organization API key into the API key field.
   * **Advanced:** Select this option if your enterprise security policy requires separate authentication tokens for **Data Security** and **Identity Posture**.
2. Click **Test** to validate the connection.
3. If the connection is successful, the wizard displays a green **Verified** status indicator.
4. Click **Save** to save the connection settings.
5. Click **Next**.

#### Summary tab

1. On the **Summary** tab, verify that each selected capability displays a **Connected** status.
2. If validation succeeds, the wizard displays a **Verification Success** message.
3. Click **Create Instance** to create the Claude connector.

#### Task 2. Post verification

After configuration is complete, verify asset discovery and data security findings.

#### 1. Verify discovered assets

1. Go to **Inventory** > **All Assets**.
2. Filter the asset list by setting **Provider** to **Anthropic**.
3. Verify that Cortex discovers the following supported asset types:
   * **Claude Personal Workspace:** Individual user conversations, chat history, and associated metadata.
   * **Claude Project:** Shared workspaces, custom prompt instructions, and attached knowledge repositories.

#### 2. Verify policy findings

1. Select an asset to open the details panel.
2. Click the **Overview** tab to review general properties and total finding counts.
3. Click **Findings** or navigate to the **Compliance** tabs to review detected security findings, such as:
   * Personally identifiable information (PII)
   * API keys or secrets
   * Credit card numbers
   * Unauthorized data sharing

