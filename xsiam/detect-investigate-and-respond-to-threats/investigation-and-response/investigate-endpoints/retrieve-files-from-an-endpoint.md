# Retrieve files from an endpoint

During an investigation, you can retrieve files from one or more endpoints by initiating a files retrieval request. For each file retrieval request, Cortex XSIAM supports up to:

* 20 files
* 500MB in total size
* 10 different endpoints

The request instructs the agent to locate the files on the endpoint and upload them to Cortex XSIAM. The agent collects all requested files into one archive and includes a log in JSON format containing additional status information. When the files are successfully uploaded, you can download them from the **Action Center**.

### How to retrieve files from an endpoint

1. Go to Investigation & Response → Response → Action Center → **New Action**.
2. Select **Files Retrieval**.
3.  Select the operating system and enter the paths for the files you want to retrieve. Press **ADD** after each completed path.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>You cannot define a path using environment variables on Mac and Linux endpoints.</p></div>
4. Click **Next**.
5. Select the target endpoints (up to 10) from which you want to retrieve files and click **Next**.
6.  Review the action summary and click **Done**.

    To track the status of a file retrieval action, return to the **Action Center**. Cortex XSIAM retains retrieved files for up to 30 days.

    If at any time you need to cancel the action, right-click, and select **Cancel for pending endpoint**. You can cancel the retrieval action only if the endpoint is still in **Pending** status and no files have been retrieved from it yet. The cancellation does not affect endpoints that are already in the process of retrieving files.
7.  To view additional data and download the retrieved files, right-click the action and select **Additional data**.

    This view displays all endpoints from which files are being retrieved, including their **IP Address**, **Status**, and **Additional Data** such as error messages of names of files that were not retrieved.
8.  When the action status is **Completed Successfully**, right-click the action and download the retrieved files logs.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>If the <strong>Password Protection (for downloaded files)</strong> setting under <strong>Settings → Configuration → General → Server Settings</strong> is enabled, enter the password 'suspicious' to download the file.</p></div>

### Disable file retrieval

If you want to prevent Cortex XSIAM from retrieving files from an endpoint running the agent, you can disable this capability during agent installation or later on from the **All Endpoints** page. Disabling script execution is irreversible. If you later want to re-enable this capability on the endpoint, you must re-install the agent. See the XDR agent administrator’s guide for more information.

{% hint style="info" %}
Disabling File Retrieval does not take effect on file retrieval actions that are in progress.
{% endhint %}
