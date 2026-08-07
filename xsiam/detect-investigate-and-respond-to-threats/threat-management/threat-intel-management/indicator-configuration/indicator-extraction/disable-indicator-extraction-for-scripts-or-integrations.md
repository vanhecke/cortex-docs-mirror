---
description: >-
  Prevent selected scripts or integrations from automatically extracting
  indicators.
---

# Disable indicator extraction for scripts or integrations

By default, system-wide indicator extraction and enrichment is disabled.

If you have the TIM add-on and you have enabled system-wide indicator extraction and enrichment, the procedure below enables you to disable indicator extraction for a specific script or integration.

{% hint style="info" %}
### Note

The TIM add-on is included in the Cortex XSIAM Premium license.
{% endhint %}

*   To disable indicator extraction for a script, add the **`IgnoreAutoExtract`** entry with the value of **`true`**, when returning an entry.

    For example:

    ```programlisting
    entry = {
        'Type': entryTypes['note'],
        'Contents': {
        'Echo' : demisto.args()['echo']
            },
        'ContentsFormat': formats['json'],
        'ReadableContentsFormat': formats['markdown'],
        'HumanReadable': hr,
        'IgnoreAutoExtract' : True
       }
    ```
*   To disable indicator extraction for an integration, add the **`'IgnoreAutoExtract'`** entry with the value of **`true`**, when returning an entry.

    For example in the ServiceNow integration:

    ```programlisting
    entry = {
            'Type': entryTypes['note'],
            'Contents': result,
            'ContentsFormat': formats['json'],
            'ReadableContentsFormat': formats['markdown'],
            'HumanReadable': tableToMarkdown('ServiceNow ticket', hr, headers=headers, removeNull=True),
            'EntryContext': {
                'Ticket(val.ID===obj.ID)': context,
                'ServiceNow.Ticket(val.ID===obj.ID)': context
            },
            'IgnoreAutoExtract': True
        }
        entries.append(entry)
        return entries
    ```

For more information about command results in Python, see [Python code conventions for CommandResults](https://xsoar.pan.dev/docs/integrations/code-conventions#commandresults).
