---
description: >-
  Modify custom cloud security rules and supported out-of-the-box rule
  parameters.
---

# Edit a cloud security rule

You can edit custom cloud security rules and modify their parameters as needed.

In some cases, you can also edit and modify parameters of out-of-the-box rules:

* You can add labels to out-of-the-box attack path, config, and network exposure rules.
* You can associate AI, config, and identity rules with custom compliance controls.

To edit a rule:

1. Navigate to **Posture Management** → **Rules & Policies** → **Rules** → **Cloud Security**.
2. From the **Rules** page, there are two ways to access the option:
   1. Right-click the entry and then select **Edit.**
   2. Click on the rule. Next, on the **Details** page, click the more options icon (⋮) and then select **Edit.**
3. Make the necessary changes.
4. Click **Done** to save your changes.

Note that the following may happen as a result of editing a rule:

* When rule logic is modified, if the assets which were violating the rule earlier are not violating it anymore, the corresponding issues are closed.
* When certain rule attributes such as severity or labels are modified, if these attributes matched earlier but do not match after the edit, the rule may be excluded from the policy and the corresponding issues closed.
