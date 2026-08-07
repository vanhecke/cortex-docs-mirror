---
description: >-
  Connect a Contentful instance to detect posture risks and compliance
  violations.
---

# Onboard Contentful

For SaaS Security to detect posture risks in your Contentful instance, you must onboard your Contentful instance to SaaS Security. Through the onboarding process, SaaS Security connects to an API to scan your Contentful instance for misconfigured settings. If there are misconfigured settings, SaaS Security suggests a remediation action based on best practices.

SaaS Security gets access to Contentful's content management API by using a personal access token that you generate for a Contentful administrator account. During the onboarding process, SaaS Security prompts you for the personal access token.

To onboard your Contentful instance, complete the following actions:

* Create a personal access token in Contentful
* Connect SaaS Security to your Contentful instance

***

### Step 1: Create a Personal Access Token in Contentful

In Contentful, create a personal access token for an administrator account. The access token enables SaaS Security to carry out actions that require administrator permissions.

1. Open a web browser and go to the Contentful login page at [be.contentful.com/login](https://be.contentful.com/login).
2. Log in as an administrator.
3. Locate your profile icon and select \<profile-icon> > Account settings.
4. On the Account Settings page, navigate to the CMA Tokens tab and click Create personal access token.
5. In the Create personal access token dialog, specify a name and expiration date for the access token. You can also specify that the token should never expire.

**Note**: SaaS Security uses the access token to establish the initial connection to your Contentful instance and to perform scans at regular intervals. These scans will fail after the token expires, and you will need to onboard your Contentful instance again.

6. Click Generate. Contentful generates and displays your personal access token.
7. Copy the generated token and paste it into a text file.

Note: Do not continue to the next step unless you have copied the access token. You must provide this token to SaaS Security during the onboarding process.

***

### Step 2: Connect SaaS Security to Your Contentful Instance

By adding a Contentful app in Cortex, you enable SaaS Security to connect to your Contentful instance.

1. Log in to Cortex.
2. Select **Settings > Data Sources and Integrations > Add New**. You can use the Search bar to find the app you want to connect to.
3. Click the Contentful tile.
4. Under **Capabilities**, Enter a Name for your application.
5. Select Security Posture under Default Capabilities and click Next.
6. Under **Connections**, enter your personal access key.
7. Under **Configurations**, select a Sync Interval. Choose a meaningful **Tag** to distinguish between various applications in different environments.&#x20;
8. Click **Next** to complete the onboarding validation process.
