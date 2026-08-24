---
description: Configure a Cortex XSIAM engine to connect directly without a proxy.
---

# Configure the engine to call the server without using a proxy

In some cases, due to specific environment architecture, you may need to configure the engine to use a proxy when working with integrations, but not use a proxy when calling the Cortex XSIAM tenant.

1.  On the computer where you have installed the engine, go to the directory for `d1.conf` file.

    For RPM, DEB, Shell go to `/usr/local/demisto`.
2.  Add the following configuration:

    | Key                          | Value                               |
    | ---------------------------- | ----------------------------------- |
    | **`engine.to.server.proxy`** | **`false`** (default is **`true`**) |
