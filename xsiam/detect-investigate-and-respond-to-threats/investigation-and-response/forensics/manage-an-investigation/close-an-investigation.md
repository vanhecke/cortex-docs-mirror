# Close an investigation

From the list of ongoing investigations, you can close an investigation. You might want to close an investigation if resolved, or if you want to cancel the investigation.

{% hint style="info" %}
When you close an investigation, Palo Alto Networks has a grace period of 24 hours before deleting any collections associated with the investigation. During this timeframe, you have the option to cancel the close investigation action.
{% endhint %}

1. From the **Forensic Investigations** table, right-click an investigation and select **Close**.
2. In the **Close Investigation** widget, you can view all evidence collections exported for the investigation.
3. In the **Forensic Investigation** table, the status of the investigation changes to **Close Pending**, and the timestamp displays the time the investigation expires and the investigation data is deleted.
4. Right-click an investigation pending closure to display the following options::
   * **Edit**: Update the investigation name, description, or adjust user permissions.
   * **Open**: Cancel the close request.
   * **Permanently delete**: Delete the investigation and all associated data immediately. This action can't be canceled.
