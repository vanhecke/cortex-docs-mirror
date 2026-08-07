# Renew WEC certificates

Renewing your WEC certificates in Cortex XSIAM includes renewing your Windows Event Forwarding (WEF) client certificate and your WEC server certificate. You must install the WEF certificate on every Windows server, whether a Domain Controller (DC) or not, for the WEFs that are supposed to forward logs to the Windows Event Collector applet on the Broker VM.

#### Important

After you receive a notification for renewing your WEC CA certificate, we recommend that you do not add any new WEF clients until the WEC certification renewal process is complete. Events from these WEF clients that are added afterwards will not be collected by the server until the WEC certificates are renewed.

In addition, Cortex XSIAM manages the renewal of your WEC certificates by implementing the following time limits:

* The WEC CA certificate is increased for an extended period of time for a maximum of 20 years.
* The Broker VM applet includes an automatic renewal mechanism for a WEC server certificate, which has a lifespan of 12 months.
* The WEC client certificate after the renewal is issued with a lifespan of 5 years.

Perform the following procedures in the order listed below.

### Task 1. Renew your WEF client certificate in Cortex XSIAM

1. Select Settings → Configurations → Data Broker → Broker VMs.
2. Do one of the following:
   * On the Brokers tab, find the Broker VM, and in the APPS column, left-click the WEC connection to display the Windows Event Collector settings, and select Configure.
   * On the Clusters tab, find the Broker VM, and in the APPS column, left-click the WEC connection to display the Windows Event Collector settings, and select Configure.
3. In the Windows Event Forwarder Configuration window, perform the following tasks:
   1. In the Subscription Manager URL field, click [![copy-icon.png](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACoAAAAqCAYAAADFw8lbAAAACXBIWXMAABYlAAAWJQFJUiTwAAAAB3RJTUUH4wYZBCUdcqk62wAAAAd0RVh0QXV0aG9yAKmuzEgAAAAMdEVYdERlc2NyaXB0aW9uABMJISMAAAAKdEVYdENvcHlyaWdodACsD8w6AAAADnRFWHRDcmVhdGlvbiB0aW1lADX3DwkAAAAJdEVYdFNvZnR3YXJlAF1w/zoAAAALdEVYdERpc2NsYWltZXIAt8C0jwAAAAh0RVh0V2FybmluZwDAG+aHAAAAB3RFWHRTb3VyY2UA9f+D6wAAAAh0RVh0Q29tbWVudAD2zJa/AAAABnRFWHRUaXRsZQCo7tInAAACQklEQVRYhe2ZsU/bQBTGv8RJA4kSBQawlEpkoaq7sGVFAgRjBDvpHwAjAsFQiQHoWrVLR2BjCGKMxMKKWDwZtnawZIZKxiFtXDibpYmcENt3zjlpJH+jfc/3S+7d997ZsXf7v2yMgOLDBqBVgjXgczmD1bkUU4yiEVRODBjN4IvHDFrIC7i9Jzio/aYa/0EUsL2Uxkkl1xcsMygAGE0b1z+eqMcLceDtRLwvWOYcPaw1cFhrME+0fmy0YXNjMeZ4ZlBFI1A0wjyRopEOWEkUmOIHuuv7gfXM0VIxCdj0+XT989l3TAv29GOunbM0K+QKerMzgWyKLZeqsondC//8DQLrCppNxXAum6jKf30nlkQBe8tprP3zVyesqhPUTRtH5UzHdVZYz6VXdYvJhnYvGjgqZzpgVd1qA3X/CEUjWPiiU8EG8lE3VWUTAF7BOv+9NZeqVjdt7K1ksH5shA/aDStNJ9oGr2gE5e8PKOR77/StxbTnc7mDAp2wzmqk6hZU3eoZYz57u0toPtpyAEkUAlcjp0I1fJ6woVcmXrADKaFV2cTG2WNfTQnXzXRayXre1x4sSKKA92KCyZ8BTqCqTvDt6o/vuEJewOwUW9fUEidQC18pQEvFJFbn3gSaY2QOdxEob0WgvBWB8lYEyltDBy0Vk7j7NInSTAL1Zu+mGgipw2eRs0+4vHM/8f4HoHR9wtCXnlYRKG+NDKjnZtqcH8fm/PigWDzlCrpx9ghpOtixwUtG08at5v96slux6DsTZ70AOJoTb8LtORgAAAAASUVORK5CYII=)](https://docs-cortex.paloaltonetworks.com/viewer/attachment/5CAbsl8idaK8R43ZLhoTOw/dbHaiN1dE6xesRujYDHLiQ-5CAbsl8idaK8R43ZLhoTOw) (copy) . This will be used when you configure the subscription manager in the GPO (Global Policy Object) on your domain controller.
   2. Enter a password in the Define Client Certificate Export Password field to be used to secure the downloaded WEF certificate that establishes the connection between your DC/WEF and the WEC. You will need this password when the certificate is imported to the events forwarder.
   3. Download the WEF certificate in a PFX format to your local machine.
4.  Install your WEF Certificate on the WEF to establish connection.

    You must install the WEF certificate on every Windows Server, whether DC or not, for the WEFs that are supposed to forward logs to the Windows Event Collector applet on the Broker VM.

    1. Locate the PFX file you downloaded from the Cortex XSIAM console and double-click to open the Certificate Import Wizard.
    2. In the Certificate Import Wizard:
       1. Select Local Machine, and then click Next.
       2. Verify the File name field displays the PFX certificate file you downloaded and click Next.
       3. In the Passwords field, enter the Client Certificate Export Password you defined in the Cortex XSIAM console followed by Next.
       4. Select Automatically select the certificate store based on the type of certificate, and then click Next and Finish.
    3. From a command prompt, run `certlm.msc`.
    4.  In the file explorer, navigate to Certificates and verify the following for each of the folders:

        * In the Personal → Certificates folder, ensure the certificate `forwarder.wec.paloaltonetworks.com` is displayed.
        * In the Trusted Root Certification Authorities → Certificates folder, ensure the CA `ca.wec.paloaltonetworks.com` is displayed.

        You can see more than one `ca.wec.paloaltonetworks.com` and `forwarder.wec.paloaltonetworks.com` file from a previous installation in the directory, so select the file with the most extended Expiration Date. You can verify that you are using the correct certificate:

        * To verify the client certificate in the Personal → Certificates folder is related to the CA, you can select your `forwarder.wec.paloaltonetworks.com` file and from the Certification Path tab, double-click ca.wec.paloaltonetworks.com. In the Details tab, Show: Properties only, and verify the Thumbprint matches the `ca.wec.paloaltonetworks.com` file Thumbprint.
        * For the Trusted Root Certificate (i.e. CA certificate), you can verify the Thumbprint of your `ca.wec.paloaltonetworks.com` file matches the Subscription Manager URL by double-clicking the file and from the Details tab verifying the Thumbprint.
    5. Navigate to Certificates Personal Certificates.
    6. Right-click the certificate and navigate to All tasks → Manage Private Keys.
    7.  In the Permissions window, select Add and in the Enter the object name section, enter **`NETWORK SERVICE`**, and then click Check Names to verify the object name. The object name is displayed with an underline when valid. and then click OK.

        [![certificate-permission.png](https://docs-cortex.paloaltonetworks.com/api/khub/maps/5CAbsl8idaK8R43ZLhoTOw/resources/71vaKGu4o6DHJQZwBW7ntA-5CAbsl8idaK8R43ZLhoTOw/content?v=141acfed476fcf1b\&Ft-Calling-App=ft/turnkey-portal)](https://docs-cortex.paloaltonetworks.com/viewer/attachment/5CAbsl8idaK8R43ZLhoTOw/71vaKGu4o6DHJQZwBW7ntA-5CAbsl8idaK8R43ZLhoTOw)
    8.  Click OK, verify the Group or user names that are displayed, and then click Apply Permissions for private keys.

        [![verify-permissions.png](https://docs-cortex.paloaltonetworks.com/api/khub/maps/5CAbsl8idaK8R43ZLhoTOw/resources/YbGRZDWrzPpY3w5zqaJKgg-5CAbsl8idaK8R43ZLhoTOw/content?v=2a9899c244fce1c9\&Ft-Calling-App=ft/turnkey-portal)](https://docs-cortex.paloaltonetworks.com/viewer/attachment/5CAbsl8idaK8R43ZLhoTOw/YbGRZDWrzPpY3w5zqaJKgg-5CAbsl8idaK8R43ZLhoTOw)
5. Configure the subscription manager.
   1.  Navigate to Computer Configuration → Policies → Administrative Templates: Policy definitions → Windows Components → Event Forwarding, right-click Configure target Subscription Manager and select Edit.

       [![target-subscription-manager.png](https://docs-cortex.paloaltonetworks.com/api/khub/maps/5CAbsl8idaK8R43ZLhoTOw/resources/kKhpS4bCErDE4LObGKnX0w-5CAbsl8idaK8R43ZLhoTOw/content?v=fa163dd36f71564a\&Ft-Calling-App=ft/turnkey-portal)](https://docs-cortex.paloaltonetworks.com/viewer/attachment/5CAbsl8idaK8R43ZLhoTOw/kKhpS4bCErDE4LObGKnX0w-5CAbsl8idaK8R43ZLhoTOw)
   2. In the Configure target Subscription Manager window, perform the following:
      1. Mark Configure target Subscription Manager as Enabled.
      2. In the Options section, select Show and in the Show Contents window, paste the Subscription Manage URL you copied from the Cortex XSIAM console, and then click OK.
      3. Click Apply and OK to save your changes.
6.  Complete the WEF Client certificate renewal.

    On every WEF DC, perform the following from a command prompt:

    1. Run `gpupdate /force` to update the group policy.
    2. To apply the configurations, `Restart-Service WinRM`.

### Task 2. Renew your WEC server certificate in Cortex XSIAM

{% hint style="info" %}
Only perform this step under the following conditions:

* You have completed the WEF certification renewal process for ALL clients in your environment. Otherwise, events from the WEFs that you did not install the new client certificate will not be collected by the WEC.
* You are approaching the WEC server CA certificate expiration date, which is 2 years after the Windows Event Collector applet activation, and receive a notification in the Cortex XSIAM console.
{% endhint %}

1. Select Settings → Configurations → Data Broker → Broker VMs.
2. Do one of the following:
   * On the Brokers tab, find the Broker VM, and in the APPS column, left-click the WEC connection to display the Windows Event Collector settings, and select Renew WEC Server Certificate.
   * On the Clusters tab, find the Broker VM, and in the APPS column, left-click the WEC connection to display the Windows Event Collector settings, and select Renew WEC Server Certificate.
3.  Click Renew.

    Once Cortex XSIAM renews the WEC server certificate, the status of the WEC in the APPS field on the Broker VMs machine is Connected indicating the applet is running. In addition, the health status of the Windows Event Collector applet is now green instead of yellow and the warning message that appeared when you hovered over the health status no longer appears. Your WEC server certificate is issued with a lifespan of 12 months.

    We also suggest that you run the following XQL query to verify that your event logs are being captured:

    ```
    dataset = xdr_data 
    | filter _product = "Windows" 
    | fields _vendor,_product,action_evtlog_level,action_evtlog_event_id 
    | sort desc _time 
    | limit 20
    ```

{% hint style="info" %}
If this query does not display results with a timestamp from after the renewal process, it could indicate that the renewal process is not complete, so wait a few minutes before running another query. If you are still having a problem, contact Technical Support.
{% endhint %}
