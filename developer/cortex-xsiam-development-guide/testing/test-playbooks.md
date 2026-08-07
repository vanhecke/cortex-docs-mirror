---
description: Create test playbooks to check integration commands and scripts.
---

# Test playbooks

Use test playbooks to check integrations and scripts. Test playbooks provide full end-to-end testing. For testing small units of code, use unit testing. Test playbooks are run using the CI framework. They are run both as part of the build process and on a nightly basis.

{% hint style="info" %}
### Note

By default, test playbooks do not run in the CI for packs that are not supported by Cortex XSIAM. For content packs not supported by Cortex XSIAM, test playbooks are not required unless specifically requested by Cortex XSIAM.
{% endhint %}

A test playbook has several steps, including testing commands, verifying the results, and closing the investigation.

The naming convention for playbook tests is: `Integration_Name_Test`.

<details>

<summary>Generate a test playbook</summary>

To auto generate a test playbook based on an integration or script use the [demisto-sdk generate-test-playbook](https://app.gitbook.com/s/nozw5MT5S8KZD2eF8roV/demisto-sdk-commands/generate-test-playbook) command. You can then import the playbook and modify it to meet your needs. You can also manually create a test playbook, by navigating to **Playbooks** in the UI and clicking **New Playbook**.

</details>

<details>

<summary>Add DeleteContext</summary>

When creating a test playbook, we recommend for the first step to be `DeleteContext`, which deletes all of the context data. While not always necessary, this ensures that a test playbook has a clean beginning to test from without conflicting data. This can be useful while rerunning a playbook during the development process and can prevent existing data from creating unrelated issues.

1. Search for `deletecontext` in the **Task Library** and add the `DeleteContext` utility task to the playbook.
2. On the **Inputs** tab, for **all** ,select **yes**.
3.  Click **OK** and connect the `DeleteContext` task to the `Playbook Triggered` task.

    ![playbook-triggered.png](https://4088726609-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FurXrv6qkJRLbdhMdvPIU%2Fuploads%2Fgit-blob-63504810c816dde5d3efb9ffb9b360fefcd16218%2F399ccedead4037f59e8950d9df6a884bd938ccc999c0fd9f0c455b91d3246fab.png?alt=media)

</details>

<details>

<summary>Test a command</summary>

We recommend testing as many commands of the integration as possible as tasks. Each command should have a task. For this example we will look at the integration **IPInfo v2**, which accepts only one command called `!ip`.

1. Navigate to **Playbooks** and click **New Playbook**.
2. In the **Task Library**, search for `ipinfo`.
3. Add the **IPinfo v2** task to your playbook.
4. Enter an IP address in the **ip** field. This should be an entity that will produce consistent results, such as `8.8.8.8`, the Google DNS server.
5. Click **OK** to save your changes.
6. Connect the **DeleteContext** task to the **ip** task

</details>

<details>

<summary>Verify command results</summary>

After you run the command, you should verify you have received the expected results.

1. Open the **Task Library** and **Create Task**.
2.  Configure the task:

    | Option              | Configuration                                                                                                                                             |
    | ------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | Conditional         | Select the **Conditional** task option                                                                                                                    |
    | Task Name           | **Verify Command Results**                                                                                                                                |
    | Condition for:      | Above **From previous tasks**, click **{}** to display the **Select source** options. Click the **#2 ip** task that you created.                          |
    | IPinfo.IP           | Click **Address** and close the window. **IPinfo.IP.Address** is now displayed. This is the context path.                                                 |
    | From previous tasks | Wrap the context path using the format `${IP.Address}`. Wrapping the context path tells Cortex XSIAM to retrieve the value located in the curly brackets. |
    | As value            | Type 8.8.8.8 and click the checkmark.                                                                                                                     |

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>If you need to edit the value in a field, you can click on the value and edit it. For example, click on the value in the <strong>From previous tasks</strong> field and edit the ${IP.Address} value.</p></div>
3. (Optional) - If you need to filter or format the result, click **Filters and Operations** located in the **Select source** dialog box.
4. Click **OK**.
5. Connect the **ip** task to the **Verify Command Results** task.

</details>

<details>

<summary>Close the investigation</summary>

1. In the **Task Library**, search for `closeinvestigation`.
2. Add the **closeInvestigation** task found under **Builtin Commands**.
3. Connect the **Verify Command Results** task to the **closeInvestigation** task.
4. In the pop up dialog box, select **yes**.

</details>

<details>

<summary>Name and export the playbook</summary>

Cortex XSIAM uses a standard naming convention for playbook tests that follows this format: `Integration_Name_Test`.

1. **Save Playbook**.
2. Close the playbook editor.
3. Download the playbook from the more options icon.

</details>

<details>

<summary>Add the playbook to your project</summary>

1. Save your newly created test playbook to the `TestPlaybooks` directory in your content pack.
2. In the playbook YAML file that you created, edit the `id` so that it is identical to the `name` field.
3. Change the value in the `version` field to `-1` to prevent user changes.
4.  Using the example above, the beginning of your YAML file should look like this:

    ```programlisting
    id: IPInfo_Test
    version: -1
    name: IPInfo_Test
    ```
5.  Add the ID of the test playbook to the YAML of your content-item under the `tests` key.

    ```programlisting
    tests:
    - Test Playbook Name
    ```

</details>

<details>

<summary>Add tests to conf.json</summary>

To associate integrations with a test playbook, we create or update a `conf.json` file (at the root of the repository). The `conf.json` file is located in the `Tests` directory.

The following is an example of a `conf.json` entry for an integration.:

```programlisting
        {
            "integrations": "Forcepoint",
            "playbookID": "Forcepoint_Test",
            "timeout": 500,
            "nightly": true
        },
```

The following table describes the fields:

| Name         | Description                                                                               |
| ------------ | ----------------------------------------------------------------------------------------- |
| integrations | The ID of the integration that you are testing.                                           |
| playbookID   | The ID of the test playbook that you are running.                                         |
| timeout      | (Optional) - The time in seconds to extend the timeout to.                                |
| nightly      | (Optional) - Boolean that indicates if the test should be part of only the nightly tests. |

</details>

#### Additional Resources

* [Example of a test playbook](https://github.com/demisto/content/blob/master/Packs/Carbon_Black_Enterprise_Response/TestPlaybooks/playbook-Carbon_Black_Response_Test.yml)
* [Example of a playbook image](https://xsoar.pan.dev/assets/files/41154872-459f93fe-6b24-11e8-848b-25ca71f59629-309395de5bc3906b3f43c8973ec45b2c.png)
