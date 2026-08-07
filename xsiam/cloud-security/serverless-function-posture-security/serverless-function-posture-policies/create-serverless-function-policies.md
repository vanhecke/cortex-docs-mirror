# Create serverless function policies

The following procedure describes how to create policies for serverless functions.

1. Under **Posture Management**, select **Rules & Policies** → **Cloud Security (under Policies)** → **click Create Policy**.
2. On the **Details** step of the wizard:
   1. Fill in these fields:
      * **Policy Name** (required): An alias you provide to identify the policy
      * **Description** (required): A description of the policy
      * **Labels** (optional): Assign labels to categorize and organize the policy based on specific criteria or attributes. Labels help in easily identifying and filtering policies
   2. Click Next.
3. On the **Rules** step of the wizard.
   1.  Select rules that check for violations when scanning serverless functions: Options:

       * **All Matching Filter Criteria**: Allows you to filter for rules according to criteria
       * **From Rules List**. Filter the rues list by the type of serverless function.
         1. Select From Rules List
         2. Select **Asset Type** from the **Select Field** menu of the query.
         3. Filter for the following serverless functions, depending on the target cloud provider for the rule. Options:
            * Azure Cloud Function
            * Google Cloud Function: Google Cloud Functions - 1st gen and 2nd gen (Cloud Functions API and Cloud Run Admin API.
            *   Lambda Function

                <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>You can select multiple options.</p></div>
         4. Select a rule or multiple rules from the resulting list.
       * **All Rules**: This option is not recommended as it will probably create a large number of issues/

       <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>For more information about rules, refer to <a href="../serverless-function-posture-rules/manage-serverless-function-rules">Manage serverless function rules</a>.</p></div>
   2. Click Next.
4. On the **Scope** step of the of the wizard:
   1. Define the scope of the policy by selecting the assets it will apply to. Options:
      * **From Cloud Accounts** (recommended): Select one or more accounts to which this policy applies
      * **All Cloud Accounts** (not recommended): Selecting this option will likely result in a large volume of issues. For more relevant and higher fidelity results, select the **From Cloud Accounts** option
   2. Click Done.
