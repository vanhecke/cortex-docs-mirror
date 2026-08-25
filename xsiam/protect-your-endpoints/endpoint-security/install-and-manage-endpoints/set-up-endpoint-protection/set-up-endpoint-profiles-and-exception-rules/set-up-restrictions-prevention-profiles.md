---
description: >-
  Configure restrictions prevention profiles to control executable activity on
  endpoints in Cortex XSIAM.
---

# Set up restrictions prevention profiles

Restriction prevention profiles limit the locations from which executables can run on an endpoint.

<details>

<summary>Windows</summary>

By default, the Cortex XDR agent receives a default profile that contains a pre-defined configuration for each restriction capability. The default setting for each capability is shown in parentheses in the user interface. To fine-tune your restrictions prevention policy, you can override the default configuration of each capability as follows. For each setting that you override, clear the **Use Default** option, and select the setting of your choice.

* **Block:** Block file execution.
* **Notify:** Allow file execution, but notify the user that the file is attempting to run from a suspicious location. The Cortex XDR agent also reports the event to Cortex XSIAM.
* **Report:** Allow file execution, but report it to Cortex XSIAM.
* **Disabled:** Disable the module, and do not analyze or report execution attempts from restricted locations.

To customize the configuration for specific Cortex XDR agents, configure a new restrictions prevention profile and assign it to one or more policy rules. You can restrict files from running from specific local folders, or from removable media.

1. Add a new profile and define basic settings.
   1.  From Cortex XSIAM, select **Inventory** → **Endpoints** → **Policy Management** → **Prevention** → **Profiles**. Click **+Add Profile**, and select whether to create a new profile or import a profile from a file.

       <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>New profiles based on imported profiles are added, and do not replace existing ones.</p></div>
   2. Select the **Windows** platform, and **Restrictions** as the profile type.
   3. Click **Next**.
   4. For **Profile Name**, enter a unique name for the profile. The name can contain only letters, numbers, or spaces, and must be no more than 30 characters. The name will be visible from the list of profiles when you configure a policy rule.
   5. For **Description**, to provide additional context for the purpose or business reason for creating the profile, enter a profile description. For example, you might include a case identification number or a link to a help desk ticket.
2.  Configure **Executable Files** to restrict file execution to pre-defined locations.

    | Item        | Option                                                                 | More details                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
    | ----------- | ---------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | Action Mode | <ul><li>Block</li><li>Notify</li><li>Report</li><li>Disabled</li></ul> | <p>When the Cortex XDR agent detects execution of files from outside the pre-defined locations, it performs the configured action.</p><ul><li><p>To add files or folders to the <strong>Block List</strong>, click <strong>+Add</strong>, enter the path, and press Enter. To add more files or folders, click <strong>+Add</strong> again.</p><ul><li>You can use a wildcard to match a partial name for the folder and environment variables.</li><li>Use <strong><code>?</code></strong> to match any single character, or <em>to match any string of characters.</em></li><li><em>To match a folder, you must terminate the path with * to match all files in the folder (for example, <code>c:\temp</code></em>).</li></ul></li><li>To add files or folders to the <strong>Allow List</strong>, define a list on the <strong>Legacy Agent Exceptions</strong> page.</li></ul> |
3.  Configure **Network Location Files** to restrict access to all network locations except for explicitly trusted ones.

    | Item        | Option                                                                 | More details                                                                                                                                                                                                                                                                      |
    | ----------- | ---------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | Action Mode | <ul><li>Block</li><li>Notify</li><li>Report</li><li>Disabled</li></ul> | <p>When the Cortex XDR agent detects execution of files from network locations that are not trusted, it performs the configured action.</p><p>To add files or folders to the <strong>Allow List</strong>, define a list on the <strong>Legacy Agent Exceptions</strong> page.</p> |
4.  Configure **Removable Media Files** to restrict file execution launched from external drives that are attached to endpoints in your network.

    | Item        | Option                                                                 | More details                                                                                                                                                                                                                                              |
    | ----------- | ---------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | Action Mode | <ul><li>Block</li><li>Notify</li><li>Report</li><li>Disabled</li></ul> | <p>When the Cortex XDR agent detects execution of files from removable media,it performs the configured action.</p><p>To add files or folders to the <strong>Allow List</strong>, define a list on the <strong>Legacy Agent Exceptions</strong> page.</p> |
5.  Configure **Optical Drive Files** to restrict file execution launched from optical disc drives that are attached to endpoints in your network.

    | Item        | Option                                                                 | More details                                                                                                                                                                                                                                                     |
    | ----------- | ---------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | Action Mode | <ul><li>Block</li><li>Notify</li><li>Report</li><li>Disabled</li></ul> | <p>When the Cortex XDR agent detects execution of files from an optical disc drive, it performs the configured action.</p><p>To add files or folders to the <strong>Allow List</strong>, define a list on the <strong>Legacy Agent Exceptions</strong> page.</p> |
6.  Configure **Custom Prevention Rules**.

    | Item        | Option                                     | More details                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
    | ----------- | ------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | Action Mode | <ul><li>Enabled</li><li>Disabled</li></ul> | <p>When user-defined BIOC prevention rules are present in the system, you can enable them here. Ensure that the user-defined BIOC prevention rules that you want to enable only contain the following:</p><p><strong>Investigation types:</strong></p><ul><li>file_event</li><li>process_execution</li><li>remote_code_execution</li><li>network_event</li><li>windows_event_log</li><li>module_event</li></ul><p><strong>Subtypes:</strong></p><ul><li>file_event</li><li>network_event</li><li>registry_event</li><li>windows_event_log</li></ul><p>Other event subtypes are not supported here, and rules containing them will not be available for selection.</p><div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>Configure custom BIOC prevention rules here:</p><p><strong>Detection &#x26; Threat Intel</strong> → <strong>Detection Rules</strong> → <strong>BIOC</strong></p></div> |
7.  Configure **Custom Indicator Prevention Rules**.

    If you want to create custom indicator rules for prevention purposes, you enable their use here in the profile, and then create them in the **Detection & Threat Intel** area of Cortex XSIAM.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Notice</h3><p>A Threat Intel Management (TIM) license is required for this feature.</p></div>

    | Item        | Option                                     | More details                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
    | ----------- | ------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | Action Mode | <ul><li>Enabled</li><li>Disabled</li></ul> | <p>When user-defined prevention Indicator Rules are present in the system, you can enable them here.</p><div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>Configure this as follows:</p><p>1. Prepare this restriction profile first, make a note of its name for later, and set it to <strong>Enabled</strong>.</p><p>2. Prepare the prevention Indicator Rule (go to <strong>Detection &#x26; Threat Intel</strong> → <strong>Indicator Rules</strong>, ensuring to select <strong>Prevention</strong> when creating the rule), and while preparing it, map it to your restriction profile.</p></div> |
8. To save the profile, click **Create**.

What to do next

If you are ready to apply your new profile to endpoints, you do this by adding it to a policy rule. If you still need to define other profiles, you can do this later. During policy rule creation or editing, you select the endpoints to which to assign the policy. There are different ways of doing this, such as:

</details>

<details>

<summary>macOS</summary>

1. Add a new profile and define basic settings.
   1.  From Cortex XSIAM, select **Inventory** → **Endpoints** → **Policy Management** → **Prevention** → **Profiles**. Click **+Add Profile**, and select whether to create a new profile or import a profile from a file.

       <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>New profiles based on imported profiles are added, and do not replace existing ones.</p></div>
   2. Select the **macOS** platform, and **Restrictions** as the profile type.
   3. Click **Next**.
   4. For **Profile Name**, enter a unique name for the profile. The name can contain only letters, numbers, or spaces, and must be no more than 30 characters. The name will be visible from the list of profiles when you configure a policy rule.
   5. For **Description**, to provide additional context for the purpose or business reason for creating the profile, enter a profile description. For example, you might include a case identification number or a link to a help desk ticket.
2.  Configure **Custom Prevention Rules**.

    | Item        | Option                                     | More details                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
    | ----------- | ------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | Action Mode | <ul><li>Enabled</li><li>Disabled</li></ul> | <p>When user-defined BIOC prevention rules are present in the system, you can enable them here. Ensure that the user-defined BIOC prevention rules that you want to enable only contain the following:</p><p><strong>Investigation types:</strong></p><ul><li>file_event</li><li>process_execution</li><li>remote_code_execution</li><li>network_event</li><li>windows_event_log</li><li>module_event</li></ul><p><strong>Subtypes:</strong></p><ul><li>file_event</li><li>network_event</li><li>registry_event</li><li>windows_event_log</li></ul><p>Other event subtypes are not supported here, and rules containing them will not be available for selection.</p><div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>Configure custom BIOC prevention rules here:</p><p><strong>Detection &#x26; Threat Intel</strong> → <strong>Detection Rules</strong> → <strong>BIOC</strong></p></div> |
3.  Configure **Custom Indicator Prevention Rules**.

    If you want to create custom indicator rules for prevention purposes, you enable their use here in the profile, and then create them in the **Detection & Threat Intel** area of Cortex XSIAM.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Notice</h3><p>A Threat Intel Management (TIM) license is required for this feature.</p></div>

    | Item        | Option                                     | More details                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
    | ----------- | ------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | Action Mode | <ul><li>Enabled</li><li>Disabled</li></ul> | <p>When user-defined prevention Indicator Rules are present in the system, you can enable them here.</p><div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>Configure this as follows:</p><p>1. Prepare this restriction profile first, make a note of its name for later, and set it to <strong>Enabled</strong>.</p><p>2. Prepare the prevention Indicator Rule (go to <strong>Detection &#x26; Threat Intel</strong> → <strong>Indicator Rules</strong>, ensuring to select <strong>Prevention</strong> when creating the rule), and while preparing it, map it to your restriction profile.</p></div> |
4. To save the profile, click **Create**.

What to do next

If you are ready to apply your new profile to endpoints, you do this by adding it to a policy rule. If you still need to define other profiles, you can do this later. During policy rule creation or editing, you select the endpoints to which to assign the policy. There are different ways of doing this, such as:

</details>

<details>

<summary>Linux</summary>

1. Add a new profile and define basic settings.
   1.  From Cortex XSIAM, select **Inventory** → **Endpoints** → **Policy Management** → **Prevention** → **Profiles**. Click **+Add Profile**, and select whether to create a new profile or import a profile from a file.

       <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>New profiles based on imported profiles are added, and do not replace existing ones.</p></div>
   2. Select the **Linux** platform, and **Restrictions** as the profile type.
   3. Click **Next**.
   4. For **Profile Name**, enter a unique name for the profile. The name can contain only letters, numbers, or spaces, and must be no more than 30 characters. The name will be visible from the list of profiles when you configure a policy rule.
   5. For **Description**, to provide additional context for the purpose or business reason for creating the profile, enter a profile description. For example, you might include a case identification number or a link to a help desk ticket.
2.  Configure **Custom Prevention Rules**.

    | Item        | Option                                     | More details                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
    | ----------- | ------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | Action Mode | <ul><li>Enabled</li><li>Disabled</li></ul> | <p>When user-defined BIOC prevention rules are present in the system, you can enable them here. Ensure that the user-defined BIOC prevention rules that you want to enable only contain the following:</p><p><strong>Investigation types:</strong></p><ul><li>file_event</li><li>process_execution</li><li>remote_code_execution</li><li>network_event</li><li>windows_event_log</li><li>module_event</li></ul><p><strong>Subtypes:</strong></p><ul><li>file_event</li><li>network_event</li><li>registry_event</li><li>windows_event_log</li></ul><p>Other event subtypes are not supported here, and rules containing them will not be available for selection.</p><div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>Configure custom BIOC prevention rules here:</p><p><strong>Detection &#x26; Threat Intel</strong> → <strong>Detection Rules</strong> → <strong>BIOC</strong></p></div> |
3.  Configure **Custom Indicator Prevention Rules**.

    If you want to create custom indicator rules for prevention purposes, you enable their use here in the profile, and then create them in the **Detection & Threat Intel** area of Cortex XSIAM.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Notice</h3><p>A Threat Intel Management (TIM) license is required for this feature.</p></div>

    | Item        | Option                                     | More details                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
    | ----------- | ------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | Action Mode | <ul><li>Enabled</li><li>Disabled</li></ul> | <p>When user-defined prevention Indicator Rules are present in the system, you can enable them here.</p><div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>Configure this as follows:</p><p>1. Prepare this restriction profile first, make a note of its name for later, and set it to <strong>Enabled</strong>.</p><p>2. Prepare the prevention Indicator Rule (go to <strong>Detection &#x26; Threat Intel</strong> → <strong>Indicator Rules</strong>, ensuring to select <strong>Prevention</strong> when creating the rule), and while preparing it, map it to your restriction profile.</p></div> |
4. To save the profile, click **Create**.

What to do next

If you are ready to apply your new profile to endpoints, you do this by adding it to a policy rule. If you still need to define other profiles, you can do this later. During policy rule creation or editing, you select the endpoints to which to assign the policy. There are different ways of doing this, such as:

</details>

<details>

<summary>Serverless Function</summary>

The profile configuration for serverless functions provides runtime protection across processes, networking and file type resources in your cloud environment.

The configuration of each of the resources is based on allow/deny lists.

* Denied list (default): The system allows all resources to go through.
* Denied with exceptions: The system allows all resources to go through except those specified in the list.
* Allowed list : The system denies all resources to go through.
* Allowed with exceptions: The system denies all resources to go through except those specified in the list.

1. Add a new profile and define basic settings.
   1.  From Cortex XSIAM, select **Inventory** → **Endpoints** → **Policy Management** → **Prevention** → **Profiles**. Click **+Add Profile**, and select whether to create a new profile or import a profile from a file.

       <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>New profiles based on imported profiles are added, and do not replace existing ones.</p></div>
   2. Select the **Serverless Function** platform, and **Restrictions** as the profile type and then click **Next**.
   3. For **Profile Name**, enter a unique name for the profile. The name can contain only letters, numbers, or spaces, and must be no more than 30 characters. The name will be visible from the list of profiles when you configure a policy rule.
   4. For **Description**, to provide additional context for the purpose or business reason for creating the profile, enter a profile description.
2.  Configure **Restrictions**.

    | Item                    | Method                                | Setting details                                                          |
    | ----------------------- | ------------------------------------- | ------------------------------------------------------------------------ |
    | Process List            | <p>Allowed list</p><p>Denied list</p> | <p>Add process</p><p>**Example 137. **null<br><br></p>                   |
    | Networking              | <p>Allowed list</p><p>Denied list</p> |                                                                          |
    | Listing Ports           |                                       | <p>Add ports</p><p>**Example 138. **null<br><br></p>                     |
    | Outbound Internet Ports |                                       | <p>Add ports</p><p>**Example 139. **null<br><br></p>                     |
    | Outbound IPs            |                                       | <p>Add IPs</p><p>**Example 140. **null<br><br></p>                       |
    | Domains                 |                                       | <p>Add domains</p><p>**Example 141. **null<br><br></p>                   |
    | Files & Folders         | <p>Allowed list</p><p>Denied list</p> | <p>Add file paths and/or folders</p><p>**Example 142. **null<br><br></p> |

What to do next

If you are ready to apply your new profile to endpoints, you do this by adding it to a policy rule. If you still need to define other profiles, you can do this later. During policy rule creation or editing, you select the endpoints to which to assign the policy. There are different ways of doing this, such as:

</details>
