---
description: >-
  Add built-in controls or create and manage custom controls for custom
  standards in Cortex XSIAM.
---

# Use a built-in or custom control

When using custom standards, you can use built-in controls or create custom controls and then associate them with detection rules.

## Add a built-in control to a custom standard

Cortex XSIAM provides built-in controls that cannot be edited or deleted. When you edit or create a custom standard you can add the built-in control.

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
4. Assign a custom detection rule to the control as follows.

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

## Edit a custom control

You can edit a copy of a built-in control or edit an existing custom control. You can also delete a custom control.

1. In the **Controls** catalog, click [![cortex-cloud-compliance-three-dots.png](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAA8AAAAgCAYAAADNLCKpAAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAAAJcEhZcwAAEnQAABJ0Ad5mH3gAAADhSURBVEhL7ZQ9CoNAFIQnKW0Ua29hb2thoxewFew8gmcQPICVnSfRyiNYCza2Jk8GkgdZSAIhQvLBssMswz7e/py2K3iTM+e3+Idf5IDhtm0RBAHiOMYwDHQ1xnBd11jXFdM0oWkauhpj2HVdKsC2bSqN8W5LqbKjBIuigOM4XLnxvYfxmbLliKTTQhRFKMty1/cYy57nmQpYloVKYwzneQ7LsuB5HtI0pas54DckV1O63XUdnQdI2Y/IsmzzfX8fVVXR1Rh37vueChjHkUpjDCdJQgWEYUilOWC3n+H3wsAFdcOHmDnAN1gAAAAASUVORK5CYII=)](https://docs-cortex.paloaltonetworks.com/viewer/attachment/5CAbsl8idaK8R43ZLhoTOw/tDvVprS3kGLl_Hnh6mxouw-5CAbsl8idaK8R43ZLhoTOw) on the built-in control you want to edit and click **Save as new**.\
   To edit a custom control, click [![cortex-cloud-compliance-three-dots.png](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAA8AAAAgCAYAAADNLCKpAAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAAAJcEhZcwAAEnQAABJ0Ad5mH3gAAADhSURBVEhL7ZQ9CoNAFIQnKW0Ua29hb2thoxewFew8gmcQPICVnSfRyiNYCza2Jk8GkgdZSAIhQvLBssMswz7e/py2K3iTM+e3+Idf5IDhtm0RBAHiOMYwDHQ1xnBd11jXFdM0oWkauhpj2HVdKsC2bSqN8W5LqbKjBIuigOM4XLnxvYfxmbLliKTTQhRFKMty1/cYy57nmQpYloVKYwzneQ7LsuB5HtI0pas54DckV1O63XUdnQdI2Y/IsmzzfX8fVVXR1Rh37vueChjHkUpjDCdJQgWEYUilOWC3n+H3wsAFdcOHmDnAN1gAAAAASUVORK5CYII=)](https://docs-cortex.paloaltonetworks.com/viewer/attachment/5CAbsl8idaK8R43ZLhoTOw/tDvVprS3kGLl_Hnh6mxouw-5CAbsl8idaK8R43ZLhoTOw) on the custom control and click **Edit**.
2. Click **Next**.
3. Edit control metadata, including:
   * **Category**: You can reassign the control to a different category.
   * **Sub category** (optional): You can reassign the control to a different sub category.
   * **Control name**: You can update the control name.
   * **Description** (optional): You can update the control description.
   * **Select custom standards**: You can modify the list of custom standards with which the control should be associated.
4. Click **Save**.

If the control does not already contain a rule, assign a custom detection rule to the control.
