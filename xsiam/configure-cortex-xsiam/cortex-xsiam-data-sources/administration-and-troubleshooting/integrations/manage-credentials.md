# Manage credentials

Credentials simplify and compartmentalize administrative tasks, and enable you to save login information without exposing usernames, passwords, certificates, and SSH keys. You can reuse credentials across multiple systems, for example, when using the same administrator password across multiple endpoints.

{% hint style="warning" %}
### Prerequisite

To view the **Credentials** page and manage its content, your user role must have the following minimum permissions:

* **Integrations**: View
* **Data Sources**: View
* **External Issue Mapping**: View

Without these permissions, the **Credentials** page is hidden. Furthermore, if the **Credentials** permission itself is set to **None**, the page is hidden even if the above prerequisites are met. For more information, see [Credentials permissions](../../../../reference-and-developer-docs/role-based-access-control/configuration-permissions/credentials-permissions).

<br>
{% endhint %}

After you set up a credential, you can configure integration instances to use it instead of entering the name and password manually.

How to add credentials to an integration instance

1. Create the credential.
   1. Select **Settings** → **Configurations** → **Integrations** → **Credentials** → **New Credential**.
   2.  Add the following parameters:

       | Parameters      | Description                                                                                                                             |
       | --------------- | --------------------------------------------------------------------------------------------------------------------------------------- |
       | Credential Name | The name of the credential. You select this name when adding the credential to the integration instance.                                |
       | Username        | The username for the credential.                                                                                                        |
       | Workgroup       | The workgroup to associate this credential with. Relevant for third-party services, such as Active Directory, CyberArk, and HashiCorps. |
       | Password        | The password for the credential. For example, add the API Key when defining the API credential.                                         |
       | Certificate     | Certificate or SSH to use for the credential.                                                                                           |
   3. Save the credential.
2. Add the credential to the integration instance.
   1. Go to **Settings** → **Data Sources & Integrations** and select the integration.
   2. Click **Add Instance**.
   3.  Locate the relevant section and click **Switch to credentials**.

       If there is more than one credential, select the relevant credential.

       <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>If your user role has the <strong>Credentials</strong> permission set to <strong>None</strong>, the <strong>Switch to credentials</strong> option is hidden. Instead, the message <strong>Credentials are locked by admin</strong> is displayed, and you cannot reference stored secrets. This restriction applies to both data sources and unified connectors.</p></div>
   4. **Test** and **Save & Exit** the integration instance.

**Configure an external credentials vault**

Cortex XSIAM integrates with external credential vaults, which enables you to use them without hard coding or exposing the credentials. The credentials are not stored in Cortex XSIAM, but the integration fetches the credentials from the external vault when called. The credentials are passed to the relevant executed integrations as part of the integration parameters.

Sample credentials provider integrations:

* [CyberArk AIM v2](https://xsoar.pan.dev/docs/reference/integrations/cyber-ark-aim-v2)
* [HashiCorp Vault](https://xsoar.pan.dev/docs/reference/integrations/hashi-corp-vault)

After the integration is configured to fetch credentials, you can also use them in scripts and playbooks. To use these credentials in an integration, click **Switch to credentials** in an integration instance, and select the necessary credential from the drop-down menu.
