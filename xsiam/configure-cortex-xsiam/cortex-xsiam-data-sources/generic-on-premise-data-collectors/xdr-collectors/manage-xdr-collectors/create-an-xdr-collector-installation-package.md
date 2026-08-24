---
description: Create an XDR Collector package for Cortex XSIAM.
---

# Create an XDR Collector installation package

To install a Cortex XDR Collector for the first time, you must first create an XDR Collector installation package. After you create and download an installation package, you can then install it directly on the collector machine, or you can use a software deployment tool of your choice to distribute the software to multiple collector machines.

To install the XDR Collector software, you must use a valid installation package that exists in your XDR Collectors console. If you delete an installation package, any XDR Collectors installed from this package are not able to register to Cortex XSIAM.

{% hint style="info" %}
XDR Collectors cannot be moved between Cortex XSIAM managing servers. In this situation, you need to uninstall the existing collector, and then install a new collector using an installation package from the new managing server. For more information on uninstalling, see [Uninstall the XDR Collector](uninstall-the-xdr-collector).
{% endhint %}

To create a new installation package.

1.  In Cortex XSIAM, select Settings [![403822\_spr.png](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABcAAAAXCAMAAADX9CSSAAABMlBMVEUBExwsXHuWnaEBGSjp/P/7+fr59/pUX18KIi7///9DPx4IHjnv+P37+/z/+fA9YXjs9v///e8tExwBHC7T7Pv16tcZHSy1zOT///3Sx7xiV0gJOE5dOCsoNDEBEyan1O367NMpSVxocXMJQXX8//+EPhwnXonq8fdvksv//+cCExwBSYb+///dwqQGFyAFFx8BEx+s1u/Tpk4BEyDT6/fozJ4BE3f9//+WlJVUWFMEExwBPGr6//85ExwBWXdyb3AZJSUBEyLN7Pz//v7OoU7pzqIBOm2PWhwnXojo7/aMt9v/+OoSExwBMkp2SjABGCzM6fgVEySQtMz9//3Sx7tbU0IIHTjp9/37+fj//flbaoH//u8uExySm5sZExwGIC1DQB4BFyfi+v/p6Ofg4OQqU3TfkNjDAAAACXBIWXMAABwgAAAcIAHND5ueAAABRklEQVQoz2WS1XJCQQyGg7UsenAtUlyL68Hd3R3K+79Clz2UgSEXmz/fJJnsZgH+jcVms1nwZhwu74PH5bzCTwA+EoAA8Ym+m1AklkgpmRzkMkoqEYuEDFYoVWqNVqfHUq/TatQqpYJwAzICfN1rsTciA5Ems4V467eVeIvZxOTY7A4Apwsh5HICOOy2e63b4wWfPxD8CQb8PvB63DcYCiMUgWgsTlLisShEEAqHIJFMpTOQpXOE5+gsZNKpZALzW5xH954ofzsJLxThJR+KBcxLZVSp4v41wmu4f7WCyiVmHniaB5h5sNXpBkCzhedvNQEadJ3BoXan+3TfbqcdIrxH918evU/3iB8MVaPxZDrDcjadjEeq4YBJmC+WqzW12cJ2Q61Xy8X8Ubrbw8F/hKP/APvd6ypP58vv5Xx6X/wV/4frI/oDroEwkWhUg0UAAAAASUVORK5CYII=)](https://docs-cortex.paloaltonetworks.com/viewer/attachment/5CAbsl8idaK8R43ZLhoTOw/f5xwAeqXj9QeVUrVA9e0AQ-5CAbsl8idaK8R43ZLhoTOw) → Configurations → XDR Collectors → Installers.

    [![xdr-collectors-installations.png](https://docs-cortex.paloaltonetworks.com/api/khub/maps/5CAbsl8idaK8R43ZLhoTOw/resources/wJ88XPo6XDUSI3gvFblxgw-5CAbsl8idaK8R43ZLhoTOw/content?v=702d30e2f7701ff1\&Ft-Calling-App=ft/turnkey-portal)](https://docs-cortex.paloaltonetworks.com/viewer/attachment/5CAbsl8idaK8R43ZLhoTOw/wJ88XPo6XDUSI3gvFblxgw-5CAbsl8idaK8R43ZLhoTOw)
2.  Click Create.

    [![create-new-installer.png](https://docs-cortex.paloaltonetworks.com/api/khub/maps/5CAbsl8idaK8R43ZLhoTOw/resources/iL7pV509J9ZoaA~nFhgyIA-5CAbsl8idaK8R43ZLhoTOw/content?v=c9d03d7a60df8ccd\&Ft-Calling-App=ft/turnkey-portal)](https://docs-cortex.paloaltonetworks.com/viewer/attachment/5CAbsl8idaK8R43ZLhoTOw/iL7pV509J9ZoaA~nFhgyIA-5CAbsl8idaK8R43ZLhoTOw)
3.  Enter a unique Name and an optional Description to identify the installation package.

    The package Name must be no more than 100 characters and can contain letters, numbers, hyphens, underscores, commas, and spaces.
4. Select the Platform for which you want to create the installation package as either Windows or Linux.
5. Select the Version.
6.  Create the installation package.

    Cortex XSIAM prepares your installation package and makes it available in the XDR Collectors Installations page.
7.  Download your installation package.

    When the status of the package displays `Completed`, right-click the Collector Version row, and click Download.

    * For a Windows installation, select Download 64 bit installer.
    * For a Linux installation, you can download the Linux RPM installer or download the Linux DEB installer (according to your Linux collector machine distribution), and deploy the installers on the on-premise collector machines using the Linux package manager. Alternatively, you can download the Linux SH installer and deploy it manually on the Linux collector machine.

    Once the applicable installation package is downloaded, you can install the package.

    * [Install the XDR Collector installation package for Windows](install-the-xdr-collector-installation-package-for-windows).
    * [Install the XDR Collector installation package for Linux](install-the-xdr-collector-installation-package-for-linux).
8.  Other available options.

    As needed, you can return to the XDR Collectors Installations page to manage your XDR Collectors installation packages. To manage a specific package, right-click the Collector Version, and select the desired action:

    * Edit the package name or description.
    *   Delete the installation package. Deleting an installation package does not uninstall the XDR Collector software from any on-premise collector machines.

        Since Cortex XSIAM relies on the installation package ID to approve XDR Collector registration during install, it is not recommended to delete the installation package for any active on-premise collector machines. Hiding the installation package will remove it from the default list of available installation packages and can be useful to eliminate confusion in the XDR Collectors console main view. These hidden installations can be viewed by removing the default filter.
    * Copy text to clipboard to copy the text from a specific field in the row of an installation package.
    * Hide installation packages. Using the Hide option provides a quick method to filter out results based on a specific value in the table. You can also use the filters at the top of the page to build a filter from scratch. To create a persistent filter, save ([![save-icon.png](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABIAAAASCAYAAABWzo5XAAAACXBIWXMAABYlAAAWJQFJUiTwAAAAB3RJTUUH4woWDzcfdZU5kgAAAAd0RVh0QXV0aG9yAKmuzEgAAAAMdEVYdERlc2NyaXB0aW9uABMJISMAAAAKdEVYdENvcHlyaWdodACsD8w6AAAADnRFWHRDcmVhdGlvbiB0aW1lADX3DwkAAAAJdEVYdFNvZnR3YXJlAF1w/zoAAAALdEVYdERpc2NsYWltZXIAt8C0jwAAAAh0RVh0V2FybmluZwDAG+aHAAAAB3RFWHRTb3VyY2UA9f+D6wAAAAh0RVh0Q29tbWVudAD2zJa/AAAABnRFWHRUaXRsZQCo7tInAAACLUlEQVQ4jZ2TzUtUYRSHn2NXUiLRnPwYUdCIiKQUzUzKDIPARdFSyzYxZLQdiPA/qIg2EQRBBYWFSAhWRBZRSV8DUbTpgwELyUpNSsd7r+NpcT98G8dFvZtzf7wf5zm/c66kHFdFBFVFEBTlf7QFoApHe09RFS0jnU7zaXQMUECWjdWVZeRaudRvWk9HWwuSclzt6T3NjaFh4rEuhkde8SH5hTWFq1luTU3/orqynPaWRi5cu8XX54NYKFRGS4nHOuk9fpi5OZuOtu3EY53eLQUkIPHCucs3Gf8+yYmeQ5y91IcCOYiZS/hn7S9L1dxQZlI2s3NOqFV9IEOb58OHJCPDvj07OH+1n8b9R1jO7B+TP4nHurIRBZmUXU11rMgRigoKECEkMuPjl6/pOXgAx3VDMst7VBDxM4qyc2tdSKB482Lq2g01BqF33yKDqG/wPhVlkawkZsxfmcfmjetCohzT/f7bD7kycIeM1mTV95684GnijUFkuL82UsTJY920Nm3xCP2KAhJTv09+pqaqwvAozKihE2PjE743gRNCeUlxqAPCRc7gX/O3gxl58CxhjgjlJcUoSrQkQrbzGhCFmfyP4sKCv0pxXJeJqWmipRGvtAzrBLBAmU3ZjI6N01xfCyi7mxsMYxfbbNtuqOfn0zjOPHtbt3mdnLVdffcxyZmL1xm4+4iFhQVEMru0dCnQ3tLASOIt3xJDyIztqBi2/U6lMPXiQC7Vq/LzQv0HyDUNJLqSD+QAAAAASUVORK5CYII=)](https://docs-cortex.paloaltonetworks.com/viewer/attachment/5CAbsl8idaK8R43ZLhoTOw/2r~0bs3GbmfbBtm536gLFw-5CAbsl8idaK8R43ZLhoTOw)) it.

<br>
