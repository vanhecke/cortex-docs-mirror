---
description: Cortex XSIAM steps for creating and packaging lists.
---

# Lists

After creating a list in Cortex XSIAM, you can download it and add it to your content pack.

1. In Cortex XSIAM, when viewing a list, click the more options icon (three vertical dots) to **Download list**.
2. Add `list-` to the beginning of the file name and change the file extension to `.json`. For example, for a JSON list, rename the file `list-mylistname.json`.
3.  Edit the file to change the `id` field to be identical to the `name` field. and edit the value in the `version` field to `-1` to prevent user changes.

    Your JSON file should include the following:

    ```programlisting
    id: <name of your list>
    version: -1
    name: <name of your list>
    ```
4. Save your list in the lists directory: `Packs/<pack_name>/Lists/`.

{% hint style="info" %}
### Note

If you download the list via the `demisto-sdk download` command, you do not need to change the file extension, as it downloads as `mylist.json`.
{% endhint %}

The following is an example of a list-checked\_integrations.json file.

```programlisting
    {
        "allRead": false,
        "allReadWrite": false,
        "data": "Cylance Protect v2_instance_1,Core REST API_instance_1,Image OCR_default_instance,McAfee ESM v2_instance_1,Microsoft Defender Advanced Threat Protection_instance_2,Rasterize_default_instance,Trend Micro Deep Security_instance_1,Where is the egg?_default_instance,d2,fcm_default_instance,vt,ad-login,ad-query,splunk",
        "dbotCreatedBy": "",
        "description": "",
        "fromVersion": "6.5.0",
        "hasRole": false,
        "id": "checked integrations",
        "itemVersion": "",
        "locked": false,
        "name": "checked integrations",
        "nameLocked": false,
        "packID": "",
        "previousAllRead": false,
        "previousAllReadWrite": false,
        "previousRoles": [],
        "roles": [],
        "system": false,
        "tags": null,
        "toVersion": "",
        "truncated": false,
        "type": "plain_text",
        "version": -1
    }
```
