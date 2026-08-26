---
description: >-
  Connect a Sumo Logic instance in Cortex XSIAM to detect posture risks and
  compliance violations.
---

# Onboard Sumo Logic

SaaS Security connects to the Sumo Logic API using an access key that you generate as the Sumo Logic account owner. After connecting, SaaS Security Checks scans your Sumo Logic instance for misconfigured settings and account risks.

Note: The supported Sumo Logic account plan for SaaS Security scans is the Enterprise plan.

The onboarding process requires the following credentials:

| Item             | Description                                                                                             |
| ---------------- | ------------------------------------------------------------------------------------------------------- |
| Admin Access ID  | A unique alphanumeric string that identifies the access key pair — analogous to a user ID.              |
| Admin Access Key | The secret credential SaaS Security Checks uses to authenticate API requests — analogous to a password. |
| Endpoint Region  | The region where Sumo Logic hosts your data.                                                            |

***

#### Step 1 — Generate a Sumo Logic access key

1. Identify the Sumo Logic account you will use to generate the access key.

Required permissions: You must generate the access key from the account designated as the Sumo Logic account owner — either the user who registered the account or a user later designated as owner.

2. Log in to Sumo Logic as the account owner.
3. Navigate to your preferences: click your profile icon in the upper-right corner and select \<profile-icon> > Preferences.
4. Select the Personal Access Keys tab and click Add Access Key.
5. In the Add New Access Key window, enter a meaningful name for the key — for example, SaaS-Security-Integration.
6. Under Scopes, select the Custom option and select the following scopes:

**Note**: Because the access key is generated from the account owner (highest privilege level), explicitly limit the key's permissions to the minimum required by SaaS Security Checks.

* Access Keys - View
* Access Keys - Manage
* Users And Roles - View
* Users And Roles - Manage
* Content admin
* Manage Library
* Run Log Search - View/Manage
* View Collectors
* View Security Settings
* View Account Status

7. Click Save. Sumo Logic generates the key and displays the Access ID and Access Key.
8. Copy the Access ID and Access Key and save them to a text file.

**Note**: Do not proceed until you have copied both values. You must provide them during onboarding.

***

#### Step 2 — Identify your endpoint region

Use the following table to determine your region based on your Sumo Logic login URL:

| URL                       | Region              |
| ------------------------- | ------------------- |
| api.au.sumologic.com      | AU (Australia)      |
| api.ca.sumologic.com      | CA (Canada)         |
| service.de.sumologic.com  | DE (Germany)        |
| service.eu.sumologic.com  | EU (European Union) |
| service.fed.sumologic.com | FED (US Government) |
| service.in.sumologic.com  | IN (India)          |
| service.jp.sumologic.com  | JP (Japan)          |
| service.sumologic.com     | US1 (United States) |
| service.us2.sumologic.com | US2 (United States) |

***

#### Step 3 — Connect SaaS Security Checks to Sumo Logic

1. Log in to [Cortex](https://cortex.paloaltonetworks.com).
2. Select **Modules > SaaS Security > Add Data Source** and click the Sumo Logic tile.
3. On the **Capabilities** tab, enter a name for this instance.
4. Under Default Capabilities, confirm Security Posture is selected.
5. Click Next.
6. On the **Connections** tab, select Log in with Credentials.
7. Enter your Admin Access ID, Admin Access Key, and Endpoint Region.
8. Click Next.
9. On the **Configurations** tab:
   1. Set the **Sync Interval**.
   2. (Optional) Add a **Tag**.
10. Click **Next** to complete onboarding.
