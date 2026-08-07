# How to report a false positive in Cortex Cloud Data Classification

{% hint style="info" %}
This feature is included with a Cortex XSIAM Premium license. It is also included with any other Cortex XSIAM license that has the Cloud Posture Security or Cloud Runtime Security add-on. If you have the Endpoint DLP add-on, Data Classification is automatically available.
{% endhint %}

### Overview

When reviewing a scan of your assets, if you notice or identify that a data object (such as a file, table, or field) has been incorrectly classified, you can use the provided support case submission feature to report the false positive.

You initiate a support case submission using the designated **Report false positive** button. This triggers a structured workflow designed to gather all the necessary technical and contextual information required for our data analysts to investigate and fix the issue quickly. You will be asked to confirm or provide essential details, including the specific Data Pattern that was incorrectly matched and your description and evidence (a screenshot or the actual file or text) explaining why it is a false positive.

Once submitted, this case is handled by the Palo Alto Networks support team, which checks all the requested information that you provided. The support team is engaged with both the Data Engineering team to investigate and fix the issue, and with you to provide updates on the progress of the support case. The fix is applied to the core classification logic. You will be able to see accurate results after the next scan occurs.

### How to create a support case

1. You will need your tenant details during the reporting process. To display your tenant details, on the lower left screen, click **Your name** → **About**. You can take a screenshot and save the file for a later step in the reporting process. Alternatively, you can click the **Copy to clipboard** link to copy the information and then paste it into a file of your choice.
2.  On the screen where you found the false positive, click the **More Options** icon, and then click **Report false positive**.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>Alternatively, in Cortex Command Center, click <strong>Help</strong> → <strong>Submit a Support Case</strong>.</p></div>
3. On the Submit Support Case screen that opens, on the **Case Information** tab, do the following:
   1. In the **Describe the issue** text box, enter a description of the object that you are reporting.
   2. Under **Enter your preferred contact number**, enter either your telephone or cellphone number at your organization.
   3. (Optional) Under **Issue frequency**, select a frequency in the list. The options are **Not applicable**, **Consistent**, or **Intermittent**.
   4. (Optional) Under **Most recent issue start date & time**, select the date and time that you found the false positive.
   5. In the **Indicate the impact of the issue** list, select the one of the five options that most closely relates to your issue.
   6. In the **Select an issue category** list, select **Modules**.
   7. In the **Problem concentration** list, select **Data Classification**.
   8. Provide the Data Pattern name where you found the false positive.
   9. Under the question **Does the object with the false positive contain test data or production data?**, enter **test data** or **production data**.
   10. If you are reporting a file, enter the file path. If it is a table, enter the column name and column type.
   11. Use the **Browse** link to upload the file containing the false positive or a relevant screenshot that shows the false positive in context, such as the paragraph where it is located.
   12. Use the **Browse** link to upload the file with your tenant details that you saved in step 1.
   13. Select the checkbox allowing Palo Alto Networks' support team to access your CSP account.
   14. Click **Next**.
   15. On the **Console Recording** tab, do not create a recording. Simply click **Submit Support Case**.
4. Click **Submit**. A support case is opened and you will be contacted by the Palo Alto Networks support team.
