# Enable security auditing event IDs with GPO

Use the Group Policy Management Editor to configure security auditing policies across domain controllers or other target machines.

{% hint style="info" %}
### Note

We recommend that you configure the Group Policy Object (GPO) to apply to all endpoints and not just Domain Controllers. This ensures comprehensive auditing across your entire network.
{% endhint %}

1. Log in to a Domain Controller (DC) as a domain admin.
2. Open the **Group Policy Management Editor** using one of the following methods:
   * Navigate to **Server Manager** → **Tools** → **Group Policy Management**.
   * On your keyboard, press **Win + R**, type GPMC.exe, and press **Enter**.
3.  Create or select a GPO using one of the following methods:

    * Create a new GPO and link it to an Organizational Unit (OU) containing the computers where you want to apply the changes.
    * Use an existing GPO. For example, to apply changes to domain controllers, expand the **Domain Controllers OU**, right-click **Default Domain Controllers Policy**, and select **Edit**.

    ![image8.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-e1fa0814efb591493b54db8078405389fa569fa3%2Fa80abcceeb7eca1d2161a31f8ac15a73ff1d364ffdb11d21d2fa4a0905a863c2.png?alt=media)
4.  In the **Group Policy Management Editor**, navigate to **Computer Configuration** → **Policies** → **Windows Settings** → **Security Settings** → **Advanced Audit Policy Configuration** → **Audit Policies**.

    ![image38.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-143c0ddc408dce8eeb2226d9b3e49481017cce98%2F35eab9d817cf0002becd8ab9df2447338b08837519651abffdd36a7e0b6556fc.png?alt=media)
5.  In the **Audit Policies** settings, enable logging for both successful and failed attempts for the following events.

    | **Event IDs**                                                                      | **Audit Policy**   | **Subcategory**                          | **Additional configuration needed**                                                                                                                                                 |
    | ---------------------------------------------------------------------------------- | ------------------ | ---------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | 4776, 4822, 4823                                                                   | Account Logon      | Audit Credential Validation              |                                                                                                                                                                                     |
    | 4768, 4771, 4824                                                                   | Account Logon      | Audit Kerberos Authentication Service    | DCs only                                                                                                                                                                            |
    | 4769, 4770, 4821                                                                   | Account Logon      | Audit Kerberos Service Ticket Operations | DCs only                                                                                                                                                                            |
    | 4741, 4742, 4743                                                                   | Account Management | Audit Computer Account Management        | DCs only                                                                                                                                                                            |
    | 4727, 4728, 4729, 4731, 4732, 4733, 4735, 4737, 4754, 4755, 4756, 4757, 4764, 4799 | Account Management | Audit Security Group Management          |                                                                                                                                                                                     |
    | 4720, 4722, 4723, 4724, 4725, 4726, 4738, 4740, 4765, 4766, 4767, 4780, 4781       | Account Management | Audit User Account Management            |                                                                                                                                                                                     |
    | 4662                                                                               | DS Access          | Audit Directory Service Access           | <p><a href="additional-setup-for-active-directory-certificate-services-adcs-events">Additional setup for Active Directory Certificate Services (ADCS) events</a></p><p>DCs only</p> |
    | 4634, 4647                                                                         | Logon/Logoff       | Audit Logoff                             |                                                                                                                                                                                     |
    | 4624, 4625, 4648                                                                   | Logon/Logoff       | Audit Logon                              |                                                                                                                                                                                     |
    | 4649, 4778, 4800, 4801, 4802, 4803                                                 | Logon/Logoff       | Audit Other Logon/Logoff Events          |                                                                                                                                                                                     |
    | 4672                                                                               | Logon/Logoff       | Audit Special Logon                      |                                                                                                                                                                                     |
    | 4880, 4881, 4885, 4886, 4887, 4888, 4896, 4898, 4899, 4900                         | Object Access      | Audit Certification Services             | [Additional setup for Active Directory Certificate Services (ADCS) events](additional-setup-for-active-directory-certificate-services-adcs-events)                                  |
    | 5140                                                                               | Object Access      | Audit File Share                         |                                                                                                                                                                                     |
    | 4698, 4702                                                                         | Object Access      | Audit Other Object Access Events         |                                                                                                                                                                                     |
    | 4713                                                                               | Policy Change      | Audit Authentication Policy Change       |                                                                                                                                                                                     |
    | 4616                                                                               | System             | Audit Security State Change              |                                                                                                                                                                                     |
    | 1102                                                                               | System             | Other System Events                      | Enabled by default                                                                                                                                                                  |
