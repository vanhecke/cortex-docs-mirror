---
description: Navigate the Cortex XSIAM Parsing Rules editor.
---

# Parsing Rules editor views

{% hint style="warning" %}
### Prerequisite

Parsing Rules requires **View/Edit** RBAC permissions for **Data Management** (under **Configurations** → **Data Management**), which are the same permissions required for Dataset Management, Data Model Rules, and Event Forwarding.
{% endhint %}

The Parsing Rules editor contains the following views:

* **User Defined** (default): Displays an editor for writing your own custom parsing rules that override or extend the default rules and a **List of Errors** section to help you troubleshoot errors in your Parsing Rules.
* **Default Rules**: Displays the parsing rules that are provided by default with Cortex XSIAM in read-only mode and a **List of Errors** section to view any errors in your Parsing Rules.Any Parsing Rules that are included with your installed Content Packs from the Marketplace are also listed under Installed Rules.
* **Both**: Side-by-side view of both the **Default Rules** and **User Defined** rules, so you can easily view the different rules on one screen. In addition, the **List of Errors** section helps you troubleshoot any errors in your Parsing Rules.
* **Simulate**: Enables you to test your Parsing Rules on actual logs and validate their outputs, which helps minimize your errors when creating Parsing Rules. The editor includes the following sections.
  * **User defined**: A list of the current **User defined** rules on the left side of the window.
  * **XQL Samples**: A table of the existing Cortex Query Language (XQL) raw data samples on the right side of the window, which contain sample logs listing the **Vendor**, **Product**, **Raw Log**, and **Sample Time**. For each **Vendor** and **Product**, up to 5 different samples are available to choose from. From this list, you can select the logs used to simulate the rule.
  * **Logs Output**: Displays in a table format the following columns per dataset at the bottom of the window.
    * **Dataset**: Displays the applicable dataset name and a line number associated to this dataset in the **User defined** section.
    * **Vendor**: The vendor associated with this dataset.
    * **Product**: The product associated with this dataset.
    * **Logs Output**: Displays the output logs that are available based on your **User defined** rules and **XQL Samples** selected after simulating the results. When there is no output log to display, the text `Output logs is not available` with the corresponding error message is displayed. When there is no output due to a missing rule in the **User defined** section for the logs selected, the text **No output logs. You can change your parsing rules and try again** is displayed.
    * **Input Logs**: Displays the relevant input log with a right-click pivot to **Show diff** between the **Output Logs** and **Input Logs**.
