---
description: Review pending cloud instances in Cortex XSIAM.
---

# Pending cloud instances

In Cortex XSIAM, a pending cloud instance refers to a cloud instance created after Cortex Cloud generates an authentication template, but before that template has been fully executed within the Cloud Service Provider (CSP) environment.

A pending cloud instance is created each time you complete the onboarding wizard for a new CSP and click **Save**. You can view all cloud instances, including those in a pending state, by navigating to **Cloud Instances**. Ensure you remove any default filters that might exclude instances with a "pending" status.

A single pending instance can be leveraged to create multiple cloud instances, all sharing the same configurations defined during the cloud onboarding process. Pending instances are automatically deleted after 30 days.

### **Manage pending cloud instances**

There are some actions that can be performed specifically on cloud instances with a status of "pending".

<table data-header-hidden><thead><tr><th width="250.2890625"></th><th></th></tr></thead><tbody><tr><td>Action</td><td>Instructions</td></tr><tr><td>Manually connect an instance</td><td>After the authentication template has been executed in the CSP, you can manually connect the Cortex Cloud cloud instance to the CSP by right-clicking the pending cloud instance and selecting <strong>Manually connect an instance</strong>. For more about this process, see <a href="manually-connect-a-cloud-instance">Manually connect a cloud instance</a>.</td></tr><tr><td>View Details</td><td>To review the configuration settings defined in the onboarding wizard for a pending instance, right-click the instance and select <strong>View Details</strong>. This is helps you distinguish between pending instances when you want to create a new cloud instance from an existing pending instance or when you want to manually connect an instance.</td></tr><tr><td>Re-download Connection Template</td><td>The authentication template that you download from the onboarding wizard is valid for seven days from when it was downloaded. If you want to create a new cloud instance from a pending instance after the authentication template has expired, you can right-click the pending instance and select <strong>Re-download Connection Template</strong>. You must then execute the template in the CSP.</td></tr><tr><td>Delete</td><td>To delete a pending instance, right-click the pending instance and select <strong>Delete</strong>.</td></tr></tbody></table>
