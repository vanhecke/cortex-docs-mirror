---
description: Remove a Cortex XSIAM engine safely from its host and tenant configuration.
---

# Remove an engine

You can remove an engine when it is no longer needed.

*   Run one of the following commands according to your operating system:

    | Installation | Command                                                                                                                                                                                                                       |
    | ------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | RPM          | Get the full package: \*\*\`rpm -qa                                                                                                                                                                                           |
    | DEB          | <p>Get the full package: <strong><code>dpkg-query -W -f='${Package}' d1_*</code></strong></p><p>Remove the package: <strong><code>dpkg --purge </code></strong><em><strong><code>&#x3C;package name></code></strong></em></p> |
    | SH           | Remove an Engine: **` sudo`` `` `**_**`<engine-file-path>`**_**`-- -purge`**                                                                                                                                                  |
