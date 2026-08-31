---
description: >-
  Deploy Cortex XSIAM Network Scanner to discover assets, assess
  vulnerabilities, and investigate issues.
---

# Cortex Network Scanner

The Cortex Network Scanner is a powerful application designed to identify and analyze devices, services, and vulnerabilities in your internal network.

## **What is Cortex Network Scanner?**

The Cortex Network Scanner, a key component of the Exposure Management portfolio, is a robust tool for internal network vulnerability assessment. The scanner efficiently identifies live hosts and vulnerabilities using various methods, including remote and authenticated local checks. Distributed as a Broker VM applet, it integrates seamlessly into your existing infrastructure.

Cortex Network Scanner provides the following key capabilities:

*   **Asset discovery**

    Cortex Network Scanner identifies responsive hosts within a specified IP range, covering both on-premises and cloud-hosted assets.
*   **Vulnerability scanning**

    Cortex Network Scanner supports authenticated and non-authenticated scanning:

    * **Non-authenticated scans** use various vulnerability tests to detect vulnerabilities in the target system based on system responses without requiring credentials, including sending tailored packets to target hosts.
    * **Authenticated** scans use the supplied credentials to authenticate into a target host and identify vulnerabilities by performing deeper tests, including detailed software enumeration and service detection.
* **Customizable and targeted scanning options**
  * Select from different scan profiles for quick turnaround or deeper assessments.
  * Specify different network configurations to adapt to different environments, such as alive test methods, ports to scan, schedules, and performance settings.
  * Scan for specific vulnerabilities quickly across your asset inventory.
*   **Multi-scanner support to distribute scan loads across multiple scanners**

    Reduce the amount of time it takes to complete large network scans by assigning multiple scanners to the task.
*   **Integration with the Cortex XSIAM inventory and vulnerability management**

    Scan results are seamlessly integrated into the inventory and vulnerability management views in Cortex XSIAM, providing a centralized view of all discovered assets, vulnerabilities, and issues.
*   **Credential test scans**

    Check the credentials for service accounts before launching full-scale authenticated scan.

## **Get started with Cortex Network Scanner**

To set up and configure Cortex Network Scanner for the first time, perform the following tasks.

1. Review the [Deployment recommendations](#deployment-recommendations) and complete any prerequisites.
2. [Deploy a Broker VM](../../configure-cortex-xsiam/data-management/broker-vm)
3.  Activate Cortex Network Scanner

    Cortex Network Scanner is distributed as an applet on a Cortex Broker VM. Follow the instructions [to activate Cortex Network Scanner](#activate-cortex-network-scanner) on the Broker VM.
4. [Add a network](#add-a-network) (Optional)
5. [Define target groups](#define-target-groups) (Optional)
6. Add credentials for authenticated scans (Optional)
7. [Create a new scan](#create-a-network-scan)

After completing these set-up and configuration tasks, you can and view issues and findings from scans and manage scans.

### **Deployment recommendations**

#### **Broker VM recommendations**

Network vulnerability scanning is a resource-intensive task. To ensure optimal and consistent scan performance, we recommend the following minimal configuration for Broker VM:

* **Minimum:** 4 CPU cores and 16Gb of RAM
* **Recommended:** 8 CPU cores and 16Gb RAM

We recommend deploying a dedicated Broker VM for the Cortex Network Scanner with no other applets running, though this is not a strict technical limitation. If you plan to run other applets on the same Broker VM alongside the scanner, we recommend configuring the VM with more than 16 GB of RAM.

{% hint style="info" %}
### Note

The Cortex Network Scanner applet is not supported in High Availability (HA) cluster configurations.

The Cortex Network Scanner applet is supported for FedRAMP customers.
{% endhint %}

#### **Firewall and other security control recommendations**

The Cortex Network Scanner uses various methods to actively detect, probe and assess detected services on all or most TCP and UDP ports. The nature of vulnerability scanning conflicts with security controls such as firewalls and IPS that are meant to block such activity. When deploying Broker VMs that run the Cortex Network Scanner (further - Scanners), we recommend taking one or both of the following actions:

* \[Recommended] Deploy scanners strategically within each target security zone or segment (e.g., firewall-configured segments). This ensures scanner traffic remains local to the segment and avoids crossing the firewall or other network security device.
* Configure security policy rules on the firewall and other network security controls that prevent the blocking of traffic from Cortex Network Scanner. Follow the guidelines for your security controls and keep rules as narrow as possible. For Palo Alto Networks NGFW, you must allow traffic from the scanner to the target, using “`Application”` (App-ID) and “`Service`” (port) set to “`any`”.

#### **Authenticated scan recommendations**

Authenticated scans can collect more detailed information about target assets, and detect vulnerabilities that are not detectable with purely remote non-authenticated scans. If credentials are provided for the authenticated scan, the Cortex Network Scanner will attempt to login into the target machines using the provided account.

To set up a successful authenticated scan:

* Provide correct credentials for SMB (Windows-bases systems) and SSH service (Unix-based systems).
* Make sure related traffic (SMB or SSH) is allowed from the scanner to the target host.
* Configure the account with permissions that allow remote logins.

See [Add credentials for authenticated scans](#add-credentials-for-authenticated-scans) for more information about setting up authenticated scans.

#### **Preventing false-positive Cortex XDR alerts**

Some scanning activity (e.g. open port enumeration or local checks with authenticated scans) can trigger alerts on endpoint protection solutions, such as Cortex XDR. That is expected because the same techniques are used by the attackers. To avoid causing false positive alerts, be sure to add scanner source IP addresses into the exclusions.

#### **Recommendations for Windows-based hosts**

To ensure successful scans on Windows-based hosts, configure the following services and registry settings:

*   Under Services, enable the Remote Registry on startup.

    ![remote-registry.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-d78cd2713c2ebcda8fd097a54ca03e04fe14b124%2F7afca5d2a21a271f400760901e7287bc7f61f4b8c8c907644e266906c1b012d9.png?alt=media)
*   Create a service account and add it to the **Administrators** group.

    ![service-account-admin.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-f6c909c31b5cd2d22a7b091eef5a986310f9787c%2Fce88b1c83548575e2dff850b70380c367a2aebbc289a716cf89eab8a2a350182.png?alt=media)
*   Navigate to the active network connection under **Ethernet Properties** → **Networking** and make sure **File and Printer Sharing for Microsoft Networks** is enabled.

    ![file-printer-sharing.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-bdea22b5c4705bbb80bde67a1df85902764ad190%2Fb305315ec831824bb1037c6af6824e36a41613d970733ded2ec17e99e16502f7.png?alt=media)
*   If not part of a Windows domain, In the registry (regedit.exe), check that DWORD LocalAccountTokenFilterPolicy is set to 1.

    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System\ -Name 'LocalAccountTokenFilterPolicy' -Value 1

    ![Set\_Item\_Property.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-b5e8fbc659dd0e17828450891448a9e99905ce37%2Fc17b919a1422f2a89d78a73004ba54e978460125dde16855dfac7fe26b7b8588.png?alt=media)

Configure the following Windows Firewall settings:

* Make sure ports 149, 445, and other services you want to scan are allowed in the firewall rules.

### **Activate Cortex Network Scanner**

The Cortex Network Scanner identifies and analyzes devices, services, and vulnerabilities in your internal network. It discovers responsive hosts within specified IP ranges, including on-premises and cloud environments. The scanner supports both non-authenticated and authenticated vulnerability scanning, with authenticated scans providing deeper insights through credential-based access. Scan results are seamlessly integrated into the inventory and vulnerability management views in Cortex XSIAM, providing a centralized view of all discovered assets, vulnerabilities, and issues.

Cortex Network Scanner is installed as an applet on a Broker VM.

{% hint style="info" %}
### Notice

This feature is included with a Cortex XSIAM Premium license. It is also included with an active Cortex XSIAM NG SIEM and Cortex XSIAM Enterprise license that has the Exposure Management add-on.
{% endhint %}

{% hint style="info" %}
### Important

The Cortex Network Scanner applet is supported for FedRAMP customers.

Cortex Network Scanner does not support high availability (HA) Broker VM configuration.
{% endhint %}

{% hint style="warning" %}
### Prerequisites

* Review the Cortex Network Scanner [deployment recommendations](#deployment-recommendations) and complete any prerequisites.
* [Set up and configure Broker VM](../../configure-cortex-xsiam/data-management/broker-vm)
{% endhint %}

#### How to activate Cortex Network Scanner

1. Navigate to **Settings** → **Configurations** → **Data Broker** → **Broker VMs**.
2. Right click the Broker VM, and select **Add App** → **Network Scanner**.
3.  After the applet has installed, the scanner should automatically connect to the tenant. If the connection is successful, you’ll see a green dot next to **Network Scanner** in the Apps column of the Broker VMs table.

    A red dot indicates that an error occurred and the scanner is not connected.

    ![broker-vms-list.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-4d86fd43afa8fa8897b17c5a96a3683cb0bee9a9%2Fe15d3033f451e74cf3694acf03a687a2981bd7ae9c4491f1ac1bcde17345eea4.png?alt=media)
4. (Optional) Click on the network scanner in the table to display details about the scanner or to deactivate it.
5.  Validate the installation. Navigate to **Modules** → **Vulnerability & Exposure Management** → **Network Scanners** → **Network Scanners** and find your new scanner in the list.

    The **Network Scanners** page displays all your deployed and configured scanners, along with additional details about each of them.

    ![network-scanners.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-cf7a2bc2ce7674e95b7dd3b5118b93798ab60198%2Fa349fd14f5a91255aa2f70faf6c7722c4b11ca5519e491be39a14b7fd583c773.png?alt=media)

After setting up a Broker VM and activating Cortex Network Scanner, refer to [Get started with Cortex Network Scanner](#get-started-with-cortex-network-scanner) for information about adding networks, adding credentials for authenticated scans, and configuring scans.

## **Add a network**

When performing scans, Cortex Network Scanner primarily operates at the IP level, identifying assets as IP hosts. This means it recognizes and interacts with devices based on their unique IP addresses within the scanned network.

In certain environments, you might encounter overlapping or duplicate private IP ranges. For example, your New York and London branch offices could both be using the private network 172.16.1.0/20. If both offices are located behind Network Address Translation (NAT), a server in London and an employee's laptop in New York can legitimately have the same IP address (e.g., 172.16.1.100) without causing conflicts in their respective local networks. This is because NAT translates these private IP addresses to unique public IP addresses when they communicate outside their local network, effectively isolating the private IP spaces.

However, the scan results from the scans are being aggregated at the asset level, taking into the account that the same host can have multiple IP addresses or change the IP address during the asset’s lifecycle. To avoid confusion and mixing up the scan results at the asset level, you can configure a separate network for each location.

You can also add networks for better scan organization.

How to add a network

1. Navigate to **Settings** → **Configurations** → **Network Scanning** → **Networks** and click **+ Add Network**.
2. Enter a **Name** and **Description**.

After you've added a network, you can specify that network when configuring a scan.

## **Define target groups**

Cortex Network Scanner _target groups_ help you collate a list of hosts to be scanned. Each target group contains a mandatory list of IP addresses, IP ranges, subnets, and hostnames to be scanned, and an optional list of IPs, ranges, subnets, or hostnames to be excluded from scans.

Target group definitions are saved, so you can reuse them in multiple scans and review, edit, and delete them as needed. You can create up to 100 target groups, with each one able to include up to 10,000 individual IP addresses, IP ranges, and hostnames.

Create target groups to streamline network scanning configuration by selecting and reusing target definitions. Another benefit is that the target group's name is added as a tag to the asset's definition, so you can find, sort, filter, and create asset groups based on the target group. Target group tags will not overwrite existing tags.

How to define target groups

1.  Navigate to **Settings** → **Configurations** → **Network Scanning** → **Target Group Management**.

    The **Target Group Management** page lists all of your saved Target Groups.
2. Click **+ Add Target Group**.
3. Provide information in the following fields:
   1. **Name**: Provide a descriptive name for the Target Group.
   2. **Description**: (Optional) Enter a description.
   3.  **Add or Upload Targets**: Enter the targets to be scanned as a comma-separated list. Targets can be IP addresses, IP ranges, CIDR ranges, or hostnames. You can also add targets by uploading a .csv file.

       The Cortex Network Scanner will use the DNS server configured in the network settings of the Broker VM for hostname resolution.
   4. **Exclude Targets**: (Optional) Enter the targets to be excluded.
4.  Click **Save Target.**

    Your Target Group will appear in the list on the **Target Group Management** page.

You can edit or delete target groups by right-clicking on the target group and selecting **Edit Target** or **Delete**.

### **Auto tag discovered assets**

Leverage Network Scanner target groups to automatically tag discovered assets. You can use these tags to quickly filter assets, or create Asset Groups to narrow down Finding and Issues results to a specific scan job or asset group.

### How to add a target group

1. **Create a Target Group**: Navigate to **Settings** → **Configurations** → **Network Scanning** → **Target Group Management** and select **Add Target Group**. Enter the IP ranges, individual IPs, or hostnames you want to scan, along with any necessary exclusions.
2. Enter the IP ranges, individual IPs, or hostnames you want to scan, along with any necessary exclusions.
3. **Configure the Scan**: During scan configuration, select your Target Group from the dropdown menu, then launch or schedule the scan.
4.  **Verify Asset Tags**: After the scan completes, all observed assets will automatically receive an asset tag. The tag follows this pattern:

    * Key: _network\_scanner.target.%Target\_Group\_Name% (where %Target\_Group\_Name%_ is the name of the target group assigned to the scan).
    * Value: true

    ![asset-tags.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-0e55b44e435167a4f6792d697f59583c9f4fdfff%2Fff20ec784e8f9f6642bb6737648af5a8499a8f4c25cdd729e62192ef4ef3322e.png?alt=media)
5. **Create a Dynamic Asset Group**: You can use this tag to filter assets or create a dynamic Asset Group.
   1. Go to InventoryAsset Groups.Click **Add Group**.
   2. In the filter menu, select **Tags** and copy your tag key into the relevant field.
   3. Set the value to **True**.
   4. The Asset Group will automatically select all assets that have this tag, including those discovered in future scans.
6. **Filter Results**: You can now use your new Asset Group to filter Issues and Findings within Posture Management.

## **Manage Network Scanner credentials**

An authenticated scan provides a more comprehensive view of system vulnerabilities by examining the target both externally, via the network, and internally, using valid user credentials. For an authenticated scan, the scanner logs into the target system using pre-configured user credentials, which are used to authenticate to various services on the target.

The scanner will try credentials on all targets with a corresponding service, for example SSH credentials will be tried if the scanner detects an SSH server. You can add multiple credentials of the same type to a scan, and the scanner will try to authenticate with them one at a time until authentication is successful.

Scan results might be limited by the permissions associated with these user accounts.

### **Add credentials for authenticated scans**

Complete this task to add and save credentials to be used for authenticated network scans.

{% hint style="warning" %}
### Prerequisites

Before initiating an authenticated scan, complete the following prerequisites on your target hosts:

1.  Create dedicated service accounts.

    We highly recommend creating dedicated service accounts on your target devices specifically for the network scanner. Avoid using existing administrative accounts or personal user accounts. This practice enhances security by limiting the potential impact if the credentials are ever compromised and allows for granular control and auditing of scanner activities.
2.  Ensure that required access rights are configured and remote access is enabled.

    The service accounts must have the necessary permissions to collect system information and perform vulnerability checks remotely. Additionally, the respective remote access protocols must be enabled on the target devices.

    For Windows Targets (SMB/WinRM): Follow the guidelines in the [Get started with Cortex Network Scanner](#get-started-with-cortex-network-scanner) section.

    For Linux Targets: The service account must have permissions to execute commands via SSH.

    * Ensure the SSH daemon (sshd) is running on the target device.
    * Verify that password authentication (or public key authentication, if configured) is enabled for the service account in the sshd\_config file (located typically at /etc/ssh/sshd\_config).
3.  Verify firewall and network security device configuration.

    Remote access traffic must not be blocked by any firewalls (host-based or network-based) or other network security devices (e.g., intrusion prevention systems, network access control).

    For Windows Targets:

    * Windows Defender Firewall: Ensure inbound rules are configured to allow traffic for "File and Printer Sharing" (TCP ports 139, 445) and/or "Windows Remote Management" (TCP port 5985 for HTTP, 5986 for HTTPS).
    * Network Firewalls: If there's a network firewall between the scanner and the target, ensure that TCP ports 139, 445, 5985, and 5986 are open for communication from the scanner's IP address to the target's IP address.

    For Linux Targets

    * Host-based Firewall (e.g., ufw, firewalld): Ensure that SSH traffic (TCP port 22) is allowed. For example, using `ufw: sudo ufw allow ssh`.
    * Network Firewalls: Ensure that TCP port 22 is open for communication from the scanner's IP address to the target's IP address.
{% endhint %}

How to add credentials for authenticated scans

Add and save the credentials to be used for authenticated scans on the **Credential Management** page.

1.  Navigate to **Settings** → **Configurations** → **Network Scanners** → **Credential Management**.

    The Credential Management page lists all of your saved credentials.
2. Click **+ Add Credentials** in the upper right.
3. Provide information in the following fields:
   * **Name**: Provide a descriptive name for this set of credentials.
   * **Description**: Optionally, provide a description.
   * **Service**: Select one of the service and credential types from the dropdown menu and add the credentials:
     * **SSH (Username/Password)**: Requires username, password, port.
     * **SSH (Username/SSH Key):** Requires username, passphrase (optional), port. You will also upload your private SSH key in PEM or OpenSSH format.
     * **SMB**: Requires username and password.
     * **ESXI**: Requires a VMware vSphere UI username and password.
4. Click **Save Credential**. Your new credentials will appear in the list on the **Credential Management** page.

{% hint style="info" %}
### Note

For security reasons, you cannot edit saved credentials, but you can delete them and create new ones as needed.
{% endhint %}

### **Test saved credentials**

Cortex Network Scanner provides a convenient method for validating stored authentication credentials against target hosts. This functionality ensures that the credentials are valid and can be successfully used for authenticated scans.

When testing credentials, you'll specify one or more scanners and target hosts. Cortex Network Scanner will attempt to login to the hosts with the credentials and report back the results, without scanning for vulnerabilities. You can view credential test history and test results for each set of credentials

The solution supports authentication testing via SSH and SMB protocols.

How to test saved credentials

1. Navigate to **Settings** → **Configurations** → **Network Scanning** → **Credential Management**.
2. Right-click on a credential in the table, and select **Test Credential**.
3. Provide the following information on the **Test Credentials** dialog box:
   1. **Network**: Select a network to be scanned.
   2. **Network Scanner(s)**: Select one or more Cortex Network Scanners.
   3. Configure the targets by selecting previously defined target groups or manually adding and excluding targets.
      *   **Select Target Groups**: Select one or more previously saved Target Groups from the drop-down menu.

          Or
      *   **Manually Add Targets**: List the targets to be scanned. Targets can be IP addresses, IP ranges, CIDR ranges, or hostnames.

          **Manually Exclude Targets**: (Optional) List the targets to be excluded from the scan.

### **View credential test history and results**

You can view the test history for each credential. For each entry in the history table, you can also view the credential test results, which includes the list of target IP addresses and whether the credential was successful or a failure for each target. Perform the following steps to view the credential test history and credential test results.

1. Navigate to **Settings** → **Configurations** → **Network Scanning** → **Credential Management**.
2.  In the Credential Management table, click on the credentials you want to test.

    The Credential Test History page will open.
3.  To view the test results for one of the credential test history entries, click on that row in the table.

    The Credential Test Results page will open, which displays the list of targets that the credentials were tested on and whether each test was successful or not.

## **Create a network scan**

Cortex XSIAM uses the Network Scanner to identify active hosts, services, and vulnerabilities within your internal network (on-premises and cloud). After installing Cortex Network Scanner, you can create one or more scans that you schedule to run periodically or run on demand. Learn more about scan templates, the steps to create and schedule a scan, and the advanced scan settings.

![scan-templates.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-c3dd2bd739a24012144ba853be00eee1de8b2566%2F5067de7ab2322efd6b39842e30f2d049b72074650594199baa05472a97a4a8c4.png?alt=media)

1.  **Prerequisites and Setup**

    Before creating a scan, ensure the appropriate components are configured based on your scan type:

    * **For Network Scans** :
      * Broker VM & Applet: A Broker VM must be active with the Network Scanner applet installed and connected indicated by a green status dot in **Settings** → **Configurations** → **Data Broker** → **Broker VMs**.
    * **Optional**:
      * Target Groups: Create reusable groups of IP addresses or hostnames.
      * Credentials: Save SSH (Unix) or SMB (Windows) credentials in Settings+Configurations+General+Credentials.
2.  **Scan Creation Wizard**

    To begin, navigate to Modules+Vulnerability & Exposure Management+Scan Management and click **+ Create Scan**. Select a template based on your objective:

    * **Discovery Scan**: Identifies active hosts and gathers high-level OS information.
    * **Vulnerability Scan**: Performs deep inspection of services to identify known CVEs and security weaknesses.
    * **Focused Vulnerability Scan**: Targets specific vulnerabilities, including emerging threats and zero-day vulnerabilities (ideal for verifying patches or high-priority CVEs).
    * **Policy Audit Scan**: Helps you check if a specified Asset Group is in compliance with selected policies and standards. CIS Microsoft Windows 11 Enterprise Benchmark, Microsoft Windows Server 2022 Benchmark, Debian, and Ubuntu are currently supported

    1.  **General Configuration**

        Configure the basic identity and timing for the scan:

        * **Name & Description**: Provide a unique identifier and optional context.
        * **Scan Scheduling**:
          * Create and save the scan configuration. To launch a scan, right click on the configured scan and select **Launch Scan**.
          * **Launch Once**: Schedules a single execution at a future date/time.
          * **Recurring (Days of Week/Month)**: Sets a repeating schedule.
          * **Quiet Hours**: Define specific time windows where scanning is paused to prevent interference with business operations.
    2.  **Scope Selection**:

        Define the boundaries of the scan:

        * **Network**: Select the defined network environment to be scanned.
        * **Network Scanner**: Choose one or more Broker VMs to execute the scan. Traffic is distributed across selected scanners; ensure firewall rules allow scanner-to-target traffic.
        * **Inclusions**:
          * **Target Groups**: Select previously configured and saved Targets.
          * **Asset Groups**: Select previously saved **Asset Groups**, managed within the **Asset Inventory** as **Targets** .
          * **Manual Targets**: Directly enter IP addresses, CIDR ranges, or hostnames.
        * **Exclusions**:
          * **Manual Exclusions**: List specific IPs or ranges to skip.
          * **Exclusions override Inclusions**: When enabled, any asset excluded in one group remains excluded even if it appears in another included group.
        * **Saved Credentials**: Select one or more credentials. For security reasons you can add only up to 5 credentials to the scan. The scanner attempts these sequentially on each host until authentication succeeds.
3.  **Scan Performance and Optimization**

    To ensure optimal performance without impacting network stability:

    * Broker VM Resources: Ensure the scanner host has at least 4 CPU cores and 8GB RAM. 8 core CPU and 16 GB RAM is highly recommended for large scale scans
    * Recommended Deployment Strategy: Deploy scanners strategically within target security zones to keep traffic local and avoid crossing firewalls.
    * Firewall Rules: If scanning across network boundaries, allow traffic from the scanner to "Any" application and "Any" service/port on target devices.
    * Windows Targets: Ensure ports 139 and 445 are open for SMB-based authenticated scans.
4.  **Monitoring Results**

    Once a scan is initiated, you can track its progress in the Scans table.

    * Reviewing Issues: Completed scan data is integrated into the **Vulnerability Management** views. Navigate to Vulnerability & Exposure Management → **Issues** to investigate discovered vulnerabilities and unmanaged devices.

### **Advanced Settings**

The following sections describe the advanced scan settings. Most Cortex Network Scanner use cases can use default settings.

<details>

<summary>Discovery settings</summary>

| Discovery setting            | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | Default                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| ---------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Host Detection Method        | <ul><li><p>ICMP Ping</p><p>Uses Internet Control Message Protocol (ICMP) echo requests to determine if a host is reachable and responsive on the network.</p></li><li><p>TCP-ACK Service Ping</p><p>Sends TCP ACK packets to specific ports to check for acknowledgment responses, indicating an active host with open ports.</p></li><li><p>TCP-SYN Service Ping</p><p>Initiates a TCP handshake by sending SYN packets to target ports and waits for SYN-ACK responses to identify active hosts.</p></li><li><p>ARP Ping</p><p>Uses ARP requests to directly query the network for active hosts by mapping IP addresses to their corresponding MAC addresses.</p></li></ul> | <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Tip</strong></p><p>ICMP Ping provides the quickest discovery scan and is good for initial discovery and scoping, however in the modern enterprise environment ICMP response can be blocked by the firewall or endpoint security rules. Using additional methods increases the accuracy of the host discovery, although makes the scan take a longer time. The best approach is to use a combination of several methods to keep the balance between accuracy and speed.</p></div><p>The default setting is ICMP, TCP_ACK, ARP.</p> |
| Port List                    | List of ports that will be used to identify alive hosts (changing this setting does not change the ports to be scanned for vulnerabilities).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | The default settings enables discovery scanning on the most commonly responding services.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Order in Which to Scan Hosts | Options are random, reversed, or sequential.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | Sequential                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |

</details>

<details>

<summary>Assessment settings</summary>

| Assessment setting               | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | Default                                                                                                                        |
| -------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| Ports to Scan                    | Choose one one of the pre-defined port lists to scan for vulnerabilities.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | The default is **Common TCP ports, top 100 UDP ports**, which was determined by the Palo Alto Networks security research team. |
| Include or Exclude Ports         | <p>This setting allows you to precisely control which TCP and UDP ports are scanned by either adding them to be included or excluded from your selected port list.</p><p><strong>Inclusion Logic:</strong> If you add a port to the inclusion list that is already present in your selected port list, it will not result in a duplicate entry or change the existing scan behavior for that port.</p><p><strong>Exclusion Precedence:</strong> The exclude option takes precedence. If a port is present in both your selected port list and the "Exclude Port list", it will be excluded from the scan. This ensures that any explicitly excluded port will not be scanned, regardless of its presence in an inclusion list.</p> | None                                                                                                                           |
| Non-authenticated Test Only      | When this option is enabled, the scanner will only perform tests that do not require authentication on the target machine. No login attempts will be made whatsoever.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              | Disabled                                                                                                                       |
| Trust Service Banners            | When selected, the scanner trusts remote host banners and only launches plugins against services they have been designed to check. This default behavior optimizes scanning performance and avoids false positives.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | Selected                                                                                                                       |
| Expand vHosts                    | If selected, the scanner will expand the list of target hosts with values gathered from sources such as reverse-lookup queries and VT checks for SSL/TLS certificates.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | Enabled                                                                                                                        |
| Enable Advanced Windows Scanning | When selected, this option activates an enhanced scanning mode that attempts to start the Remote Registry service and uses WMI for file searches on Windows targets during authenticated scans. This improves vulnerability detection but may lead to alerts or blocks from endpoint protection solutions (e.g., Cortex XDR). Configure necessary exclusions in your endpoint protection policies.                                                                                                                                                                                                                                                                                                                                 | Disabled                                                                                                                       |

</details>

<details>

<summary>Performance settings</summary>

| Performance setting                    | Description                                                                                                                                                                                              | Default      |
| -------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ |
| Test Timeout (Seconds)                 | Timeout per test.                                                                                                                                                                                        | 5 seconds    |
| Wait Time Between Requests (Seconds)   | Number of seconds the security check will wait before sending another request.                                                                                                                           | 5 seconds    |
| Max Hosts to Test Simultaneously       | Maximum number of hosts to test at the same time. This value must be computed given your bandwidth, the number of hosts you want to test, your amount of memory, and the performance of your processors. | 30           |
| Max Simultaneous Tests per Host        | The maximum number of tests that will run against each host. Caution: launching too many tests simultaneously could disable the remote host.                                                             | 4            |
| Test Result Timeout (Seconds)          | Maximum number of seconds for scanner to perform the scan.                                                                                                                                               | 3600 seconds |
| Number of Test Retries After a Timeout | Maximum number of retries after a timeout.                                                                                                                                                               | 5            |
| Open Socket Max Attempts               | Number of unsuccessful retries to open the socket before setting the port to closed.                                                                                                                     | 5            |

</details>

## **Manage scans**

The **Scan Management page** lists all your configured scans along with important information about each scan, including scan progress. From this page you can perform most scan management operations.

1. Navigate to **Settings** → **Configurations** → **Network Scanners** → **Scan Management**.
2.  Right-click on a scan in the list to perform the following actions:

    | Action                  | Description                                                                                                                                                                                                              |
    | ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
    | **Launch Scan**         | <p>Start the scan.</p><p>Note that scheduled scans start automatically. Manually launching a scan will run it without quiet hour restrictions and will cause it to skip any scheduled scan, if the runtimes overlap.</p> |
    | **Edit Scan**           | Modify the scan settings.                                                                                                                                                                                                |
    | **Cancel Scan**         | Cancel an actively running scan. Changes the Scan Progress field to Canceling and then Canceled.                                                                                                                         |
    | **Pause Scan**          | Pause an actively running scan. Changes the Scan Progress field to Pausing and then Paused.                                                                                                                              |
    | **Resume Scan**         | Resume a paused scan.                                                                                                                                                                                                    |
    | **View Rescan History** | View a list of all completed rescans to assess the effectiveness of remediation efforts. You can also download a CSV report scan results here.                                                                           |
    | **Delete Scan**         | Remove scan from scan list.                                                                                                                                                                                              |
3. (Optional) Click on a scan to display the scan history, including the status of every historical scan, whether a scan is currently running and the progress, scan duration, and the number of dead, alive, and completed hosts.

### **Scan Progress values**

The following table explains the Scan Progress field values on the Scan Management page.

| Scan Progress value | Description                                                                             |
| ------------------- | --------------------------------------------------------------------------------------- |
| New                 | Scan has never been run.                                                                |
| Completed           | The last scan completed successfully.                                                   |
| Canceled            | The last scan was canceled.                                                             |
| Canceling           | Scan is in the process of being canceled.                                               |
| Failed              | The last scan failed.                                                                   |
| Paused              | The scan was manually paused or automatically paused because of configured quiet hours. |
| Pausing             | Scan is in the process of being paused.                                                 |

## **View issues triggered by network scanner findings**

Cortex Network Scanner creates findings when it observes CVEs on scanned assets. Cortex XSIAM creates issues if any of those findings match vulnerability issue policies. Cortex Network Scanner findings are part of the overall Cortex XSIAM inventory and vulnerability management views and workflows. Complete the following steps to view issues triggered by network scanner findings:

1. Navigate to **Posture Management** → **Vulnerability Management** → **Vulnerability Issues**.
2. Filter the list of vulnerability issues on **Source = Network Scanner**.

Alternatively, you can also view issues triggered by the Network Scanner from the Findings page, **Posture Management** → **Vulnerability Management** → **Vulnerability Issues** → **All Vulnerability Findings**.When viewing an issue you also have the option to initiate a rescan to evaluate the success of remediation efforts as described below:

1. Navigate to **Posture Management** → **Vulnerability Management** → **Vulnerability Issues**. From the list view, select the issue you wish to rescan.
2.  Right-click on the issue and select **Scan Now** from the drop-down options.

    ![rescan-1.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-b3c8312a49dbc6f01bec45b59b973ecff48e6bfd%2Fb403622f02833657a8d7e39f9b965dc194ab1b984ed47a20ba6df4e01129be6f.png?alt=media)
3. Alternatively, Select **Scan Now** from the options menu to quickly repeat the scan for the already scanned assets. Keep in mind that the rescan option is only available for assets that have already been scanned by the Cortex Network Scanner.
4. On the confirmation modal, select **Scan Now** to initiate the scan. Rescan can take up to a few hours. You will not be able to launch another rescan of the same asset until the previous one is completed or if less than 4 hours passed. You can cancel the ongoing rescan through the Scan History view (see below).
5. Navigate to **Settings** → **Configurations** → **Network Scanners** → **Scan Management** → **Rescan History** to view updated scan history for the scanned asset. You will also receive an email confirmation when the rescan is complete. If the previously detected vulnerability no longer exists, the original issue or finding will be closed.
