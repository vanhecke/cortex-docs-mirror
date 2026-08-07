# How to create and validate a custom data pattern

{% hint style="info" %}
This feature is included with a Cortex XSIAM Premium license. It is also included with any other Cortex XSIAM license that has the Cloud Posture Security or Cloud Runtime Security add-on. If you have the Endpoint DLP add-on, Data Classification is automatically available.
{% endhint %}

### Overview

Custom data patterns allow you to define specific criteria for identifying sensitive data tailored to your organization's unique requirements. These patterns are applied globally across all modules that utilize Cortex Cloud Data Classification.

### Parameters and definitions

To create a new custom data pattern, you will need to use the following parameters:

| Parameter           | Definition                                                                                                                                                                                                                                                                                                                                                                                                                    |
| ------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| regex               | Define your pattern using regular expressions that are compatible with Rust syntax.                                                                                                                                                                                                                                                                                                                                           |
| context words       | Specify keywords that should appear in proximity to the regex match. These words are included in the search. A context word can be just one word or a phrase of a few words. Separate the context words or phrases with a comma (,).                                                                                                                                                                                          |
| proximity           | Define a proximity for each custom data pattern. The proximity parameter defines the maximum number of characters allowed between the context words and a regex match. The proximity parameter finds regex values only after the context word.                                                                                                                                                                                |
| masking level       | <p>Define a specific masking level for each custom data pattern you create. Any changes to this setting only affect future data collection.</p><p>The possible masking level options are:</p><ul><li><strong>Mask all:</strong> Displays only the number of strings with asterisks (*).</li><li><strong>Partial:</strong> Partial masking hides the last 70% of the value. Only alphanumeric characters are masked.</li></ul> |
| profile association | You can associate your custom data pattern with one or more custom data profiles. This allows the pattern to be included in the definition of a data profile.                                                                                                                                                                                                                                                                 |

### Create a new custom data pattern

1. In the lower left part of the screen, click **Settings** → **Configurations**.
2. In the **Configurations** column, under **Data Classification**, click **Data Patterns**.
3. On the **Data Patterns** screen, click **+ Add Pattern**.
4. On the **Create New Data Pattern** screen, do the following (the starred fields are mandatory):
   1. In the **Data Pattern Name** field, enter a data pattern name. To add an optional description, click **Add description** and enter a description in the text box that opens. If you change your mind and want to remove it, click **Remove description**.
   2. In the **Regular Expression (Regex)** field, enter a regex.
   3. In the **Context Words** line, enter the context words you want to use for your new data pattern.
   4. In the **Proximity** field, enter an integer that is greater than 10 and less than 150. The proximity is the maximum distance in characters from the context word to a regex value. If a context word is found, the proximity is counted from the end of the context word. The entire regex value must be found within this proximity window to be considered as found.
5. You can now test your new data pattern to validate it.

{% hint style="info" %}
### Note

Once a custom data pattern is saved, it runs on all data in the same way as any out-of-the-box (OOTB) pattern, becoming globally applicable for all modules using Cortex Cloud Data Classification.
{% endhint %}

### Validate the data pattern

It is crucial to validate your custom data pattern before saving it to ensure that it functions as intended and does not negatively impact system performance.

Validation does the following:

* Helps you understand if your custom classifier is properly defined in order to capture the data that you require. If it is not properly defined, the validator provides insights into the problem and assists with modifications.
* Verifies that the custom pattern does not cause the classification engine to get stuck or work slowly, which could affect functionality or the user experience.

To validate your data pattern, do the following:

1. In the **Test Data Pattern** text box, enter your test text and click **Test**. Based on your configured regex value, any matches that are found appear in the test results box and are highlighted.
2. You can adjust your regex value and click **Test** again to get different results.

### Validator behavior and results

* **Check regex:**
  * A text that is found by regex appears with highlighting.
  * If the regex text is found within the defined proximity range, it is highlighted in green, even if only one text is found within the correct proximity of a context word.
  * If the text is found outside of the defined proximity range for all context words, it is highlighted in gray.
* **Check context words:**
  * Texts that are found under different context words are underlined.
  * If a text is found within the proximity range, it is highlighted in green.
  * If a text is found outside the proximity range, it is highlighted in gray.
* **Textual explanation and guidance:** The checker provides messages based on the test results.
* **Sanity check (performance):** A critical check runs automatically when you click **Save** for your custom pattern, even if you don't manually run the data pattern check.
  * If a regex fails the sanity check, a notification informs you that the regex is too broad and needs to be narrowed.
  * You cannot save a custom classifier until its regex passes this performance test.

### Manage custom data patterns

* **Delete custom data patterns:** You can delete custom data patterns. Be aware that deleting a data pattern erases all past data associated with it in each module using Cortex Cloud Data Classification. It can take up to two days for the data deletion process to be completed in all places where this custom data pattern exists.
* **Attach Geo tags to patterns:** You can attach Geo tags to each pattern to help filter or view information based on specific locations. These tags can be added or removed only from custom patterns.
* **Enable or disable a data pattern:** You can enable or disable a data pattern. This action is global and applies to all modules using Cortex Cloud Data Classification. Enabling or disabling only affects future scans; past results are still presented.

{% hint style="info" %}
### Note

For more information, see [How to disable and enable data patterns in Data Classification](how-to-disable-and-enable-data-patterns-in-data-classification).
{% endhint %}
