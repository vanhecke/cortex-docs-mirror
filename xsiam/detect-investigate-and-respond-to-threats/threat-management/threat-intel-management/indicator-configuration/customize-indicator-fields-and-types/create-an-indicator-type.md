---
description: >-
  Create custom indicator types and configure their profiles, scripts, and field
  mappings.
---

# Create an indicator type

Indicators are categorized by indicator type, which determines the indicator layout and fields that are displayed and which scripts are run on indicators of that type. Cortex XSIAM includes several out-of-the-box indicator types, such as:

* IP Address
* Domain
* URL
*   File

    For information about file indicators and file hash configuration, review the indicator type settings.

When you create a new indicator type, you define its properties, including whether and how to format the indicator data and how the verdict is calculated.

1. Go to Settings → Configurations → Object Setup → Indicators → **Types**.
2. Click **New**.
3.  In the **Settings** tab, add the required indicator profile, such as name and Regex.

    For more information, see [Indicator type profile](create-an-indicator-type/indicator-type-profile).
4.  In the **Custom Fields** tab, map the fields, as required.

    For more information, see [Map custom indicator fields](create-an-indicator-type/map-custom-indicator-fields).

Example 191. Create a company email indicator type

The following example describes how to create a new indicator type to manage employee emails, for example for resource management or inside threat investigation.

Create a new indicator type for the employee email addresses which contain the “our\_company.com” company domain.

1. Under Settings → Configurations → Object Setup → Indicators → **Types** → **New**, in the **Settings** tab, define the following.
   * Name: Company email
   * Regex: `.*?@our_company.com` (simplified to capture all the email addresses using the our\_company.com domain).
   * Reputation command: Not relevant for this example, since we don't want any external enrichment.
   * Formatting script: If more formatting is needed, you can use a formatting script to edit the saved value.
   * Reputation script: If needed, you can create a reputation script to affect the DBot score given to the new custom indicator.
2.  In the **Custom Fields** tab, map custom fields for the new indicator type.

    You can map fields returned using an integration such as Active Directory to obtain more data about the actual user to whom the email belongs. You can also collect data using integrations such as Okta (MFA, SSO), SIEM, and email security. Fields such as **Username**, **Full name**, and various groups the user is part of as well as other identifiers are returned to context and mapped into the indicator using the custom fields.

    ![use-case-custom-indicator-type-mapping.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-e5cacb18f289dff366533e2a41fbe53a0cee5614%2F6cb827f28e337b847fe751688832ce5fb2bd6b7d9c48c03ee7f7e2771dd492b5.png?alt=media)

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>If you miss mapping any field, you can create additional new indicator fields and either relate them to all indicator types, or relate them only to the new indicator type (recommended).</p></div>
