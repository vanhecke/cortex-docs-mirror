---
description: Create cloud security policies that select rules and define their asset scope.
---

# Create a cloud security policy

To create a cloud security policy:

1. Navigate to **Posture Management** → **Rules & Policies** → **Policies** → **Cloud Security**.
2. Click **Create Policy**.
3. On the **Details** page, provide **Policy Name**, **Description**, and **Labels** (optional).
4. Click **Next**.
5. On the **Rules** page, select which rules to be alerted on by using the available filters. You have three options:
   1. **All Matching Filter Criteria** - Include rules that match specific attributes (e.g., all critical severity rules).
   2. **From Rules List** - Manually select specific rules from the available inventory.
   3. **All Rules** - Include all available rules.
6. Click **Next**.
7. On the **Scope** page, select which scope to be alerted on:
   1. From Cloud Accounts - Select the specific cloud provider account to which the asset belongs.
   2. From Asset Groups - Select the specific logical groupings of assets (e.g., "Production" or "PCI Environment"). An asset group can have assets across different accounts, as the filter logic for the group can be generic (e.g., provider = AWS).
   3. All Cloud Assets - Apply to the entire tenant.
8. Click **Done** to save the policy.
