# Set up Microsoft Entra ID as the Identity Provider Using SAML 2.0

This topic provides specific instructions for using Microsoft Entra ID (formerly Azure AD) to authenticate your Cortex XSIAM users. As Microsoft Entra ID is a third-party software, specific procedures, and screenshots may change without notice. We encourage you to also review the [Microsoft Entra ID documentation](https://learn.microsoft.com/en-us/azure/active-directory/manage-apps/add-application-portal-setup-sso).

To configure SAML SSO in Cortex XSIAM, you must be a user who can access the Cortex XSIAM tenant and have either the Account Admin or Instance Administrator role assigned.

The following video is a step-by-step guide configuring SSO for Microsoft Entra ID: [Microsoft Entra ID SSO](https://www.youtube.com/watch?v=nwF3hY3wgc0).

<details>

<summary>Task 1. Configure Microsoft Entra ID Security Groups</summary>

Within Microsoft Entra ID, assign users to [security groups](https://learn.microsoft.com/en-us/azure/active-directory/fundamentals/how-to-manage-groups) that match the user groups they will belong to in Cortex XSIAM. Users can be assigned to multiple Microsoft Entra ID groups and receive permissions associated with multiple user groups in Cortex XSIAM. Use an identifying word or phrase, such as Cortex XSIAM, within the group names. For example, Cortex XSIAM Analysts. This allows you to send only relevant group information to Cortex XSIAM, based on a filter you will set in the group attribute statement.

</details>

<details>

<summary>Task 2. Copy Single SSO and Audience URI Values from Cortex XSIAM</summary>

1. In Cortex XSIAM go to Settings → Configurations → Access Management → **Authentication Settings**.
2.  In the **Login Options** tab, toggle **SSO Disabled** to on.

    By default, SSO is disabled in Cortex XSIAM.
3. Expand the **SSO Integration** settings.
4.  Copy and save the values for **Single Sign-On URL** and **Audience URI (SP Entity ID)**.

    Both values are needed to configure your IdP settings.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Important</h3><p>When copying the <strong>Single Sign-On URL</strong> value, remove <code>idp/saml</code> and leave the trailing <code>/</code>.</p><p>For example, if the <strong>Single Sign-On URL</strong> is <code>https://clientname.panproduct.region.paloaltonetworks.com/idp/saml</code>, just copy <code>https://clientname.panproduct.region.paloaltonetworks.com/</code>.</p></div>
5. You cannot save the enabled SSO Integration at this time, as it requires values from your IdP.

</details>

<details>

<summary>Task 3. Configure Cortex XSIAM Application in Microsoft Entra ID</summary>

1.  From within Microsoft Entra ID, create a Cortex XSIAM application and **Edit** the **Basic SAML Configuration**.

    ![Azure-Basic-SAML-8.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-85f4f582526efad63865a493fbfe299d8b66903a%2F5d9059fd43ccdd79d3bb9c02468582bc63c136cb752a192328903fc42efa14ef.png?alt=media)
2.  Paste the **Single sign-on URL** and the **Audience URI (SP Entity ID)** that you copied from the Cortex XSIAM SSO settings. The **Single sign-on URL** from Cortex XSIAM should be pasted in the **Reply URL** and the **Sign on URL** fields. The **Audience URI (SP Entity ID)** value from Cortex XSIAM should be pasted in the **Identifier (Entity ID)** and **Relay State** fields. This allows users to log in to Cortex XSIAM directly from Microsoft Entra ID.

    ![azure-basic-saml.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-eb9b1983e2265d7a1d0ece3ae1046a8e46cc0922%2F8fbcadf2f51fc81161133413e77aec4d47252eea8cee8eae09ba7635d0823cde.png?alt=media)
3.  In the **SAML Certificates** section, click **Edit** and verify that Microsoft Entra ID is configured to sign both the response and the assertion.

    ![Azure-Sign-Certificate-8.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-d1c1104a7f6ddd9d21777c8511fe62ac89bfacde%2F3613d1ba7aba13986fbe7e0f968d29647908e036d9b385475509d34c9d06931b.png?alt=media)
4.  To have Microsoft Entra ID send group membership for the user in the SAML token, you must **+ Add a group claim** in the **Attributes & Claims** section. Send the **Security groups**, using the source attribute **Group ID**. Use the word or phrase you selected when configuring Microsoft Entra ID security groups (such as Cortex XSIAM) to create a filter. Customize the name of the group claim as **memberOf**.

    ![Azure-memberof-Group-8.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-c089d4f3411e072709edfc8c66bf8bfabf3662ba%2F6f50e9f9f45b3ca78660c01afd8b892b38a44f64cc8ab0cf74b9379c1323325c.png?alt=media)
5. In addition to group membership, verify that there are also claims for:
   * Email address
   * First Name
   * Last Name

</details>

<details>

<summary>Task 4. Copy Login URL, Microsoft Entra ID Identifier, and Attribute Claims</summary>

1.  In Microsoft Entra ID, from the **Single sign-on** page, in the **Set up Cortex XSIAM Production** section, copy the values for the **Login URL** and **Microsoft Entra ID Identifier**. You need these values to configure the SSO Integration in Cortex XSIAM.

    ![Azure-XSOAR-Settings-8.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-b0ce012448027c1e7cdf40dfc4eb8f3125224369%2F2d47e9f2ab42dda32880a4cb8120a91af116d242a4481376554d286e2890e41d.png?alt=media)
2.  **Edit** **Attributes & Claims** and copy the values in the **Claim name** column. The claim name is case sensitive. You need these values to configure the SSO Integration in Cortex XSIAM.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>The default attributes shown on the main single sign-on page in Microsoft Entra ID are not the values you need. You must click <strong>Edit</strong> next to <strong>Attributes and Claims</strong> to view and copy the actual values.</p></div>

    ![Azure-claim-names-8.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-5ab8d9abf01fbe6bf33cc0bd1702a89e95869388%2F8a8b69cf57443281440354a935aca2b2e9666103068f99e23ae272024fb8a585.png?alt=media)

</details>

<details>

<summary>Task 5. Download the Certificate</summary>

From the SAML Certificates section in Microsoft Entra ID, **Download** the **Certificate (Base64)**. You need the contents of this file to configure the Cortex XSIAM SSO Integration.

![Azure-download-certificate-8.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-8ad69d3e110b2fe82439a8b351cc57cc1a40cec7%2F2325737f0859508b8178d05f118eef0d26e6a6d03af19b61c840f0efe7d01f70.png?alt=media)

</details>

<details>

<summary>Task 6. Copy the Source IDs for Microsoft Entra ID Security Groups</summary>

The claim for the [membership attribute](#UUID-1192642a-c44e-58e5-4af1-b3654ab2e41a_N1698222696896) that is sent to Cortex XSIAM uses the **Object Id** of the group. The **Object Id** is different from the Microsoft Entra ID security group name. You can find the **Object Id** for each of your Microsoft Entra ID security groups by navigating to **Users and groups** in Microsoft Entra ID, clicking on the group name, and viewing the **Object id**. Create a list of the group names and corresponding **Object Ids** for every Microsoft Entra ID security group you want to map to a Cortex XSIAM user group.

</details>

<details>

<summary>Task 7. Configure the Cortex XSIAM SSO Integration</summary>

1. In Cortex XSIAM go to Settings → Configurations → Access Management → **Authentication Settings**.
2.  In the **Login Options** tab, toggle **SSO Disabled** to on.

    By default, SSO is disabled in Cortex XSIAM.
3. Expand the **SSO Integration** settings.
4.  Use the following table to complete the SSO Integration settings, based on the values you saved from Microsoft Entra ID.

    | Microsoft Entra ID                           | Cortex XSIAM Field |
    | -------------------------------------------- | ------------------ |
    | Login URL                                    | IdP SSO URL        |
    | Microsoft Entra ID Identifier                | IdP Issuer ID      |
    | Contents of the downloaded certificate file. | X.509 Certificate  |
5.  In the **IdP Attributes Mapping** section, enter the attribute claim names from Microsoft Entra ID. The names are case sensitive and must match exactly.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>The attribute claim name must exactly match the value sent by your IdP. In some cases, this may be the full attribute name/namespace, depending on the configuration of our IdP</p></div>

    ![Azure-XSOAR-Attributes-8.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-47afc425dbbded48a09af338f5c3444e4724044b%2F94f233633ba78bd359a0d21be1be07f2322dadb5b580fe7a67ac0bebcd55dbe1.png?alt=media)
6. (Optional) Under **Advanced Settings**, select the checkboxes for **ADFS** and **Compress encode URL (ADFS)**. In some circumstances, these fields may be required by your Microsoft Entra ID configuration.
7. Save your settings.

</details>

<details>

<summary>Task 8. Map SAML Group Memberships to Cortex XSIAM User Groups</summary>

1. Select Settings → Configurations → Access Management → **User Groups**.
2. Right-click a user group and select **Edit Group**.
3. In the **SAML Group Mapping** field add the Microsoft Entra ID group(s) Object Ids that should be associated with this user group. Multiple Object Ids should be separated with a comma. The Microsoft Entra ID group Object Id must match the exact value sent in the token.
4. Save your settings.
5. Repeat for each user group.

</details>

<details>

<summary>Task 9. Test SSO Login</summary>

1.  Go to the Cortex XSIAM tenant URL and **Sign-In with SSO**.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>When using SAML 2.0, users are required to authenticate by logging in directly at the tenant URL. They cannot log in via Cortex Gateway.</p></div>
2. After authentication to Microsoft Entra ID, you are redirected again to the Cortex XSIAM tenant.
3.  When logged in, validate that you have been assigned the proper roles.

    To view your role and any role assigned to a user group you are a member of, click your name in the bottom left-hand corner, and click **About**.

</details>
