---
description: >-
  Connect a Businessmap instance in Cortex XSIAM to detect posture risks and
  compliance violations.
---

# Onboard Businessmap

For SaaS Security to detect posture risks in your Businessmap (formerly Kanbanize) instance, you must onboard your Businessmap instance to SaaS Security. Through the onboarding process, SaaS Security connects to a Businessmap API by using an API key that you generate from a Businessmap account. After connecting to the Businessmap API, SaaS Security scans your Businessmap instance for misconfigured settings and account risks.

To access your Businessmap instance, SaaS Security requires the following information, which you specify during the onboarding process.

<table data-header-hidden><thead><tr><th width="290">Item</th><th>Description</th></tr></thead><tbody><tr><td>API Key</td><td>A generated character string that identifies a Businessmap administrator to the Businessmap API. SaaS Security requires this API key to authenticate to the API. The key inherits the permissions of the administrator who creates it. Required permissions: The user who generates the API key must have the following Admin privileges: Manage Integrations, Access Audit Logs.</td></tr><tr><td>Host name</td><td>A unique subdomain for your Businessmap instance, which appears as part of your Businessmap URL.</td></tr></tbody></table>

To onboard your Businessmap instance, complete the following actions.

***

### Step 1: Identify the Businessmap Account for API Key Generation

Identify the Businessmap account that you will use to generate the API key.

Required permissions: The account that generates the API key must have the following Admin privileges:

* Manage Integrations
* Access Audit Logs

***

### Step 2: Log In to Businessmap

Open a web browser to the [Businessmap login page](https://businessmap.io/) or your unique company subdomain URL, and log in to the account you identified.

***

### Step 3: Identify Your Host Name

After you log in to Businessmap, your host name appears as a unique subdomain in the URL. For example, \<subdomain>.kanbanize.com.

Note: Make note of your host name before you continue to the next step. You will provide this host name to SaaS Security during the onboarding process.

***

### Step 4: Generate and Copy an API Key

1. Click your profile icon in the top-right corner of the page and select API. Businessmap opens your My Account settings to the API tab.
2. If an API key was already generated for the account, it is shown on the API tab. If not, click Generate API key.
3. Copy your API key and paste it into a text file.

Note: Do not continue to the next step unless you have copied your API key. You will provide this key to SaaS Security during the onboarding process.

***

### Step 5: Connect SaaS Security to Your Businessmap Instance

By adding a Businessmap app in Cortex, you enable SaaS Security to connect to your Businessmap instance.

1. Log in to Cortex.
2. Select **Settings > Data Sources and Integrations > Add New**. You can use the Search bar to find the app you want to connect to.
3. Click the Businessmap tile.
4. Under **Capabilities**, Enter a Name for your application.
5. Select **Security Posture** under Default Capabilities and click Next.
6. Under **Connections**, provide the API key and Host ID.
7. Under **Configurations**, select a **Sync Interval**. Choose a meaningful **Tag** to distinguish between various applications in different environments.
8. Click **Next** to complete the onboarding validation process.

<br>
