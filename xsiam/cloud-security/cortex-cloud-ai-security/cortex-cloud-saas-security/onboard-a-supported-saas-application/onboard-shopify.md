---
description: >-
  Onboard Shopify to Cortex XSIAM for SaaS security posture monitoring and
  compliance visibility.
---

# Onboard Shopify

SaaS Security connects to the Shopify API using an API token generated from a custom Shopify app. Creating a custom app ensures the token is scoped to only the permissions SaaS Security requires. After connecting, SaaS Security scans your Shopify store for misconfigured settings and account risks.

**Note**: These steps onboard a single Shopify store. To scan multiple stores, onboard each store separately. The supported Shopify account plan for SaaS Security scans is the Shopify Plus plan.

The onboarding process requires the following credentials:

| Item       | Description                                                                                                                                                                                    |
| ---------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| API Token  | A unique alphanumeric string that Shopify generates for a custom app you create. SaaS Security uses this token to authenticate to the Shopify API with the scopes specified in the custom app. |
| Store Name | The permanent subdomain identifier for your store, derived from the default URL Shopify assigned: \<store-name>.myshopify.com.                                                                 |

***

#### Step 1 — Identify the Shopify account

Identify the Shopify account you will use to create the custom app.

Required permissions: The account must be assigned to the Organization Owner role to create a custom app and generate an API token.

***

#### Step 2 — Create a custom app and generate an API token

1. Open a browser to the [Shopify admin login page](https://admin.shopify.com/) and log in to the store you want SaaS Security to scan.
2. Click Settings in the lower-left corner to open store settings.
3. From the left navigation pane, select Apps and sales channels.
4. Click Develop apps.
5. Click Create app.
6. In the Create an app dialog, enter a name for the app and click Create app. Shopify displays a tabbed configuration page for the new app.
7. On the Configuration tab, configure the Admin API Integration scopes:
   1. Click Configure under Admin API Integration.
   2. Select the following scopes:

* read\_apps
* read\_privacy\_settings

**Note**: The read\_users scope is also required but is restricted by default and not available for selection here. You will request access to this scope from Shopify Plus Support in a later step.

8. Click Save.
9. On the API credentials tab, click Install app, then confirm by clicking Install in the dialog.
10. Contact Shopify Plus Support to request access to the read\_users scope for your app:
    1. In the upper-right corner of the page, locate your store's brand name (default: My Store) and select \<brand-name> > Shopify Plus Support.
    2. Click Chat with us and ask the support agent to enable the read\_users scope for your application.

It can take a few minutes to an hour for Shopify Plus Support to enable the scope.

11. After Shopify Plus Support enables read\_users, add the scope to your app:
    1. On the Configuration tab, click Edit under Admin API Integration.
    2. Select the read\_users scope.
    3. Click Save.
12. On the API credentials tab, click Reveal token once to display the API token.
13. Copy the API token and save it to a text file.

**Note**: Do not proceed until you have copied the API token. You must provide it during the onboarding process.

***

#### Step 3 — Identify your store name

Your store name is the subdomain of the default URL Shopify assigned when you created the store (\<store-name>.myshopify.com).

1. Click Settings in the lower-left corner to open store settings.
2. In the left navigation pane, locate the default URL for your store. The store name is the value before .myshopify.com.

***

#### Step 4 — Connect SaaS Security to Shopify

1. Log in to [Cortex](https://cortex.paloaltonetworks.com).
2. Select **Settings > Data Sources and Integrations > Add New** and click the Shopify tile.
3. On the **Capabilities** tab, enter a name for this instance.
4. Under Default Capabilities, confirm Security Posture is selected.
5. Click Next.
6. On the **Connections** tab, select Log in with Credentials.
7. Enter your API Token and Store Name.
8. Click Next.
9. On the Configurations tab:
   1. Set the Sync Interval.
   2. (Optional) Add a Tag.
10. Click **Next** to complete onboarding.
