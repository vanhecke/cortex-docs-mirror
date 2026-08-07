# XQL Query best practices

Cortex XSIAM includes built-in mechanisms for mitigating long-running queries. These include default limits for allowed issues and returned rows. XDM queries search only specified mapped datasets. The following suggestions help streamline your queries:

*   Add a smaller limit by using a `limit` stage.

    The default result limit is 1,000 for XDM and dataset queries. This applies when no limit is stated. It applies to basic queries with no stages except `fields`. It does not apply to widgets, Correlation Rules, public APIs, saved queries, or scheduled queries. Those allow up to 1,000,000 results. Legacy templates allow 10,000 results.

    ```programlisting
    datamodel dataset = microsoft_windows_raw 
    | fields *host* 
    | limit 100
    ```
* Use a small **Timeframe**. Select **Relative time** and define **Last 30 Minutes** where possible.
* Use filters that exclude data, along with other applicable filters.
* Select only the fields required in the results.
