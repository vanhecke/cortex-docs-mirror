# Create a configuration rule for serverless functions

Config rules for serverless functions identify security misconfigurations within the settings and deployment infrastructure of your individual serverless resources.

1. Under **Posture Management**, select **Rules & Policies** → **Cloud Security (under Rules)** → **click Create Rule**.
2. Select **Config**.
3. On the **Overview** step of the **Create Config Rule** wizard.
   1. Fill in these fields:
      * **Rule Name**: (required): A user-provided to identify the rule
      * **Description** (required): A description of the rule
      * **Severity** (required): Select the severity level. Only findings with this exact severity level will trigger this rule. Findings with different severity levels will be ignored
      * **Labels**: (optional): Assign labels to categorize and organize the rule based on specific criteria or attributes. Labels help in easily identifying and filtering rules
      * **Enable How to Fix**: (Default: ON): Enable to take action when the rule is violated
   2. Click Next.
4. Define the logic for the configuration rule on the **Rule Logic** step of the wizard in the query editor.
   1. Under the **Value** menu in the **Find** field:
      1. Select **Compute**.
      2.  Select the relevant serverless function from the list that is displayed. Options: **Lambda Function**, **Google Cloud Function**, **Azure Cloud Function**.

          The JSON configuration file for the selected serverless function is displayed. Note that each type of serverless function has a unique configuration file and unique properties.
   2. Select a property or multiple properties of the serverless function configuration file and provide a value.
   3.  Click Search.

       All assets matching the search criteria are displayed. This allows you to validate the rule's effectiveness on existing functions and provides valuable context for refining the rule's logic to accurately identify future functions.
   4. Click **Next** if you have enabled a fix in step 1a above, or **Done** if fix is disabled.
5. Define the fix in the **How to Fix** step (when enabled in step 1a above), and click Done.
