---
description: Manage, edit, and clone serverless function security rules in Cortex XSIAM.
---

# Manage serverless function rules

Serverless function rules are designed to detect security threats within your serverless function environment that can potentially introduce vulnerabilities to its security. Serverless function rules identify and flag issues based on predefined criteria, ensuring that potential threats are proactively detected and addressed to enhance the overall security posture of your serverless functions. There are three categories or types of serverless function rules:

* **Attack Path**: These rules identify combined risks in your serverless function configurations, like overly permissive roles and network exposure, that could be exploited to breach your serverless applications
* **Config**: These rules detect security resource misconfigurations in your serverless function configurations and their related code and pipeline infrastructure
* **Network Exposure**: These rules detect internet-exposed serverless functions by leveraging network configurations monitored across your cloud environment

### How to access serverless function rules

To access serverless function rules:

1. Under **Posture Management**, select **Rules & Policies** → **Cloud Security (under Rules)**.
2. Select the **Show filter panel** icon.
3.  Under the **Select field** menu, select the **Asset Types** category and select your cloud provider serverless function type from the **Select values** menu. Options:

    * **Azure Cloud Function**
    * **Google Cloud Function** (Gen 1 only)
    * **Lambda Function (AWS)**

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>You can select multiple types to view all your serverless function policies across your cloud providers.</p></div>

    A table of serverless function rules filtered by asset type is displayed. Serverless functions properties unique or important enough to mention to serverless functions include:

    * **Provider**: The cloud provider (such as WAS) associated with the serverless function
    * **Severity**: The severity level of findings associated with the rule
    * **Asset Types**: The type of serverless function. Options: Lambda Function, Google Cloud Function, Azure Cloud Function
    * **Type**: The type of serverless function rule. Options: Attack Path, Config, Network Exposure

### Manage serverless function rules

You can edit or clone serverless function rules.

* Edit a rule to fine-tune existing rules
* Clone a rule to saves time by reusing settings and applying policies uniformly across similar assets, ensuring standardized policies and predictable behavior

1. Under **Posture Management**, select **Rules & Policies** → **Cloud Security (under Rules)**.
2. Filter for the list of serverless function rules. Refer to [How to access serverless function rules](#how-to-access-serverless-function-rules) above for more information.
3.  Right-click on a rule.

    *   To edit a rule, click **Edit**.

        You are redirected to the **Overview** step of the **Edit Rule** wizard.
    *   To clone a rule, select **Save as new**.

        You are redirected to the **Overview** step of the new rules wizard.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>Refer to <a href="create-serverless-function-rules">Create serverless function rules</a> for more information on how to define the steps of a rule in the wizard.</p></div>
