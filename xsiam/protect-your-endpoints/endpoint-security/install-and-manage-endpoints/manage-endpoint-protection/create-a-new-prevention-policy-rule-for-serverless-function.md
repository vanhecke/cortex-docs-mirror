---
description: Create Cortex XSIAM prevention policy rules for serverless functions.
---

# Create a new prevention policy rule for serverless function

{% stepper %}
{% step %}
From **Inventory → Endpoints → Policy Management → Prevention → Profiles**, right-click the profile and select **Create a new policy rule using this profile**.

Cortex XSIAM automatically populates the Platform selection based on your profile configuration as well as the Restricitons selection with the selected profile.
{% endstep %}

{% step %}
For **Policy Name**, enter a meaningful name, and optionally, add a description for the policy rule, and then click **Next**.
{% endstep %}

{% step %}
Use the filters to define criteria for the policy rule to apply, and then click **Next**.

#### Select from the following function parameters:

* Cloud provider
* Region
* Runtime
* Function version
* Endpoint name
{% endstep %}

{% step %}
Review the policy rule summary, and then click **Done**.
{% endstep %}
{% endstepper %}

{% hint style="info" %}
The filter is stored within the policy definition and assessed during runtime to extract the functions that match the filter criteria.
{% endhint %}
