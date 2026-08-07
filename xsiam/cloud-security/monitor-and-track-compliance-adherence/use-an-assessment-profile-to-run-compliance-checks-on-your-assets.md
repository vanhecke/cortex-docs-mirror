---
description: >-
  Create assessment profiles to check asset groups against selected compliance
  standards.
---

# Use an assessment profile to run compliance checks on your assets

## What is a compliance assessment profile?

The compliance assessment profiles are configurations that define which standard to run on which asset group. An assessment profile runs scans on asset groups to check whether the assets adhere to a specific standard.

Compliance assessment profiles can be managed from **Posture Management → Compliance → Assessment Profiles.**

## Create a new assessment profile

To create a new assessment profile, select a compliance standard and one or more asset groups you want to run it on.

1. Under **Posture Management → Compliance → Assessment Profiles**, click **Create New Assessment**.
2. Define assessment profile metadata, including:
   * Profile name
   * Description (optional)
   * Optionally schedule generating a report.
     1. Enter one or more report email recipients, clicking `enter` or
     2. Set the cadence for the report generation.
3. Click **Next**.
4. Select a compliance standard to associate with the assessment profile.
5. Select an asset group to run the standard against.
6. Click **Next**.
7. Review the profile details in the **Summary** and click **Create**.\
   \
   The assessment profile evaluates the compliance posture and generates a report at the optionally defined cadence, and sends it to the defined emails.

## Manage existing assessment profiles

Compliance assessment profiles can be managed from **Posture Management → Compliance → Assessment Profiles.** Right click on the profile to disable, edit, or delete an existing profile.
