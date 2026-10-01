---
description: Use Salesforce data in Cortex XSIAM.
---

# Salesforce connector

Cortex XSIAM provides different methods for connecting to your Salesforce instance. Your choice depends on whether you need to ingest security event logs for monitoring, use the guided wizard setup for integrated services, or deploy specific legacy content packs for niche workflows.

### Product availability and licensing

Secure configurations, monitor identity risks, and automate threat remediation across your Salesforce environment.

This connector includes the following capabilities and sub-capabilities (if applicable):

* **Automation and Remediation:** Automate identity lifecycle management including user provisioning, updates, and access control. This capability is available with any active Cortex AgentiX, Cortex Cloud Runtime Security, Cortex XSIAM, Cortex XDR, or Cortex Cloud license.\
  Requires the following OAuth scopes:
  * Access and manage your data (`api`) Required for all standard operations on Cases, Users, Indicators, and Custom Objects (Fusion). Covers REST API queries and searches.
  * Access and manage your Chatter data (`chatter_api`) Required specifically for SOC playbooks that post comments and thread replies to the Salesforce Chatter feed.
  * Perform requests on your behalf at any time (`refresh_token`) Essential for background automation. Allows Cortex XSIAM to rotate expired tokens and stay connected 24/7 without manual login.
* **Data Security:** Scan and protect Salesforce data including files, attachments, and records. This capability is available with any active Cortex XSIAM, Cortex Cloud Posture Security, Cortex Cloud Runtime Security, or Cortex Data Security license.
* **Identity Posture:** Maintain visibility and control over Salesforce identities, including users, groups, roles, and granular permissions. This capability is available with any active Cortex XSIAM, Cortex Cloud Posture Security, Cortex Cloud Runtime Security, or Cortex Data Security license.
* **Security Posture:** Detect, monitor and alert on settings of your SaaS application. This capability is available with any active Cortex XSIAM or Cortex Cloud Posture Security license.
  * **saas-posture-config-remediation:** Help remediate the misconfigured security settings of your SaaS application. This sub-capability is available with any active Cortex XSIAM or Cortex Cloud Posture Security license.

### Supported capabilities and sub-capabilities

Cortex XSIAM can ingest identity metadata, login history, audit trails, and security monitoring events from Salesforce via capabilities to help you secure user identities, monitor for real-time threats, and automate issue response. To simplify setup, a wizard enables you to select specific capabilities based on your operational needs. The wizard then automatically identifies and provisions the underlying sub-capabilities required to support these capabilities.

The following table outlines the capabilities currently available in the wizard and the sub-capaibilities it uses for each.

<table><thead><tr><th width="163">Capability</th><th width="165">Functionality</th><th width="245">Use Cases</th><th>Underlying Sub-capabilities Used</th></tr></thead><tbody><tr><td>Automation and Remediation</td><td>Execute automations and commands across Salesforce and its Identity Access Management (IAM) services.<br><br></td><td><ul><li>Real-time investigations</li><li>Automated playbook workflows</li><li>Employee lifecycle management</li></ul></td><td><ul><li>Salesforce (CRM services)</li><li>Salesforce IAM (Identity operations)</li></ul></td></tr><tr><td>Data Security</td><td>Scan and protect Salesforce data including files, attachments, and records.</td><td><ul><li>Sensitive data discovery: Identify PII, PCI, or PHI stored in Salesforce objects or Chatter messages to ensure compliance.</li><li>Malware prevention: Scan file uploads and attachments in real time to prevent malicious content from spreading within the CRM.</li><li>Exposure monitoring: Detect and alert on data shared with external collaborators or inadvertently made public.</li></ul></td><td>N/A</td></tr><tr><td>Identity Posture</td><td>Maintain visibility and control over SaaS-based identities, including users, groups, roles, and granular permissions.</td><td></td><td>N/A</td></tr><tr><td>Security Posture</td><td>Detect, monitor, and alert on your cloud application settings.</td><td><ul><li>Identifying misconfigurations</li><li>Security health monitoring</li><li>Compliance and risk visibility</li></ul></td><td>N/A</td></tr></tbody></table>

{% hint style="warning" %}
### **Prerequisite**

**Cortex XSIAM tenant**

* RBAC permissions: Requires View/Edit permissions for Log Collections, Data Sources, and Integrations (under **Configurations & Data Collections**).
* Content packs: Ensure the Salesforce and Base content packs are installed or updated to the latest version.
* Store credentials (optional): You can configure vault credentials to securely manage and reuse authentication data across multiple sub-capabilities under **Settings** → **Configurations** → **Integrations** → **Credentials**.
* Gateway permissions: Requires Account Admin or Instance Administrator permissions for configuring egress settings in the Cortex Gateway to allow communication with your Salesforce Domain URL.

**Salesforce environment**

Salesforce requirements depend on the capabilities you use:

<details>

<summary>Security Posture capability prerequisites</summary>

Requires the following permissions enabled in Salesforce:

* API Enabled
* Enable Chatter
* Modify All Data
* Query All Files
*   View All Users, Manage Users, and Monitor Login History: These can be added by creating/modifying a Permission Set or enabling them via the user's Profile.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3><strong>Note</strong></h3><p>Manage Users is only required if User Sharing is not enabled.</p></div>
* (Optional) Ensure the region-specific IP addresses are added to the allowed list on your NGFW or Prisma Access tenant.

</details>

<details>

<summary>Automation and Remediation capability prerequisites</summary>

Requires the Full System Admin permission enabled in Salesforce.

</details>
{% endhint %}

### How to configure the Salesforce connector

Perform the following procedures in the order that they appear, below.

#### Task 1. Configure the external client app in Salesforce

Salesforce is deprecating "Connected Apps"; it is recommended to use an external client app.

1. On the **Setup** page, search for **App Manager** and click **New External Client App**.
2. Provide a name (such as `panw_cortex_integration`), and your email address (used to retrieve the **Consumer Key** and **Consumer Secret**).
3. Under **API** (enable OAuth settings), select **Enable OAuth**.
4.  Enter the following **Callback URLs** on separate lines (replacing `{tenant external URL}` with your tenant name):

    * `https://{your-salesforce-domain}.my.salesforce.com/services/oauth2/callback`
    * `https://{tenant external URL}.paloaltonetworks.com/configuration/data-sources`

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>Do not use the generic <code>login.salesforce.com</code> address if your organization uses a custom Salesforce domain or a sandbox. You must replace <code>{your-salesforce-domain}</code> with your specific Salesforce instance name (for example, <code>acme-inc.my.salesforce.com</code>) to ensure proper authentication redirection.</p></div>
5. Select these **OAuth Scopes**:
   * `Access and manage your Chatter data (chatter_api)`
   * `Manage user data via APIs (api)`
   * `Perform requests at any time (refresh_token, offline_access)`
6. Enable only these checkboxes after **OAuth Scopes**: **Require Secret for Web Server Flow**, **Require Secret for Refresh Token Flow**, and **Enable Client Credentials Flow**. For more information, see [Salesforce Client Credentials Flow](https://help.salesforce.com/s/articleView?id=xcloud.remoteaccess_oauth_client_credentials_flow.htm\&type=5).
7. Click **Save**, then **Continue**.

#### Task 2. Retrieve credentials in Salesforce

**Consumer Key** will be used for `client_id`, and **Consumer Secret** will be used for `client_secret` in OAuth 2.0.

1. On the **Setup** page, search for **External Client App Manager**.
2. Find your application (the one that you defined for Cortex XSIAM), click the arrow button in the last column, and select **Edit Settings**.
3. In the **OAuth Settings** area, click **Consumer Key and Secret**.
4. Go back to the Salesforce **Verify Your Identity** page, paste the code received via email in the `Verification Code` box, and click **Verify**. One of the following will happen:
   * The **Consumer Key** and **Consumer Secret** will be sent to the email address that you configured earlier for the Cortex XSIAM External Client App.
   * On the Salesforce **External Client App Name** page, the **Consumer Details** area will display the **Consumer Key** and **Consumer Secret**, and you will be able to copy them from here when required in the following procedures.

#### Task 3. Configure the refresh token expiration policy in Salesforce

1. On the **Setup** page, search for **External Client App Manager**.
2. Find your application (the one that you defined for Cortex XSIAM), click the arrow button in the last column, and select **Edit Policies**.
3. In the **OAuth Policies** area:
   * Under **Plugin Policies - Permitted Users**, select **All users can self-authorize**.
   * Set the refresh token policy to **Expire refresh token if not used for specific time** (recommended). For example, select this option and set it for 7 days.

#### Task 4. Configure the OAuth 2.0 application for Salesforce

Configure OAuth 2.0 authentication to call the Salesforce API with one of the following flows:

* Client credentials flow: For more information, see [Configure an External Client App OAuth 2.0 Client Credentials Flow](https://help.salesforce.com/s/articleView?id=xcloud.remoteaccess_oauth_client_credentials_flow.htm\&type=5).
* Web server flow: For more information, see [OAuth 2.0 Web Server Flow](https://help.salesforce.com/s/articleView?id=xcloud.remoteaccess_oauth_web_server_flow.htm\&language=en_US\&type=5).

#### Task 5. Configure egress in Cortex Gateway

An Account Admin or Instance Administrator must configure egress settings in the Cortex Gateway to allow communication with your Salesforce Domain URL. For more information, see [Egress Configurations](https://docs-cortex.paloaltonetworks.com/r/Cortex/Cortex-Gateway-Administrator-Guide/Egress-configurations).

1. Log in to the Cortex Gateway with Account Admin or Instance Administrator permissions and click **Permission Management**.
2. From the side menu, select **Egress Configurations**.
3. In the **TENANT** dropdown, select the tenant where you are configuring the Salesforce integration.
4. Click **+Path** to initiate a new path request.
5. In the **New Path** dialog box, configure the following:
   * **Requester**: In the dropdown, select the requester from the list of users.
   * **Flow**: In the dropdown, select the appropriate data service option for a generic webhook/host out (or Salesforce if it is explicitly listed).
   *   **Path**: Enter the domain name or host of your Salesforce instance (for example, your-company.my.salesforce.com).

       <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>Do not include https:// or trailing slashes.</p></div>
6. Click **Add** to create the path. Once the status of the path shows as Approved in the **Egress Configuration** table, Cortex XSIAM can successfully authenticate and execute commands against your Salesforce environment.

#### Task 6. Configure the Salesforce connector in Cortex XSIAM

1. Navigate to **Settings** → **Data Sources & Integrations**.
2. Click **+ Add new**.
3. In the **Add Data Sources or Integrations** page, search for Salesforce.
4. Under **Recommended**, hover over the new Salesforce integration and click **Add Instance** to launch the Salesforce wizard.\
   The new Salesforce connector has the description: Salesforce CRM services for identity management, automation, remediation and SaaS Posture Security.
5. Set up your Salesforce instance by following the wizard steps in the following tabs.

<details>

<summary>Capabilities tab</summary>

Configure the following.

1. **Instance name**: Enter a unique name for your instance.
2. **Select capabilities**: Choose the required instance functionality:
   *   **Data Security**: Scan and protect Salesforce data including files, attachments, and records.

       <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>To select this capability, you must first select the Identity Posture capability.</p></div>
   * **Automation and Remediation**: Enables executing commands, running automated workflows, managing cases, updating Chatter, or executing access control and CRUD (create, read, update, delete) operations across Salesforce and its IAM services. This capability includes commands for automation and remediation.
   * **Security Posture**: Detect, monitor and alert on settings of your SaaS application. It includes a sub-capability to remediate misconfigured security settings.
   * **Identity Posture**: Maintain visibility and control over SaaS-based identities, including users, groups, roles, and granular permissions.
3. Click Next.

</details>

<details>

<summary>Connection tab</summary>

Enter credentials to securely authorize the connection.

1. **Domain URL**: Copy the URL from your browser's address bar while logged into Salesforce and paste it into this field. This must be identical to the domain URL defined in the Cortex Gateway egress configuration in the **Path** field as explained in Task 5. If you did not configure egress in Cortex Gateway, you will get an error during verification. You can continue with instance configuration without verifying and set up egress at a later point.
2. Click **Apply**.

{% hint style="warning" %}
### **Important**

You cannot proceed with the authentication configuration until you provide a domain URL and click **Apply**. When you click **Apply**, the instance is connected to a unique URL in Salesforce, and it cannot be changed. To change it, you need to exit the wizard and start over.
{% endhint %}

3. Select **Recommended** or **Advanced**.
   * **Recommended** applies the suggested authentication method for all capabilities.
   * **Advanced** enables configuring unique credentials for each capability individually.
4. Authenticate using OAuth 2.0 client credentials, vault credentials, or OAuth 2.0 web server.
   * For more information about the client credentials flow, see [Configure an External Client App OAuth 2.0 Client Credentials Flow](https://help.salesforce.com/s/articleView?id=xcloud.remoteaccess_oauth_client_credentials_flow.htm\&type=5).
   * To use stored credentials, click **Select credentials** and choose a saved **Credential** from the drop down.
   * For more information about the web server flow, see [OAuth 2.0 Web Server Flow](https://help.salesforce.com/s/articleView?id=xcloud.remoteaccess_oauth_web_server_flow.htm\&language=en_US\&type=5).
5. Click **Done** for each authentication method.

</details>

<details>

<summary>Configuration tab</summary>

Configure the following.

* **Under Automation and remediation:**
  * **Allow creating users, Allow updating users, Allow enabling users, and Allow disabling users**: Toggle these specific user permissions on or off. You can also choose to automatically create a user if they are not found during an update command.
  * **Default Locale SID Key**: Choose how dates, times, numbers, and currency are displayed throughout the application based on your geographic region. The default is en\_US.
  * **Default Email Encoding Key**: Sets the standard used to display characters in your outgoing emails. This ensures that special characters, symbols, and different languages appear correctly for your recipients. The default is ISO-8859-1.
  * **Integration Log Level**: Possible values are Off (default), Debug, and Verbose.
* **Under Security Posture:**
  * **Sync Interval**: Defines how often the system checks your cloud environment for security risks, misconfigurations, and compliance updates. More frequent syncs may impact API rate limits. The default is every 15 minutes.
  * **Application Tag**: Assigns a category to your cloud resources based on their operational purpose. This helps you filter security alerts and apply different compliance policies to specific environments. The default is None.

</details>

<details>

<summary>Summary tab</summary>

A confirmation message shows that your Salesforce instance is successfully connected, with a list of relevant capabilities and sub capabilities statuses.

Once you confirm the summary details, click **Save instance**.

</details>

#### **Task 7. (Optional) Edit or test existing Salesforce instance settings in Cortex XSIAM**

You can edit and test an existing instance after a successful initial connection between Salesforce and Cortex XSIAM. Do this by clicking **Test**.

{% hint style="warning" %}
**Important**

If a “connected application” for Cortex XSIAM data collection already exists, there is no obligation to migrate to an “External Client App” - but as Connected Applications are deprecated by Salesforce, it is recommended to migrate.
{% endhint %}
