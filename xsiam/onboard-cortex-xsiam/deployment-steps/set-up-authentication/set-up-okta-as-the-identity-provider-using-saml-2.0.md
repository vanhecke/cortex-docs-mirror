# Set up Okta as the Identity Provider Using SAML 2.0

This topic provides specific instructions for using Okta to authenticate your Cortex XSIAM users. As Okta is a third-party software, specific procedures, and screenshots may change without notice. We encourage you to also review the [Okta documentation for app integrations](https://help.okta.com/oie/en-us/content/topics/apps/apps_apps.htm).

To configure SAML SSO in Cortex XSIAM, you must be a user who can access the Cortex XSIAM tenant and have either the Account Admin or Instance Administrator role assigned.

<details>

<summary>Task 1. Configure Okta Groups</summary>

Within Okta, assign users to [groups](https://help.okta.com/asa/en-us/content/topics/adv_server_access/docs/setup/create-a-group.htm) that match the user groups they will belong to in Cortex XSIAM. Users can be assigned to multiple Okta groups and receive permissions associated with multiple user groups in Cortex XSIAM. Use an identifying word or phrase, such as Cortex XSIAM, within the group names. For example, Cortex XSIAM Analysts. This allows you to send only relevant group information to Cortex XSIAM, based on a filter you will set in the group attribute statement.

Create a list of the Okta groups and their corresponding Cortex XSIAM user groups (or the Cortex XSIAM user groups you intend to create) and save this list for later use when configuring user groups in Cortex XSIAM.

</details>

<details>

<summary>Task 2. Copy Single SSO and Audience URI Values from Cortex XSIAM</summary>

1. In Cortex XSIAM, go to Settings → Configurations → Access Management → **Authentication Settings**.
2. In the **Login Options** tab, toggle **SSO Disabled** to on.
3. Expand the **SSO Integration** settings.
4.  Copy and save the values for **Single Sign-On URL** and **Audience URI (SP Entity ID)**.

    Both values are needed to configure your IdP settings.

    You cannot save the enabled SSO Integration at this time, as it requires values from your IdP.

</details>

<details>

<summary>Task 3. Configure Cortex XSIAM Application in Okta</summary>

1. In Okta, create a Cortex XSIAM application and **Edit** the **SAML Settings**.
2. Paste the **Single sign-on URL** and the **Audience URI (SP Entity ID)** that you copied from the Cortex XSIAM SSO settings. The Audience URI should also be pasted in the **Default RelayState** field, which allows users to log in to Cortex XSIAM directly from the Okta dashboard.
3. Click **Show Advanced Settings**, verify that Okta is configured to sign both the response and the assertion signature for the SAML token, and then click **Hide Advanced Settings**.
4.  Cortex XSIAM requires the IdP to send four attributes in the SAML token for the authenticating user.

    * Email address
    * Group membership
    * First Name
    * Last Name

    Configure Okta to send group memberships of the users using the `memberOf` attribute. Use the word or phrase you selected when configuring Okta groups (such as Cortex XSIAM) to create a filter for the relevant groups.
5. Copy the exact names of the attribute statements from Okta and save them, as they are required to configure the Cortex XSIAM SSO integration. In the example above, the names are FirstName, LastName, Email, and memberOf. The attribute names are case-sensitive.

</details>

<details>

<summary>Task 4. Copy IdP SSO URL, Identity Provider Issuer, and X.509 Certificate Values</summary>

1. In Okta, from your Cortex XSIAM application page, click **View SAML setup instructions**. If you do not see this button, verify you are on the **Sign On** tab of the application.
2. Copy and save the values for **Identity Provider Single Sign-On URL**, **Identity Provider Insurer**, and the **X.509 Certificate**. These values are needed to configure your Cortex XSIAM SSO Integration.

</details>

<details>

<summary>Task 5. Configure the Cortex XSIAM SSO Integration</summary>

1. In Cortex XSIAM go to Settings → Configurations → Access Management → **Authentication Settings**.
2. In the **Login Options** tab, toggle **SSO Disabled** to on.
3. Expand the **SSO Integration** settings.
4.  Use the following table to complete the SSO Integration settings, based on the values you saved from Okta.

    | Okta                                 | Cortex XSIAM Field |
    | ------------------------------------ | ------------------ |
    | Identity Provider Single Sign-On URL | IdP SSO URL        |
    | Identity Provider Issuer             | IdP Issuer ID      |
    | X.509 Certificate                    | X.509 Certificate  |
5. In the **IdP Attributes Mapping** section, enter the attribute names from Okta. The names are case-sensitive and must match exactly.
6. **Save** your settings.

</details>

<details>

<summary>Task 6. Map SAML Group Memberships to Cortex XSIAM User Groups</summary>

1. Select Settings → Configurations → Access Management → **User Groups**.
2. Right-click a user group and select **Edit Group**.
3. In the **SAML Group Mapping** field add the Okta group(s) that should be associated with this user group. Multiple groups should be separated with a comma. The Okta group name must match the exact value sent in the token.
4. **Save** your settings.
5. Repeat for each user group.

</details>

<details>

<summary>Task 7. Test SSO Login</summary>

1.  Go to the Cortex XSIAM tenant URL and **Sign-In with SSO**.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>When using SAML 2.0, users are required to authenticate by logging in directly at the tenant URL. They cannot log in via Cortex Gateway.</p></div>
2. After authentication to Okta, you are redirected again to the Cortex XSIAM tenant.
3.  When logged in, validate that you have been assigned the proper roles.

    To view your role and any role assigned to a user group you are a member of, click your name in the bottom left-hand corner, and click **About**.

</details>
