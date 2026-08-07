# Import file hash exceptions

The **Action Center** displays information on files that are quarantined, or included in the allow list and block list. To import hashes from the Endpoint Security Manager or from external feeds, take the following steps:

1. Go to **Investigation & Response → Response → Action Center →** **New Action**.
2. Select **Import Hash Exceptions**.
3.  Drag your file to the drop area.

    Files must be in csv format, for example `Verdict_Override_Exports.csv`. If necessary, resolve any conflicts encountered during the upload and retry.
4. Click **Next**.
5.  Review the action summary, and click **Done**.

    Cortex XSIAM imports your hashes. Depending on the assigned verdict, Cortex XSIAM then distributes them to the allow list or block list.
