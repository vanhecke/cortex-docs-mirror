# Offline triage collection

The Forensics add-on provides a triage collection option for endpoints with no network connection or no Cortex XDR agent currently installed.

Note that the procedure differs between Windows, macOS, and Linux.

<details>

<summary>Windows</summary>

1. Select **Investigation & Response** → **Forensics**.
2. Click the investigation link and from the **Collections** tab, find the triage and click the menu options button (![menu\_options\_button.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-331c8c3490835539d195f8e04f03b118319faf9c%2F14295c9ed3582f910adab35625272fabebd445feea2f94953c97bab3f3569464.png?alt=media))/ Depending on the system type of the endpoint, select **Download 32-bit Collector** or **Download 64-bit Collector** .
3. Copy the downloaded file to a location accessible from the targeted endpoint.
4.  From the endpoint, open the folder containing the offline triage collector and right-click on the executable file **cortex-xdr-payload.exe** and select `Run as administrator`.

    The `cortex-xdr-payload.exe` opens a command window that displays the status of each artifact collection.

    After the collection is completed, a zip file with the hostname and a timestamp in the file name is created in the same directory as the executable.
5. From the **Collections** page, select the triage and click the menu options button (![menu\_options\_button.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-331c8c3490835539d195f8e04f03b118319faf9c%2F14295c9ed3582f910adab35625272fabebd445feea2f94953c97bab3f3569464.png?alt=media)) and select **Upload Offline Package**.
6.  In the **Import Offline Triage** dialog, browse for or drag and drop the zip file, and click **Done**.

    The triage file is ingested, and the results are available for review.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>Security software running on the endpoint (including the Cortex agent) can interfere with or block the execution of the offline triage collector. Disable any security software on the endpoint while the collector is running, or whitelist the collector in your security software before running the offline triage collector.</p></div>

</details>

<details>

<summary>macOS</summary>

1. Select **Investigation & Response** → **Forensics**.
2. Click the investigation link and from the **Collections** tab, find the triage and click the menu options button (![menu\_options\_button.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-331c8c3490835539d195f8e04f03b118319faf9c%2F14295c9ed3582f910adab35625272fabebd445feea2f94953c97bab3f3569464.png?alt=media)) and select **Download Collector**.
3. Open the folder containing the zip file and run the command `xattr -c <triage_configuration_name>.zip` to remove any extended attributes that macOS might have applied to the file.
4. Copy the downloaded zip file to a destination that is accessible from the targeted endpoint.
5.  From the endpoint, open the folder containing the offline triage collector and run the **cortex-xdr-payload.exe** file, or from a command line, enter: `sudo cortex-xdr-payload`.

    After the collection is completed, a zip file with the hostname and a timestamp in the file name is created in the same directory as the executable.
6. From the **Collections** page, select the triage and click the menu options button (![menu\_options\_button.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-331c8c3490835539d195f8e04f03b118319faf9c%2F14295c9ed3582f910adab35625272fabebd445feea2f94953c97bab3f3569464.png?alt=media)) and select **Upload Offline Package**.
7.  In the **Import Offline Triage** dialog, browse for or drag and drop the zip file, and click **Done**.

    The triage file is ingested, and the results are available for review.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>Security software running on the endpoint (including the Cortex agent) can interfere with or block the execution of the offline triage collector. Disable any security software on the endpoint while the collector is running, or whitelist the collector in your security software before running the offline triage collector.</p></div>

</details>

<details>

<summary>Linux</summary>

1. Select **Investigation & Response** → **Forensics**.
2. Click the investigation link and from the **Collections** tab, find the triage and click the menu options button (![menu\_options\_button.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-331c8c3490835539d195f8e04f03b118319faf9c%2F14295c9ed3582f910adab35625272fabebd445feea2f94953c97bab3f3569464.png?alt=media)) and select **Download x86 Collector** or **Download ARM64 Collector**.
3. Copy the downloaded zip file to a destination that is accessible from the targeted endpoint.
4.  From the endpoint, open the folder containing the offline triage collector and run the **cortex-xdr-payload** file, or from a command line, enter: `sudo ./cortex-xdr-payload`.

    After the collection is completed, a zip file with the hostname and a timestamp in the file name is created in the same directory as the executable.
5. From the **Collections** page, select the triage and click the menu options button (![menu\_options\_button.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-331c8c3490835539d195f8e04f03b118319faf9c%2F14295c9ed3582f910adab35625272fabebd445feea2f94953c97bab3f3569464.png?alt=media)) and select **Upload Offline Package**.
6.  In the **Import Offline Triage** dialog, browse for or drag and drop the zip file, and click **Done**.

    The triage file is ingested, and the results are available for review.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>Security software running on the endpoint (including the Cortex agent) can interfere with or block the execution of the offline triage collector. Disable any security software on the endpoint while the collector is running, or whitelist the collector in your security software before running the offline triage collector.</p></div>

</details>
