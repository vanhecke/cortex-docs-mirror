# Manage file execution

You can manage file execution on your endpoints by adding file hashes to your allow and block lists. If you trust a certain file and know it to be benign, you can add the file hash to the allow list. This allows the file to be executed on all your endpoints regardless of the WildFire or local analysis verdict. Similarly, if you want to always block a file from running on your endpoints, you can add the associated hash to the block list.

Adding files to the allow and block lists takes precedence over any other policy rules that are applied to these files. In the **Action Center**, you can monitor the allow and block list actions performed in your network, and add or remove files from these lists.

Supported file types are:

| Operating system | Supported file types                                                                                                                                        |
| ---------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Windows          | <ul><li>PE, PE64</li><li>doc, docx, xls, xlsx (only if they contain macro files)</li><li>PS1</li><li>VBS, VBE, JSE, Java (JAR/WAR), JS, JSP, JSPX</li></ul> |
| Mac              | <ul><li>macho, DMG</li><li>JS, JSP, JSPX</li></ul>                                                                                                          |
| Linux            | <ul><li>ELFS</li><li>JE, JSP, JSPX</li></ul>                                                                                                                |

If **On-write File Examination** is enabled, the following file type hashes are also supported in the allow and block list: War, Asp, Aspx.

### How to add a file to the allow or block list or allow list

1. Go to Investigation & Response → Response → Action Center → **New Action**.
2. Select **Add to Block List** or **Add to Allow List**.
3.  Enter the SHA-256 hash of the file and click ![blue-arrow.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-b47968b899f3a98d57cf861065aea89ac279de34%2Fabd4b966d975f5dbafe0a11234eccca4542a43850825284f0bf43eda2f372695.png?alt=media).

    You can add up to 100 file hashes at one time. If you add a comment, it is added to all the hashes you added in this action.
4. Click **Next**.
5.  Review the summary and click **Done**.

    In the next heartbeat, the agent retrieves the updated lists from Cortex XDR.
6. You are automatically redirected to the **Block List** or **Allow List** that corresponds to the action in the **Action Center**.
7. To manage the file hashes on the **Block List** or the **Allow List**, right-click a file to see the available actions.
