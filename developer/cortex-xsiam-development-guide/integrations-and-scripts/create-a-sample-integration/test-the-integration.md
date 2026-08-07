---
description: Check the integration you created works.
---

# Test the integration

1.  Go to **Settings** → **Data Collection** → **Automation & Feed Integrations**, and search for Yoda. Click **Add instance**.

    ![](https://4088726609-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FurXrv6qkJRLbdhMdvPIU%2Fuploads%2Fgit-blob-2ab11dfa944bf0ba2b08f22caf47316446ae4b1d%2F038d064fde352c0eb30bf21b0331a5be1d21ac01060ac5c449af9a4876e352c1.png?alt=media)

    We will not enter an API key, but will instead use the free option with a limited number of API calls.
2.  To test connectivity, click the **Test** button. If the connection is successful, you will see Success and the date/time displayed.

    ![](https://4088726609-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FurXrv6qkJRLbdhMdvPIU%2Fuploads%2Fgit-blob-73cf62bcb0d821177cd6ced9ef68423e69ea9239%2F5857aca762a5f4a7d52fd1060c2d305660b147b330262945c56722c7e0339638.png?alt=media)
3.  Click **Save & Exit**.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>If you have an integration open in two different tabs, you may encounter an error where your changes aren’t saved. In this case, take a screenshot of your changes, close both tabs, and then reopen one tab. Enter your changes again and save.</p></div>
4.  To test the integration, create a new incident. At the CLI, enter `!yoda-speak-translate` and any English string for the argument, for example "Hello, my name is John Smith. We are learning about integrations."

    ![xsiam-yoda-speak-cli.png](https://4088726609-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FurXrv6qkJRLbdhMdvPIU%2Fuploads%2Fgit-blob-9b5fecfe5a9b5bde555f9ffff0411c22786196a1%2F29c2c2194e2fb622d191eaac2f629d9f7eb925aa261c113916457b1f896b51a5.png?alt=media)

    In the War Room, you can see the table we created with the `tableToMarkdown` function, with the results.

    ![](https://4088726609-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FurXrv6qkJRLbdhMdvPIU%2Fuploads%2Fgit-blob-60ed8ff6b79ab231ccfd6f9f962c67a05311a108%2F78ae8f7ff04468205474836e7f31a2c1a44b3e23044ac0f5852b8ff1a1373a4e.png?alt=media)
5.  View the integration output in the context.

    In this example, `YodaSpeak` is the root for `The Force`. If the translation changes the next time we run the command, the translation field will be updated.

**Include the integration script in a playbook**

You can see the power of integrations when you include them in a playbook. We will create a playbook that translates the `Details` field in an incident into Yoda Speak and then prints it to the War Room.

1. Go to the **Playbooks** page and click **+New Playbook**.
2. Name the playbook Yoda Speak.
3. In the task library, search for yoda and click **Add**.
4.  You can see there is a field for text, which is a required argument. Instead of typing our text here, we want to pull the text string from incident `Details`.

    1. Click the curly brackets, then Alert details+Details.
    2. Click **Close** and then **Save**.

    ![](https://4088726609-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FurXrv6qkJRLbdhMdvPIU%2Fuploads%2Fgit-blob-62c24e4f2d959855a548a7c4a3400fd011547d79%2Fb2a7ec7c844395a79c7c8df3e08d79a33e81dd83ec4b4528d5221c3dbf65cddd.png?alt=media)
5. Add a print task. Click **+Create Task** and name it print. In the task library, search for `print` and select the **Print** script.
6. Once again, we want to pull our text from the incident, so click the curly brackets. Our options now include `yoda-speak-translate`.
7.  Under `yoda-speak-translate`, choose **Translation** and click **Close** and then **Save**.

    ![](https://4088726609-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FurXrv6qkJRLbdhMdvPIU%2Fuploads%2Fgit-blob-71e0e33202e7b5f8c4c4cd7b5aef41ae79190601%2Fe98d6c11267737244a6dcd6f9ac34ca756330026c2cd7508c5672e0abd6c39b9.png?alt=media)
8.  Connect the tasks in the playbook. Use your cursor to create lines between **Playbook Triggered** and **yoda-speak-translate** and between **yoda-speak-translate** and **print**.

    ![](https://4088726609-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FurXrv6qkJRLbdhMdvPIU%2Fuploads%2Fgit-blob-671f213f1411428f8d3687923064f9b323797de9%2Ffbb44c314614ccc2b2c6a13754170bf427b5e22d34e189af2e6a2ca5690a2b48.png?alt=media)
9. Save the playbook.
10. Test the playbook. Click **Edit**, then click **Debugger Panel** and then click **New Mock Alert**. Select an alert with a **Description** field. Click **Run**.

    Check the **Context** in the Debugger Panel for the YodaSpeak output. See [Debugging](../../testing/debugging) for more details.

This example integration is now complete, and we can use it throughout Cortex XSIAM.

Real world integrations are usually more complex than our example. Like any code, integrations require maintenance and can be extended over time, for example with new features and commands.

To ensure integrations perform as expected, packs can have [unit tests](../../testing/unit-testing), as well as [test playbooks](../../testing/test-playbooks). Learn more about [contributing content](../../contributing-content).
