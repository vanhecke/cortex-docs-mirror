---
description: Use MongoDB Atlas (Posture) data with Cortex XSIAM.
---

# How to onboard MongoDB Atlas (Posture)

## Overview

Integrate Cloud Security with your MongoDB Atlas account to gain comprehensive visibility into any data and posture risk existing in your MongoDB Atlas environment. This integration enables automated scanning of all assets in MongoDB Atlas, including data classification and risk assessment.

## Prerequisites

* You are an administrator.
* You have the following information:
  * Organization ID
  * Service account client ID
  * Service account client secret
* You have created a service principal and granted it permissions.

## Add configuration details

1. Go to **Settings > Data Sources & Integrations** and then on the **Data Sources & Integrations** screen, click **+ Add New**.
2. On the **Add Data Sources or Integrations** page, click **Show More > Database** and then click on the **MongoDB Atlas (Posture)** card and then click **Add**.\
   Alternatively, you can enter “Mongo” in the **Search Sources** filter field, and then click on the **MongoDB Atlas (Posture)** card > **Add** as mentioned above.
3. In the **MongoDB Atlas (Posture) Instance** screen, enter the following:
   * Display Name
   * MongoDB Atlas Organization ID
   * Client ID
   * Client Secret
4. Optional: If your MongoDB Atlas account is protected by network policies, turn on the toggle, then select the required regions for each cloud provider (AWS, Azure, GCP).
5. Click **Next**.

## Establish a connection

1. In the **IP List**, select the IPs from the regions that you had selected that you want to whitelist. A tooltip shows the selected regions for the cloud platforms you are using.
2. A script is generated that needs to be run in the MongoDB Atlas account.

### Set up your MongoDB Atlas connection

1. Open your MongoDB console in a new tab.
2. Copy or download the script provided in step 2 above and run it in the MongoDB CLI.
3. Proceed to verifying the connection.

## Verify the connection

1. Click **Verify Connection**.\
   **NOTE**: Keep the screen open for the duration of the connection verification.
2. Once you see the **Instance Created Successfully** message on the screen, you can click **Close**.
3. You can now go back to the **Data Sources & Integrations** screen and **MongoDB Atlas (Posture)** should appear in the list with relevant details such as **Vendor** and **Instances Status**. To see more details, click on the row and a pane opens with further account details such as connection status and more.
