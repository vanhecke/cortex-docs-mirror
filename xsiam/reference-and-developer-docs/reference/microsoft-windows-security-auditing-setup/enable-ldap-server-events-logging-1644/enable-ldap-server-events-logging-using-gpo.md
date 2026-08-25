---
description: >-
  Configure LDAP server Event ID 1644 logging through Group Policy for Cortex
  XSIAM.
---

# Enable LDAP server events logging using GPO

1. On a domain controller or a system with Remote Server Administration Tools (RSAT) installed, open the **Group Policy Management Console** (GPMC).
2. Create a new Group Policy Object (GPO): Right-click on the domain or organizational unit (OU) where your domain controllers reside, then select **Create a GPO in this domain, and Link it here...**. Give it a descriptive name, e.g. Domain Controller Registry Settings.
3. Edit the GPO.
   1.  Right-click on the newly created GPO and select **Edit**.

       ![image33.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-b7c4ac4a3ac3a49c48b677c76a509c8aa64c96e0%2F2b80decb3d1e81a0260d2b48f393a043c314f18933bf817a83c77b5ee8108c3e.png?alt=media)
   2.  In the **Group Policy Management Editor**, navigate to **Computer Configuration** → **Preferences** → **Windows Settings** → **Registry**.

       ![image18.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-f321353771877172429f929a592f7c9fd0f1a368%2F120e7d50fd89ada8a6819c8aa213a7cd5c0d26326a087fe4a9bec3e5bc8665c6.png?alt=media)
   3.  Add Registry Items: Right-click on **Registry** and select **New** → **Registry Item**.

       ![image36.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-719de7fa2bfec6a7442cf81f85d205a7fb790fe5%2F29954139a75e6ad4370698869e47f3f1402265810113a7abf245c86ee6d3c499.png?alt=media)
   4. Configure Registry Keys: For each of the registry keys you want to set, create a new Registry Item.

<details>

<summary>\[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NTDS\Diagnostics\]</summary>

Create the following Registry item:

15 Field Engineering

* Action: Update
* Hive: HKEY\_LOCAL\_MACHINE
* Key Path: SYSTEM\CurrentControlSet\Services\NTDS\Diagnostics
* Value name: 15 Field Engineering
* Value type: REG\_DWORD
* Value data: 5

| [![image19.png](https://docs-cortex.paloaltonetworks.com/api/khub/maps/5CAbsl8idaK8R43ZLhoTOw/resources/vEZJTcCs9lKn5Amq5W3xRg-5CAbsl8idaK8R43ZLhoTOw/content?v=63af2757424f52ea\&Ft-Calling-App=ft/turnkey-portal)](https://docs-cortex.paloaltonetworks.com/viewer/attachment/5CAbsl8idaK8R43ZLhoTOw/vEZJTcCs9lKn5Amq5W3xRg-5CAbsl8idaK8R43ZLhoTOw) |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

</details>

<details>

<summary>[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NTDS\Parameters]</summary>

Create the following Registry items:

Expensive Search Results Threshold

* Action: Update
* Hive: HKEY\_LOCAL\_MACHINE
* Key Path: SYSTEM\CurrentControlSet\Services\NTDS\Parameters
* Value name: Expensive Search Results Threshold
* Value type: REG\_DWORD
* Value data: 1

| [![image13.png](https://docs-cortex.paloaltonetworks.com/api/khub/maps/5CAbsl8idaK8R43ZLhoTOw/resources/2HpxdNC8WZhPpJH2eq4eSg-5CAbsl8idaK8R43ZLhoTOw/content?v=00455b9076715007\&Ft-Calling-App=ft/turnkey-portal)](https://docs-cortex.paloaltonetworks.com/viewer/attachment/5CAbsl8idaK8R43ZLhoTOw/2HpxdNC8WZhPpJH2eq4eSg-5CAbsl8idaK8R43ZLhoTOw) |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

Inefficient Search Results Threshold

* Action: Update
* Hive: HKEY\_LOCAL\_MACHINE
* Key Path: SYSTEM\CurrentControlSet\Services\NTDS\Parameters
* Value name: Inefficient Search Results Threshold
* Value type: REG\_DWORD
* Value data: 1

| [![image6.png](https://docs-cortex.paloaltonetworks.com/api/khub/maps/5CAbsl8idaK8R43ZLhoTOw/resources/NbalKIbhQXzRh44l6w2tTQ-5CAbsl8idaK8R43ZLhoTOw/content?v=c6e272aad32627e0\&Ft-Calling-App=ft/turnkey-portal)](https://docs-cortex.paloaltonetworks.com/viewer/attachment/5CAbsl8idaK8R43ZLhoTOw/NbalKIbhQXzRh44l6w2tTQ-5CAbsl8idaK8R43ZLhoTOw) |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

Search Time Threshold (msecs)

* Action: Update
* Hive: HKEY\_LOCAL\_MACHINE
* Key Path: SYSTEM\CurrentControlSet\Services\NTDS\Parameters
* Value name: Search Time Threshold (msecs)
* Value type: REG\_DWORD
* Value data: 1

| [![image26.png](https://docs-cortex.paloaltonetworks.com/api/khub/maps/5CAbsl8idaK8R43ZLhoTOw/resources/K7YtRnvJDve3NnJv4HSaKg-5CAbsl8idaK8R43ZLhoTOw/content?v=e761e90e3d379c17\&Ft-Calling-App=ft/turnkey-portal)](https://docs-cortex.paloaltonetworks.com/viewer/attachment/5CAbsl8idaK8R43ZLhoTOw/K7YtRnvJDve3NnJv4HSaKg-5CAbsl8idaK8R43ZLhoTOw) |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

</details>

4. Close the Group Policy Management Editor.
5. To link the GPO to the OU where your domain controllers reside, in Group Policy Management, right-click the OU, select Link an Existing GPO, then select the GPO you just created.\
   ![](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2FO9YvBqtITkUuDMZa5K8H%2Fimage.png?alt=media\&token=770f0147-db0b-4026-89df-6c85c053e49e)
6. Force Group Policy Update: Force a Group Policy update using the `gpupdate /force` command on each domain controller or by restarting them.
