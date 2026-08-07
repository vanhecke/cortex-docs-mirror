# Create a triage

Use triage collections when a certain activity, group of activities, or the actions of a specific user on that endpoint have been identified, and additional information is required. The triage functionality collects detailed system information, including a full file listing for all of the connected drives, full event logs, and registry hives, to provide you with a complete, holistic picture of an endpoint.

Triage supports data collection from both online and offline hosts, on both Windows and macOS platforms.

1. In the **Triage Collection Name** field, enter a name that will be easy to find in the collections table.
2. Select the **Platform** either Windows, macOS or Linux.
3. In the **Description** field, enter information that is relevant to the collection you are creating .
4. For **Triage Type**, you can select **Offline** or **Online** or both.
5. Select **Offline** to upload archives containing forensic data collected by the Offline Collector. After the archive is uploaded, the data is extracted and ingested into the Forensics tables on the tenant. Import Offline Triage supports uploading packages created on Windows, macOS, and Linux platforms.
6. Click **Save Collection and Exit** or click **Next** to continue.
7. On the **Configuration** page, refer to [Configure Collection](../configure-collection) for information about each artifact.
8.  You can select a preset from **Select Presets (Windows/macOS/Linux)** to copy the options for artifacts, volatiles, and file collections from another collection.

    You can also click **Save new preset** to save the current collection as a potential triage collection.
9. Click **Save Collection and Exit** or click **Next** to continue.
