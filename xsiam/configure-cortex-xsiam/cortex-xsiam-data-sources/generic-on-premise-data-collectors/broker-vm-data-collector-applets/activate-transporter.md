# Activate Transporter

## **Activate Transporter**

{% hint style="info" %}
### Notice

This feature is included with a Cloud Runtime Security, Cloud Posture Security, or Cortex XSIAM Premium license.
{% endhint %}

The Transporter over Broker VM enables secure communication between your self-hosted Version Control Systems (VCS) and Cortex XSIAM. This solution addresses the need for secure code scanning without exposing your internal network to the cloud.

{% hint style="warning" %}
### Prerequisites

* **Permissions**: To configure and manage Transporter applet settings, you must have permissions to manage **Broker Service** configurations (such as an **Instance Administrator**)
* [Set up and configure Broker VM](../../../data-management/broker-vm/set-up-and-configure-broker-vm)
* Confirm that your Broker is v 28 or above
* Whitelist IP addresses to enable access to Cortex XSIAM resources. The IP addresses for the Transporter are in the Broker VM Resources section of the [Enable access to required PANW resources](../../../../onboard-cortex-xsiam/deployment-steps/activate-cortex-xsiam/enable-access-to-required-panw-resources) document
* Open port `4052`, which is required for the Transporter's IP address communication
* Open Port `443` (outbound), which is required for the Broker VM to pull data from your version control system (VCS)
{% endhint %}

**License**

To gain access to and use the Transporter applet, you must possess one of these license types: Cloud Posture Security or Runtime Management) or XSIAM Premium. If you plan to use the Transporter for Code Security scanning, you will also need the Code Security add-on license.

{% hint style="warning" %}
### Warning

The Transporter applet is not supported for FedRAMP customers.
{% endhint %}

**How to activate the Transporter applet**

1. Select Settings → Configurations → Broker VMs (under Data Broker.
2. **Select the Brokers tab** → **locate your Broker VM** → **hover and click + Add under the Apps column** → **AppSec Transporter**.
3. Configure the Transporter connection in the provided fields:
   * **Transporter Name** (required). Requires a unique name as you can integrate multiple applets for different integrations
   * **Provider Self Signed CA Certificate Path**: Specify the file path for a custom Certificate Authority (CA) certificate used by the Transporter to securely communicate with services
4. Click Save.
5. Verify connectivity: Navigate to the **Apps** column and verify that your **AppSec Transporter** applet has been added and displays a connected status.
6.  **Next step**: After activating the Transporter, proceed to configure the Transporter applet on your self-managed VCS data source instance.

    For more information, refer to [Set up a Transporter on your VCS](https://app.gitbook.com/s/8Z0RLJ1BFF5TQL8VtUeK/application-security/onboard-data-sources/transporter-over-broker-vm/set-up-a-transporter-on-your-vcs).

**Manage Transporter applets**

To manage Transporter applet configurations, disable connections, or deactivate an applet, navigate to the Broker VMs page. From there, select your **Appsec Transporter** under the App column.

* **Edit applet configurations**: **Select the Appsec Transporter under the App column** → **Configure**. You are redirected to the Transporter applet settings to manage its configurations
* **Disable applet connection for a single integration**:
  1. **Select the Appsec Transporter under the App column** → **Configure**.
  2.  On the Transporter applet configurations page, **click on the specific Transporter applet** → **Disable**.

      This disables the specific integration, but it can be re-enabled.
*   **Deactivate an applet** (all connections): **Select the Appsec Transporter under the App column** → **Deactivate** → **Confirm when prompted**

    All existing connections are deleted but their configurations are saved in the database. When adding a new connection, you'll be prompted if you want to reuse previous configurations.
