---
description: Learn how to create a custom detection rule in Cloud Identity Security.
---

# Create a custom detection rule in Cloud Identity Security

{% hint style="info" %}
This feature is included with a Cortex XSIAM Premium license. It is also included with any other Cortex XSIAM license that has the Cloud Posture Security or Cloud Runtime Security add-on.
{% endhint %}

Cloud Identity Security comes with a comprehensive set of out-of-the-box detection rules, helping you to detect, prioritize, and remediate Identity Security gaps in your environment. This set of rules is written and maintained by a team of Identity Security experts, aimed to look for the most common and severe Identity Security use cases. In order to provide a complete solution and be able to create issues for any required use case, Cloud Identity Security allows you to create custom detection rules, which allow you to customize the identity and permissions scenarios you are looking for and trying to avoid and remediate. You can create a custom detection rule and attach it to a policy in order to raise issues from the rule.

Identity and permissions are based on relations entities have with one another, therefore the rule builder is based on defining a logic for entities, their attributes, and the relations they have with other entities.

Each identity rule you define scans your environment for permissions that answer the criteria of each rule, raising issues for each defined asset that match the criteria.

A permission consists of five main entities:

* **Permissions source**: The human or nonhuman identity, account, service account, or identity provider that can conduct actions in your cloud environment. With certain configurations, the source can also be the general public or all authenticated users.
* **Permissions destination**: The cloud resource, or wildcard pattern, where permissions are granted on (a source can act on a destination).
* **Policy**: The IAM policy or role that defines permissions. Permissions can be granted using IAM policies as well as resource-based policies.
* **Granter**: The entity that connects the source to the relevant policy. For a permission that is granted by a resource-based policy, the granter should be identical to the destination. For inline policies or managed policies directly attached to the source, the granter should be identical to the source.
* **Permission**: The actual action that is granted to the source on the destination. A permission is a single cloud action and also has additional attributes such as last access, access level, which conditions are applied to the permission, and more.

Each rule consists of choosing an asset that has certain permissions while filtering attributes of that asset, the relationships it has with other assets, and their attributes.

Each custom rule creates issues for one pillar only: the source, the granter, or the destination of the permissions. Each issue must be assigned to a single asset. Since a permission can involve multiple related assets (source, granter, or destination), the system determines which of these three pillars is correlated with the entity that you choose first.

Create a custom identity detection rule

1. From the navigation pane on the left, go to **Posture Management** → **Rules & Policies** → **Rules** → **Cloud Security**.
2. On the **Cloud Posture Security Rules** screen, click **Create Rule** → **Identity**.
3. On the **Overview** tab of the **Create Identity Rule** screen, do the following:
   1. Enter a rule name.
   2. Enter a brief description of the rule (less than 300 characters).
   3. In the list, select a severity level.
   4. (Optional) Add a label.
   5. (Optional) Turn on the **Enable Remediation** toggle to add actions to take in the event that a rule is violated.
   6. In the **Compliance Controls** box, click **+ Add** to add and assign compliance controls to the rule.
   7. Click **Next**.
4. On the **Rule Logic** tab, define the logic for your rule.
5. Click **Search**. The results of your query are shown at the bottom of the screen under **Query Results**.
6. (Optional) On the **Remediation** tab, in the **Remediation** text box, define the actions to be performed when the new custom rule is violated.
7.  Click **Done**.

    The new rule appears in the list on the **Cloud Posture Security Rules** screen.

#### Example

Below is an example of a custom detection rule in Cloud Identity Security.

This is an example of a rule that looks for an AWS IAM user (source) with the following conditions:

* Has no MFA configured
* Gets administrative permissions from an IAM role whose name starts with “PROD”

![example\_identity\_custom\_detection\_rule.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-0cd438ef6b6d761ff85c3b3a6b3c240e233d884f%2F7b7e5cb8d0284dfa1ee4aa0d46b7d17f1ce0435e59735cd0c1f97cbe02df0707.png?alt=media)
