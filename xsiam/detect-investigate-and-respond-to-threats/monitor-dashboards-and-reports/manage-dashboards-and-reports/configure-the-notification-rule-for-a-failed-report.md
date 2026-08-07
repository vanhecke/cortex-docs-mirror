# Configure the notification rule for a failed report

You can receive an email or send a notification to a syslog server if a report fails to run due to a timeout or fails to upload to the GCP bucket.

1. Under **Settings → Configurations → General → Notifications**, click **Add Forwarding Configuration**.
2. Enter a name and a description for your rule, and under **Log Type**, select **Management Audit Logs**.
3. Use a filter to select the **Type** as Reporting, **Subtype** as Run Report, and **Result** as Fail.
4. Enter a distribution list to receive notifications by email or select a syslog server.
5. Click **Next**.
6. Review settings and click **Create**.
