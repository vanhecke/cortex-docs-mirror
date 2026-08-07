# Cortex DLP threat detection and issues

The Cortex DLP module prevents sensitive data exfiltration. If instances of data-in-motion rules have been violated, a DLP issue is generated. To view the DLP Issues, go to **Data Security** → **Data Security Issues** → **Threats**. The **Detection Method** is set to DLP.

DLP issues provide visibility into instances where [data-in-motion rules](../configure-dlp-end-to-end#create-data-in-motion-rules) have been violated.

From **Data Security** → **Data Security Issues** → **Threats**, you can view the DLP issues. The **Detection Method** is set to DLP.

{% hint style="info" %}
### Note

Access to this page is restricted to users with the roles: Data Security Admin, Instance Administrator, and Account Admin.
{% endhint %}

The parameters configured during rule creation are shown as issue attributes on this page. These include:

* **Name**: Taken from the **Raised Issue Name** field defined when creating the rule.
* **Severity**: The assigned severity level of the Issue.
* **Description**: The predefined description from the rule.
* **Detection method**: When an issue arises from a data-in-motion rule violation, its **Detection Method** is **DLP**.
* **Action**: How the rule responded to the issue: **Prevented (Blocked)**, **Allow**, or **Report**.

{% hint style="info" %}
### Note

If the default action configured in **Endpoint DLP Settings** is set to **Block file movement (fail-close)**, an issue is raised where the assigned severity is set to low, and includes the **Name** Data movement blocked by Endpoint DLP default action
{% endhint %}

**View the DLP issue card panel**

Click a DLP issue to open the DLP security card, where you can investigate the issue, take any required actions, and view remediation suggestions.

From the three-dot menu, you can open the issue in a new tab, copy the issue URL, retrieve the file, or view raw data (JSON).

Some other important actions:

* **Retrieve File**: From the asset card, click ![Image\_20-01-2026\_at\_10\_16.jpeg](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-9534f1ee31f1a8751a0fb0f662578180bf73e338%2F97c719ce63b9056ce450d5238a1768931c58170d844ae516aa0147e042afa5aa.jpg?alt=media) to obtain a copy of the file that triggered the security alert.\
  **Note**: Files remain available for retrieval until they are deleted.
* Click ![Image\_22-01-2026\_at\_16\_43.jpeg](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-0a65872034d34d225ad43942a3f8674ba4ac4203%2F2fb16d6f22f1891d6b64f8385088a354388308e42bb3e8c94fccb2b07cac373e.jpg?alt=media) to open the related rule that triggered the issue.

At the top of the card, you can view information about the issue, including the severity, detection tags, category, and detection method. In the tabs, you can see more information about the cause of the issue, take any required actions, and view remediation suggestions.

You can also see the details of the user who logged into the browser.

<details>

<summary>Overview</summary>

Displays a description of the issue and provides key information, such as the assignee, status, action taken, and the time that the issue was created and updated.

You can also see the following:

*   **Evidence**: which includes data classification details such as **Data Profiles**, **Data Patterns**, **Classification Status,** and **Profile Indicators**.

    Click the **Profile Indicators** link to view the list of sensitive data contained in the file.

    The graph enables you to view information on the relevant file and logged-in user details.
*   **File** that includes the **Name**, **Hash**, **Path**, and **Data Volume** of the file.

    The path shows the full path of the uploaded file.
* **Local Applications**, which include **Process Name**, **Signer**, **Application Name**, and **Application Group Name**.
* **User Interaction** that includes **User Response**.

</details>

<details>

<summary>War Room</summary>

A comprehensive collection of all investigation actions, artifacts, and collaboration. It is a chronological journal of the issue investigation. For information, see [Use the War Room in an investigation](../../detect-investigate-and-respond-to-threats/investigation-and-response/investigate-issues/use-the-war-room-in-an-investigation).

</details>

<details>

<summary>Work Plan</summary>

A visual representation of the running playbook that is assigned to the issue. For more information, see [Use the Work Plan in an investigation](../../detect-investigate-and-respond-to-threats/investigation-and-response/investigate-issues/use-the-work-plan-in-an-investigation).

</details>
