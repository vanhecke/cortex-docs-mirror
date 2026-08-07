# Activate Windows Event Collector on Windows Core

After you have configured and registered your Broker VM, you can activate your Windows Event Collector application on Windows Core OS (WCOS). WCOS is a stripped-down, lightweight version of Windows that can be adapted to run on a wide variety of devices with minimal work compared to the previous way explained in [Activate Windows Event Collector]().

The Windows Event Collector (WEC) runs on the Broker VM collecting event logs from Windows Servers, including Domain Controllers (DCs). The Windows Event Collector can be deployed in multiple setups, and can be connected directly to multiple event generators (DCs or Windows Servers) or routed using one or more Windows Event Collectors. Behind each Windows event collector there may be multiple generating sources.

To enable the collection of the event logs, you are configuring and establishing trust between the Windows Event Forwarding (WEF) collectors and the WEC. Establishing trust between the WEFs and the WEC is achieved by mutual authentication over TLS using server and client certificates. The WEF, a WinRM plugin, runs under the Network Service account. Therefore, you need to provide the WEFs with the relevant certificates and grant the account access permissions to the private key used for client authentication, for example, authenticate with WEC.

#### Prerequisite

* [Set up and configure Broker VM](../../../../data-management/broker-vm/set-up-and-configure-broker-vm)
* Broker VM version 8.0 and later
* You have knowledge of Windows Active Directory and Domain Controllers.
* You must configure different settings related to the FQDN where the instructions differ depending on whether you are configuring a standalone Broker VM or High Availability (HA) cluster.\
  **Standalone broker**\
  A FQDN must be configured for the standalone broker as configured in your local DNS server. Therefore, the Broker VM is registered in the DNS, its FQDN is resolvable from the events forwarder (Windows server), and the Broker VM FQDN is configured. For more information, see [Edit Broker VM Configuration](../../../../data-management/broker-vm/manage-broker-vm/edit-broker-vm-configuration). **HA cluster** A FQDN must be configured in the cluster settings as configured in your local DNS server, which points to a Load Balancer. For more information, see [Configure High Availability Cluster](../../../../data-management/broker-vm/broker-vm-high-availability-cluster/configure-high-availability-cluster).
* Windows Server 2012 r2 or later.

After ingestion, Cortex XSIAM normalizes and saves the Windows event logs in the dataset `xdr_data`. The normalized logs are also saved in a unified format in `microsoft_windows_raw`. This enables you to search the data using XQL queries, build correlation rules, and generate dashboards based on the data.

Perform the following procedures in the order listed below.

### Task 1. Add, configure, and activate a Windows Event Collector

1. Select Settings → Configurations → Data Broker → Broker VMs.
2. Do one of the following:
   * On the Brokers tab, find the Broker VM, and in the APPS column, left-click Add → Windows Event Collector.
   * On the Clusters tab, find the Broker VM, and in the APPS column, left-click Add → Windows Event Collector.
3.  In the Activate Windows Event Collector window, define the Collected Events to configure the events collected by the applet. This lists event sources from which you want to collect events.

    | Field               | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
    | ------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | Source              | <p>Select from the pre-populated list with the most common event sources on Windows Servers. The event source is the name of the software that logs the events.</p><p>A source provider can only appear once in your list. When selecting event sources, depending on the type event you want to forward, ensure the event source is enabled, for example <a href="https://docs.microsoft.com/en-us/defender-for-identity/configure-windows-event-collection">auditing security events</a>. If the source is not enabled, the source configuration in the given row will fail.</p> |
    | Min. Event Level    | Minimum severity level of events that are collected.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
    | Event IDs Group     | Whether to Include, Exclude, or collect All event ID groups.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
    | Minimal TLS Version | Select either 1.0 or 1.2 (default) as the minimum TLS version allowed. Ensure that you verify that all Windows event forwarders are supporting the minimal defined TLS version.                                                                                                                                                                                                                                                                                                                                                                                                    |

    To forward all the Windows Event Collector events to the Broker VM, define as follows:

    * Source: **`ForwardedEvents`**
    * Min. Event Level: **`Verbose`**
    * Event IDs Group: **`All`**

    By default, Cortex XSIAM collects Palo Alto Networks predefined Security events that are used by the Cortex XSIAM detectors. Removing the Security collector interferes with the Cortex XSIAM detection functionality. Restore to Default to reinstate the Security event collection.
4. Click Activate. After a successful activation, the APPS field displays WEC with a green dot indicating a successful connection.

### Task 2. Configure the Windows Event Collector settings

1. In the APPS column, left-click the WEC connection to display the Windows Event Collector settings, and select Configure.
2.  In the Windows Event Forwarder Configuration window, perform the following tasks.:

    1. In the Subscription Manager URL field, click [![copy-icon.png](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACoAAAAqCAYAAADFw8lbAAAACXBIWXMAABYlAAAWJQFJUiTwAAAAB3RJTUUH4wYZBCUdcqk62wAAAAd0RVh0QXV0aG9yAKmuzEgAAAAMdEVYdERlc2NyaXB0aW9uABMJISMAAAAKdEVYdENvcHlyaWdodACsD8w6AAAADnRFWHRDcmVhdGlvbiB0aW1lADX3DwkAAAAJdEVYdFNvZnR3YXJlAF1w/zoAAAALdEVYdERpc2NsYWltZXIAt8C0jwAAAAh0RVh0V2FybmluZwDAG+aHAAAAB3RFWHRTb3VyY2UA9f+D6wAAAAh0RVh0Q29tbWVudAD2zJa/AAAABnRFWHRUaXRsZQCo7tInAAACQklEQVRYhe2ZsU/bQBTGv8RJA4kSBQawlEpkoaq7sGVFAgRjBDvpHwAjAsFQiQHoWrVLR2BjCGKMxMKKWDwZtnawZIZKxiFtXDibpYmcENt3zjlpJH+jfc/3S+7d997ZsXf7v2yMgOLDBqBVgjXgczmD1bkUU4yiEVRODBjN4IvHDFrIC7i9Jzio/aYa/0EUsL2Uxkkl1xcsMygAGE0b1z+eqMcLceDtRLwvWOYcPaw1cFhrME+0fmy0YXNjMeZ4ZlBFI1A0wjyRopEOWEkUmOIHuuv7gfXM0VIxCdj0+XT989l3TAv29GOunbM0K+QKerMzgWyKLZeqsondC//8DQLrCppNxXAum6jKf30nlkQBe8tprP3zVyesqhPUTRtH5UzHdVZYz6VXdYvJhnYvGjgqZzpgVd1qA3X/CEUjWPiiU8EG8lE3VWUTAF7BOv+9NZeqVjdt7K1ksH5shA/aDStNJ9oGr2gE5e8PKOR77/StxbTnc7mDAp2wzmqk6hZU3eoZYz57u0toPtpyAEkUAlcjp0I1fJ6woVcmXrADKaFV2cTG2WNfTQnXzXRayXre1x4sSKKA92KCyZ8BTqCqTvDt6o/vuEJewOwUW9fUEidQC18pQEvFJFbn3gSaY2QOdxEob0WgvBWB8lYEyltDBy0Vk7j7NInSTAL1Zu+mGgipw2eRs0+4vHM/8f4HoHR9wtCXnlYRKG+NDKjnZtqcH8fm/PigWDzlCrpx9ghpOtixwUtG08at5v96slux6DsTZ70AOJoTb8LtORgAAAAASUVORK5CYII=)](https://docs-cortex.paloaltonetworks.com/viewer/attachment/5CAbsl8idaK8R43ZLhoTOw/dbHaiN1dE6xesRujYDHLiQ-5CAbsl8idaK8R43ZLhoTOw) (copy) . This will be used when you configure the subscription manager in the GPO (Global Policy Object) on your domain controller.
    2. Enter a password in the Define Client Certificate Export Password field to be used to secure the downloaded WEF certificate that establishes the connection between your DC/WEF and the WEC. You will need this password when the certificate is imported to the events forwarder.
    3.  Download the WEF certificate in a PFX format to your local machine.

        To view your Windows Event Forwarding configuration details at any time, select your Broker VM, right-click and navigate to Windows Event Collector → Configure.

    Cortex XSIAM monitors the certificate and triggers a Certificate Expiration notification 30 days prior to the expiration date. The notification is sent daily specifying the number of days left on the certificate, or if the certificate has already expired.

Cortex XSIAM monitors the certificate and triggers a Certificate Expiration notification 30 days prior to the expiration date. The notification is sent daily specifying the number of days left on the certificate, or if the certificate has already expired.

### Task 3. Install your WEF Certificate on the WEF to establish connection

1. Start PowerShell with elevated privileges.
   1.  Run PowerShell with the following command:

       ```
       PowerShell
       ```
   2.  From inside a `PowerShell` command run the following command:

       ```
       Start-Process -Verb RunAs PowerShell
       ```
2. Copy the PFX file that you downloaded to the local Core machine in one of the following ways:
   * (Recommended) If you're able to RDP to your server, open Notepad, and select File → Open to copy and paste files from your local machine directly to the server. If you have any local drives mapped through the RDP options, the local drives are also displayed. We recommend this method as it's the simplest.
   *   If you have enabled `WinRM` for remote `PowerShell` execution, you can copy over PowerShell using this command:

       ```
       $session = New-PSSession –ComputerName <computer name>
       ```

       ```
       Copy-Item –Path <path to PFX certificate file> –Destination '<temporary file path>' –ToSession $session
       ```

       ```
       $session = New-PSSession –ComputerName SERVER1
       ```

       ```
       Copy-Item –Path C:\Downloads\forwarder.wec.paloaltonetworks.com.pfx –Destination 'C:\temp\forwarder.wec.paloaltonetworks.com.pfx' –ToSession $session
       ```

       <br>

       To enable `WinRM`, use this command:

       ```
       Execute "Start-Service winRM"
       ```

       ```
       Execute "WinRM quickconfig"
       ```
   * Use SSH on server core. This includes enabling SSH on server core and using `winscp` to drag and drop the PFX file.
   *   Use SMB to open the file share `c$` on the `\\server1\c$` server. You can only use this option if you are an administrator and the firewall on your network isn't set to block file sharing.

       You can also launch PowerShell and run the following command to tell the remote server to copy a file from your local computer using SMB:

       ```
       Copy-Item –Path <path to PFX certificate file> –Destination '\\<computer name>\c$\<path to PFX file>
       ```

       ```
       Copy-Item –Path C:\Downloads\forwarder.wec.paloaltonetworks.com.pfx –Destination '\\windows-core-server\c$\forwarder.wec.paloaltonetworks.com.pfx
       ```

       <br>
3.  Import the PFX file from PowerShell.

    Use the following command to import the PFX file:

    ```
    certutil -f -importpfx '<path to PFX file from Destination>'
    ```

    ```
    certutil -f -importpfx '.\forwarder.wec.paloaltonetworks.com.pfx'
    ```

    <br>

    You will need to enter the Client Certificate Export Password you defined in the Cortex XSIAM console.

    When the import is complete, the following message is displayed:

    ```
    CertUtil: -importPFX command completed successfully. 
    ```
4. Verify that the certificates are in the correct locations.
   *   Ensure the client certificate appears in "My" (Personal) store by running the following command:

       ```
       certutil -store My
       ```
   *   Ensure the CA appears in Trusted Root Certification Authorities by running the following command:

       ```
       certutil -store root
       ```
5.  Manage the private key of the `forwarder.wec.paloaltonetworks.com.pfx` certificate.

    This entails applying permissions for the `NETWORK SERVICE` user.

    1.  Retrieve the Thumbprint of the `forwarder.wec.paloaltonetworks.com.pfx` certificate by running the following script:

        ```
        $store = New-Object System.Security.Cryptography.X509Certificates.X509Store("My","LocalMachine")
        $store.Open("ReadWrite")
        echo $store.Certificates
        ```

        After the script runs, copy the relevant thumbprint.
    2.  Grant `NT AUTHORITY\NETWORK SERVICE` with read permissions by running the following script with the `$thumbprint` set to the value you copied in the previous step by replacing `<Thumbprint retrieved value>`.

        ```
        $thumbprint = '<Thumbprint retrieved value>'
        $account = 'NT AUTHORITY\NETWORK SERVICE'
        #Open Certificate store and locate certificate based on provided thumbprint
        $store = New-Object System.Security.Cryptography.X509Certificates.X509Store("My","LocalMachine")
        $store.Open("ReadWrite")
        $cert = $store.Certificates | where {$_.Thumbprint -eq $thumbprint}
         
        #Create new CSP object based on existing certificate provider and key name
        #Note: Ensure this command is pasted to the same row and doesn’t break to multiple rows. 
        #Otherwise, the command will fail with errors.
        $csp = New-Object System.Security.Cryptography.CspParameters($cert.PrivateKey.CspKeyContainerInfo.ProviderType, $cert.PrivateKey.CspKeyContainerInfo.ProviderName,
        $cert.PrivateKey.CspKeyContainerInfo.KeyContainerName)
         
        # Set flags and key security based on existing cert
        $csp.Flags = "UseExistingKey","UseMachineKeyStore"
        $csp.CryptoKeySecurity = $cert.PrivateKey.CspKeyContainerInfo.CryptoKeySecurity
        $csp.KeyNumber = $cert.PrivateKey.CspKeyContainerInfo.KeyNumber
         
        # Create new access rule - could use parameters for permissions, but I only needed GenericRead
        $access = New-Object System.Security.AccessControl.CryptoKeyAccessRule($account,"GenericRead","Allow")
        # Add access rule to CSP object

        $csp.CryptoKeySecurity.AddAccessRule($access)
         
        #Create new CryptoServiceProvider object which updates Key with CSP information created/modified above
        $rsa2 = New-Object System.Security.Cryptography.RSACryptoServiceProvider($csp)
         
        #Close certificate store
        $store.Close()
        echo $csp.CryptoKeySecurity
        ```
    3.  After the script runs, validate the permissions are now set correctly.

        [![windows-core-script-permissions.png](https://docs-cortex.paloaltonetworks.com/api/khub/maps/5CAbsl8idaK8R43ZLhoTOw/resources/X~v8rioE151OoaoLx3G6Tg-5CAbsl8idaK8R43ZLhoTOw/content?v=d80756ce327cff89\&Ft-Calling-App=ft/turnkey-portal)](https://docs-cortex.paloaltonetworks.com/viewer/attachment/5CAbsl8idaK8R43ZLhoTOw/X~v8rioE151OoaoLx3G6Tg-5CAbsl8idaK8R43ZLhoTOw)

### Task 4. Add the Network Service account to the domain controller Event Log Readers group

{% hint style="info" %}
You must install the WEF certificate on every Windows Server, whether DC or not, for the WEFs that are supposed to forward logs to the Windows Event Collector applet on the Broker VM.
{% endhint %}

1.  To enable events forwarders to forward events, the Network Service account must be a member of the Active Directory Event Log Readers group. In PowerShell, execute the following command on the domain controller that is acting as the event forwarder:

    ```
    PS C:\> net localgroup "Event Log Readers" "NT Authority\Network Service" /add
    ```

    Make sure you see `The command completed successfully` message.
2.  Grant access to view the security event logs.

    The security event logs are provided by default and the instruction below explain how to to grant access to view these logs. You'll need to apply these instructions to any other event logs that you configure the WEC to access.

    1.  Run `wevtutil gl security` and take note of your `channelAccess` value.

        ```
        `PS C:\Users\Administrator> wevtutil gl security
        name: security
        enabled: true
        type: Admin
        owningPublisher:
        isolation: Custom
        channelAccess: O:BAG:SYD:(A;;0xf0005;;;SY)(A;;0x5;;;BA)(A;;0x1;;;S-1-5-32-573)
        logging:
          logFileName: %SystemRoot%\System32\Winevt\Logs\security.evtx
          retention: false
          autoBackup: false
          maxSize: 134217728
        publishing:
          fileMax: 1
        ```

        Take note of value: `channelAccess: O:BAG:SYD:(A;;0xf0005;;;SY)(A;;0x5;;;BA)(A;;0x1;;;S-1-5-32-573)`

        <br>
    2.  Run `wevtutil sl security "/ca:<channelAccess value>(A;;0x1;;;S-1-5-20)"`

        ```
        PS C:\Users\Administrator> wevtutil sl security "/ca:O:BAG:SYD:(A;;0xf0005;;;SY)(A;;0x5;;;BA)(A;;0x1;;;S-1-5-32-573)(A;;0x1;;;S-1-5-20)"
        ```

Make sure you grant access on each of your domain controller hosts.

### Task 5. Create a WEF Group Policy that applies to every Windows server you want to configure as a WEF

As a Group Policy Management Console is not available on Core servers, it’s not possible to fully edit a Group Policy Object (GPO) either with PowerShell or using a web solution. As a result, follow this alternative method, which is based on configuring a group policy from another Windows DC by remotely configuring the group policy.

1. Use any DC that has the Group Policy Management Console available in the same domain as the Core server, and verify the connection between the servers with a simple ping.
2. Run `cmd` as an administrator.
3.  Run the following command:

    ```
    gpmc.msc /gpcomputer: <computer name.Domain>
    ```

    ```
    gpmc.msc /gpcomputer: WIN-SI2SVDOKIMV.ENV21.LOCAL
    ```

    <br>
4. In the Group Policy Management window, navigate to Domains → your domain name → Group Policy Object, right-click and select New.
5. In the New GPO window, enter your group policy Name: as Windows Event Forwarding, and click OK.
6.  Navigate to Domains → your domain name → Group Policy Objects → Windows Event Forwarding, right-click and select Edit.

    [![group-policy-management.png](https://docs-cortex.paloaltonetworks.com/api/khub/maps/5CAbsl8idaK8R43ZLhoTOw/resources/7VoVcp8rtrQ216Y5pPMdzw-5CAbsl8idaK8R43ZLhoTOw/content?v=888bd3d3d51f301f\&Ft-Calling-App=ft/turnkey-portal)](https://docs-cortex.paloaltonetworks.com/viewer/attachment/5CAbsl8idaK8R43ZLhoTOw/7VoVcp8rtrQ216Y5pPMdzw-5CAbsl8idaK8R43ZLhoTOw)
7. In the Group Policy Management Editor:
   * Set the Windows Remote Management Service for automatic startup.
     1. Select Computer Configuration → Policies → Windows Settings → Security Settings → System Services, and in the view panel locate and double-click Windows Remote Management (WS-Management).
     2. Mark the Define this policy setting checkbox, select Automatic, and then click Apply and OK.
   *   At a minimum for your WEC configuration, you must enable logging of the same events that you have configured to be collected in your WEC configuration on your domain controller. Otherwise, you will not be able to view these events as the WEC only controls querying not logging. For example, if you have configured authentication events to be collected by your WEC using an authentication protocol, such as Kerberos, you should ensure all relevant audit events for authentication are configured on your domain controller. In addition, you should ensure that all relevant audit events that you want collected, such as the success and failure of account logins for Windows Event ID 4625, are properly configured, particularly for those that you want Cortex XSIAM to apply grouping and analytics inspection.

       This step overrides any local policy settings.

       Here is an example of how to configure the WEC to collect authentication events using Kerberos as the authentication protocol to enable the collection of Broker VM supported Kerberos events, Kerberos pre-authentication, authentication, request, and renewal tickets.

       1. Select Computer Configuration → Policies → Windows Settings → Security Settings → Advanced Audit Policy Configuration → Audit Policies → Account Logon.
       2.  In the view pane, right-click Audit Kerberos Authentication Service and select Properties. In the Audit Kerberos Authentication Service window, mark Configure the following audit events:, and click Success and Failure followed by Apply and OK.

           Repeat for Audit Kerberos Service Ticket Operations.

       <br>
8.  Configure the subscription manager.

    Navigate to Computer Configuration → Policies → Administrative Templates: Policy definitions → Windows Components → Event Forwarding, right-click Configure target Subscription Manager and select Edit.

    [![target-subscription-manager.png](https://docs-cortex.paloaltonetworks.com/api/khub/maps/5CAbsl8idaK8R43ZLhoTOw/resources/kKhpS4bCErDE4LObGKnX0w-5CAbsl8idaK8R43ZLhoTOw/content?v=fa163dd36f71564a\&Ft-Calling-App=ft/turnkey-portal)](https://docs-cortex.paloaltonetworks.com/viewer/attachment/5CAbsl8idaK8R43ZLhoTOw/kKhpS4bCErDE4LObGKnX0w-5CAbsl8idaK8R43ZLhoTOw)

    In the Configure target Subscription Manager window:

    1. Mark Configure target Subscription Manager as Enabled.
    2. In the Options section, select Show and in the Show Contents window, paste the [Subscription Manage URL](https://docs-cortex.paloaltonetworks.com/r/5CAbsl8idaK8R43ZLhoTOw/yg8Af6ssEaXJvF__dIDLQw?section=UUID-f8dd2f2e-e8d4-bb35-15b8-6e7b0d4d07a5_N1719238276117) you copied from the Cortex XSIAM console, and then click OK.
    3. Click Apply and OK to save your changes.
9.  Add Network Service to Event Log Readers group.

    Select Computer Configuration → Preferences → Control Panel Settings → Local Users and Groups, right-click and select New → Local Group.

    [![event-log-readers.png](https://docs-cortex.paloaltonetworks.com/api/khub/maps/5CAbsl8idaK8R43ZLhoTOw/resources/CTxRtqyW6sGQYQwidqYAXw-5CAbsl8idaK8R43ZLhoTOw/content?v=3957ccd3c535faa4\&Ft-Calling-App=ft/turnkey-portal)](https://docs-cortex.paloaltonetworks.com/viewer/attachment/5CAbsl8idaK8R43ZLhoTOw/CTxRtqyW6sGQYQwidqYAXw-5CAbsl8idaK8R43ZLhoTOw)

    In the New Local Group Properties window:

    1. In the Group name field, select Event Log Readers (built-in).
    2.  In the Members section, click Add and enter in the Name filed **`Network Service`** followed by OK.

        You must type out the name, do not select the name from the browse button.
    3. Click Apply and OK to save your changes, and close the Group Policy Management Editor window.
10. Configure the Windows Firewall.

    If Windows Firewall is enabled on your event forwarders, you will have to define an outbound rule to enable the WEF to reach port 5986 on the WEC.

    In the Group Policy Management window, select Computer Configuration → Policies → Windows Settings → Security Settings → Windows Firewall with Advanced Security → Outbound Rules, right-click and select New Rule.

    In the New Outbound Rule Wizard define the following Steps:

    1. Rule Type: Select Port followed by Next.
    2. Protocols and Ports: Select TCP and in the Specific Remote Ports field enter **`5986`** followed by Next.
    3. Action: Select Allow the connection followed by Next.
    4. Profile: Select Domain and disable Private and Public followed by Next.
    5. Name: Specify **`Windows Event Forwarding`**.
    6. To save your changes, click Finish.

### Task 6. Apply the WEF Group Policy

Link the policy to the OU or the group of Windows servers you would like to configure as event forwarders. In the following flow, the domain controllers are configured as an event forwarder.

1. Select Group Policy Management → \<your domain name> → Domain Controllers, right-click and select Link an existing GPO....
2. In the Select GPO window, click Windows Event Forwarding followed by OK.
3. In an administrative PowerShell console, execute the following commands:
   1.  ```
       PS C:\Users\Administrator> gpupdate /force
       ```

       Verify that the `Computer Policy update has completed successfully. User Policy update has completed successfully.` confirmation message is displayed.
   2. ```
      PS C:\Users\Administrator> Restart-Service WinRM
      ```

### Task 7. Verify Windows Event Forwarding

1. Select Group Policy Management → \<your domain name> → Domain Controllers, right-click and select Link an existing GPO....
2. In the Select GPO window, click Windows Event Forwarding followed by OK.
3. In an administrative PowerShell console, execute the following commands:
   1.  ```
       PS C:\Users\Administrator> gpupdate /force
       ```

       Verify that the `Computer Policy update has completed successfully. User Policy update has completed successfully.` confirmation message is displayed.
   2. ```
      PS C:\Users\Administrator> Restart-Service WinRM
      ```

### Task 8. Manage the Window Event Collector (Optional)

After the Windows Event Collector has been activated in the Cortex XSIAM Management Console, left-click the WEC connection in the APPS column to display the Windows Event Collector settings, and select:

* Configure to define the event configuration information.
* Collection Configuration to view or edit existing or add new events to collect.
* Deactivate to disable the Windows Event Collector.

### Task 9. View Windows Event Collector metrics (Optional)

To view metrics about the Windows Event Collector, left-click the WEC connection in the APPS field for your Broker VM, and you'll see the following metrics:

* Connectivity Status: Whether the applet is connected to Cortex XSIAM.
* Logs Received and Logs Sent: Number of logs received and sent by the applet per second over the last 24 hours. If the number of incoming logs received is larger than the number of logs sent, it could indicate a connectivity issue.
* Resources: Displays the amount of CPU, Memory, and Disk space the applet is using.
