---
description: Filter data extracted from a Cortex XSIAM JSON list.
---

# Filter extracted data

Filter an extracted data subset to analyze a specific information set. This example filters `Box1` information from the list created in [Extract data from a JSON object](extract-data-from-a-json-object).

1. Reopen the task you created.
2. Select the **value** field.
3. Under **Filter**, select **Add Filter**.
4.  Set the condition you want to filter.

    In this example, retrieve the list of machines named **`Box1`** from **`Test1`** list by setting the filter **`lists.Test1.domain.servers.machine Equals Box1`**.

    ![work-with-json-lists-filter-data-8-x.png](https://paloaltonetworks.fluidtopics.net/api/khub/maps/5CAbsl8idaK8R43ZLhoTOw/resources/fyxMwQXDfsFwMu2b2kp6Ug-5CAbsl8idaK8R43ZLhoTOw/content?v=d8cfb68e514de1a0\&Ft-Calling-App=ft/turnkey-portal)

    1. Click Test.
    2.  Check whether the data subset was accessed successfully by selecting the data source from an issue. You can see the results returned **`machine: Box1`**.

        ![lists-test.png](https://paloaltonetworks.fluidtopics.net/api/khub/maps/5CAbsl8idaK8R43ZLhoTOw/resources/IpBjKgAl6_feyg9tRy9G4g-5CAbsl8idaK8R43ZLhoTOw/content?v=9694f128722026c1\&Ft-Calling-App=ft/turnkey-portal)
