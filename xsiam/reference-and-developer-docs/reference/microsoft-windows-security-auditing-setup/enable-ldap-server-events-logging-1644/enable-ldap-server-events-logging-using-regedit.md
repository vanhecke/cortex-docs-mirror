# Enable LDAP server events logging using RegEdit

Make the following changes on all LDAP servers in the domain for which you want to configure auditing.

1. Log in as an administrator to a computer in the domain that you want to configure.
2. In the **Start** menu, type **regedit** to open the Registry Editor.
3.  Add the following values on the Domain controller registry.

    ```programlisting
    [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NTDS\Diagnostics]
    "15 Field Engineering"=dword:00000005
    [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NTDS\Parameters]
    "Expensive Search Results Threshold"=dword:00000001
    "Inefficient Search Results Threshold"=dword:00000001
    "Search Time Threshold (msecs)"=dword:00000001
    ```
