# Install the XDR collector on Windows using the MSI

Use the following workflow to install the XDR Collector using the MSI file.

Before completing this task, ensure that you [create and download a Cortex XDR Collector installation package](../create-an-xdr-collector-installation-package) in Cortex XSIAM.

To install an XDR Collector installation package on Windows using the MSI file.

{% hint style="info" %}
When the package is executed using the MSI, an installation log is generated in `%TEMP%\MSI<Random characters>.log` by default.
{% endhint %}

1. With Administrator level privileges, run the MSI file that you downloaded in Cortex XSIAM on the collector machine. The installer displays a welcome dialog.
2. Click Next.
3. Select I accept the terms in the License Agreement and click Next.
4. Install the XDR Collector. The installer displays the User Account Control dialog box.
5. Click Yes.
6. After you complete the installation, verify that the Cortex XDR Collector can establish a connection with Cortex XSIAM.

{% hint style="info" %}
If the XDR Collector does not connect to Cortex XSIAM, verify your internet connection on the collector machine. If the XDR Collector still does not connect, verify that the installation package has not been removed from the Cortex XSIAM tenant.
{% endhint %}
