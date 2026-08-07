# Import a lookup dataset

{% hint style="warning" %}
### Prerequisite

Dataset Management requires **View/Edit** RBAC permissions for **Data Management** (under **Configurations** → **Data Management**), which are the same permissions required for Parsing Rules, Data Model Rules, and Event Forwarding.
{% endhint %}

You can import data from CSV, TSV, or JSON files into Cortex XSIAM to create or update lookup datasets.

{% hint style="warning" %}
### Prerequisite

When uploading a CSV, TSV, or JSON file, ensure that the file meets the following requirements:

* The maximum size for the total data to be imported into a lookup dataset is 30 MB from the **Dataset Management** page. Otherwise, the limit is 50 MB using Cortex Query Language (XQL) or APIs.
* Field names can contain characters from different languages, special characters, numbers (**`0-9`**), and underscores (**`_`**).
* Field names can't exceed 128 characters.
* Field names can't contain duplicate names, white spaces, or carriage returns.
* The file doesn't contain a byte array (binary data) as it can't be uploaded.
* Each line in the JSON file must represent one JSON object. Ensure no brackets enclose the objects at the top-level.
{% endhint %}

Here's an example of a JSON file in the correct format for upload:

```programlisting
{"firstName": "NAME_1", "SurName": "NAME_11", "employeeID": {"id": "ID_AAAAA_2"}}
{"firstName": "NAME_2", "SurName": "NAME_22", "employeeID": {"id": "ID_AAAAA_3"}}
{"firstName": "NAME_3", "SurName": "NAME_32", "employeeID": {"id": "ID_AAAAA_4"}}
```

1. Select **Settings** → **Configurations** → **Data Management** → **Dataset Management** → **+ Lookup**.
2. Browse to your CSV, TSV, or JSON file. You can only upload a TSV file if it contains a `.tsv` file extension.
3.  (Optional) Under **Name**, type a new name for the target dataset.

    By default, Cortex XSIAM uses the name of the original file as the dataset name. You can change this name to something that will be more meaningful for your users when they query the dataset. For example, if the original file name is mrkdptusrsnov23.json, you can save the dataset as marketing\_dept\_users\_Nov\_2023.

    Dataset names can contain special characters from different languages, numbers (**`0-9`**) and underscores (**`_`**). You can create dataset names using uppercase characters, but in queries, dataset names are always treated as if they are lowercase.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Important</h3><p>The name of a dataset created from a TSV file must always include the extension. For example, if the original file name is <code>mrkdptusrsnov23.tsv</code>, you can save the dataset with the name <code>marketing_dept_users_Nov_2023.tsv</code>.</p></div>
4. **Replace the existing data in the dataset** overwrites the data in an existing lookup dataset with the contents of the new file.
5. Click **Add** to add the file as a lookup.
6.  After receiving a notification reporting that the upload succeeded, **Refresh** ![refresh.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-c3392fdef566b75ef9b2dfde07bfba8a49b63680%2F7a4eb5211231592aa33941e052b5e97bff6cd77ea80ceb63c7851a247327884e.png?alt=media) to view it in your list of datasets.

    If the upload fails for any reason, you'll receive a notification in the Notification Center.
