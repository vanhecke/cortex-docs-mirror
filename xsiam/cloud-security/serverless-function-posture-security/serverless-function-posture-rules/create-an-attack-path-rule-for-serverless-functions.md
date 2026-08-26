---
description: >-
  Create serverless function attack path rules to identify connected risks in
  Cortex XSIAM.
---

# Create an attack path rule for serverless functions

Attack Path policies for serverless functions identify critical risks arising from interconnected weaknesses across your serverless architecture (such as correlating findings across functions, triggers, and permissions), to expose complex attack paths revealing complex attack paths beyond individual findings.

1. Under **Posture Management**, select **Rules & Policies** → **Cloud Security (under Rules)** → **click Create Rule**.
2. Select **Attack Path**.
3. On the **Overview** step of the **Create Attack Path Rule** wizard.
   1. Fill in these fields.
      * **Rule Name**: (Required): A user-provided to identify the rule
      * **Rule Name**: (Required): A user-provided to identify the rule
      * **Description** (Required): A description of the policy
      * **Severity** (Required): Select the severity level. Only findings with this exact severity level will trigger this rule. Findings with different severity levels will be ignored
      * **Labels**: (Optional): Assign labels to categorize and organize the rule based on specific criteria or attributes. Labels help in easily identifying and filtering rules
      * **Enable How to Fix** (Optional. Default: **ON**): Enable to take action when the rule is violated
   2. Click Next.
4. Define the logic for the rule on the **Rule Logic** step of the wizard in the query editor.
   1. Under the value menu in the **Find** field:
      1. Select **Compute**.
      2. In the corresponding table, search for a serverless function. Options: **Lambda Function**, **Google Cloud Function**, **Azure Cloud Function**.
   2. Select the `+` icon in the editor.
   3. Select an option: **Finding**, **Vulnerability**.
      * **Findings**: Define the logic for findings.
        1. Provide the finding name. The name must match the name of the policy that will generate the security finding.
        2. Click on the **Finding Name** card that is displayed In the **WHERE** field.
        3. Select the value `in` under the **Operator** field.
        4. Select the required finding or findings from the list that is displayed.
        5.  Click **Search**.

            All assets matching the search criteria are displayed. This allows you to validate the rule's effectiveness on existing functions and provides valuable context for refining the rule's logic to accurately identify future functions.
        6. Select Next.
        7. Provide suggested mitigation in the **How to Fix** step and click **Done**.
      * **Vulnerability**: Define the logic rule for types of vulnerabilities. Options: **CVE ID** (The unique identifier of the vulnerability), **Vulnerability Severity** (The impact level of the vulnerability), **CVSS Score** (The numerical rating of a vulnerability's severity)
        1. **CVE ID**: **Select in as the operator** → **enter the CVE ID** → **Search**.
        2. **Vulnerability Severity**: **Select > or >= as the operator** → **Severity level (such as High, Low)** → **Search**.
        3. **CVSS Score**: **Select > or >= as the operator** → **enter a score** → **Search**.
   4. Click **Next** if you have enabled a fix in step 1a above, or **Done** if fix is disabled.
5. Define the fix in the **How to Fix** step (when enabled in step 1a above), and click Done.
