# Enable auditing access to AD domain objects - 4662

1. Log in to a Domain Controller as a domain admin.
2. In the **Start** menu, under **Administrative Tools**, open **Active Directory Users and Computers**.
3. In the left pane, locate the domain you want to audit. This will typically be the name of your network.
4.  To see more details, in the **View** menu, select **Advanced Features**.

    ![image5.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-3b7da58b160f861f2fa91d5a9211499677fbefb9%2F1e9b061b035b75753b676810e2c9481cf7364ef906b426a134ea529df04371f0.png?alt=media){width=70%\}
5.  To view detailed information about your domain, right-click its name and select **Properties**.

    ![image2.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-ba2f783fdb9637d4c6911d855550db8bb3ecebcd%2F8b9c0465f7fced758daf5dc61811577d37453b8cc61221dac4d004cf4c479afc.png?alt=media){width=70%\}
6. Click the **Security** tab, usually located near the top of the **Properties** window.
7.  Click **Advanced** which is located within the Security tab or near the bottom of the window.

    ![image4.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-3838b55dbfb030c18991114485acaf2237a68b87%2F27a969dd7519611ed159856e6b7279de077aa44e2fbfa43b0d924a7f673409f7.png?alt=media){width=70%\}
8.  In the **Advanced Security Settings** window that opens, select the **Auditing** tab and click **Add**.

    ![image1.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-4b67ce4826687ad331a6c53a8ef7f67768d54a63%2F53f17b0a44e08bf46944e38d5509bcc6f430df72a434d206231f2e352a39de25.png?alt=media){width=70%\}
9.  Click **Select a principal**.

    ![image3.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-caf2ee74bedab427fc208d57ea61dcf705ba942a%2F23efd93f6ea2da30ed28b8e4d75dd434181a3353d5a66957dd046b00bdea2150.png?alt=media){width=70%\}
10. In the window that opens, under **Enter the object name to select**, type **Everyone**, click **Check Names**, and then **OK**.

    ![image34.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-be09f65bbf1bb809538b64aaf2055dd0de4c86d8%2F3987669e5badd47fb1747d38f368afa229e3860da1121e656bfd25d40a3ae912.png?alt=media){width=70%\}
11. In the **Auditing Entry** window, do the following:
    * **Type:** To track only successful attempts, select **Success**.
    *   **Applies to:** To monitor actions by users within this group and any subgroups, select **Descendant User objects**.

        ![image16.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-ddc4240709e04b724dfcc460606415d1600bd950%2F4760da133641656b530967fc872b43173c14d81022b1672f213a3c124bc1dc26.png?alt=media){width=70%\}
    *   **Permissions:** To remove any existing permissions from this audit entry, click **Clear all**.

        ![image23.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-370b33eb26f0a2ff2952db1bf396b5b4a0c080c6%2F705de0200539e04cc15c2c05273b97c1298a554132458325f65182e5ebd7f904.png?alt=media){width=70%\}
    * Scroll up to **Permissions** to see view the list of permissions. Click the checkbox next to **Full Control** which automatically selects all the individual permissions below it.
    *   Uncheck the boxes next to the following:

        * **List contents**
        * **Read all properties**
        * **Read permissions**

        ![image35.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-69dc2aeafef7fb5f42cb59058467a828589e7350%2F26479eddca55e9def6e3632551e4070c72cb0d026bf1290c13b4e8b89c6824f0.png?alt=media){width=70%\}
    * Click **OK** to save the changes.
12. Repeat step 11, with the following values in **Applies to**:
    * **Descendant Group Objects**
    * **Descendant Computer Objects**
    * **Descendant msDS-GroupManagedServiceAccount Objects**
    * **Descendant msDS-ManagedServiceAccount Objects**
    *   **Descendant msDS-DelegatedManagedServiceAccount Objects**

        <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>The <strong>Descendant msDS-DelegatedManagedServiceAccount Objects</strong> configuration is relevant only for Windows Server 2025.</p></div>
