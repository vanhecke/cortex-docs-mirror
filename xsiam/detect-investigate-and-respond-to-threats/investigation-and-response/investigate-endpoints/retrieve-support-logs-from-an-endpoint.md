# Retrieve support logs from an endpoint

When you need to investigate or share additional forensic data, you can initiate a request to retrieve all the support logs and issue data dump files from an endpoint. After Cortex XSIAM receives the logs, you can download the log files or generate a secured link to access them on the Cortex XSIAM server.

### How to retrieve support files

1.  Retrieve support files.

    1. Go to **Investigation & Response → Response → Action Center → Run Action**.
    2. Select **Retrieve Support File** and click **Next**.
    3. Select the target endpoints (up to 10) from which you want to retrieve logs and click **Next**.
    4.  Review the action summary and click **Done**.

        In the next heartbeat, the agent will retrieve the request to package and send all logs to Cortex XSIAM .

    You can also retrieve support files from the **All Endpoints** table by right-clicking and selecting **Endpoint Control** → **Retrieve Support File**.
2.  In the **Action Center**, locate your **Support File Retrieval** action type and wait for the **Status** field to display **Completed Successfully**.

    If you need to cancel the action, you can right-click it and select **Cancel for pending endpoint**. You can cancel the retrieval action only if the endpoint is still in `Pending` status and no files have been retrieved from it yet. The cancellation does not affect endpoints that are already in the process of retrieving files.
3.  When the status is **Completed Successfully**, right-click and select **Additional data**.

    In the **Actions** table, you can see the endpoints from which support files were retrieved.
4.  Select an endpoint, right-click and select either **Download files** or **Generate support file link**.

    Cortex XSIAM retains retrieved files for up to 30 days.

    The secured link is valid for only 7 days. Following the 7 day period, in order to access the files, you will need to initiate a new support file link.

    To open the file you will need the support file password. For more information, see [Retrieve support file password](retrieve-support-file-password).
