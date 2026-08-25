---
description: >-
  Onboard Slack Enterprise to Cortex XSIAM for SaaS security posture monitoring
  and compliance visibility.
---

# Onboard Slack Enterprise

SaaS Security connects to the Slack Enterprise API using a User OAuth Token generated from a Slack org-wide app that you create. A Slack org-wide app is deployed across all workspaces in your organization.

**Note**: The Slack Enterprise connector was updated in May 2025 to support the Identity Security dashboard. If you onboarded your Slack Enterprise instance before this update and want to view account risks in the Identity Security dashboard, you must re-onboard your Slack instance. Before re-onboarding, add the admin.users:read OAuth scope to your existing org-wide app.

Onboarding consists of two tasks:

1. Create an org-wide app and generate a User OAuth Token
2. Connect SaaS Security to your Slack Enterprise instance

***

#### Task 1 — Create an App for Accessing Your Slack Enterprise Instance

**Step 1 — Identify the administrator account**

Identify the Slack administrator account you will use to create the org-wide app.

Required permissions: The account must be assigned to the Org Admin role or a role with greater permissions, because you will install the app across all workspaces in your organization.

**Step 2 — Create the Slack app**

1. Log in to the Slack API console and navigate to the Your Apps page at [api.slack.com/apps](https://api.slack.com/apps).
2. Click Create New App.
3. In the Create an app dialog, select From scratch.
4. In the Name app & choose workspace dialog, enter a name for your app and select a workspace. You will configure the app in this workspace and later deploy it across your organization.
5. Click Create App. Slack Enterprise displays the configuration settings for your new app.

**Step 3 — Configure the app scopes and opt in to org-wide deployment**

1. Navigate to OAuth and Permissions settings and locate the Scopes section.
2. Under Bot Token Scopes, click Add an OAuth Scope and select team:read.
3. Navigate to Org Level Apps settings and click Opt in to the org apps program.
4. Navigate back to OAuth and Permissions settings and locate the Scopes section.
5. Under User Token Scopes, click Add an OAuth Scope and add the following scopes:
   1. admin.teams:read
   2. auditlogs:read
   3. team:read
   4. admin.users:read (required for identity scans)

**Step 4 — Install the app and copy the User OAuth Token**

1. In the OAuth and Permissions settings, locate the OAuth Tokens for Your Workspace section and click Install to Organization. Slack Enterprise generates tokens for your app.
2. Copy the User OAuth Token and save it to a text file.

**Note**: Do not proceed until you have copied the User OAuth Token. You must provide this token during onboarding when SaaS Security prompts you for an API Key.

***

#### Task 2 — Connect SaaS Security to Your Slack Enterprise Instance

1. Log in to [Cortex](https://cortex.paloaltonetworks.com).
2. Select **Settings > Data Sources and Integrations > Add New** and click the Slack Enterprise tile.
3. On the **Capabilities** tab, enter a name for this instance.
4. Under Default Capabilities, confirm Security Posture is selected.
5. Click Next.
6. On the **Connections** tab, enter your User OAuth Token in the API Key field.
7. Click Next.
8. On the **Configurations** tab:
   1. Set the **Sync Interval**.
   2. (Optional) Add a Tag.
9. Click **Next** to complete onboarding.
