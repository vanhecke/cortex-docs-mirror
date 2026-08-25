---
description: >-
  Ingest AWS API Gateway logs into Cortex XSIAM for API traffic analysis, threat
  detection, and risk assessment.
---

# Ingest AWS API Gateway

Integrate AWS API Gateway with Cortex XSIAM to begin scanning the APIs for potential threats and vulnerabilities.

<details>

<summary>Settings in Cortex XSIAM</summary>

In Cortex XSIAM, set up the **AWS API Gateway** data source to integrate with the AWS API Gateway.

1. From **Settings** → **Data Sources** , click ![add\_data\_source.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2FOIaeLn27a0CE3EfKco5n%2Fadd_data_source.png?alt=media\&token=f14b9dae-3afe-40e9-a6b8-573bef61a16f) and search for **AWS API Gateway** and then click **Connect** or **Connect Another Instance**.
2. In the **AWS API Collector** wizard, enter a relevant name and click **Create and Proceed**.
3.  Copy the key and save it for later.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>You must generate a new key if you did not save.</p></div>
4. Click **Close**.

</details>

<details>

<summary>Settings in AWS Management Console</summary>

Configure the settings in the AWS Management Console to integrate with Cortex XSIAM:

1. Log in to the [AWS Management Console](https://aws.amazon.com/console/).
2. In AWS Management Console, navigate to **API Gateway**.
   1. Expand the left-hand menu of the API project.
   2. Go to **Settings** → **Logging** and click **Edit**. Verify that the **CloudWatch log role ARN** is filled.
   3. Click **Stages** and from **Stages**, select the relevant stage.
   4. From **Logs and Tracing**, click **Edit** and configure the following:
      * **CloudWatch Logs**: Select **Errors and info logs**
      * Select **Data tracing**
      * Select **Detailed metrics**
   5.  Click **Save**.

       This creates a unique log group inside CloudWatch.
3. Open CloudWatch in another window by typing **CloudWatch** in the search bar.
   1.  Go to **Logs** → **Log groups** and search for the log group just created.

       The group name follows the following format: `“API-Gateway-Execution-Logs_<gw ID>/<stage name>”`
   2. Click the log group, and from the **Log group details**, copy the **ARN**.
4.  Return to **Edit logs and tracing**, go to **enable the custom access logging** , and paste the ARN without the \* in the **Access log destination ARN** field.

    Example 45.

    ARN: `arn:aws:logs:us-east-1:123456789012:log-group:API-Gateway-Execution-Logs_153tp249k2/Prod:*`

    Paste in **Access log destination ARN**: `arn:aws:logs:us-east-1:123456789012:log-group:API-Gateway-Execution-Logs_153tp249k2/Prod`
5.  In **Log format**, type the following and click **Save**:

    ```programlisting
    ($context.requestId) accountID: $context.accountId;
    requestTimeMs: $context.requestTimeEpoch;
    path: $context.path;
    region: us-east-1;
    apiID: $context.apiId;
    stage: $context.stage;
    extensionVersion: 1.0
    ```
6. Click **Create Firehose stream**.
   1. Configure the following:
      * **Source**: **Direct PUT**
      * **Destination**: **HTTP Endpoint**
      * **Firehose stream name**: Add a relevant name.
   2. In **Destination settings**, configure the following:
      * **HTTP endpoint URL** : Add the API URL from Cortex XSIAM.
      * **Authentication**: Select **Use access key**.
      * **Access key**: Paste the generated token from **AWS API Gateway**.
      * **Content encoding**: Select **GZIP**.
   3. In **Backup settings**, configure the following:
      * **Source record backup in Amazon S3**: select **Failed date only**.
      * **S3 backup bucket**: select a bucket or enter a bucket URI.
   4.  Click **Create**.

       It takes up to 5 minutes for the stream to be activated.
7.  Refer to [Subscription filters with Amazon Data Firehose](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/SubscriptionFilters.html#FirehoseExample). To create an IAM Role and provide CloudWatch with the appropriate permissions for the streaming, refer to steps 8-11.

    After the Data Firehose delivery stream is active and you have created the IAM role, you can create the CloudWatch Logs subscription filter. The subscription filter immediately starts the flow of real-time log data from the chosen log group to your Amazon Data Firehose delivery stream:

    ```programlisting
    aws logs put-subscription-filter \
        --log-group-name "<YOUR_LOG_GROUP_NAME>" \
        --filter-name "<any_filter_name>" \
        --filter-pattern "" \
        --destination-arn "arn:aws:firehose:region:123456789012:deliverystream/<YOUR_DELIVERY_STREAM>" \
        --role-arn "arn:aws:iam::<ACCOUNT_ID>:role/<YOUR_IAM_ROLE>"
    ```

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Important</h3><p>Leave <code>–filter-pattern</code> empty as displayed above.</p></div>

    After you create the filter, go back to **Data Sources** → **AWS API Gateway** to see the logs starting to come in.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>If no logs are showing, send some API requests on Postman or CURL.</p></div>

</details>
