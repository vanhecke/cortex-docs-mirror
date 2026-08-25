---
description: >-
  Explore permissions with the Simple and Advanced access tables in Cortex
  XSIAM.
---

# Explore permissions using the simple and advanced access tables

{% hint style="info" %}
Requires a Cloud Posture Security, Cloud Runtime Security, or Cortex XSIAM Premium license.
{% endhint %}

### Overview

Analyzing an identity's permissions can be complex due to the numerous ways permissions are granted, including various granters, policy types, wildcards, and explicit resource access.

The access tables in Cloud Identity Security simplify this task by providing distinct views for exploring permissions of both identities and destinations at different levels of granularity.

Open an access table

1. In the Cloud Identity Security module, open an asset.
2.  Click the **Identity** tab.

    The **Graph** view of the asset's identity is displayed.
3.  Click **Table** to display the graph content in table view.

    A simple table is displayed.
4. To display the advanced view of the table, click the **Advanced view** toggle.
5. To go back to the simple table display, click the **Advanced view** toggle again.

### Access table granularities

Cloud Identity Security offers two access views: the Simple access table and the Advanced access table.

**Simple access table**

The Simple access table provides a high-level overview of the following:

* **Identities:** Shows the services an identity can access (such as RDS, cloud storage, or Vertex).
* **Destinations:** Shows the identity types that have access to the destination asset.

**Advanced access table**

The Advanced access table offers a deeper, more granular view of permissions, including crucial context for security analysis:.

* **Granters:** Identifies granters that provide the specific permission.
* **Policy Patterns:** Shows the patterns written in the policies that grant access to destination assets. For example, if a policy includes a wildcard pattern that is relevant to many assets, you are able to explore which specific patterns granted access to each one.
* **Security Context:** Provides additional insights, such as:
  * Unused permissions
  * Excessive policies
  * Cross-account access
  * Sensitive data related to the permission

### Exploring an identity's permissions

When exploring an identity, its **Access** tab lists all the permissions that the identity holds.

* **Simple view:** Initially displays the broad service categories that the identity can access, such as RDS, cloud storage, or Vertex.
* **Drill down:** Clicking on each service reveals the exact assets the identity can access within that service.
* **Advanced analysis:** To understand how permissions are granted, use the Advanced access table.
  * Hovering over an access line exposes a redirection button.
  * Clicking the **Advanced** toggle button displays the Advanced access table, where you can analyze the granting policies, view the last used time for the permission, and check for associated sensitive data, unused permissions, or excessive permissions.

### Exploring a destination asset's permissions

When exploring a destination asset, such as a specific Amazon S3 bucket or database, the focus shifts to who can access it.

* **Simple view:** The Simple access table shows all the identity asset types such as roles, users, and functions that can access the destination.
* **Advanced analysis:** To understand the details of access for a specific identity type:
  * Explore that identity type in the Advanced access table.
  * This view shows how the permission is granted, the specific permission pattern used, and provides contextual data, for example, the exact sensitive data that is related to the permission.
