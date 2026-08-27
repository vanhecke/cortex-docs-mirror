---
description: Create legacy process queries to investigate process activity in Cortex XSIAM.
---

# Create process query

From the **Query Builder** you can investigate connections between processes, child processes, and endpoints.

For example, you can create a process query to search for processes executed on a specific endpoint.

### How to build a process query

1. From Cortex XSIAM, select **Investigation & Response** → **Search** → **Query Builder**.
2. Select **PROCESS**.
3. Enter the search criteria for the process query.
   * Process action: Select the type of process action you want to search: On process **Execution** or **Injection** into another process.
   *   Process attributes—Define any additional process attributes for which you want to search.

       Use a pipe (**`|`**) to separate multiple values. Use an asterisk (**`*`**) to match any string of characters.

       By default, Cortex XSIAM will return results that match the attribute you specify. To exclude an attribute value, toggle the operator from **`=`** to **`!=`**. Attributes are:

       * **NAME**: Name of the process. For example, `notepad.exe`.
       * **PATH**: Path to the process. For example, `C:\windows\system32\notepad.exe`.
       * **CMD**: Command-line used to initiate the process including any arguments, up to 128 characters.
       * **MD5**: MD5 hash value of the process.
       * **SHA256**: SHA256 hash value of the process.
       * **USER NAME**: User who executed the process.
       * **SIGNATURE**: Signing status of the process: Signature Unavailable, Signed, Invalid Signature, Unsigned, Revoked, Signature Fail.
       * **SIGNER**: Signer of the process.
       * **PID**: Process ID.
       * **PROCESS\_FILE\_INFO**: Metadata of the process file, including file property details, file entropy, company name, encryption status, and version number.
       * **PROCESS\_SCHEDULED\_TASK\_NAME**: Name of the task scheduled by the process to run in the Task Scheduler.
       * **PROCESS\_TOKEN\_INFORMATION**: Bitwise token of the process privileges.
       * **DEVICE TYPE**: Type of device used to run the process: Unknown, Fixed, Removable Media, CD-ROM.
       * **DEVICE SERIAL NUMBER**: Serial number of the device type used to run the process.

       To specify an additional exception (match this value except), click the **+** to the right of the value and specify the exception value.
4.  (Optional) Limit the scope to a specific acting process:

    Select **+PROCESS** and specify one or more of the following attributes for the acting (parent) process.

    * **NAME**: Name of the parent process.
    * **PATH**: Path to the parent process.
    * **CMD**: Command-line used to initiate the parent process including any arguments, up to 128 characters.
    * **MD5**: MD5 hash value of the parent process.
    * **SHA256**: SHA256 hash value of the process.
    * **USER NAME**: User who executed the process.
    * **SIGNATURE**: Signing status of the parent process: Signed, Unsigned, N/A, Invalid Signature, Weak Hash
    * **SIGNER**: Entity that signed the certificate of the parent process.
    * **PID**: Process ID of the parent process.
    * **Run search on process, Causality and OS actors**: The causality actor—also referred to as the causality group owner (CGO)—is the parent process in the execution chain that the Cortex XDR agent identified as being responsible for initiating the process tree. The OS actor is the parent process that creates an OS process on behalf of a different initiator. By default, this option is enabled to apply the same search criteria to initiating processes. To configure different attributes for the parent or initiate a process,
5.  (Optional) Limit the scope to an endpoint or endpoint attributes:

    Select **+HOST** and specify one or more of the following attributes:

    *   **HOST**: **HOST NAME**, **HOST IP** address, **HOST OS**, **HOST MAC ADDRESS**, or **INSTALLATION TYPE**.

        **INSTALLATION TYPE** can be Cortex XDR agent.
    * **PROCESS**: **NAME**, **PATH**, **CMD**, **MD5**, **SHA256**, **USER NAME**, **SIGNATURE**, or **PID**.
6.  Specify the time period for which you want to search for events.

    Options are **Last 24H** (hours), **Last 7D** (days), **Last 1M** (month), or select a **Custom** time period.
7.  Choose when to run the query.

    Select the calendar icon to schedule a query to run on or before a specific date or **Run** to run the query immediately and view the results in the **Query Center**.

    While the query is running, you can always navigate away from the page and a notification is sent when the query completes. You can also **Cancel** the query or run a new query, where you have the option to **Run only new query (cancel previous)** or **Run both queries**.
8. When you are ready, view the results of the query. For more information, see [Review XQL query results](../how-to-build-xql-queries/review-xql-query-results).
