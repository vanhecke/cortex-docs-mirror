---
description: View and use context data stored for an issue.
---

# Issue context data

When an issue is generated, context data is captured from the issue fields and from any automations, such as commands, playbooks, correlation rules, and scripts. Context data includes keys (strings) and values (numbers, maps, arrays, and strings).

To see context data for an issue, open the issue card and click the **Issue Context Data** icon<img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-88cb4f7945525cb468e8fa56dbcb298e7b78ed9d%2Fae76e5cb2c8aed2b391a270074eff3eb6bce9358e7ab46680cfbc6a3a6d9be34.png?alt=media" alt="issue_context_data_icon.png" data-size="line">.

Consider the following information when working with context data:

* When an issue is created, the issue field data is stored under the `issue` key in the context data. When an investigation is opened and commands are run, the data returned from those commands is stored outside of the main `issue` key.
* Issue context data is split into two tabs. The **Issue** tab contains the context data from the issue fields and the commands run on the issue. The **Case** tab contains the parent case fields and other case data. None of this data is added to the context data for the parent case unless you add it.
* You can add keys and values to the context data. This is useful when developing playbooks and other automations. For more information, see [Add context data to an issue](add-context-data-to-an-issue).
* When running automations on an issue, the issue can access context data from its parent case; however, it cannot access context data from other issues. If you want to use context data from other issues, add it to the parent case.
