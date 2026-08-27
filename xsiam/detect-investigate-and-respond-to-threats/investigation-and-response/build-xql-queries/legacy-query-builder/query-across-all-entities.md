---
description: >-
  Create legacy queries across all supported security data entities in Cortex
  XSIAM.
---

# Query across all entities

From the **Query Builder** you can perform a simple search for hosts and processes across all file events, network events, registry events, process events, event logs for Windows, and system authentication logs for Linux.

Some examples of queries you can run across all entities include:

* All activities on a host
* All activities initiated by a process on a host

### How to build a query

1. From Cortex XSIAM, select **Investigation & Response** → **Search** → **Query Builder**.
2. Select **ALL ACTIONS**.
3.  (Optional) Limit the scope to a specific acting process:

    Select Add Process to your search, and specify one or more of the following attributes for the acting (parent) process. Use a pipe (|) to separate multiple values. Use an asterisk (\*) to match any string of characters.

    | Field                                          | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
    | ---------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | NAME                                           | Name of the parent process.                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
    | PATH                                           | Path to the parent process.                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
    | CMD                                            | Command line used to initiate the parent process including any arguments, up to 128 characters.                                                                                                                                                                                                                                                                                                                                                                                                   |
    | MD5                                            | MD5 hash value of the parent process.                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
    | SHA256                                         | SHA256 hash value of the process.                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
    | USER NAME                                      | User who executed the process.                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
    | SIGNATURE                                      | Signing status of the parent process: Signed, Unsigned, N/A, Invalid Signature, Weak Hash.                                                                                                                                                                                                                                                                                                                                                                                                        |
    | SIGNER                                         | Entity that signed the certificate of the parent process.                                                                                                                                                                                                                                                                                                                                                                                                                                         |
    | PID                                            | Process ID of the parent process.                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
    | Run search on process, Causality and OS actors | The causality actor, also referred to as the causality group owner (CGO), is the parent process in the execution chain that the agent identified as being responsible for initiating the process tree. The OS actor is the parent process that creates an OS process on behalf of a different initiator. By default, this option is enabled to apply the same search criteria to initiating processes. To configure different attributes for the parent or initiating process, clear this option. |
4.  (Optional) Limit the scope to an endpoint or endpoint attributes:

    Select Add Host to your search and specify one or more of the following attributes:

    * HOST: HOST NAME, HOST IP address, HOST OS, HOST ADDRESS, or INSTALLATION TYPE.
    * INSTALLATION TYPE can be either an agent, or data collector.
    *   PROCESS: NAME , PATH , CMD , MD5 , SHA256 , USER NAME , SIGNATURE, or PID.

        Use a pipe (|) to separate multiple values. Use an asterisk (\*) to match any string of characters.
5.  Specify the time period for which you want to search for events.

    Options are Last 24H (hours), Last7D (days), Last1M (month), or select a Custom time period.
6.  Choose when to run the query.

    Select the calendar icon to schedule a query to run on or before a specific date or Run the query immediately and view the results in the Query Center.

    While the query is running, you can always navigate away from the page and a notification is sent when the query completes. You can also **Cancel** the query or run a new query, where you have the option to **Run only new query (cancel previous)** or **Run both queries**.
7. When ready, view the results in a query.
