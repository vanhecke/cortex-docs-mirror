# Ingest authentication logs and data from PingOne

{% hint style="info" %}
**License**

Requires the Data Collection add-on.
{% endhint %}

To receive authentication logs and data from PingOne for Enterprise, you must first set up a Poll subscription in PingOne and then configure the Collection Integrations settings in Cortex XSIAM. After you set up collection integration, Cortex XSIAM immediately begins receiving new authentication logs and data from the source. These logs and data are then searchable in Cortex XSIAM.

1.  Set up PingOne for Enterprise to send logs and data.

    To set up the integration, you must have an account for the PingOne management dashboard and access to create a subscription for SSO logs.

    From the PingOne Dashboard:

    * [Set up a Poll subscription](https://docs.pingidentity.com/pingoneforenterprise/pingone_for_enterprise/p14e_add_poll_subscription.html).
      1. Select **Reporting → Subscriptions → Add Subscription**.
      2. Enter a **NAME** for the subscription.
      3. Select **Poll** as the subscription type.
      4. Leave the remaining defaults and select **Done**.
    * Identify your account ID and subscription ID.
      1.  Select the subscription you just set up and note the part of the poll URL between `/reports/` and `/poll-subscriptions`. This is your PingOne account ID.

          For example:

          `https://admin-api.pingone.com/v3/reports/1234567890asdfghjk-123456-zxcvbn/poll-subscriptions/***-0912348765-4567-98012***/events`

          In this URL, the account ID is `1234567890asdfghjk-123456-zxcvbn`.
      2.  Next, note the part of the poll URL between `/poll-subscriptions/` and `/events`. This is your subscription ID.

          In the example above, the subscription ID is `***-0912348765-4567-98012***`.
2. Navigate to **Settings → Data Sources & Integrations**.
3. On the **Data Sources & Integrations** page, click **+ Add New**, search for **PingOne**, then hover over and click **Add**.
4. Connect Cortex XSIAM to your PingOne for Enterprise authentication service.
   1. Enter your PingOne **ACCOUNT ID**.
   2. Enter your PingOne **SUBSCRIPTION ID**.
   3. Enter your PingOne **USER NAME**.
   4. Enter your PingOne **PASSWORD**.
   5. Test the connection settings.
   6. If successful, **Enable** PingOne authentication log collection.

After configuration is complete, Cortex XSIAM begins receiving information from the authentication service. From the Integrations page, you can view the log collection summary.

5. To search for specific authentication logs or data, you can **Create an Authentication Query** or **Create an XQL Query**.
