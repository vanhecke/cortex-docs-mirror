---
description: >-
  Before you begin onboarding Alibaba Cloud, you must review the following
  prerequisites.
---

# Prerequisites for onboarding Alibaba Cloud

### Permissions

Before you begin to onboard Alibaba Cloud to Cortex XSIAM, ensure that you have the necessary permissions:

* In Cortex XSIAM, you must have a Cortex XSIAM role with Data Sources - View & Edit permissions (to add/configure cloud accounts in Cortex XSIAM). This role is included in the following built-in roles: Instance Administrator, Security Admin, and IT Admin.
* In Alibaba Cloud, your credentials must have the necessary [RAM permissions](#required-ram-permissions-in-alibaba-cloud) to deploy templates, manage roles and policies, as well as perform create and update operations for OIDC.

### Additional prerequisites

Before you begin onboarding Alibaba Cloud, ensure that:

* You have [added an OIDC provider](#add-cortex-cloud-as-an-oidc-provider-in-alibaba-cloud) for Cortex XSIAM in Alibaba Cloud.
* You have the Alibaba Cloud account ID of the account you want to onboard.
* You are logged into the Alibaba Cloud account.
* If you are onboarding your first Alibaba Cloud account, you must first request manual provisioning of the cloud scanning environment. Open a customer support ticket to have the cloud scan environment created and ensure that the environment is ready for you to start onboarding. (Attempting to onboard Alibaba Cloud without first having the cloud scanning environment created will result in the following UI error: "No valid outpost scan env ALIBABA\_CLOUD".)

### **Required RAM permissions in Alibaba Cloud**

Before onboarding Alibaba Cloud to Cortex XSIAM, ensure the user or role performing the onboarding has the necessary RAM permissions.

#### Required permissions for onboarding Alibaba Cloud account scope

Use the following template to create a custom policy with the permissions required for onboarding an Alibaba Cloud account to Cortex Cloud. The custom policy can be created in Alibaba Cloud RAM Console at **Permissions → Policies → Create Policy → Script** and attach the policy to the RAM user or role that will run the Terraform apply.

```json
{
  "Version": "1",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "ram:CreateRole",
        "ram:GetRole",
        "ram:UpdateRole",
        "ram:DeleteRole",
        "ram:ListRoles",
        "ram:CreatePolicy",
        "ram:GetPolicy",
        "ram:GetPolicyVersion",
        "ram:DeletePolicy",
        "ram:ListPolicies",
        "ram:ListPolicyVersions",
        "ram:CreatePolicyVersion",
        "ram:DeletePolicyVersion",
        "ram:SetDefaultPolicyVersion",
        "ram:AttachPolicyToRole",
        "ram:DetachPolicyFromRole",
        "ram:ListPoliciesForRole",
        "sts:GetCallerIdentity"
      ],
      "Resource": "*"
    }
  ]
}

```

### Add Cortex XSIAM as an OIDC provider in Alibaba Cloud

In order to establish trust between Cortex XSIAM and Alibaba Cloud, you must add an OpenID Connect (OIDC) provider. If you already have an existing OIDC provider for `accounts.google.com`, you can add Cortex XSIAM as an audience to the existing provider. Otherwise, create a new OIDC provider.

#### Add the audience to an existing OIDC provider

1. In Alibaba Cloud Console, navigate to **RAM → Integrations → SSO**.
2. In **SSO**, select the **OIDC** tab.
3. In the list of IdPs, identify the existing entry for GCP (`accounts.google.com`) and click it.
4. Under **Client ID**, click **Add**.
5. Enter `alibaba-cortex-wif` as the audience value for the new client ID and save the changes.

#### Create a new OIDC provider

Before you begin, obtain the Cortex XSIAM Project ID of your tenant by clicking on the User menu and then selecting About.

1. In Alibaba Cloud Console, navigate to **RAM → Integrations → SSO**.
2. In **SSO**, select the **OIDC** tab.
3. Click **Create IdP**.
4. In **Create IdP**, enter the **IdP Name**. For example, `CortexGCPProvider`.
5. In **Issuer URL**, enter the GCP IdP URL: `https://accounts.google.com`.
6. In **Client ID**, enter: `alibaba-cortex-wif-<accountID>` where `<accountID>` corresponds to the Cortex XSIAM Project ID.
7. In **Fingerprint**, enter the SHA1 fingerprint of the signing certificate for `accounts.google.com`. Note that this fingerprint changes periodically and must be kept up-to-date.
8. Save the changes.

#### <br>
