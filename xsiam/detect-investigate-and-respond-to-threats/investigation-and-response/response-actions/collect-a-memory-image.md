---
description: >-
  Collect endpoint memory images in Cortex XSIAM for forensic investigation and
  analysis.
---

# Collect a memory image

{% hint style="info" %}
This functionality requires a Forensics add-on license.
{% endhint %}

Certain forensic artifacts exist only in the computer’s memory, such as volatile data created by running processes. The **Memory Collection** option enables Cortex XSIAM to capture the memory of a Windows endpoint. After the memory image has been captured from the Cortex XSIAM endpoint, the image is available to download. Use the image to perform a full analysis using industry-standard tools.

### How to collect a memory image

1. From the **Action Center** select **Run Action** → **Memory Collection**.
2. Select the target Windows endpoint from which you want to collect the memory image (only one endpoint at a time). Click **Next**.
3.  Review the summary and initiate the action.

    A summary of the memory collection action is displayed. If you need to change your settings, click **Back**. If all the details are correct, click **Done**. The **Memory Collection** action is added to the **Action Center**.
4.  Review the collection results.

    In the **Action Center**, you can monitor the action progress in real-time and view the status for the target endpoint. For a detailed view of the results, right-click the action and select **Additional data**. Cortex XSIAM displays the action, timestamp, and real-time status of the action on the target endpoint.
5.  Download the file of the image.

    In the **Detailed Results - Memory Collection** screen, right-click the action and select **Download files**.

    The file is downloaded to the local computer.
