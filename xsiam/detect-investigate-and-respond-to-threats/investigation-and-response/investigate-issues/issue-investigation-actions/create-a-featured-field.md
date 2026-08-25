---
description: Create Cortex XSIAM featured fields to highlight important issue attributes.
---

# Create a featured field

To help you to track issues involving specific hosts, users, and IP addresses, you can label specific issue attributes as featured fields. Issues that contain a matching featured field value are identified with a ![featured-alert-field-flag.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-2bd8d659933ac3b2db859d096e4d906e39bb74b8%2F51168d952b300ec2376c3ada4e1f381c8747716358f8e62a79557dcb169f0260.png?alt=media) flag in the **Name** field of the **Issues** table. After setting up featured fields, you can use them filter the **Issues** table and to create case scoring rules.

{% hint style="info" %}
Featured Active Directory values are displayed in the **User** and **Host** fields accordingly.
{% endhint %}

### How to create a featured field

1. Go to Cases & Issues → Case Configuration → **Featured Fields** and select a type of featured field.
2. Click **Add featured \<field-type>** and select one of the following options:
   *   **Create New**

       To create a new featured field from scratch, enter one or more field-type values and click **Add**.
   *   **Upload from File**

       To upload field values from a CSV file, upload your file and click **Import**. Click **Download example file** to ensure you are using the correct format.
3.  Find issues containing featured fields.

    In the **Issues** table, use the **Contains Featured** filters.
4. (Optional) Create a case scoring rule using the **Contains Featured** fields to further highlight and prioritize issues containing the Host, User, and IP address attributes.
