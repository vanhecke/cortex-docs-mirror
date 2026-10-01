---
description: >-
  Add built-in controls or create and manage custom controls for custom
  standards in Cortex XSIAM.
---

# Use a built-in or custom control

When using custom standards, you can use built-in controls or create custom controls and then associate them with detection rules.

## Add a built-in control to a custom standard

Cortex XSIAM provides built-in controls that cannot be edited or deleted. When you edit or create a custom standard you can add the built-in controls.

## Create a custom control to use in a custom standard

You can create a new control that is tailored to your own business needs, standards, and organizational policies to use in a custom standard.

1. In the **Controls** catalog, click **+ Create Control**.
2. Define control metadata, including:
   * A single category
   * A single sub category (optional)
   * Control name
   * ​Description (optional)
   * One or more custom standards to associate the control with
3. Click **Create**.
4. Assign a custom detection rule to the control. See [Associate a custom control to a detection rule](#associate-a-custom-control-to-a-detection-rule).

## Associate a custom control to a detection rule

You can associate custom compliance controls with workload security and cloud security rules. This tailors compliance checks to your organization’s needs. You can associate controls while creating custom rules. You can also associate them when editing custom or built-in rules.

{% hint style="info" %}
**NOTE**

Custom rules can only be associated with custom compliance controls.
{% endhint %}

The following table summarizes supported rule associations.

| Rule type                | Built-in rules                                                                    | Custom rules                                                                                |
| ------------------------ | --------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| **Cloud workload rules** | Not applicable.                                                                   | Associate custom compliance controls while creating or editing custom cloud workload rules. |
| **Cloud security rules** | Associate custom compliance controls while editing built-in cloud security rules. | Associate custom compliance controls while creating or editing custom cloud security rules. |

{% hint style="info" %}
**NOTE**

You can associate custom compliance controls only with `ConfigIdentityAI` cloud security rules.
{% endhint %}

To associate a custom compliance control:

1. Go to **Posture Management → Rules & Policies → Rules → Cloud Workload** or **Cloud Security**.
2. Create a custom policy, or edit an existing rule.
3. In **Overview → Compliance Controls**, click **Add**.
4. Select one or more custom compliance controls.
5. Click **Assign**.
6. Save your changes.

## Manage existing controls

Existing compliance controls can be managed from **Posture Management → Compliance → Controls Catalog.**&#x20;

### Edit or delete a custom control

Custom controls can be edited or deleted. Right click on a control or select <img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2FY4XEarbH6eoofHx6zLlS%2Freusable-menu.png?alt=media&#x26;token=bae02a0f-56cb-4d38-acb0-9cbc5b21b741" alt="" data-size="line"> from the control's side pane to access the **Edit** and **Delete** options. When editing a control, you can update all its parameters.

### Clone a control

All controls can be cloned using the **Save as new** option. Right click on a control or select <img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2FY4XEarbH6eoofHx6zLlS%2Freusable-menu.png?alt=media&#x26;token=bae02a0f-56cb-4d38-acb0-9cbc5b21b741" alt="" data-size="line"> from the control's side pane to access the option to **Save as new**. When cloning a control, you can update all its parameters. By default the original built-in control name is used with “\_copy“ appended.&#x20;
