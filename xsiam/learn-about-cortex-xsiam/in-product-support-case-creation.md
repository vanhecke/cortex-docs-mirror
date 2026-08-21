---
description: >-
  Open a support ticket directly in Cortex XSIAM and record your console to
  capture your issues and have the ticket handled efficiently.
---

# In-product support ticket creation

To simplify the process of creating a support ticket, you can open a support ticket directly in Cortex XSIAM. Opening the ticket in Cortex XSIAM allows all of the relevant context to be included, such as the option to record the console and upload relevant logs. When relevant, Cortex XSIAM will create and send the agent tech support file (TSF) for the endpoint you select. All relevant data about your tenant is logged and included in the support ticket, including license details. Using the **Submit Support Ticket** wizard makes it easier for you to include all of the necessary details and log files while first submitting your support ticket, thereby enabling the support team to solve it more quickly and easily.

{% hint style="info" %}
If you have the Cortex Agentic Assistant enabled, when you click **Help**, you have two options: **Documentation Portal** and **Initiate Support Request**. If you select **Initiate Support Request,** the **Help Center** agent opens to assist with finding relevant documentation, troubleshooting, and creating a support ticket. After your first prompt to the **Help Center** agent, you can click **Submit support ticket** above the chat. If you click **Submit Support Ticket**, you are brought directly to the **Submit Support Ticket** wizard.

If you do not have the Cortex Agentic Assistant enabled, when you click **Help**, you have two options: **Documentation Portal** and **Initiate Support Request**. If you select **Initiate Support Request,** you are brought directly to the **Submit Support Ticket** wizard.
{% endhint %}

To use the embedded support ticket feature, you must have a user account in the Customer Support Portal, and your Cortex XSIAM user must be granted the **Help** permission in Cortex Gateway.

{% stepper %}
{% step %}
From Cortex XSIAM, select **Help** → **Initiate Support Request**.
{% endstep %}

{% step %}
In the **Submit Support Ticket** wizard, enter the requested ticket information. Be precise when indicating the impact of the issue. When an issue is critical, you will be asked to input the most critical information so that support can understand the issue and start addressing it immediately.

{% hint style="info" %}
When opening a support ticket through the Customer Support Portal, you need to manually select Cortex XSIAM as the product. While there may be discrepancies between the categories in this wizard and the Customer Support Portal process, that's because this wizard is designed specifically to focus on options relevant to Cortex XSIAM.
{% endhint %}
{% endstep %}

{% step %}
When the issue you are opening a support ticket for is related to the agent, you can select the relevant endpoint. If you select the endpoint, Cortex XSIAM will create and send the TSF for the agent you selected, when possible.

{% hint style="info" %}
Selecting an endpoint from the endpoint table and retrieving TSF requires full **Retrieve Endpoint Data** permissions under **Endpoint Administration**.
{% endhint %}
{% endstep %}

{% step %}
To provide more context for your support ticket, you can record the Cortex XSIAM console directly from the support ticket wizard. If you choose to record the console, you can also opt to have the HAR file generated and sent to further assist support in solving the ticket. To record the console, select **Record Console**. To submit your support ticket without recording the console, select **Skip**.
{% endstep %}

{% step %}
If you choose to record the console, your browser may prompt you for permission for Cortex XSIAM to see the contents of the tab. To allow recording, select **Allow**. You can now recreate the issue in your Cortex XSIAM environment, and all of your actions are recorded. The console recording and HAR file generation only take place within the context of the browser tab that Cortex XSIAM is running in. When you are ready to stop recording, select **Stop Sharing**.

If you wish to recreate the recording, you must first delete the existing console recording by clicking the **x** symbol next to the **Console Recording**. Then select **Record Console**.

{% hint style="info" %}
Console recordings cannot exceed 10 minutes. The current recording time is displayed at the top of the window.
{% endhint %}
{% endstep %}

{% step %}
To submit the support ticket, click **Submit Support Ticket**.

While the ticket attachments are uploading, do not refresh or navigate away from Cortex XSIAM until you get a notification in the Notification Center that uploading is complete. In the meantime, you can close this wizard and continue working in Cortex XSIAM.

Once the support ticket is created successfully, the support ticket number is displayed, and you will receive an email notification from Palo Alto Networks Support. You can manage the support ticket and monitor its progress in the Customer Support Portal.
{% endstep %}
{% endstepper %}
