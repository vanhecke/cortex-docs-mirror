---
description: Connect a Sentry instance to detect posture risks and compliance violations.
---

# Onboard Sentry

SaaS Security connects to the Sentry API using a personal access token that you generate from a Sentry account. After connecting, SaaS Security scans your Sentry instance for misconfigured settings and account risks.

**Note**: The supported Sentry account plan for SaaS Security scans is the Business Plan.

The onboarding process requires the following credential:

| Item           | Description                                                                                                                                                                              |
| -------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Personal Token | A personal access token generated from a Sentry account. This unique alphanumeric string gives SaaS Security read-only access to organization and member data for a Sentry organization. |

***

#### Step 1 — Generate a personal access token

1. Identify the Sentry account you will use to generate the token.

Required permissions: No elevated permissions are required, but the account must be a member of the organization you want SaaS Security to scan.

2. Open a browser to the [Sentry login page](https://sentry.io/auth/login/) and log in to the account you identified.
3. On the Sentry dashboard, open the account drop-down menu in the upper-left corner and select Personal Tokens.
4. On the Personal Tokens page, click Create New Token.
5. Select the following permission scopes for the token:

* member:read
* org:read

6. Enter a name for the token — for example, SaaS-Security-Integration-Token — then click Create Token.
7. Copy the personal access token and save it to a text file.

**Note**: Do not proceed to the next step until you have copied the personal token. You must provide this token during the onboarding process.

***

#### Step 2 — Connect SaaS Security to Sentry

1. Log in to [Cortex](https://cortex.paloaltonetworks.com).
2. Select **Settings > Data Sources and Integrations > Add New** and click the Sentry tile.
3. On the **Capabilities** tab, enter a name for this instance.
4. Under Default Capabilities, confirm Security Posture is selected.
5. Click Next.
6. On the **Connections** tab, select Log in with Credentials and enter your personal token.
7. Click Next.
8. On the Configurations tab:
   1. Set the Sync Interval.
   2. (Optional) Add a Tag.
9. Click **Next** to complete onboarding.
