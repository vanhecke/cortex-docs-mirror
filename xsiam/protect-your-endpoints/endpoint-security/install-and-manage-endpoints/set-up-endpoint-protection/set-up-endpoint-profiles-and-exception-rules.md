---
description: >-
  Configure Cortex XSIAM endpoint profiles and exception rules for consistent
  protection.
---

# Set up endpoint profiles and exception rules

Cortex XSIAM provides default security profiles that you can use out-of-the-box to immediately begin protecting your endpoints from threats. These profiles are applied to endpoints by mapping them to policies, and then mapping the policies to endpoints.

While security rules enable you to block or allow files to run on your endpoints, security profiles help you customize and reuse settings across different groups of endpoints. When the Cortex XDR agent detects behavior that matches a rule defined in your security policy, the Cortex XDR agent applies the security profile that is attached to the rule for further inspection.

{% hint style="info" %}
Profiles associated with one or more targets that are beyond the scope of your defined user permissions are locked and cannot be edited.
{% endhint %}
