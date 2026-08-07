# Ingest alerts and metadata from Crowdstrike APIs

{% hint style="info" %}
To enable some of the APIs, you may need to reach out to CrowdStrike support.
{% endhint %}

To receive CrowdStrike API real-time alerts and logs, you must first configure data collection from CrowdStrike APIs. You can then configure the data source settings in Cortex XSIAM for the CrowdStrike APIs.

For more information on configuring data collection from CrowdStrike APIs, see the CrowdStrike Documentation.

When Cortex XSIAM begins receiving alerts and logs, it automatically creates a CrowdStrike API XQL dataset (`crowdstrike_falcon_incident_raw`). You can use the issues created by Cortex XSIAM in rules, and search the logs using XQL Search. For example queries, refer to the in-app XQL Library.

In order to ingest alert and host data, they must be configured correctly at both the CrowdStrike and the Cortex XSIAM sides, as explained in the following steps.

1.  Configure data collection from CrowdStrike APIs.

    1. In the CrowdStrike Falcon application, select [![cs-logo.png](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADsAAAAoCAYAAABAZ4KGAAAACXBIWXMAAA7EAAAOxAGVKw4bAAAAB3RJTUUH5QQSDTsWRXPQfwAAA5FJREFUaIHtmSFQKlsYgD/efaOWJThDcRPqjIsFC5u0uCaTG3RMazIxJIu7llcAixpcumDDGSWZWBJp6boUk2yz7ElYeOEODDqKqIBzuXxx55zd/+P8/zn/GUKLi4st/hL++ekARslEdlyZyI4rPWWTyeSo4hgJPWV93yedTr94JsvyUAMaJj1lb25uCIVCL4RlWUbX9aEHNgw+rNlsNsvy8jLn5+dIkoTruiQSiT9S+EPZcDiMYRiEQiHy+TyKomBZFolEovMD/Cn8mp2d/a/XgFgsxsrKCqenp8zPz5PJZAiCgLOzM2ZmZjg5OSEIAjzPG1HIXyfUT29smiZBEJDL5VBVlUwmw+PjI8fHxwDYtk2r1SKXy+E4DkKIoQf+Ffo6Z7PZLOFwmHw+z/39PbquU6/Xub6+RtM0dF3H930ymQzlcpl0Os36+vqwY39BsVikWCz2HPNhGrepVqsIIbBtm2az2VnF3d1dVldXOTg4IBKJEI/HicVibG5uYhgG0WiUcDhMo9Hg+fl5EF5vsr29DcDV1dW7Y/pK424kScI0TVRVxbIsXNfFMAw0TcOyLGzbZmlp6c25juPgOA6lUukznxwYn5Zto6oqyWSSVqvF0dERkiShaRq1Wo2Li4uec4UQFAoFCoXCSOu77zR+TaPRoFQq4fs+pmnSbDapVqs8PDwQiURQFOXdudPT06iqytraGre3t0NN726+fRFwXZe9vT1830fXdYQQZLPZvlZMUZSRNicDu/U4joNt26iqihCCXC7X1zzXdQcVwod8WVaW5U6qSpKELMsIITrBFwqFvjaiQTUjAz16XiOEIB6Ps7+/36nBra0t6vV6J4Vd12VhYYFoNPruezRNY2pqiqenp29tVkM5el4jSRKGYaDrOnNzc8DvJqRSqaAoCo7joOs6mqaRSCR69tKVSgXTNIe2Q39bthtFUdA0jY2NDe7u7ri8vMS2bcrlckdAkqQXO7UQAt/3UVWVVquF4zh91/tnGahsN7IsI8syQRCQz+c/vB05joPneRiGQSqVGsrGNTTZbnRd5/Dw8E3hWq1GqVSi0WgQBAEAhmFgWdbA4/h34G98ByHEC9l2b/3WbjwMURjRysLves5ms52+uX1MeZ43kLaxfezs7Oy8O2ZkK+t5XucC0a7nVCqFJEnEYrGRNBcjW9lu2sfVqC8CPyL7U0z+ERhXJrLjykR2XJnIjit/lez/1yKHlwoJ8FgAAAAASUVORK5CYII=)](https://docs-cortex.paloaltonetworks.com/viewer/attachment/5CAbsl8idaK8R43ZLhoTOw/qATr_yEenE8HnjMR5rtXLw-5CAbsl8idaK8R43ZLhoTOw) Support → API Clients and Keys.
    2. Under the OAuth2 API Clients section, Add new API client.
    3.  Configure your new API client with these settings:

        [![cs-add-new-api-client.png](https://docs-cortex.paloaltonetworks.com/api/khub/maps/5CAbsl8idaK8R43ZLhoTOw/resources/Z18IdWiHcHDfIYxyQvqhtQ-5CAbsl8idaK8R43ZLhoTOw/content?v=89f7b852d0aa3dcb\&Ft-Calling-App=ft/turnkey-portal)](https://docs-cortex.paloaltonetworks.com/viewer/attachment/5CAbsl8idaK8R43ZLhoTOw/Z18IdWiHcHDfIYxyQvqhtQ-5CAbsl8idaK8R43ZLhoTOw)

        * CLIENT NAME: Specify a name for the new API client.
        * DESCRIPTION: (Optional) Specify a description for the new API client.
        * API SCOPES → Event streams: Select the Read permissions check box.
        * API SCOPES → Hosts: Select the Read permissions check box.
    4. Click ADD.
    5.  Copy the values for the CLIENT ID, SECRET, and BASE URL, and save them, because you will need them when you configure the Data Collection settings in Cortex XSIAM.

        Ensure that you save the SECRET value because this is the only time that it is displayed.

    [![cs-api-client-created.png](https://docs-cortex.paloaltonetworks.com/api/khub/maps/5CAbsl8idaK8R43ZLhoTOw/resources/gKtp7yoLJE_DiJXWwYrcNA-5CAbsl8idaK8R43ZLhoTOw/content?v=4800c4acd76fd792\&Ft-Calling-App=ft/turnkey-portal)](https://docs-cortex.paloaltonetworks.com/viewer/attachment/5CAbsl8idaK8R43ZLhoTOw/gKtp7yoLJE_DiJXWwYrcNA-5CAbsl8idaK8R43ZLhoTOw)

    f. Click DONE.
2.  Configure the CrowdStrike Platform collection in Cortex XSIAM.

    1. Navigate to Settings → Data Sources & Integrations.
    2. On the Data Sources & Integrations page, click + Add New, search for CrowdStrike Platform, then hover over it and click Add.
    3. Set these parameters:
       * Name: Specify a descriptive name for your log collection configuration, preferably the same CLIENT NAME used when adding a new client API in the CrowdStrike Falcon application, as explained above.
       * Base URL: Specify the BASE URL you received when you created the client API in the CrowdStrike Falcon application, as explained above.
       * Client ID: Specify the CLIENT ID you received when you created the client API in the CrowdStrike Falcon application, as explained above.
       * Secret: Specify the SECRET you received when you created the client API in the CrowdStrike Falcon application, as explained above.
       * Collect: Select the items that you want to collect (Alerts, Hosts).
    4. Click Test to validate access, and then click Enable.

    When events start to come in, a green check mark appears below the CrowdStrike Platform configuration, along with the amount of data received.
