---
description: >-
  Learn how to grant authorization to Cortex XSIAM to scan within your GCP
  service perimeter.
---

# Monitor GCP resources inside service perimeters

A service perimeter can provide an additional layer of security for your GCP projects. It serves as a fortified boundary around your Google Cloud resources. While resources inside the perimeter can communicate freely, the perimeter is designed to prevent unauthorized communication to Google Cloud services beyond its confines.

To enable Cortex XSIAM to scan assets and resources within your GCP perimeter, you must authorize Cortex XSIAM's identities to access the perimeter from within GCP. If you have a perimeter set up in your GCP project and you have not authorized Cortex XSIAM's identities to scan the perimeter, you will receive the following error:

```varname
Request is prohibited by organization's policy. vpcServiceControlsUniqueIdentifier: {{<GCP-perimeter-ID>}}
```

{% hint style="info" %}
#### **Note**

Each GCP cloud instance is assigned a scope within GCP. If the scope, whether it be organization, folder, or project, includes any projects with a service perimeter, this procedure must be performed for that cloud instance to authorize Cortex XSIAM to scan the resources in the perimeter.
{% endhint %}

### Obtain Cortex XSIAM identity details

1. In your Cortex XSIAM tenant, select **Settings → Data Sources & Integrations**.
2. Hover over the Google Cloud Platform (GCP) row and select **View Details**.
3. In the Cloud Instances page, identify the GCP instance with the perimeter, right-click it and select **Details**.
4. In the details pane, click the **more options** icon and select **Authorization Details**.
5. The authorization values that you need to add as approved identities in GCP are listed in the **Authorization Details** dialog box.

### Add Cortex XSIAM authorization values to GCP perimeter

1. Log into [Google Cloud Platform Console](https://console.cloud.google.com/).
2. Navigate to VPC Service Controls.
3. In the list of perimeters, select the perimeter to which you want to grant access to Cortex XSIAM.
4. In the **Service perimeter details** screen, click **Edit**.
5. In the **Edit service perimeter** screen, select **Ingress policy**.
6. In the **Ingress rules** pane, click **Add an ingress rule**.
7. Enter a **Title** for the ingress rule.
8. In the **From** section, under **Identities**, select **Select identities & groups**.
9. Click **Add identities**. In the **Add identities** pane, under **Search identities**, paste Cortex discovery role from Cortex XSIAM's **Authorization Details** dialog box. If there are more authorized values, paste each of them under **Search identities**. Click **Add identities**.
10. In the **To section**, under **Resources**, select **Select projects**.
11. Click **Add projects**. In the **Add projects** pane, select the relevant projects.
12. Under **Operations or IAM roles**, select **All operations**.
13. Click **Next** to add an egress rule.
14. In the **Egress rules** pane, click **Add an egress rule**.
15. Enter a **Title** for the egress rule.
16. In the **From** section, under **Identities**, select **Select identities & groups**.
17. Click **Add identities**. In the **Add identities** pane, under **Search identities**, paste Cortex discovery role from Cortex XSIAM's **Authorization Details** dialog box. If there are more authorized values, paste each of them under **Search identities**. Click **Add identities**.
18. In the **To** section, under **Resources**, select **Select projects**.
19. Click **Add projects**. In the **Add projects** pane, select the relevant projects.
20. Click **Save**. Confirm the changes and click **Confirm**.

The Cortex XSIAM authorization values have been added as approved identities in GCP.
