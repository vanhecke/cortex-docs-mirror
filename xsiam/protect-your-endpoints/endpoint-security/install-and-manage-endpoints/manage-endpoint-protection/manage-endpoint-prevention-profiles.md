# Manage endpoint prevention profiles

You can manage the endpoint prevention profiles of your Cortex XDR agent endpoints in various ways, including editing, duplicating, and populating endpoint prevention policy rules.

After you create and customize your endpoint prevention profiles, you can manage them from the Prevention Profiles page as needed.

### View the prevention policy rules that use a specific prevention profile

Before you modify or delete a profile, you can check which policy rules, if any, use the profile.

* From **Inventory → Endpoints → Policy Management → Prevention → Profiles**, right-click the profile and select **View policy Rules**.

Cortex XSIAM opens the Prevention Policy Rules page on a new tab. This page is filtered, and only displays the rules that use the profile that you selected.

### Edit, export, duplicate, or delete an endpoint prevention profile

#### Edit a profile:

{% stepper %}
{% step %}
From **Inventory → Endpoints → Policy Management → Prevention → Profiles**, right-click the profile and select **Edit**.
{% endstep %}

{% step %}
Make your changes, and then click **Save**.
{% endstep %}
{% endstepper %}

#### Export a profile:

{% stepper %}
{% step %}
From **Inventory → Endpoints → Policy Management → Prevention → Profiles**, right-click the profile and select **Export Profile**.
{% endstep %}

{% step %}
Click **Export**. The profile is downloaded to your computer.
{% endstep %}
{% endstepper %}

#### Duplicate a profile:

{% stepper %}
{% step %}
From **Inventory → Endpoints → Policy Management → Prevention → Profiles**, right-click the prevention profile and select **Save as New**. A new profile is displayed, containing the values from the profile that you selected.
{% endstep %}

{% step %}
Edit the profile name and description, edit any values that you want to change, and then click **Create**.
{% endstep %}

{% step %}
Populate a new prevention policy rule with your new profile.
{% endstep %}
{% endstepper %}

#### Delete a profile:

{% hint style="warning" %}
If necessary, delete or detach any policy rules that use the profile before attempting to delete it.
{% endhint %}

{% stepper %}
{% step %}
From **Inventory → Endpoints → Policy Management → Prevention → Profiles**, locate the profile that you want to remove. The profile's **Usage Count** cell must have a 0 (zero) value.
{% endstep %}

{% step %}
Right-click the prevention profile and select **Delete**.
{% endstep %}

{% step %}
To confirm the deletion, click **Yes**.
{% endstep %}
{% endstepper %}

### Populate a new prevention policy rule with a prevention profile

{% stepper %}
{% step %}
From **Inventory → Endpoints → Policy Management → Prevention → Profiles**, right-click the profile and select **Create a new policy rule using this profile**.

Cortex XSIAM automatically populates the Platform selection based on your profile configuration, and assigns the profile based on the profile type.
{% endstep %}

{% step %}
For Policy Name, enter a meaningful name, and optionally, add a description for the policy rule.
{% endstep %}

{% step %}
Assign any additional profiles that you want to apply to your policy rule, and click **Next**. A list of endpoints is displayed.
{% endstep %}

{% step %}
Select the target endpoints for the policy rule, or use the filters to define criteria for the policy rule to apply, and then click **Next**.
{% endstep %}

{% step %}
Review the policy rule summary, and then click **Done**.
{% endstep %}
{% endstepper %}
