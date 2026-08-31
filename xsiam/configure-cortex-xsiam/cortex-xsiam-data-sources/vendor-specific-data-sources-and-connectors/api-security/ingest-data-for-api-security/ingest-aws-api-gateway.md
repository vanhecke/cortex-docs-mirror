---
description: Collect AWS API Gateway data with Cortex XSIAM.
---

# Ingest AWS API Gateway

Integrate AWS API Gateway with Cortex XSIAM to begin scanning the APIs for potential threats and vulnerabilities.

### Settings in Cortex XSIAM

In Cortex XSIAM, set up the AWS API Gateway data source to integrate with the AWS API Gateway.

1. From Settings → Data Sources, click **Add Data Source** and search for AWS API Gateway and then click Connect or Connect Another Instance.
2. In the AWS API Collector wizard, enter a relevant name and click Create and Proceed.
3. Copy the key and save it for later.

{% hint style="info" %}
You must generate a new key if you did not save it.
{% endhint %}

4. Click Close.

### Settings in AWS Management Console

Configure the settings in the AWS Management Console to integrate with Cortex XSIAM:

1. Log in to the [AWS Management Console](https://aws.amazon.com/console/).
2. In AWS Management Console, navigate to API Gateway.
   1. Expand the left-hand menu of the API project.
   2. Go to Settings → Logging and click Edit. Verify that the CloudWatch log role ARN is filled.
   3. Click Stages and from Stages, select the relevant stage.
   4. From Logs and Tracing, click Edit and configure the following:
      * CloudWatch Logs: Select Errors and info logs
      * Select Data tracing
      * Select Detailed metrics
   5.  Click Save.

       This creates a unique log group inside CloudWatch.
3. Open CloudWatch in another window by typing CloudWatch in the search bar.
   1.  Go to Logs → Log groups and search for the log group just created.

       The group name follows the following format: `“API-Gateway-Execution-Logs_<gw ID>/<stage name>”`
   2. Click the log group, and from the Log group details, copy the ARN.
4.  Return to Edit logs and tracing, go to enable the custom access logging , and paste the ARN without the \* in the Access log destination ARN field.

    ARN: `arn:aws:logs:us-east-1:123456789012:log-group:API-Gateway-Execution-Logs_153tp249k2/Prod:*`

    Paste in Access log destination ARN: `arn:aws:logs:us-east-1:123456789012:log-group:API-Gateway-Execution-Logs_153tp249k2/Prod`

    <br>
5.  In Log format, type the following and click Save:

    ```
    ($context.requestId) accountId: $context.accountId;
    requestTime: $context.requestTime;
    path: $context.path
    ```
6. Click Create Firehose stream.
   1. Configure the following:
      * Source: Direct PUT
      * Destination: HTTP Endpoint
      * Firehose stream name: Add a relevant name.
   2. In Destination settings, configure the following:
      * HTTP endpoint URL : Add the API URL from Cortex XSIAM.
      * Authentication: Select Use access key.
      * Access key: Paste the generated token from AWS API Gateway.
      * Content encoding: Select GZIP.
   3. In Backup settings, configure the following:
      * Source record backup in Amazon S3: select Failed date only.
      * S3 backup bucket: select a bucket or enter a bucket URI.
   4.  Click Create.

       It takes up to 5 minutes for the stream to be activated.
7.  Refer to [Subscription filters with Amazon Data Firehose](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/SubscriptionFilters.html#FirehoseExample). To create an IAM Role and provide CloudWatch with the appropriate permissions for the streaming, refer to steps 8-11.

    After the Data Firehose delivery stream is active and you have created the IAM role, you can create the CloudWatch Logs subscription filter. The subscription filter immediately starts the flow of real-time log data from the chosen log group to your Amazon Data Firehose delivery stream:

    ```
    aws logs put-subscription-filter \
        --log-group-name "<YOUR_LOG_GROUP_NAME>" \
        --filter-name "<any_filter_name>" \
        --filter-pattern "" \
        --destination-arn "arn:aws:firehose:region:123456789012:deliverystream/<YOUR_DELIVERY_STREAM>" \
        --role-arn "arn:aws:iam::<ACCOUNT_ID>:role/<YOUR_IAM_ROLE>"
    ```

{% hint style="warning" %}
**Important**

Leave `–filter-pattern` empty as displayed above.
{% endhint %}

After you create the filter, go back to Data Sources → AWS API Gateway to see the logs starting to come in.

{% hint style="info" %}
If no logs are showing, send some API requests using Postman or cURL.
{% endhint %}
