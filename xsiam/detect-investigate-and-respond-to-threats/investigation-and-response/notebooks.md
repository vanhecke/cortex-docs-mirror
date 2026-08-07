---
description: >-
  Leverage the data collected by Cortex XSIAM using Jupyter Notebooks' data
  analysis and visualization capabilities within your existing security
  infrastructure.
---

# Notebooks

Jupyter Notebooks provide security analysts and threat hunters with a highly flexible, code-based environment for deep security data analysis. Integrated directly into Cortex XSIAM, these Notebooks, powered by the Jupyter framework, enable users to combine live code (primarily Python for data science and machine learning), XQL queries, and generate more advanced visualizations into a single, shareable document.

Using Jupyter tools, you can build machine learning models to visualize clusters, identify anomalies, and then feed your findings into the Cortex XSIAM environment to generate security insights. Notebooks serve as a crucial tool for transforming raw security telemetry, which Cortex XSIAM collects from endpoints, networks, and cloud environments, into actionable threat intelligence and custom detection models.

Although you can use the XQL Query, Notebook is designed for advanced statistical analysis. In particular, you can do the following:

* Create customized analytics and bring your own machine learning models into Cortex XSIAM.
* Utilize existing public resources.
* Visualize analytics using existing libraries and applications.
* Document, automate, and reuse hunting processes.
* Use the existing data manipulation and visualization tools to identify patterns, anomalies, and trends in the data.
* Automate the custom investigation process and make it available as part of a case with actions, such as creating issues and adding a comment to a case.

{% hint style="info" %}
You need a daily minimum of 1000 compute units. After activation, 1,000 units are deducted daily at 00:00 UTC.

XQL and BQ queries performed in Cortex XSIAM Notebooks are calculated similarly to Compute Unit usage of XQL queries originating from public APIs. You can't create a Jupyter instance without sufficient Compute Units.

Based on your security analysis and data volume requirements, you may need to increase your allocated Compute Units to support extensive analysis, complex queries, or frequent usage of the Notebooks.
{% endhint %}

#### Example: Advanced Visualizations - PyGWalker

PyGWalker is a Python library that allows you to turn a Pandas DataFrame into an interactive, Tableau-like user interface for visual data exploration, all within the Jupyter environment. A threat hunter can quickly drag and drop variables (like user\_name, source\_ip, event\_type) to visually identify anomalies, spikes, or patterns in large volumes of log data without writing dozens of complex visualization scripts.

![notebook\_pyg.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-0adc946f8221dca12ced8d03c37150575c0c585f%2F14da7264cd043f38a29c10e3ac0898579b39c0b0f9388d12483825de9a7a7b9d.png?alt=media)

### Set up the Jupyter Notebook in Cortex XSIAM

{% hint style="info" %}
This is an admin task.
{% endhint %}

Before you begin, ensure that you have the **View/Edit** permissions in **Settings** → **Configurations** → **Access Management** → **Roles** → **Configurations** → **Apps**. This enables an administrator to perform initial setup of the Notebooks instance, manage integration settings, and configure the Notebooks environment.

{% hint style="info" %}
The Instance Administrator role has these permissions by default.
{% endhint %}

1. In Cortex XSIAM, select **Settings** → **Configurations** → **Integrations** → **Apps**.
2.  Click **Install**.

    Cortex XSIAM displays a notification that the instance is being prepared, which may take time.

    When completed, the instance is available in the navigation menu under **Apps**.
3.  Review the **App Service Account** role.

    When you create a Notebooks instance, the API key is assigned the **App Service Account** role.

    This API key is used by the underlying service (the Notebooks container environment) to communicate with Cortex XSIAM's APIs to retrieve data using XQL queries. The **App Service Account** role is generally designed for API consumption by applications or integrations. Its default permissions allow it to view and triage cases/issues and support public APIs relevant for apps. The **App Service Account** role relies on default unrestricted access.

    The Notebook functions via an API key assigned to this role. If the role tied to that key is missing the dataset permission, the code will fail with an authorization error, even if an analyst can run the same query in the Query Builder. If so, you should do the following:

    1. Duplicate the **App Service Account** role and add the new dataset permissions.
    2. Update the API key with the new role.
    3. Add the API Key with the new role to the Notebook by hovering over **Notebooks** and selecting the edit icon.

{% hint style="info" %}
* You can only add one instance of Notebooks.
* Notebooks have access to approved sites on the internet when embedded in Cortex XSIAM.
* To delete the Notebook, hover over **Notebooks** and select the delete icon.
* Installing or uninstalling some plug-ins and packages requires the Notebooks server to refresh the web page. For these actions, go to **File** → **Shut Down** , and then refresh the page.
{% endhint %}

### Access and build Notebooks

Once the instance is provisioned, any authorized user can access the environment.

Before you begin, ensure you have the following permissions:

* **View/Edit** permissions in **Settings** → **Configurations** → **Access Management** → **Roles** → **Apps** → **Jupyter**. This enables you to open the Notebooks application and create, view, edit, and execute code with notebooks.
* To query data, you must be granted at least read access to the specific XDL datasets the notebook will use for analysis.

1.  Select **Investigation and Response** → **Notebooks**.

    The JupyterLab or Jupyter Notebook interface launches within the tenant.
2.  You can now create a new notebook and use Python (along with security-focused Python libraries and the XSIAM platform's data connectors) to query XSIAM data using XQL.

    Every notebook you create is preconfigured with Cortex SDK access, enabling you to query the data using it.
