---
description: Connect a Mural instance to detect posture risks and compliance violations.
---

# Onboard Mural

For SaaS Security to detect posture risks in your Mural instance, you must onboard your Mural instance to SaaS Security. Through the onboarding process, SaaS Security connects to a Mural API by using an Enterprise API key. You generate this key from the Company Dashboard in Mural. After connecting to the Mural API, SaaS Security scans your Mural instance for misconfigured settings and account risks.

The supported Mural account plan for SaaS Security scans is the Enterprise plan. This plan is required for you to create an Enterprise API key.

To onboard your Mural instance, SaaS Security requires the following information, which you specify during the onboarding process.

| Item    | Description                                                                                                                                                                                                                                                       |
| ------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| API Key | A generated character string that gives SaaS Security access to Mural's Enterprise API. You configure this key to limit SaaS Security' access to only the scopes it requires. Required permissions: You must be a Company Admin to create the Enterprise API key. |

To onboard your Mural instance, complete the following actions.

***

### Step 1: Identify the Mural Account

Identify the Mural account that you will use to generate the Enterprise API key.

Required permissions: The account that generates the API key must be assigned to the Company Admin role in Mural.

***

### Step 2: Log In to Mural

Open a web browser to the [Mural login page](https://app.mural.co/) and log in to the account you identified.

***

### Step 3: Generate and Copy the Enterprise API Key

1. Navigate to the Company Dashboard in Mural. Locate your avatar in the upper-right corner of the Mural page and select \<your-avatar> > Manage company.
2. From the Company Dashboard's left-hand navigation pane, select API keys. The API keys item appears under the Development section.
3. On the API Keys page, click Create API Key. The Create API key dialog prompts you to select the API scopes that the key will authorize SaaS Security to access.
4. In the Create API key dialog, select the following scopes, which SaaS Security requires:

* Member information
* User activity logs
* Reports

5. Click Create API key. Mural generates and displays the Enterprise API key.
6. Copy the API key and paste it into a text file.

Note: Do not continue to the next step unless you have copied the API key. This is the only time that Mural displays the API key, and you must provide this key to SaaS Security during the onboarding process.

***

### Step 4: Connect SaaS Security to Your Mural Instance

By adding a Mural app in Cortex, you enable SaaS Security to connect to your Mural instance.

1. Log in to Cortex.
2. Select **Settings > Data Sources and Integrations > Add New**. You can use the Search bar to find the app you want to connect to.
3. Click the Mural tile.
4. Under **Capabilities**, enter a name for your application.
5. Select Security Posture under Default Capabilities and click Next.
6. Under **Connections**, enter your API key.
7. Under **Configurations**, select a **Sync Interval**. Choose a meaningful **Tag** to distinguish between various applications in different environments.
8. Click **Next** to complete the onboarding validation process.
