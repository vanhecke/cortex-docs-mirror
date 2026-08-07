---
description: Use trigger scripts to run actions when indicator field values change.
---

# Indicator field trigger scripts

Indicator field trigger scripts are automated responses that are triggered by a change in an indicator field value. In the script, you define the change in the indicator field value to check for and the actions to take when the change occurs. For example, you can:

* Create a script that runs when the **Verdict** field of an indicator changes. For example, the script will fetch all issues related to the indicator and take any action that is configured, such as reopening or changing severity.
*   Create a script that runs when the **Expiration Status** field changes. For example, you can define a script that will immediately update the relevant allow/block list and not wait for the next iteration, as seen in the following sample script:

    ```programlisting
    indicators = demisto.args().get('indicators')
    new_value = demisto.args().get('new')

    indicator_values = []
    for indicator in indicators:
        current_value = indicator.get('value')
        indicator_values.append(current_value)

    if new_value == "Expired":
        # update allow/block list regarding expired indicators
    else:
        # update allow/block list regarding active indicators
    ```

<details>

<summary>Indicator field trigger script arguments</summary>

Scripts can be created in Python, PowerShell, or JavaScript on the Scripts page. To use a field trigger script, you need to add the **field-change-triggered-indicator** tag when creating the script. You can then add the script in the Attributes tab when you edit or create a custom indicator field. If you did not add the tag when creating the script, the script will not be available for use.

Indicator field trigger scripts have the following triggered field information available as arguments (args):

| Argument              | Description                                                                                    |
| --------------------- | ---------------------------------------------------------------------------------------------- |
| **`associatedToAll`** | Whether the field is associated with all or some indicators. Value: **`true`** or **`false`**. |
| **`associatedTypes`** | An array of the indicator types the field is associated with.                                  |
| **`cliName`**         | The name of the field when called from the CLI.                                                |
| **`description`**     | The description of the field.                                                                  |
| **`indicators`**      | A list of indicators that have the current change.                                             |
| **`isReadOnly`**      | Specifies whether the field is non-editable. Value: **`true`** or **`false`**.                 |
| **`name`**            | The name of the field.                                                                         |
| **`new`**             | The new value of the field.                                                                    |
| **`old`**             | The old value of the field.                                                                    |
| **`ownerOnly`**       | Specifies that only the creator of the field can edit. Value: **`true`** or **`false`**.       |
| **`placeholder`**     | The placeholder text.                                                                          |
| **`required`**        | Specifies whether this is a mandatory field. Value: **`true`** or **`false`**.                 |
| **`selectValues`**    | If this is a multi-select type field, these are the values the field can take.                 |
| **`system`**          | Whether it is a Cortex XSIAM defined field.                                                    |
| **`type`**            | The field type.                                                                                |
| **`user`**            | The username of the user who triggered the script.                                             |

</details>

<details>

<summary>Indicator field trigger script best practices</summary>

* Indicator field trigger scripts react to changes that have already occurred to the field and cannot validate or block changes to the field.
* Indicator field trigger scripts can be configured on the **Verdict**, **Related Incidents**, **Expiration Status**, and **Indicator Type** fields, as well as any custom indicator fields.
* Indicator field trigger scripts work in all TIM (Threat Intelligence Management) scenarios and workflows, except for feed ingestion.
* Fields that can hold a list (related incidents, multi-select/tag/role type custom fields) will provide an array of the delta. For example, if a multi-select field value has changed from \["a"] to \["a", "b"], the new argument of the script will get a value of \["b"].
*   Indicator field trigger scripts run as a batch. This means that if multiple indicators are changed in the same way and are set to trigger the same action, it will happen in one batch.

    For example, in the following scenario for a configured indicator field trigger script named **`myTriggerScript`** on the **Verdict** indicator field:

    * The Threat Intel Library has two existing Malicious indicators: 1.1.1.1 and 2.2.2.2.
    * The user runs the following command **`!setIndicators indicatorsValues="1.1.1.1,2.2.2.2" verdict=Benign`**.
    * The **`myTriggerScript`** script will run just once, with the following parameters:
      * new - "Benign"
      * old - "Malicious"
      * indicators - "\[{\<indicator\_1.1.1.1>},{\<indicator\_2.2.2.2}]"
* When writing indicator field trigger scripts, avoid scenarios that call the scripts endlessly (for example, a change in field A triggers script X, which changes field B's value, which in turn calls script Y, which changes field A's value).

</details>

<details>

<summary>Add an indicator field trigger script to an indicator field</summary>

After creating an indicator field trigger script in the **Scripts** page in Python, PowerShell, or JavaScript, you can then associate it with an indicator field.

1. Go to Settings → Configurations → Object Setup → Indicators → **Fields**.
2. Select the indicator field and click **Edit**.
3.  In the **Attributes** tab, under **Script to run when field value changes**, select the desired indicator field trigger script.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>Indicator field trigger scripts must have the <strong><code>field-change-triggered-indicator</code></strong> tag to appear in the list.</p></div>

</details>
