# Manage serverless function policies

Serverless function policies define how a system should respond to serverless function threats. They include conditions that trigger the policy, the scope of its application, and the actions to be taken when these conditions are met. When policies detect a threat, they generate issues for remediation.

### How to access serverless function policies

1. Under **Posture Management**, select **Rules & Policies** → **Cloud Security (under Policies)**.
2. Select the **Show filter panel** icon.
3.  Filter the table by the **Asset Types** category and select your cloud provider serverless function type from the **Select values** menu. Options:

    * **Azure Cloud Function**
    * **Google Cloud Functions:** 1st gen and 2nd gen (Cloud Functions API and Cloud Run Admin API)
    * **Lambda Function (AWS)**

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>You can select multiple types to view all your serverless function rules across your cloud providers.</p></div>

    A list of serverless function rules filtered by asset type is displayed.

### Manage serverless function policies

You can delete, edit or clone serverless function policies.

* Delete a policy when no longer relevant, to avoid overhead
* Edit a policy to fine-tune existing policies
* Clone a policy to saves time by reusing settings and applying policies uniformly across similar assets, ensuring standardized policies and predictable behavior

1. Under **Posture Management**, select **Rules & Policies** → **Cloud Security (under Policies)**.
2. Filter for the list of serverless function policies. Refer to [How to access serverless function policies](#how-to-access-serverless-function-policies) above for more information.
3.  Right-click on a policy.

    * To delete a policy, click **Delete**, and confirm the deletion in the popup
    *   To edit a policy, click **Edit**.

        You are redirected to the **Details** step of the **Edit Policy** wizard.
    *   To clone a policy, select **Save as new**.

        You are redirected to the **Details** step of the new policy wizard.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>Refer to <a href="create-serverless-function-policies">Create serverless function policies</a> for more information on how to define the steps of a policy in the wizard.</p></div>
