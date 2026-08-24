---
description: Apply collection profiles to Cortex XSIAM policies.
---

# Apply profiles to collection machine policies

Enable a Cortex XDR Collector profile by mapping it to a policy. Each policy that you create must apply to one or more collector machines or collector machine groups.

1. In Cortex XSIAM, do one of the following:
   * To create a policy from scratch on the XDR Collectors Policies page, select Settings → Configurations → XDR Collectors → Policies → +Add Policy.
   * To add a profile to an existing policy, select Settings → Configurations → XDR Collectors → Policies, then right-click the policy that you want to edit, and select Edit.
   * To create a new policy from a profile on the XDR Collectors Profiles page, select Settings → Configurations → XDR Collectors → Profiles, right-click the profile, and select Create a new policy rule using this profile.
2. Configure the General settings for the policy:
   1. Policy Name: Enter a unique name to identify the policy. The name can contain only letters, numbers, or spaces, and must be no more than 30 characters. The name that you enter here will be displayed when you view and configure policies.
   2. (Optional) Description: To provide additional context for the purpose or business reason for your policy, enter a policy description.
   3. Platform: Select the operating system of the XDR Collector machines that will use the policy.
   4. Select the profiles that you want to map to the policy. If you do not specify a profile, the XDR Collector uses the Default profile.
   5. Click Next.
3.  On the XDR Collectors Endpoints page, select the XDR Collectors (endpoints) or XDR Collector groups to which you want to map the policy. You can use the provided filters to find XDR Collectors listed on this page.

    Cortex XSIAM automatically applies a filter for the platform that you selected in the previous step. To change the platform, go Back to the general policy settings.
4. Click Next.
5.  On the Summary page, review the settings that you configured for the new policy.

    If everything is correct, click Done. Otherwise, click Back to make changes.
6.  (Optional) If necessary, change a policy's position relative to other policies in the table on the XDR Collectors Policies page.

    The XDR Collector evaluates policies from top to bottom. When an XDR Collector finds the first match, it applies that policy as the active policy. To change the policy order, click and drag the arrows in the Name cell of a policy to the desired location in the policy hierarchy.

### Additional XDR Collector policy management options

As needed, you can return to the XDR Collectors Policies page to manage your XDR Collector policies. To manage a specific policy, right-click anywhere in an XDR Collector policy row, and select the desired action. You cannot delete or disable default policies.

| Option                 | More details                                                                                                                                |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| Disable                | Disables the selected XDR Collector policy                                                                                                  |
| Delete                 | Deletes the selected XDR Collector policy                                                                                                   |
| View Policy Details    | Opens a new dialog box that displays details about the profiles mapped to the policy                                                        |
| Save As New            | Copies the existing policy with its current settings, so that you can make modifications, and save it as a new policy with a different name |
| Edit                   | Lets you edit the XDR Collector policy                                                                                                      |
| Copy text to clipboard | Copies the text from a specific field in the row of a XDR Collector policy                                                                  |
| Copy entire row        | Copies the text from the entire row of a XDR Collector policy                                                                               |
