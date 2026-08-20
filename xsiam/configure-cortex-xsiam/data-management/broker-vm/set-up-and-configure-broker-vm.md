# Set up and configure Broker VM

Learn more about how to set up and configure a Broker VM as a standalone broker or add the broker to a high availability (HA) cluster.

You can set up a standalone Broker VM or add a Broker VM to a High Availability (HA) cluster to prevent a single point of failure. For more information, see [Broker VM High Availability Cluster](broker-vm-high-availability-cluster).

To set up the Broker virtual machine (VM), you need to deploy an image created by Palo Alto Networks on your network or supported cloud infrastructure and activate the available applications. You can set up several Broker VMs for the same tenant to support larger environments. Ensure each environment matches the necessary requirements.

### Requirements

Before you set up the Broker VM, verify you meet the following requirements:

#### Hardware

For standard installation, use a minimum of a 4-core processor, 8 GB RAM, and 512 GB disk.

* If you only intend to use the Broker VM for the agent proxy, you can use a 2-core processor.
* If you intend to use the Broker VM for the agent installer and content caching, you must use a minimum of an 8-core processor and increase the disk space allocated for data storage to 1024 GB. For more information, see [Increase Broker VM storage allocated for data caching](manage-broker-vm/increase-broker-vm-storage-allocated-for-data-caching).

{% hint style="info" %}
#### Note

The Broker VM comes with a 512 GB disk. Therefore, deploy the Broker VM with thin provisioning, meaning the hard disk can grow up to 512 GB but will do so only if needed.
{% endhint %}

#### Bandwidth

Bandwidth is higher than 10 mbit/s.

When the Broker VM is collecting data, the optimal outgoing bandwidth into the Cortex XSIAM server should be about 25% of the incoming data traffic into the Broker VM applets.

{% hint style="warning" %}
#### Important

There can be instances in which the Broker VM requires up to 50% of the incoming bandwidth as outgoing. Such instances can be, network instability between the Broker VM and Cortex XSIAM, or data that is being collected, but not well compressed.
{% endhint %}

#### Virtual machine compatibility

Before downloading, ensure that your virtual machine (VM) is compatible with one of the options below. To download the image, select Settings → Configurations → Data Broker → Broker VMs, click Add Broker, and select the applicable image you want to install:

| Infrastructure            | Image Type  | Broker Image Installation                                                                                                                                                                          |
| ------------------------- | ----------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Alibaba Cloud             | QCOW2       | [Set up Broker VM on Alibaba Cloud](set-up-and-configure-broker-vm/broker-vm-image-installations/set-up-broker-vm-on-alibaba-cloud)                                                                |
| Amazon Web Services (AWS) | VMDK        | [Set up Broker VM on Amazon Web Services](set-up-and-configure-broker-vm/broker-vm-image-installations/set-up-broker-vm-on-amazon-web-services)                                                    |
| Google Cloud Platform     | VMDK        | [Set up Broker VM on Google Cloud Platform (GCP)](set-up-and-configure-broker-vm/broker-vm-image-installations/set-up-broker-vm-on-google-cloud-platform-gcp)                                      |
| KVM                       | QCOW2       | [Set up Broker VM on KVM using Ubuntu](set-up-and-configure-broker-vm/broker-vm-image-installations/set-up-broker-vm-on-kvm-using-ubuntu)                                                          |
| Microsoft Azure           | VHD (Azure) | [Set up Broker VM on Microsoft Azure](set-up-and-configure-broker-vm/broker-vm-image-installations/set-up-broker-vm-on-microsoft-azure)                                                            |
| Microsoft Hyper-V 2012    | VHD         | Hyper-V 2012 or later [Set up Broker VM on Microsoft Hyper-V](set-up-and-configure-broker-vm/broker-vm-image-installations/set-up-broker-vm-on-microsoft-hyper-v)                                  |
| Nutanix Hypervisor        | QCOW2       | Nutanix AHV 10.3 or later [Set up Broker VM on Nutanix Hypervisor](set-up-and-configure-broker-vm/broker-vm-image-installations/set-up-broker-vm-on-nutanix-hypervisor)                            |
| VMware ESXi               | OVA         | VMware ESXi 6.5 or later [Set up Broker VM on VMware ESXi using vSphere Client](set-up-and-configure-broker-vm/broker-vm-image-installations/set-up-broker-vm-on-vmware-esxi-using-vsphere-client) |

#### Communication between services and applications

Enable communication between the Broker Service, and other Palo Alto Networks services and applications.

{% hint style="warning" %}
#### Important

The internal network for the Broker VM must be unique and reserved. Other devices should not use the same IP as the Broker VM internal network as it can lead to communication issues with the Broker VM.
{% endhint %}

| FQDN, Protocol, and Port                                                                                                                                                                             | Description                                                                                                                                                                        |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p>(Default)</p><ul><li><strong><code>time.google.com</code></strong></li><li><strong><code>pool.ntp.org</code></strong></li></ul><p>UDP port 123</p>                                                | Broker's NTP server used for broker registration and communication encryption. The Broker VM provides default servers you can use, or you can define an NTP server of your choice. |
| <p><strong><code>br-</code></strong><em><strong><code>&#x3C;XDR tenant></code></strong></em><strong><code>.xdr.&#x3C;region>.paloaltonetworks.com</code></strong> </p><p>HTTPS over TCP port 443</p> | Broker Service server depending on the region of your deployment, such as **`us`** or **`eu`**.                                                                                    |
| **`distributions.traps.paloaltonetworks.com`** HTTPS over TCP port 443                                                                                                                               | Information needed to communicate with your Cortex XSIAM tenant. Used by tenants deployed in all regions.                                                                          |
| **`br-`**_**`<xdr-tenant>`**_**`.xdr.federal.paloaltonetworks.com`**&#x48;TTPS over TCP port 443                                                                                                     | Broker Service server for Federal (US Government) deployment.                                                                                                                      |
| <p><strong><code>distributions-prod-fed.traps.paloaltonetworks.com</code></strong> </p><p>HTTPS over TCP port 443</p>                                                                                | Used by tenants with Federal (US Government) deployment                                                                                                                            |
| From Broker VM version 19.x.x and later, you can navigate to the following URL to open the Broker VM web console: **`https://<broker_vm_ip_address>.:4443`** HTTPS over TCP port 4443                | Broker VM web console                                                                                                                                                              |

{% hint style="info" %}
#### Note

When DHCP is not enabled in your network and there isn't an IP address for your Broker VM, configure the Broker VM with a static IP using the serial console menu.
{% endhint %}

#### Enable access to Cortex XSIAM

Enable access to Cortex XSIAM from the Broker VM to allow communication between agents and collectors and Cortex XSIAM. The Broker VM communicates with the Cortex XSIAM tenant with TLS 1.2 (or higher, if that applies).

For more information on enabling access to Cortex XSIAM, see [Enable access to required PANW resources](../../../onboard-cortex-xsiam/deployment-steps/activate-cortex-xsiam/enable-access-to-required-panw-resources).

{% hint style="warning" %}
#### Important

If you use SSL decryption in your firewalls and proxies, see the Understanding CA certificate functionality in Broker VM deployments section below. In addition, verify that the proxies used support HTTP/2, gRPC-specific headers, and HTTP/2 trailers, and the inspection policies support gRPC traffic. Any devices that you use with this configuration should also support these standards.

When adding a CA certificate to the broker is not possible, ensure that you’ve added the Broker Service FQDNs to the SSL Decryption Exclusion list on your firewalls. For more information on adding a trusted self-signed certificate authority, see [Update the Trusted CA Certificate for the Broker VM](set-up-and-configure-broker-vm) in Task 1. Configure the Broker VM settings.
{% endhint %}

### Understanding CA certificate functionality in Broker VM deployments

The Broker VM utilizes a CA certificate to establish trust with intermediary network devices, such as firewalls performing SSL/TLS decryption, positioned between the Broker VM and the tenant environment. Failure of the Broker VM to validate the certificate presented by an intermediate network component results in the termination of the SSL/TLS connection.

This CA certificate is optional to configure depending on your system configurations and helps provide more flexibility in securing communications between the Broker VM and the tenant according to your preferences and network topology. Specifically, it can help facilitate all communication between the Broker VM and tenant, such as the following:

* Broker VM configuration: Secure transmission of configuration parameters.
* Broker VM upgrades: Authenticated delivery and execution of upgrade packages.
* Metric Uploads: Encrypted and authenticated transfer of operational metrics to the tenant.

{% hint style="info" %}
#### Note

* When configuring a Local Agent Settings applet with installer and content caching, you need to configure an SSL certificate for the Broker VM as explained in the task below. For more information on specific requirements for the Local Agent Settings applet, see [Activate Local Agent Settings](../../cortex-xsiam-data-sources/generic-on-premise-data-collectors/broker-vm-data-collector-applets/activate-local-agent-settings).
* Keep in mind that several Broker VM applets, such as the Syslog Collector and Kafka Collector, have their own dedicated CA certificate bundle.
{% endhint %}

### Initial Setup

Perform the following procedures in the order listed below.

{% hint style="info" %}
#### Note

When a Broker VM is disconnected for more than 30 days, it will have to go through a re-registration process.
{% endhint %}

{% stepper %}
{% step %}
#### Task 1. Generate a token for your broker

1. Select Settings → Configurations → Data Broker → Broker VMs.
2. Click Add Broker → Generate Token, and copy to your clipboard. The token is valid for 24 hours. A new token is generated each time you select Generate Token. You'll paste this token after configuring settings and the Broker VM is registered in [Task 2. Register your Broker VM](#task-2.-register-your-broker-vm).
{% endstep %}

{% step %}
#### Task 2. Open the Broker VM URL

Depending on the Broker VM version, navigate to either of the following URLs:

* From Broker VM version 19.x.x and later: **`https://<broker_vm_ip_address>.:4443`**
* From Broker VM version 18.x.x and earlier: **`https://<broker_vm_ip_address>/`**

{% hint style="info" %}
#### Note

When DHCP is not enabled in your network and there isn't an IP address for your Broker VM, configure the Broker VM with a static IP using the serial console menu.
{% endhint %}
{% endstep %}

{% step %}
#### Task 3. Log in and set a new password

Log in with the default password **`!nitialPassw0rd`**, and then define your own unique password. The password must contain a minimum of twelve characters, contain letters and numbers, and at least one capital letter and one special character.
{% endstep %}
{% endstepper %}

### How to configure Broker VM settings

Perform the following procedures in the order listed below.

#### Task 1. Configure the Broker VM settings

1. Define the network interfaces settings. Review the pre-configured Name, IP address, and MAC Address, and select the Address Allocation: DHCP (default) or Static. If you choose Static, define the static IP address, Netmask, Default Gateway, and DNS Server settings, and then save your configurations.

{% hint style="warning" %}
#### Important

When configuring more than one network interface, ensure that only one Default Gateway is defined. The rest must be set to `0.0.0.0`, which configures them as undefined. In addition, we recommend assigning each network interface to a different subnet, as oppose to configuring two interfaces on the same subnet which can potentially cause unexpected behavior. You can also specify which of the network interfaces is designated as the Admin and can be used to access the Broker VM web interface. Only one interface can be assigned for this purpose from all of the available network interfaces on the Broker VM, and the rest should be set to **Disable**.
{% endhint %}

2. (Optional) Set the internal network settings (requires Broker VM 14.0.42 and later). Specify a network subnet to avoid the Broker VM dockers colliding with your internal network. By default, the **Network Subnet** is set to `172.17.0.1/16`.

{% hint style="warning" %}
#### Important

Internal IP must be:

* Formatted as **`prefix/mask`**, for example **`192.0.2.1/24`**.
* Must be within `/8` to `/24` range.
* Cannot be configured to end with a zero.

For Broker VM version 9.0 and earlier, Cortex XSIAM will only accept `172.17.0.0/16`.
{% endhint %}

3.  (Optional) Configure a proxy server address and other related details to route Broker VM communication.

    1. Select the proxy Type as HTTP, SOCKS4, or SOCKS5. For any proxy selected, you must ensure the proxy supports HTTP/2, gRPC-specific headers, and HTTP/2 trailers, and the inspection policies support gRPC traffic. Any devices that you use with this configuration should also support these standards.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h4>Note</h4><p>You can configure another Broker VM as a proxy server for this Broker VM by selecting the HTTP type. When selecting HTTP to route Broker VM communication, you need to add the IP Address and Port number (set when activating the Agent Proxy) for another Broker VM registered in your tenant. This designates the other Broker VM as a proxy for this Broker VM.</p></div>

    2. Specify the proxy Address (IP or FQDN), Port, and an optional User and Password. Select the pencil icon to specify the password. Avoid using special characters in the proxy username and password.
    3. Save your configurations.
4. (Optional) Configure your NTP servers (requires Broker VM 8.0 and later). Specify the required server addresses using the FQDN or IP address of the server.
5.  (Optional) Allow SSH connections to the Broker VM (Requires Broker VM 8.0 and later).

    <div data-gb-custom-block data-tag="hint" data-style="warning" class="hint hint-warning"><h4>Important</h4><ul><li>We strongly recommend disabling SSH connectivity when it's not being used. Therefore, activate SSH connectivity when it's needed and disable it right afterwards.</li><li>When generating a new SSH key ensure to avoid embedding the domain-style username, by not using any backslashes (<code>\</code>) in the comment field, to ensure the SSH key passes validation.</li></ul></div>

    Enable or disable SSH connections to the Broker VM. SSH access is authenticated using a public key, provided by the user. Using a public key grants remote access to colleagues and Cortex XSIAM support who need the private key. You must have Instance Administrator role permissions to configure SSH access.\
    \
    To enable connection, generate an RSA Key Pair, and enter the public key in the SSH Public Key section. Once one SSH public key is added, you can Add Another. When you are finished, Save your configuration.\
    \
    When using PuTTYgen to create your public and private key pairs, you need to copy the public key generated in the Public key for pasting into OpenSSH authorized\_keys file box, and paste it in the Broker VM SSH Public Key section as explained above. This public key is only available when the PuTTYgen console is open after the public key is generated. If you close the PuTTYgen console before pasting the public key, you will need to generate a new public key.\
    \
    When you SSH the Broker VM using PuTTY or a command prompt, you need to use the **`admin`** username.\
    For example: `ssh -i [/path/to/private.key] admin@[broker_vm_address]`
6. (Optional) Update the SSL Server certificates for the Broker VM. Upload your signed server certificate and key to establish a validated secure SSL connection between your endpoints and the Broker VM. Ensure the Private Key is uploaded in an unencrypted format. When you configure the server certificate and the key files in the Broker VM, Cortex XSIAM automatically updates them in the tenant UI. Cortex XSIAM validates that the certificate and key match, but does not validate the Certificate Authority (CA).

{% hint style="info" %}
#### Note

The Palo Alto Networks Broker VM supports only strong cipher SHA256-based certificates. MD5/SHA1-based certificates are not supported.
{% endhint %}

7. Update the Trusted CA Certificate for the Broker VM. Upload your Certificate Authority (CA) bundle file associated with the public TLS certificates belonging to the applicable firewalls, and click Save. These applicable firewalls include SSL/TLS decryption. For example, when [configuring Palo Alto Networks NGFW to decrypt SSL](https://knowledgebase.paloaltonetworks.com/KCSArticleDetail?id=kA10g000000ClmyCAC) using a self-signed certificate, you need to ensure the Broker VM can validate a self-signed CA by uploading the `cert_ssl-decrypt.crt` file on the Broker VM.

{% hint style="info" %}
#### Note

If adding a CA certificate to the Broker VM is not possible, ensure that you’ve added the Broker Service FQDNs to the SSL Decryption Exclusion list on your firewalls. See [Enable Access to Cortex XSIAM](../../../onboard-cortex-xsiam/deployment-steps/activate-cortex-xsiam/enable-access-to-required-panw-resources).
{% endhint %}

8. (Optional) Configure the advanced settings of the Broker VM.

* **Only use recommended cipher suites**: Select this to use a limited set of strong cipher suites for Broker VM communications. You must enable this option to comply with Spain's Esquema Nacional de Seguridad (ENS) National Security Framework. It is critical that you configure this option before you register the Broker VM with a tenant for compliance reasons.
* **Enforce TLS 1.3**: Select this to enforce the TLS 1.3 cryptographic protocol for communication between the Broker VM and the tenant. This setting is often required to meet specific regional security standards. When this option is unchecked, the broker continues to use the default TLS 1.2 (or higher, if applicable) connection protocols. This option is unchecked by default for new brokers.
* **Allow legacy SSL renegotiation**: Select this to allow connections to servers still using legacy SSL renegotiation. This option is unchecked by default.
* **Accept certificates without AKID**: Select this to accept certificates that do not contain the Authority Key Identifier (AKID) extension. This option is unchecked by default.

9. (Optional) Collect and Generate New Logs (Requires Broker VM 8.0 and later). Your Cortex XSIAM logs will download automatically after approximately 30 seconds.

#### Task 2. Register your Broker VM

Register and enter your unique Token, created in the Broker VMs page. This can take up to 30 seconds.

After a successful registration, Cortex XSIAM displays a notification.

You are directed to Settings → Configurations → Data Broker → Broker VMs. The Broker VMs page displays your Broker VM details and allows you to edit the defined configurations.
