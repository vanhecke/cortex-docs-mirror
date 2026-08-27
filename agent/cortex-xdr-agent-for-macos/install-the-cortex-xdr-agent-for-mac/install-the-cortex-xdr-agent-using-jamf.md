---
description: >-
  Step-by-step instructions to configure a JAMF installation profile for the
  Cortex XDR agent on macOS endpoints.
---

# Install the Cortex XDR Agent Using JAMF

To deploy the Cortex XDR agent to multiple endpoints, you can set up a JAMF profile. As part of your JAMF deployment you must grant full disk access, approve system extensions, content filter configuration, notifications and managed login items. Depending on your macOS version.

For a seamless configuration using JAMF that does not require creating the configuration profile manually, refer to [Install with a unified configuration profile for MDMs](install-with-a-unified-configuration-profile-for-mdms).

{% hint style="warning" %}
### Caution

Following the changes Apple introduced in [macOS 11.3 for MDMs](https://support.apple.com/en-us/HT211911), when you remove an MDM configuration profile that includes permissions for system extensions (for Cortex XDR agents or Global Protect), the system extensions will be instantly unloaded from all endpoints. As a result, the Cortex XDR protection status will be disabled.
{% endhint %}

To set up a JAMF profile step-by-step, use the following workflow. The figures given here are as examples only. For additional information, refer directly to the [JAMF documentation on configuring configuration profiles](https://learn.jamf.com/bundle/jamf-pro-documentation-current/page/Computer_Configuration_Profiles.html).

1.  Create a new **Computer Configuration Profile** in JAMF.

    Under General Options, assign the following:

    * Name: **`Cortex XDR Agent Unified Configuration Profile`**
    * Level: Select **Computer level**.

    ![Unified\_Config\_Profile.png](https://517755450-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FuBmMrMEHkk0xAv8axZos%2Fuploads%2FpkJf0xphsLTc0uLqqLup%2F08ecb34c768b18d842d71f2538e159ebab61374a062aeb1a0353ee5a005d458b.png?alt=media\&token=58334f9e-1cd5-41b4-8bd3-04b5382d33cb)
2.  Configure **System Extensions**.

    ![JAMF\_System\_Extentions\_2023.png](https://517755450-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FuBmMrMEHkk0xAv8axZos%2Fuploads%2FQET8D1KGBXXbP2R9lGbs%2F38bb2d6eaf91e2ff45a6fd859e4b946b1d91883cb9d10b5e512d1c6df5ebdde2.png?alt=media\&token=602d4509-9340-41ec-b586-992019bff797)

    1. Select**Allow users to approve system extensions**.
    2. Add an approved Team ID for Palo Alto Networks:
       * System Extension Types—**Allowed System Extensions**
       * Team Identifier—**`PXPZ95SK77`**
       * Allowed system extension bundles—**`com.paloaltonetworks.traps.securityextension`** and **`com.paloaltonetworks.traps.networkextension`**
    3. Add the allowed system extensions and save each item.
3.  Configure **Content Filter**.

    1. Configure the following Content Filter in your JAMF profile:
       * Filter name: **`Cortex XDR Network Filter`**
       * Identifier: **`com.paloaltonetworks.cortex.app`**
       * Filter Order: **`Firewall`**
    2. Set the socket filter to enabled, and define the following:
       * Socket Filter Bundle Identifier: **`com.paloaltonetworks.traps.networkextension`**
       * Socket Filter Designated Requirement: **`identifier "com.paloaltonetworks.traps.networkextension" and anchor apple generic and certificate 1[field.1.2.840.113635.100.6.2.6] /* exists / and certificate leaf[field.1.2.840.113635.100.6.1.13] / exists */ and certificate leaf[subject.OU] = PXPZ95SK77`**
    3. The network (packet) filter is set to enabled. Cortex XDR agent disables the filter when it gets a default policy. The packet filter provider is enabled by the Cortex XDR agent when it is required.
       * Network Filter Bundle Identifier: **`com.paloaltonetworks.traps.networkextension`**
       * Network Filter Designated Requirement: **`identifier "com.paloaltonetworks.traps.networkextension" and anchor apple generic and certificate 1[field.1.2.840.113635.100.6.2.6] /* exists / and certificate leaf[field.1.2.840.113635.100.6.1.13] / exists */ and certificate leaf[subject.OU] = PXPZ95SK77`**

    ![JAMF\_Config\_Settings-Content\_Filter\_2023.png](https://517755450-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FuBmMrMEHkk0xAv8axZos%2Fuploads%2FIQUUYCuHrcPXD6oPpHur%2F5096e34288e91694ce4f06f30a51d764513e0b81297cf118f5602ed183632302.png?alt=media\&token=8ca1614c-5020-437d-bc58-3558651eea35)
4.  Configure **Privacy Preferences Policy Control** as described in Steps 4, 5, and 6:

    ![JAMF\_Privacy\_Preferences\_Policy\_Control\_2023.png](https://517755450-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FuBmMrMEHkk0xAv8axZos%2Fuploads%2Fta9eddtnVO2VacAADY8S%2Ff41ea5f9684f1c90ceafeed970d5f0de9be86a58da0840aa2951547f36b7d6ec.png?alt=media\&token=f7a3a6d2-1240-4e47-b297-1f9d73fd1dbe)

    1. Use the following settings to define the entity:
       * Identifier: **`com.paloaltonetworks.cortex.agent`**
       * Identifier Type: **Bundle ID**
       * Code Requirement: **`identifier "com.paloaltonetworks.cortex.agent" and anchor apple generic and certificate 1[field.1.2.840.113635.100.6.2.6] /* exists / and certificate leaf[field.1.2.840.113635.100.6.1.13] / exists */ and certificate leaf[subject.OU] = PXPZ95SK77`**
    2. Add and **Allow** Accessibility service.
    3. Save the app or service item.
5.  Add a new **App Access** configuration to grant Full Disk Access to the Cortex XDR security extension.

    This configuration is required to enable the security extension to communicate with the OS.

    ![JAMF\_Privacy\_Preferences\_Policy\_Control\_b\_2023.png](https://517755450-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FuBmMrMEHkk0xAv8axZos%2Fuploads%2FdtJbEslH7GWmlgx5ctXl%2Ffc3c2b699de610acbf23310daa27f1229d27c36a208e6d6ebbb08374aea26229.png?alt=media\&token=d448051c-b715-4a6d-a4eb-0d10368ec30b)

    1. Use the following settings to define the following entity:
       * Identifier: **`com.paloaltonetworks.traps.securityextension`**
       * Identifier Type: **Bundle ID**
       * Code Requirement: **`identifier "com.paloaltonetworks.traps.securityextension" and anchor apple generic and certificate 1[field.1.2.840.113635.100.6.2.6] /* exists */ and certificate leaf[field.1.2.840.113635.100.6.1.13] /* exists */ and certificate leaf[subject.OU] = PXPZ95SK77`**
    2. In **App or Service**, set **SystemPolicyAllFiles** to **Allow**.
    3. **Save** the app or service item.
6.  Add a new **App Access** configuration to grant Full Disk Access to Cortex XDR pmd.

    This configuration allows the daemon access to analyze processes, files, disk access, utilities and more.

    ![JAMF\_Privacy\_Preferences\_Policy\_Control\_c\_2023.png](https://517755450-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FuBmMrMEHkk0xAv8axZos%2Fuploads%2F8ANlCm2lrxflEzNM3AeU%2F4b9be74911acc8cab83bf40c32e189933a84a5148999a235c1b3cf56ea01dcd3.png?alt=media\&token=89b178f9-cbc7-4507-8f3b-c124dcc9dfe3)

    1. Use the following settings to define the entity:
       * Identifier: **`/Library/Application Support/PaloAltoNetworks/Traps/bin/pmd`**
       * Identifier Type: **Path**
       * Code Requirement: **`identifier pmd and anchor apple generic and certificate 1[field.1.2.840.113635.100.6.2.6] /* exists */ and certificate leaf[field.1.2.840.113635.100.6.1.13] /* exists */ and certificate leaf[subject.OU] = PXPZ95SK77`**
    2. In **App or Service**, set **SystemPolicyAllFiles** to **Allow**.
    3. **Save** the app or service item.
7.  Configure **Notifications**.

    Configure the following Notifications payload in your JAMF profile:

    *   Bundle ID for agent 8.2 and earlier: **`com.paloaltonetworks.traps-agent`**

        Bundle ID for agent 8.3 and later: **`com.paloaltonetworks.cortex.agent`**
    * Critical alerts: **`Enable and include`**.
    * Notifications: **`Enable and include`**.
    * Banner alert type: **`Temporary and include`**.
    * Notifications on Lock Screen: **`Display and include`**.
    * Notifications on Notification Center: **`Display and include`**.
    * Badge app icon: **`Display and include`**.
    * Play sound for notifications: **`Enable`**.

    ![JAMF\_Notifications\_2023.png](https://517755450-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FuBmMrMEHkk0xAv8axZos%2Fuploads%2FaRrx6DqAP3S6XkX5OUE5%2F623a1d4deae5a63ad1a955f15b9c521763fe2809c56e27ca56034e15fd607758.png?alt=media\&token=9361873a-70c2-4db2-9a87-cfce6d60b516)
8.  Configure Managed Login Items.

    * Rule type: **`Label prefix`**
    * Rule value: **`com.paloaltonetworks.cortex`**
    * Team identifier: **`PXPZ95SK77`**
    * Rule comment: **`Allows Cortex XDR launch daemons and launch agents`**

    ![Configuration\_profile\_Notifications\_2.png](https://517755450-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FuBmMrMEHkk0xAv8axZos%2Fuploads%2FN6ngqE6ZKpsHxCq4bYU5%2F25f98fa7fe63acca4c32c7789d62fc4b945f6f8c4d7f18cf612f42eb76717f2f.png?alt=media\&token=5ab3bf4e-02a5-4c38-9a02-7a32c83d9514)
9. Configure **Application & Custom Settings** and click **Upload**.
   1.  Select **+Add** to add the configuration details for each web browser:

       **Chrome**:

       * Preference Domain: `com.google.Chrome`
       *   Property List:

           ```programlisting
           <?xml version="1.0" encoding="UTF-8"?>
           <!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
           <plist version="1.0">
             <dict>
               <key>ExtensionSettings</key>
               <dict>
                 <key>aalncdhjokfcbldaemnehledpfpibopi</key>
                 <dict>
                   <key>installation_mode</key>
                   <string>force_installed</string>
                   <key>toolbar_pin</key>
                   <string>force_pinned</string>
                   <key>update_url</key>
                   <string>file:///Library/Application Support/PaloAltoNetworks/Traps/cdsx/extension.xml</string>
                 </dict>
               </dict>
             </dict>
           </plist>
           ```

           ![CdsxMdmChrome.png](https://517755450-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FuBmMrMEHkk0xAv8axZos%2Fuploads%2FN3LXdf1dXd4oAYMid73f%2Fdf5f70097c2a938991c6ca54878efae802413d1f19c61a2edad0ae2282816415.png?alt=media\&token=88882d84-9f84-47e7-b95c-bd1489be86e7)

       **Edge**

       * Preference Domain: `com.microsoft.Edge`
       *   Property List:

           ```programlisting
           <?xml version="1.0" encoding="UTF-8"?>
           <!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
           <plist version="1.0">
             <dict>
               <key>ExtensionSettings</key>
               <dict>
                 <key>aalncdhjokfcbldaemnehledpfpibopi</key>
                 <dict>
                   <key>installation_mode</key>
                   <string>force_installed</string>
                   <key>toolbar_state</key>
                   <string>force_shown</string>
                   <key>update_url</key>
                   <string>file:///Library/Application Support/PaloAltoNetworks/Traps/cdsx/extension.xml</string>
                 </dict>
               </dict>
             </dict>
           </plist>
           ```

           ![CdsxMdmEdge.png](https://517755450-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FuBmMrMEHkk0xAv8axZos%2Fuploads%2FUgVQXrbdK4x1QhzmfGyx%2Fb123bfd6830fb951236152cbd5638cb5a6d6762a4c4b9eaea4450ac180a3adca.png?alt=media\&token=f8e38791-b8c3-49b6-83fd-cf826c92dd9f)
10. **Save** the configuration profile.
11. After you set up your computer configuration profiles, create a new agent installation package in the Cortex XDR management console, upload the ZIP package you downloaded from Cortex XDR to your MDM (do not extract it), and then add it to a distribution point.

    For instructions, see the following documentation resource from JAMF: [Manually Adding a Package to a Distribution Point and Jamf Pro](https://learn.jamf.com/bundle/jamf-pro-documentation-current/page/Package_Management.html).
12. Create a new policy and install the package.
    * JAMF [Package Deployment](https://learn.jamf.com/bundle/jamf-pro-documentation-current/page/Package_Deployment.html) instructions.
    * JAMF [Policy Management](https://learn.jamf.com/bundle/jamf-pro-documentation-current/page/Policy_Management.html) instructions.
