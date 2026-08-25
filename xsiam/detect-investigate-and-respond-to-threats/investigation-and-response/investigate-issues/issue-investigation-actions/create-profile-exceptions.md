---
description: Create Cortex XSIAM profile exceptions for relevant XDR agent issues.
---

# Create profile exceptions

For Cortex XDR agent related issues, you can create profile exceptions for Window processes, BTP, and JAVA deserialization issues directly from the **Issues** table.

1. Identify an **XDR Agent** issue which has a category of **Exploit**, right-click and select **Manage Issue** → **Create issue exception**.
2. Select an **Exception Scope**:
   * **Global:** Apply the exception across your organization.
   * **Profile:** Apply the exception to an existing profile or click and enter a **Profile Name** to create a new profile.
3. Click **Add** to add the scope.
4. (Optional) View your profile exceptions.
   1. Go to **Inventory → Endpoints → Policy Management** → **Profiles**.
   2. In the **Profiles** table, locate the OS in which you created your global or profile exception and right-click to view or edit the exception properties.
