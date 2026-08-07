# Filter and Transform data

### Filter and transform data

Use filters and transformers to manipulate data. Add them to playbook tasks or instance mappings.

Cortex XSIAM collects data from playbook tasks, command results, and fetched issues. It presents this data in JSON format. Filters and transformers manipulate this data.

### Filters

Filters extract relevant data for use elsewhere in Cortex XSIAM. For example, an issue can contain files with different types and extensions. Filter these files by extension or type, then use them in a detonation playbook.

You can filter as many objects as needed. Cortex XSIAM automatically calculates the context root for each filter. Change it only when necessary.

{% hint style="warning" %}
**Caution:** Changing the context data root can affect filter results. The drop-down list displays the filter root for backward compatibility.
{% endhint %}

### Transformers

Transformers modify or format data for further processing or presentation. For example, convert a non-Unix date to Unix format. The `count` transformer returns the number of elements.

When you add multiple transformers, Cortex XSIAM applies them in displayed order. Drag and drop transformers to reorder them.

### Add filters and transformers to a playbook task

1. Create or edit a playbook task.
2. In the relevant field, such as inputs or outputs, click the curly brackets.
3. Select **Filters and Transformers**.
4. In **Get**, enter or select the data to filter or transform. For example, `EWS.Items.Name`.
5. Optional: Add a filter.
   1. In **Filter**, click **Add filter**. The context root is populated automatically.
   2. Select the data to filter.
   3. Select the filter operators.
   4. Enter a value.
   5. Select the checkbox to save the filter.
6. Optional: Add a transformer.
   1. Click **Add transformer**.
   2. Select the transformer. The default is `To upper case(String)`.
   3. Select the transformer operators.
   4. Select the checkbox to save.
7. Optional: Click **Test** to test the filter or transformation. Select an investigation or add one manually.

<details>

<summary>Example: Filter items with an EXE extension</summary>

In this example, we want to filter all EWS Item names that have the extension **`exe`**.

[![playbook-context.png](https://docs-cortex.paloaltonetworks.com/api/khub/maps/5CAbsl8idaK8R43ZLhoTOw/resources/rgUnRM4xGU~VYImG3Q2WNw-5CAbsl8idaK8R43ZLhoTOw/content?v=5050733512ad3fe5\&Ft-Calling-App=ft/turnkey-portal)](https://docs-cortex.paloaltonetworks.com/viewer/attachment/5CAbsl8idaK8R43ZLhoTOw/rgUnRM4xGU~VYImG3Q2WNw-5CAbsl8idaK8R43ZLhoTOw)

1.  From the Filters & transformers window, in the Get field, type **`EWS.Items.Name`** to extract all Item names in EWS.

    The context root to filter is **`EWS,Items`**.

    [![filter-name.png](https://docs-cortex.paloaltonetworks.com/api/khub/maps/5CAbsl8idaK8R43ZLhoTOw/resources/jwTmxvdmPdem_X5ONmBlIw-5CAbsl8idaK8R43ZLhoTOw/content?v=cc30b7aa67c0d70f\&Ft-Calling-App=ft/turnkey-portal)](https://docs-cortex.paloaltonetworks.com/viewer/attachment/5CAbsl8idaK8R43ZLhoTOw/jwTmxvdmPdem_X5ONmBlIw-5CAbsl8idaK8R43ZLhoTOw)
2. In the Filter section, click Add filter.
3. In the left-hand side, add **`Extension`** to the filter.
4. Select Equals (String) → ignore case.
5.  In the right-hand side add **`exe`**.

    [![filter-exe.png](https://docs-cortex.paloaltonetworks.com/api/khub/maps/5CAbsl8idaK8R43ZLhoTOw/resources/igqRBWKQV9D7SP_GHjl5uw-5CAbsl8idaK8R43ZLhoTOw/content?v=42738521ce167791\&Ft-Calling-App=ft/turnkey-portal)](https://docs-cortex.paloaltonetworks.com/viewer/attachment/5CAbsl8idaK8R43ZLhoTOw/igqRBWKQV9D7SP_GHjl5uw-5CAbsl8idaK8R43ZLhoTOw)
6. Click the tick box to save the filter.
7.  Click Test.

    You should see Item names are filtered with the extension **`exe`**.

</details>

<details>

<summary>Example (advanced): Filter hostname for the last resolved time</summary>

This example returns the `LastResolved` time for the `demisto.com` hostname.

Use the following data:

```json
{
  "IP": [
    {
      "Address": "192.168.10.96",
      "AutoFocus": {
        "Resolutions": [
          {
            "Hostname": "79463wwfqq,dattolocal.net",
            "LastResolved": "2022-08-02 04:01:02"
          },
          {
            "Hostname": "demisto.com",
            "LastResolved": "2022-09-10 09:47:17"
          },
          {
            "Hostname": "securesense.call4pchelp.com",
            "LastResolved": "2022-04-22 11:49:06"
          }
        ]
      }
    },
    {
      "Address": "192.168.10.96",
      "AutoFocus": {
        "Resolutions": [
          {
            "Hostname": "79463wwfqq,dattolocal.net",
            "LastResolved": "2022-08-02 04:01:02"
          },
          {
            "Hostname": "demisto.com",
            "LastResolved": "2022-09-10 09:47:17"
          },
          {
            "Hostname": "securesense.call4pchelp.com",
            "LastResolved": "2022-04-22 11:49:06"
          }
        ]
      }
    }
  ]
}
```

1.  From the Filters & transformers window, in the Get field, type **`IP.AutoFocus.Resolutions.LastResolve`**.

    | [![playbook-filter-auto.png](https://docs-cortex.paloaltonetworks.com/api/khub/maps/5CAbsl8idaK8R43ZLhoTOw/resources/V~icGiDLWnFo7szpvAcoiw-5CAbsl8idaK8R43ZLhoTOw/content?v=03519d4d6a0c3664\&Ft-Calling-App=ft/turnkey-portal)](https://docs-cortex.paloaltonetworks.com/viewer/attachment/5CAbsl8idaK8R43ZLhoTOw/V~icGiDLWnFo7szpvAcoiw-5CAbsl8idaK8R43ZLhoTOw) |
    | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
2.  In the Filter section, click Add filter.

    Cortex XSIAM automatically calculates that the context root to filter is **`IP.AutoFocus.Resolutions`**.

    | [![playbook-filter-autores.png](https://docs-cortex.paloaltonetworks.com/api/khub/maps/5CAbsl8idaK8R43ZLhoTOw/resources/PipxoFsQUeA_F~KtiiB1fA-5CAbsl8idaK8R43ZLhoTOw/content?v=cdfd5beb4add721a\&Ft-Calling-App=ft/turnkey-portal)](https://docs-cortex.paloaltonetworks.com/viewer/attachment/5CAbsl8idaK8R43ZLhoTOw/PipxoFsQUeA_F~KtiiB1fA-5CAbsl8idaK8R43ZLhoTOw) |
    | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
3. In the left-hand side, add **`Hostname`** to the filter.
4. Select Equals (String) → Ends with.
5. In the right-hand side, add **`demisto.com`**.
6.  Click the checkbox to save.

    | [![playbook-filter-autofilter.png](https://docs-cortex.paloaltonetworks.com/api/khub/maps/5CAbsl8idaK8R43ZLhoTOw/resources/YtAXZUsSW_HioJ_pJLx9uA-5CAbsl8idaK8R43ZLhoTOw/content?v=5a55dc026c2e2af7\&Ft-Calling-App=ft/turnkey-portal)](https://docs-cortex.paloaltonetworks.com/viewer/attachment/5CAbsl8idaK8R43ZLhoTOw/YtAXZUsSW_HioJ_pJLx9uA-5CAbsl8idaK8R43ZLhoTOw) |
    | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
7.  Click Test.

    | [![playbook-filter-autotest.png](https://docs-cortex.paloaltonetworks.com/api/khub/maps/5CAbsl8idaK8R43ZLhoTOw/resources/woOUejDSmq0jm61SZRcAHA-5CAbsl8idaK8R43ZLhoTOw/content?v=f983673136f5f40d\&Ft-Calling-App=ft/turnkey-portal)](https://docs-cortex.paloaltonetworks.com/viewer/attachment/5CAbsl8idaK8R43ZLhoTOw/woOUejDSmq0jm61SZRcAHA-5CAbsl8idaK8R43ZLhoTOw) |
    | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

</details>
