# Close an issue

Once you complete your investigation, perform one of the following actions to close an issue:

* **Manually close an issue:** Right-click an issue and select **Change Status** → Resolved and select a resolution reason.
* **Automatically close an issue:** Run the `closeInvestigation` command in the CLI, in a script, or a playbook task. You can configure this command to run as part of a flow when automating issue investigation.

The `closeInvestigation` command supports the `closeReason` and `closeNotes` arguments. The `closeReason` argument accepts a free text value; however, if the free text value doesn't match one of the defined resolution reasons the `resolution_status` field is set to `Resolved - Other`. To see a description of the resolution reasons, see [Resolution reasons for cases and issues](../../analyze-and-resolve-cases/resolve-the-case/resolution-reasons-for-cases-and-issues).

{% hint style="info" %}
When an issue is resolved it remains linked to a case. Once all of the issues in a case are resolved, the case is automatically closed.
{% endhint %}

### Example of using the closeInvestigation command in the CLI

In this example, the command specifies to close the issue and set values for `closeReason` and `closeNotes`.

```
!closeInvestigation closeReason="Resolved - Known Issue" closeNotes= "Mitigated"
```

### Example of using the closeInvestigation command in a playbook

In this example, the `closeInvestigation` command is used in a playbook and values are set for `closeReason` and `closeNotes`.

![closeInvestigation\_playbook\_example.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-ef31a41777c13de7c87c3000c5cd71b5f6927f3a%2F0b64ff8633e4da3b328a1db9dde837293578330a20181bd8fe49a01e197a092c.png?alt=media)

### Example of using a variable in the closeReason field

In this example the close reason field specifies the `${tmpCloseReason}` variable value. The `tmpCloseReason` key was added to the issue context data, and the value is drawn from this field.

1.  Add the `tmpCloseReason` key and set the value, run the following command in the issue **War Room**:

    ```
    !Set key=tmpCloseReason value="Resolved - True Positive"
    ```
2.  Create a task in your playbook for the closeInvestigation command and set the closeReason field to `${tmpCloseReason}`.

    ![closeInvestigation\_playbook\_example2.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-7000019d95f4a849b0f3bdc9057517b56f9e0a2a%2F36cbc948dfea09c38c79c64a44b547debd9c07363c5eccf566748254abcc4705.png?alt=media)

    When the playbook runs, it draws the value from this field in the context data:

    ![tmpCloseReason\_context\_data.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-e9d6a94d52e48d278457ada1b195daa6909830b5%2F31e5cd7d82feaa890ca4d8c0b697c992ecc08aa36797e63c7b2e6dcad19fa81b.png?alt=media)
