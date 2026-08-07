# Extract a subset of the data

In a playbook, you can extract subsets of context data to analyze a specific information set. This approach also applies when working with lists, such as extracting a subset of data from a JSON object. In this example, we extract server information from the list created above.

1. In a playbook, create a task.
   1. In the Choose Script field, select Set .
   2. In the key field, define a context key name for the data; for example, JSONDataSubset.
   3. In the value field, set the list you want to extract by clicking the curly brackets.
   4. Click Filters And Transformers.
   5. In the Get field, enter **`lists.Test1.domain.servers`**.
   6. In the Fetch data field, select an issue to test the data.
   7. Click Test.
   8. When the test completes, click Save.
   9. Save the task and the playbook.
2. Check that all the data is stored in the context key you defined by testing the playbook using the debugger.
   1. Click **`Run`** Debugger Panel.
   2.  The key you defined (JSONDataSubset) holds the subset of the data in context from the JSON object.

       [![work-with-json-lists-subset-8x.png](https://docs-cortex.paloaltonetworks.com/api/khub/maps/5CAbsl8idaK8R43ZLhoTOw/resources/UfEhYthyCCam5cqqwiiSRQ-5CAbsl8idaK8R43ZLhoTOw/content?v=508f115bed9cc5d7\&Ft-Calling-App=ft/turnkey-portal)](https://docs-cortex.paloaltonetworks.com/viewer/attachment/5CAbsl8idaK8R43ZLhoTOw/UfEhYthyCCam5cqqwiiSRQ-5CAbsl8idaK8R43ZLhoTOw)
