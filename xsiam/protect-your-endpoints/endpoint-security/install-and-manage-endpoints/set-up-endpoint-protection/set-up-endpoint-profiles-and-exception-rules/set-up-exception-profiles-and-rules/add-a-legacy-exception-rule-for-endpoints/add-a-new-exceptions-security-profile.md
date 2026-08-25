---
description: Create Cortex XSIAM exceptions security profiles for legacy endpoint policies.
---

# Add a new exceptions security profile

You can configure exceptions that apply to specific groups of endpoints or you can add a global endpoint policy exception.

{% hint style="info" %}
### Important

Starting with version 1.3, Cortex XSIAM enables you to manage the exception security rules from a central location and easily apply them across multiple profiles in the **Legacy Agent Exceptions management** page.

To manage the exceptions from **Exception Configuration**, you must first migrate your existing exceptions configured via the exceptions security profiles.

To create new exception security profile rules using the **Legacy Agent Exceptions management** page, see [Add a legacy exception rule for endpoints](#UUID-5d26f4f4-345d-a0e7-ee52-d70e1a310a86).

If you don't migrate the legacy exceptions, you can continue to create exceptions as described below.
{% endhint %}

How to create an endpoint-specific exception

1. Add a new profile.
   1.  From Cortex XSIAM, select **Inventory** → **Endpoints** → **Policy Management** → **Prevention** → **Profiles** → **+Add Profile** and select whether to **Create New** or **Import from File** a new profile.

       <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>New imported profiles are added and not replaced.</p></div>
   2. Select the platform to which the profile applies and **Exceptions** as the profile type.
   3. Click **Next**.
2. Define the basic settings.
   1. Select a unique **Profile Name** to identify the profile. The name can contain only letters, numbers, or spaces, and must be no more than 30 characters. The name will be visible from the list of profiles when you configure a policy rule.
   2. To provide additional context for the purpose or business reason for creating the profile, specify a profile **Description**. For example, you might include a case identification number or a link to a help desk ticket.
3. Configure the exceptions profile.

<details>

<summary>Configure a process exception</summary>

1. Select the operating system.
2. Enter the process name.
3. Select the endpoint protection modules that allow the process to run.
   * Select **All** to apply the exception across all security modules.
   * Select **Disable Injection** to apply the exception across these exploit modules: APC Guard, CPL Execution Protection, DEP, DLL Hijacking Protection, DLL Security, EPM D02, Exception Heap Spray Check, Exception SysExist Check, Exploit Kit Fingerprinting Protection, Font Protection, Hot Patch Protection, JIT Mitigation, Library Preallocation, Memory Limit Heap Spray Check, Null Dereference Protection, Password Theft Protection, ROP Mitigation, SEH Protection, Shellcode Preallocation, and UASLR.
4. Click the adjacent arrow.
5. After adding all processes, select **Create**.

You can later edit these settings from the **Process Execution** profile.

</details>

<details>

<summary>Configure a support exception</summary>

1. Import the JSON file from Palo Alto Networks Support. Browse for it or drag it onto the page.
2. Click **Create**.

</details>

<details>

<summary>Configure module-specific exceptions for the selected profile platform</summary>

* **Behavioral Threat Protection Rule Exception**: Right-click a Behavioral Threat alert and select **Create alert exception**. Review the platform and rule name. Select **CGO hash**, **CGO signer**, **CGO process path**, or **CGO command arguments** as needed. Select **Profile** from **Exception Scope**, then click **Create**.
* **Digital Signer Exception**: Right-click a Digital Signer Restriction issue and select **Create issue exception**. Set **Exception Scope** to **Profile**, select the exception profile name, then click **Add**.
* **Java Deserialization Exception**: Right-click a benign Suspicious Input Deserialization issue and select **Create issue exception**. Set **Exception Scope** to **Profile**, select the exception profile name, then click **Add**.
* **Local File Threat Examination Exception**: Right-click a PHP file issue and select **Create issue exception**. Set **Exception Scope** to **Profile**, select the exception profile name, then click **Add**.
* **Gatekeeper Enhancement Exception**: Right-click the issue and select **Create issue exception**. Set **Exception Scope** to **Profile**, select the exception profile name, then click **Add**. This keeps enforcement active for other child processes.

At any point, click the **Generating Issue ID** to return to the issue that generated the exception. You cannot edit module-specific exceptions.

</details>

4.  Apply profiles to endpoints.

    To remove an exceptions profile, go to the **Profiles** page, right-click the profile, then select **Delete**.
