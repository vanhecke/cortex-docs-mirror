---
description: Connect a YouTrack instance to detect posture risks and compliance violations.
---

# Onboard YouTrack

SaaS Security connects to the YouTrack API using a permanent token that you generate from a YouTrack administrator account. After connecting, SaaS Security scans your YouTrack instance for misconfigured settings.

Onboarding consists of two tasks:

1. Collect the instance name and generate a permanent token
2. Connect SaaS Security to YouTrack

The onboarding process requires the following credentials:

| Item            | Description                                                                                                                                                  |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Instance Name   | The unique subdomain that identifies your organization's YouTrack instance, as shown in your YouTrack URL: \<instance-name>.youtrack.cloud.                  |
| Permanent Token | A token generated from a YouTrack administrator account assigned to the System Admin role. The token must be scoped to YouTrack and YouTrack Administration. |

***

#### Task 1 — Collect Information for Accessing Your YouTrack Instance

**Step 1 — Identify your YouTrack instance name**

Open a browser and go to your YouTrack login page. Your instance name is the subdomain shown in the URL: \<instance-name>.youtrack.cloud.

**Note**: Record your instance name before proceeding. You must provide it during onboarding.

**Step 2 — Generate a permanent token**

1. Log in to YouTrack as an administrator assigned to the System Admin role.
2. Click your account avatar in the upper-right corner and select \<your-avatar> > Profile.
3. On your profile page, go to Account Security.
4. In the Tokens section, click New token.
5. In the New Permanent Token dialog:

* Enter a name for the token.
* Select the following scopes:
* YouTrack
* YouTrack Administration

6. Click Create. YouTrack displays the new permanent token.
7. Click Copy token and save it to a text file.

Note: Do not proceed until you have copied the token. You must provide it during onboarding.

***

#### Task 2 — Connect SaaS Security to YouTrack

1. Log in to [Cortex](https://cortex.paloaltonetworks.com).
2. Select **Settings > Data Sources and Integrations > Add New** and click the YouTrack tile.
3. On the **Capabilities** tab, enter a name for this instance.
4. Under Default Capabilities, confirm Security Posture is selected.
5. Click Next.
6. On the **Connections** tab, enter your Instance Name and Permanent Token.
7. Click Next.
8. On the **Configurations** tab:
   1. Set the Sync Interval.
   2. (Optional) Add a Tag.
9. Click **Next** to complete onboarding.
