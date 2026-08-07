# Set up an HTTP log collector to receive logs

In addition to logs from supported vendors, you can set up a custom HTTP log collector to receive logs in Raw, JSON, CEF, or LEEF format. The HTTP Log Collector can ingest up to 80,000 events per sec.

When Cortex XSIAM begins receiving logs from the third-party source, Cortex XSIAM automatically parses the logs and creates a dataset with the name `<Vendor>_< Product>_raw`. You can then use XQL Search queries to view logs and create new Correlation rules.

To set up an HTTP log collector to receive logs from an external source.

1.  Create an HTTP Log collector in Cortex XSIAM.

    a. Navigate to **Settings → Data Sources & Integrations**.

    b. On the **Data Sources & Integrations** page, click **+ Add New**, search for **HTTP**, then hover over it and click **Add**.

    c. Specify a descriptive **Name** for your HTTP log collection configuration.

    d. Select the data object **Compression**, either gzip or uncompressed.

    e. Select the **Log Format** as **Raw**, **JSON**, **CEF**, or **LEEF**.

    Cortex XSIAM supports logs in single line format or multiline format. For a JSON format, multiline logs are collected automatically when the **Log Format** is configured as JSON. When configuring a Raw format, you must also define the **Multiline Parsing Regex** as explained below.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>The Vendor and Product defaults to Auto-Detect when the <strong>Log Format</strong> is set to CEF or LEEF.</p><p>For a Log Format set to CEF or LEEF, Cortex XSIAM reads events row by row to look for the Vendor and Product configured in the logs. When the values are populated in the event log row, Cortex XSIAM uses these values even if you specified a value in the Vendor and Product fields in the HTTP collector settings. However, when the values are blank in the event log row, Cortex XSIAM uses the Vendor and Product that you specified in the HTTP collector settings. If you did not specify a Vendor or Product in the HTTP collector settings, and the values are blank in the event log row, the values for both fields are set to unknown.</p></div>

    f. Specify the Vendor and Product for the type of logs you are ingesting.

    g. (Optional) Specify the **Multiline Parsing Regex** for logs with multilines.

    This option is only displayed when the Log Format is set to Raw, so you can set the regular expression that identifies when the multiline event starts in logs with multilines. It is assumed that when a new event begins, the previous one has ended.

    h. **Save & Generate Token**.

    Click the copy icon next to the key and record it somewhere safe. You will need to provide this key when you configure your HTTP POST request and define the `api_key`. If you forget to record the key and close the window you will need to generate a new key and repeat this process. Click **Done** when finished.
2.  Send data to your Cortex XSIAM HTTP log collector.

    a. Send an HTTP POST request to the URL for your HTTP Log Collector.

    You can view a sample curl or python request on an HTTP collector instance by selecting **View Example**.

    Here is a CURL example:

    ```shell
    curl -X POST https://api-{tenant external URL}/logs/v1/event -H 'Authorization: {api_key}' -H 'Content-Type: text/plain' -d '{"example1": "test", "timestamp": 1609100113039} {"example2": [12321,546456,45687,1]}'
    ```

    Python 3 example:

    ```python
    import requests

    def test_http_collector(api_key):
        headers = {
            "Authorization": api_key,
            "Content-Type": "text/plain"
        }
        # Note: the logs must be separated by a new line
        body = "{'example1': 'test', 'timestamp': 1609100113039}" \
               "{'example2': [12321,546456,45687,1]}"
        res = requests.post(url="https://api-{tenant external URL}/logs/v1/event", headers=headers, data=body)
        return res
    ```

    b. Substitute the values specific to your configuration.

    * `url`: You can copy the URL for your HTTP log collector from the Custom Collectors page. For example: `https://api-{tenant external URL}/logs/v1/event`.
    * `Authorization`: Paste the `api_key` you previously recorded for your HTTP log collector, which is defined in the header.
    * `Content-Type`: Depending on the data object format you selected during setup, this will be `application/json` for JSON format or `text/plain` for Text format. This is defined as part of the header.
    * `Body`: The body contains the records you want to send to Cortex XSIAM. Separate records with a `\n` (new line) delimiter. The request body can contain up to 10 Mib records, but 1 Mib is recommended. In the case of a curl command, the records are contained in the `-d ‘<records>’` parameter.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>Each record cannot exceed 5 MB in size.</p></div>

    c. Review the possible success and failure code responses to your HTTP Post requests.

    The following table provides the various success and failure code responses to your HTTP Post requests, which can help you troubleshoot any problems with your HTTP Collector configuration.

    | Success/failure response code | Description                                                                                                                                             | Output code displayed (if applicable)                                          |
    | ----------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------ |
    | 200                           | Success code that indicates there are no errors and the request was successful.                                                                         | `{ "error": "false"}`                                                          |
    | 401                           | Unauthorized error code that indicates either an incorrect authorization token is being used or that the HTTP Collector is deleted/disabled.            |                                                                                |
    | 404                           | Error code 404 page not found that indicates a wrong URL.                                                                                               |                                                                                |
    | 413                           | Error code indicating the payload is too large as the request size limit is 10 MB.                                                                      |                                                                                |
    | 500                           | Error code indicating the request was not able to be processed due to an incorrect log format between the request and the HTTP collector configuration. | `{ "error": "error processing request, error: failed to process the request"}` |
    | 429                           | Error code indicating too many requests as the rate limit is 400 requests per second per customer per endpoint.                                         |                                                                                |
3. Monitor your HTTP Log Collection integration.

You can return to the **Settings → Data Sources & Integrations** page to monitor the status of your HTTP Log Collection configuration. For each instance, Cortex XSIAM displays the number of logs received in the last hour, day, and week. You can also use the Data Ingestion Dashboard to view general statistics about your data ingestion configurations.

4. After Cortex XSIAM begins receiving logs, use the XQL Search to search your logs.
