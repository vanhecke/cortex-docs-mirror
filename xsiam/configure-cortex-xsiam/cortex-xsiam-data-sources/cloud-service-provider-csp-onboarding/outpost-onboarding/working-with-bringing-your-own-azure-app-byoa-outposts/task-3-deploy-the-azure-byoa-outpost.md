---
description: >-
  You can customize your own outpost by bringing your own app (BYOA). This page
  describes the steps for deploying the Azure BYOA outpost.
---

# Task 3: Deploy the Azure BYOA outpost

While creating the Azure BYOA outpost, you supply the relevant BYOA IDs to Cortex. This topic provides the instructions for deploying the outpost with the advanced BYOA settings.

## Step 1. Create the Azure BYOA outpost in Cortex

1. In Cortex XSIAM, navigate to **Settings → Data Sources & Integrations → Outposts**.
2. Click **New Outpost**.
3. In Cortex XSIAM, choose **Azure**.
4. If you are using a FedRAMP-certified (Government) Cortex XSIAM tenant, you are able to choose between the following environments:
   * **Commercial:** (Default) Standard cloud deployment typically used for private and public sector organizations that do not require isolated government-specific infrastructure.
   * **Government:** Microsoft Azure Government environments for compatibility with FedRAMP-certified tenants.
5. Enter the instance name and the Entra tenant ID of the Azure tenant in which you want to establish the outpost. The Entra tenant ID is validated automatically.\
   \
   **Note**: Due to limitations in Terraform, the Azure subscription name cannot contain blanks.
6. Click **Show advanced settings** and toggle **Bring Your Own App (BYOA)** on.
7. Enter the following IDs:
   * **Tenant ID**: Your Entra ID tenant ID, which is validated automatically.
   * **Application (client) ID**: The Azure application ID, which you retrieved while creating and configuring the app registration in Task 2, either:
     * Using the `customer_app_client_id` value outputted by the helper shell script's output.
     * Manually, in the Azure portal's **Register an application > Overview** page.
   * **Service Principal Object ID**: The app's service principal object ID This you defined while creating and configuring the app registration in Task 2, either:
     * Using the `customer_sp_object_id` value outputted by the helper shell script's output.
     * Manually, in the Azure portal's **Microsoft Entra ID → App registrations → \<your AppReg> → Owners → Add owners** page. You can find the value in the app registration's Overview page's **Object ID** field.
8. If you also created the scanner managed identities, enable the **Bring Your Own Scanner Managed Identities** toggle in the wizard and paste the UAMI resource IDs that you saved in Task 2 (either using the helper shell script's output or manually in the Azure portal).
9. (Optional) Define tags and tag values to be added to any new resource created by Cortex in the cloud environment. Click **Next**.
10. Click **Download Terraform** to download the Terraform template file.

## **Step 2. Execute the template in Azure to deploy the outpost**

In the previous step, you downloaded the Terraform template file in the outpost creation wizard.

Now, you log in to your CSP and execute the Terraform template file.

Follow the instructions for deploying standard Azure outposts.

To view outposts and their details, navigate to **Settings → Data Sources & Integrations → Outposts**.

## What's next?

Proceed to [Task 4: Verify the BYOA outpost deployment](task-4-verify-the-byoa-outpost-deployment).
