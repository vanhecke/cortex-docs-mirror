# Create registry query

From the Query Builder you can investigate connections between registry activity, processes, and endpoints.

Some examples of a registry query you can run include:

* Modified registry keys on specific endpoints.
* Registry keys related to process activity that exist on specific endpoints.

### How to build a registry query

1. From Cortex XSIAM, select **Investigation & Response** → **Search** → **Query Builder**.
2. Select **REGISTRY**.
3. Enter the search criteria for the registry events query.
   * Registry action: Select the type or types of registry actions you want to search: **Key Create**, **Key Delete**, **Key Rename**, **Value Set**, or **Value Delete**.
   *   Registry attributes: Define any additional registry attributes for which you want to search. By default, Cortex XSIAM will return the events that match the attribute you specify. To exclude an attribute value, toggle the **`=`** option to **`=!`**. Attributes are:

       *   **KEY NAME**: Registry key name.

           <div data-gb-custom-block data-tag="hint" data-style="warning" class="hint hint-warning"><p>Ensure the <strong>KEY NAME</strong> is entered as a real registry key name, and not as a symbolic link. Otherwise, the query will not retrieve results.</p><p>Instead of <code>HKEY_LOCAL_MACHINE\System\CurrentControlSet</code>, which is a symbolic link, use <code>KEY_LOCAL_MACHINE\System\ControlSet001</code>.</p><p>Instead of <code>HKEY_CURRENT_USER</code>, use <code>HKEY_USERS&#x26;#x3C;SID></code>, where SID is either a SID of the current user or an asterisk (<code>*</code>) to represent any SID.</p></div>
       * **DATA**: Registry key data value.
       * **KEY PREVIOUS NAME**: Name of the registry key before modification.
       * **VALUE NAME**: Registry value name.

       To specify an additional exception (match this value except), click the **+** to the right of the value and specify the exception value.
4.  (Optional) To limit the scope to a specific source, click the **+** to the right of the value and specify the exception value.

    Specify one or more attributes for the source.

    Use a pipe (**|**) to separate multiple values. Use an asterisk (**\***) to match any string of characters.

    * **NAME**: Name of the parent process.
    * **PATH**: Path to the parent process.
    * **CMD**: Command-line used to initiate the process, including any arguments, up to 128 characters.
    * **MD5**: MD5 hash value of the process.
    * **SHA256**: SHA256 hash value of the process.
    * **USER NAME**: User who executed the process.
    * **SIGNATURE**: Signing status of the parent process: Signature Unavailable, Signed, Invalid Signature, Unsigned, Revoked, Signature Fail.
    * **SIGNER**: Entity that signed the certificate of the parent process.
    * **PID**: Process ID of the parent process.
    * **Run search for process, Causality, and OS actors**: The causality actor—also referred to as the causality group owner (CGO)—is the parent process in the execution chain that the Cortex XDR agent identified as being responsible for initiating the process tree. The OS actor is the parent process that creates an OS process on behalf of a different indicator. By default, this option is enabled to apply the same search criteria to initiating processes. To configure different attributes for the parent or initiate the process, clear this option.
5.  (_Optional_) Limit the scope to an endpoint or endpoint attributes:

    Specify one or more of the following attributes: Use a pipe (**|**) to separate multiple values.

    Use an asterisk (**\***) to match any string of characters.

    * **HOST**: **HOST NAME**, **HOST IP** address, **HOST OS**, **HOST MAC ADDRESS**, or **INSTALLATION TYPE**.
    * **INSTALLATION TYPE** can be either Cortex XDR agent or Data Collector.
    * **PROCESS**: **NAME**, **PATH**, **CMD**, **MD5**, **SHA256**, **USER NAME**, **SIGNATURE**, or **PID**.
6.  Specify the time period for which you want to search for events.

    Options are **Last 24H** (hours), **Last 7D** (days), **Last 1M** (month), or select a **Custom** time period.
7.  Choose when to run the query.

    Select the calendar icon to schedule a query to run on or before a specific date or **Run** to run the query immediately and view the results in the **Query Center**.

    While the query is running, you can always navigate away from the page and a notification is sent when the query completes. You can also **Cancel** the query or run a new query, where you have the option to **Run only new query (cancel previous)** or **Run both queries**.
8. When you are ready, view the results of the query. For more information, see [Review XQL query results](../how-to-build-xql-queries/review-xql-query-results).
