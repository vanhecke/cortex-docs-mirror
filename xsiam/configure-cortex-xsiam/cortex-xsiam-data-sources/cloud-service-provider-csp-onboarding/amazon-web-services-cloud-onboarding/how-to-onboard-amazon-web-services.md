---
description: >-
  Follow the AWS onboarding wizard and Cortex XSIAM creates a custom
  authentication template to be deployed in AWS CloudFormation.
---

# How to onboard Amazon Web Services

{% hint style="info" %}
#### License type

This feature is included with a Cortex XSIAM Premium license. It is also included with any other Cortex XSIAM license that has the Cloud Runtime Security or Cloud Posture Security add-ons.

For Cortex XSIAM NG SIEM, Cortex XSIAM Enterprise, and Cortex XSIAM Enterprise+ licenses, see [How to onboard Amazon Web Services with foundational configuration](onboard-amazon-web-services).
{% endhint %}

After completing the prerequisites, follow these instructions to onboard your Amazon Web Services (AWS) environment to Cortex XSIAM.

## Access the AWS onboarding wizard in Cortex XSIAM:

1. In Cortex XSIAM, select Settings → Data Sources & Integrations.
2. On the Data Sources & Integrations page, click + Add New.
3. On the Add Data Sources or Integrations page, search for Amazon Web Services (AWS), then hover over it and click Add.

## Select the AWS environment

* In the AWS onboarding wizard, select the type of AWS environment:
  * **Government:** AWS GovCloud environments for compatibility with FedRAMP-certified tenants.
  * **Commercial:** (Default) Standard cloud deployment typically used for private and public sector organizations that do not require isolated government-specific infrastructure.

## Select the scope

* Select the scope for this cloud instance:
  * **Organization:** (Default) A collection of AWS accounts that are managed centrally.
  * **Organizational Unit:** A group of AWS accounts within an organization. An organizational unit can also contain other organizational units.
  * **Account:** A single AWS account.

## Choose the scan mode

* Specify the scanning infrastructure for your cloud instance by selecting one of the following scan modes:
  * **Cloud Scan:** (Recommended) Security scanning is performed in the Cortex XSIAM cloud environment.
  *   **Scan with Outpost:** Security scanning is performed on infrastructure deployed to a cloud account owned by you. If you select this option, choose the outpost account to use for this instance.

      #### Note

      Scanning with an outpost may require additional AWS permissions and may incur additional CSP costs.

## Configure advanced settings (optional)

*   Click Show advanced settings to define the following advanced settings:

    * **Instance Name:** Enter a unique instance name or leave it empty to be automatically populated. The automatic naming convention is ``AWS- or `AWS-`<organizationID>``. Cortex XSIAM does not prevent you from reusing instance names, but it is best practice to use a unique name for every cloud instance.
    * **Scope Modifications:** Use these settings to fine-tune your AWS scope, you can modify the scope by including or excluding specific regions. If you selected a Government environment, only AWS GovCloud regions are displayed. Additionally, if you selected an organization or organizational unit as the scope, you can modify the scope by including or excluding specific organizational units or accounts. For more details, see [Apply region or account filters](../..#step-5-apply-region-or-account-filters-optional).
    * **Additional Security Capabilities:** Choose which security capabilities you want to benefit from. Some security capabilities are enabled by default and can be modified. Adding security capability typically requires additional cloud provider permissions. For detailed information on the permissions required, see [Cloud service provider permissions](../cloud-service-provider-permissions).
      * **Data security posture management:** An agentless data security scanner that discovers, classifies, protects, and governs sensitive data. DSPM is not currently available in AWS GovCloud environments.
      * **Registry scanning:** A container registry scanner that scans registry images for vulnerabilities, malware, and secrets. For more details, see [Configure registry scanning for cloud accounts](../../cloud-posture-and-runtime-security-data-sources/container-registry-scanning/configure-registry-scanning-for-cloud-accounts).
      * **Serverless functions scanning:** Implement serverless scanning to detect and remediate vulnerabilities within serverless functions during the development lifecycle. Seamless integration into CI/CD pipelines enables automated security scans for a continuously secure pre-production environment.
      * **Automation:** Use automation to pre-configure a list of integrations and associated commands to automate security issue responses. Commands can be utilized individually or as part of custom playbooks for issue remediation.
        * **Log Level:** (Optional - for Automation only) Configure the automation integration logging level. Possible values are:
          * Off (Default)
          * Debug
          * Verbose
      * **Agentless disk scanning:** (Recommended) Implement agentless disk scanning to remotely detect and remediate vulnerabilities during the development lifecycle.
      * **Kubernetes security:** Implement Kubernetes security to scan and assess Kubernetes cluster configurations, workloads, and security controls to identify misconfigurations, compliance violations, and security risks. This option detects issues in RBAC policies, network policies, pod security standards, container image security, and resource constraints. Keeping this enabled is strongly recommended to maintain continuous visibility into the cluster's security posture and to prevent undetected configuration gaps.
    * **Cloud Tags:** Define tags and tag values to be added to any new resource created by Cortex XSIAM in AWS. Note: The `managed_by = paloaltonetworks` tag is automatically added to all resources. This tag is mandatory. You cannot edit or remove this tag.
    *   **Log Collection Configuration:** To maximize security coverage, include the collection of audit logs using CloudTrail. Select the collection method:

        * **Automated:** Select this option to have Cortex XSIAM provisions CloudTrail, S3, SQS, SNS, and KMS key resources in your AWS environment to collect audit logs.
          * **Collect data events:** You can choose to collect data events, which captures S3 object-level and Lambda invocation events for enhanced visibility.
          * **Cost considerations:** Data events can generate high volumes in active environments (millions of events per day for busy S3 buckets). We recommend you review your CloudTrail pricing and expected event volume before enabling.
        * **Custom**: (Default) Use this option to use an existing Amazon S3 bucket for storing your CloudTrail logs.
          * When you deploy the authentication template, you will enter the following details: S3 bucket name, SNS topic ARN, KMS key ARN (optional, if bucket is encrypted). For CloudFormation, these are entered as stack parameters. For Terraform, you are prompted for these values when you run terraform apply.
          * Cortex XSIAM creates the SQS queue, the **CortexLogsReadRole** IAM role, and the S3-to-SNS-to-SQS event notification infrastructure.
          * After you deploy the authentication template, you must configure the S3 bucket event notification to send to the Cortex XSIAM-created SQS queue.
        * **Custom - Control Tower:** Select this option if your AWS Organization is managed by AWS Control Tower and uses a centralized Log Archive account. This option is only available for organization scope.
          * When you deploy the authentication template in CloudFormation, you will enter the following details: S3 bucket name (the centralized Control Tower bucket in the Log Archive account), SNS topic ARN (the Control Tower-provisioned `aws-controltower-AllConfigNotifications` topic), KMS key ARN (optional), and the logging account ID (the AWS account ID of the Log Archive account).
          * Cortex XSIAM deploys the IAM role into the Log Archive account and creates the SQS queue in the same account that hosts the customer's CloudTrail SNS topic.

        <div data-gb-custom-block data-tag="hint" data-style="warning" class="hint hint-warning"><h4>Important</h4><p>It is critical to ensure that your KMS key region and SNS topic region are the exact same as the AWS region where you are deploying the authentication template. For custom Control Tower (BYOB), deploy the stack in the same region as your Control Tower home region, where the <code>aws-controltower-AllConfigNotifications</code> SNS topic resides.</p></div>
    *   **Upload unknown files to WildFire:** Use this option to upload unknown files scanned during registry image scans to WildFire for detonation analysis.

        This option expands malware detection by allowing WildFire to analyze new samples found in your registry images. When a detonation result returns a malicious verdict, the system re-evaluates the relevant registry image and creates a malware finding.<br>

        <figure><img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2FbLVVFbhzGA2oRZS73rxU%2Fimage.png?alt=media&#x26;token=cd29d9e4-72d8-401b-8cf0-d66079761890" alt=""><figcaption></figcaption></figure>

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h4>Notes</h4><ul><li>The file types sent for WildFire analysis depend on the platform type. WildFire accepts files up to 300 MB in size.</li><li>This setting applies only to registry image scans and is enabled by default for new AWS instances. For existing instances, this setting is disabled by default to preserve current behavior. You can enable it at any time by editing the instance configuration.</li><li>Your cloud provider may charge standard outbound data transfer (egress) fees when scanning with an <a href="../outpost-onboarding">Outpost</a>.</li></ul></div>

## Save the configuration

* Click **Save**. Cortex XSIAM generates an authentication template based on the settings you configured in the AWS onboarding wizard. Cortex XSIAM creates an instance in the pending state. For details on pending instances, see Pending cloud instances.

## Deploy the template

To complete the process, deploy the authentication template using one of the following methods:

1.  **Automated:** (Recommended) Click Execute in AWS to be redirected to AWS CloudFormation to create the stack. Before you select Automated, verify that you are logged into the correct AWS account in your browser. For account scope, it is the account you are onboarding. For organization or OU scope, it is the management account. Deploying to the wrong account will cause deployment failures or create resources in the wrong location.

    You are redirected to the AWS CloudFormation console with the pre-populated template. Click through the wizard to create the stack.
2. **Generate template:** Download one of the setup files and deploy it in your AWS account:
   * Click **CloudFormation** to download the CloudFormation template file.
   * Click **Terraform** (account scope only) to download the Terraform template archive.
3. [Deploy the template in AWS](deploy-the-authentication-template-in-aws).
