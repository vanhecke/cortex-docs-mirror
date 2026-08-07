# Add a global endpoint policy exception

Learn how to define and manage global endpoint policy exceptions in Cortex XSIAM.

As an alternative to endpoint-specific policy exceptions, define global exceptions for all endpoints. On the **Global Exceptions** page, manage organization-wide exceptions for every platform. Profiles assigned to targets outside your user scope are locked.

{% hint style="info" %}
### Important

* Starting with version 1.3, manage Global Endpoint Policy exceptions centrally in **Legacy Agent Exceptions management**.
* Before managing prevention profile exceptions from **Exception Configuration**, migrate existing global exceptions.
* Migrated rules appear in **Settings** → **Exception Configurations** → **Legacy Agent Exceptions**. See [Exception configuration](../exception-configuration).
* To create new global endpoint policy exceptions from **Legacy Agent Exceptions**, see [Add a legacy exception rule for endpoints]().
* If you do not migrate legacy exceptions, continue adding exceptions as described here.
{% endhint %}

<details>

<summary>Add a global process exception</summary>

Configure centralized exception rules for Cortex XSIAM protection and prevention actions.

1. Go to **Inventory** → **Endpoints** → **Policy Management** → **Policy Exceptions**.
2. Select **Process exceptions**.
   1. Select the operating system.
   2. Enter the process name.
   3. Select the endpoint protection modules that allow the process to run. The list contains modules relevant to the selected operating system.
      * Select **All** to apply the exception to all security modules.
      * Select **Disable Injection** to apply the exception to all exploit security modules.
   4. Click the adjacent arrow to add the exception.
3. After adding all exceptions, select **Save**.

The new exception applies across all rules and policies. To edit or delete it, select the exception and click the relevant icon.

</details>

<details>

<summary>Add a global support exception</summary>

Configure centralized support exception rules for Cortex XSIAM protection and prevention actions.

1. Go to **Inventory** → **Endpoints** → **Prevention** → **Global Exceptions**.
2. Select **Support Exceptions**. Import the JSON file from Palo Alto Networks Support. Browse for the file or drag and drop it onto the page.
3. Click **Save**.

The new support exception applies across all rules and policies.

</details>

<details>

<summary>Add a behavioral threat protection rule exception</summary>

Create a global exception for a Behavioral Threat rule you want to allow.

1. Right-click the BTP issue and select **Create issue exception**.
2. Review the platform and rule name. Choose the required exception criteria.
3. From **Scope**, select **Global** or select a profile.
4. Click **Create**.

The exception applies across all rules and policies. Click **Generating Issue ID** to return to the source issue. To delete an exception, select it and click **X**.

{% hint style="info" %}
You cannot edit global exceptions generated from BTP security events.
{% endhint %}

</details>

<details>

<summary>Use recommended exception criteria</summary>

Use Cortex XSIAM recommended fields to define precise exception criteria.

1.  Select the criterion that triggered the alert.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>Select only one criterion per alert. Create a separate exception for each additional criterion.</p></div>
2. Select one or more displayed parameters relevant to the exception.
3.  Edit an editable parameter if needed.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>Select at least one parameter. Cortex XSIAM validates entered values. Wildcards are supported, but use specific values. Some parameters are not editable.</p></div>

</details>

<details>

<summary>Use CGO information</summary>

Select CGO attributes to define general exception criteria:

1. **CGO hash**: Causality Group Owner (CGO) hash value.
2. **CGO signer**: CGO signer entity. Available for Windows and Mac only.
3. **CGO process path**: Directory path of the CGO process.
4. **CGO command arguments**: Available only with **CGO process path** and Cortex XDR Agent 7.5 or later. Check each relevant command argument's full path in quotation marks. Edit displayed paths if needed.

</details>

<details>

<summary>Add a global credential gathering protection exception</summary>

1. Right-click the Credential Gathering Protection issue and select **Create issue exception**.
2. Review the platform and module name. Select the required options:
   1. **CGO hash**: Causality Group Owner hash value.
   2. **CGO signer**: CGO signer entity. Available for Windows and Mac only.
   3. **CGO process path**: Directory path of the CGO process.
   4. **CGO command arguments**: Available only with **CGO process path**. Check each relevant command argument's full path in quotation marks. Edit displayed paths if needed.
   5. From **Exception Scope**, select **Global**.
3. Click **Create**.

The exception applies across all rules and policies. Click **Generating Issue ID** to return to the source issue. To delete it, select it and click **X**.

{% hint style="info" %}
You cannot edit global exceptions generated from Credential Gathering Protection security events.
{% endhint %}

</details>

<details>

<summary>Add a global anti webshell protection exception</summary>

1. Right-click the Anti Webshell Protection issue and select **Create issue exception**.
2. Review the platform and module name. Select **CGO hash**, **CGO signer**, **CGO process path**, or **CGO command arguments** as needed. Command arguments require **CGO process path** and Cortex XDR Agent 7.5 or later. From **Exception Scope**, select **Global**.
3. Click **Create**.

The exception applies across all rules and policies. Click **Generating Issue ID** to return to the source issue. To delete it, select it and click **X**.

{% hint style="info" %}
You cannot edit global exceptions generated from Anti Webshell Protection security events.
{% endhint %}

</details>

<details>

<summary>Add a global local analysis rules exception</summary>

1. Right-click the Local Analysis issue and select **Create issue exception**.
2. Review the platform and rule name, then set **Exception Scope** to **Global**.
3. Click **Add**.

The exception applies across all rules and policies. It allows every rule that triggered the issue. You cannot allow only selected rules. Click **Generating Issue ID** to return to the source issue. To delete the exception, select it and click **X**. You cannot edit exceptions generated from local analysis security events.

</details>

<details>

<summary>Review advanced analysis exceptions</summary>

Advanced Analysis provides secondary validation for exploit protection issues. Cortex XSIAM analyzes issue data sent by the Cortex XDR agent. When an issue is benign, Cortex XSIAM can automatically create exceptions and distribute updated policy to endpoints.

Enable automatic Advanced Analysis exceptions in **Settings** → **Configurations** → **General** → **Agent Configurations**.

Each exception displays the platform, exception name, and relevant issue ID. Click **Generating Issue ID** to view issue details.

</details>

<details>

<summary>Add a global digital signer exception</summary>

1. Right-click a trusted Digital Signer Restriction issue and select **Create issue exception**.
2. Review the platform, signer, and issue ID. Set **Exception Scope** to **Global**.
3. Click **Add**.

The exception applies across all rules and policies. Click **Generating Issue ID** to return to the source issue. To delete it, select it and click **X**. You cannot edit exceptions generated from Digital Signer Restriction security events.

</details>

<details>

<summary>Add a global Java deserialization exception</summary>

1. Right-click a Suspicious Input Desensitization issue and select **Create issue exception**.
2. Review the platform, process, Java executable, and issue ID. Set **Exception Scope** to **Global**.
3. Click **Add**.

The exception applies across all rules and policies. Click **Generating Issue ID** to return to the source issue. To delete it, select it and click **X**. You cannot edit exceptions generated from Java deserialization security events.

</details>

<details>

<summary>Add a global local file threat examination exception</summary>

1. Right-click a Local Threat Detected issue for a PHP file and select **Create issue exception**.
2. Review the process, path, and hash. Set **Exception Scope** to **Global**.
3. Click **Add**.

The PHP file exception applies across all rules and policies. Click **Generating Issue ID** to return to the source issue. To delete it, select it and click **X**. You cannot edit exceptions generated from local file threat examination security events.

</details>

<details>

<summary>Add a global Gatekeeper Enhancement exception</summary>

Create an exception for a specific bundle or source-child combination. Gatekeeper Enhancement remains active for other child processes.

1. Right-click the Gatekeeper Enhancement issue and select **Create issue exception**.
2. Review the platform, source process, target process, and issue ID. Set **Exception Scope** to **Global**.
3. Click **Add**.

The source and target process exception applies across all rules and policies. Click **Generating Issue ID** to return to the source issue. To delete it, select it and click **X**. You cannot edit exceptions generated from Gatekeeper Enhancement security events.

</details>

<details>

<summary>Import and export exceptions</summary>

Select **+ Import/Export** to export the exceptions list or import exceptions from a file.

{% hint style="info" %}
Exported files use Base64 encoding and cannot be edited.
{% endhint %}

</details>
