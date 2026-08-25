---
description: Send Cortex XSIAM push notifications to supported iOS endpoints.
---

# Send push notifications to iOS

You can push a notification to the Cortex XDR agent on the iOS device from Cortex XSIAM.

1. Navigate to **Inventory+Endpoints → All Endpoints** and locate the required iOS device or devices.
2. Right-click and select **Endpoint Control → Send Push Notification**.
3. Select one of the following notifications to send to the agent:

| Notification               | Action                                                                                                                                                                                                                                                                             |
| -------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Device Checkup**         | When the App user taps the received notification, the app will open on the device, ready to perform the checkup. Tap Perform Check Up to initiate a device checkup.                                                                                                                |
| **Verify App Permissions** | If the Phone permissions are not set correctly for full protection, the user is instructed to allow permission. The App user must tap Open Permissions Wizard from the iOS device Home screen and follow the wizard to enable and allow the required settings for full protection. |
| **Custom message**         | Admin can send a message with a header and body text to designated App users. The App user will receive this textual message.                                                                                                                                                      |
