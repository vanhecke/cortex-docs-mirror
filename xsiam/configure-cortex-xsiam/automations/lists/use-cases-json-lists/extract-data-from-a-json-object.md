# Extract data from a JSON object

Create a JSON list and use the **Set** automation to create a context key from its data.

1. Create a List:
   1. In the Name field, type `Test1`.
   2. Select **Settings** → **Configurations** → **Object Setup** → **Lists** → **Add a List**.
   3.  In the **Content Type** field, select **JSON** and add the following content:

       ```programlisting
       {    
           "domain": {
               "name": "mwidomain",
               "prod_mode": "prod",
               "user": "weblogic",
               "admin": {
                   "servername": "AdminServer",
                   "listenport": "8001"
               },
               "machines": [
                   {
                       "refname": "Machine1",
                       "name": "MWINODE01"
                   },
                   {
                       "refname": "Machine2",
                       "name": "MWINODE02"
                   }
               ],
               "clusters": [
                   {
                       "refname": "Cluster1",
                       "name": "App1Cluster",
                       "machine": "Box1"
                   },
                   {
                       "refname": "Cluster1",
                       "name": "App2Cluster",
                       "machine": "Box2"
                   }
               ],
               "servers": [
                   {
                       "name": "ms1",
                       "port": 9001,
                       "machine": "Box1",
                       "clusterrefname": "Cluster1"
                   },
                   {
                       "name": "ms2",
                       "port": 9002,
                       "machine": "Box2",
                       "clusterrefname": "Cluster2"
                   }
               ]
           }
       }
       ```
   4. **Save** the list.
2. Create a playbook task with the **Set** automation:
   1. Select **Investigation & Response** → **Automation** → **Playbooks** → **New Playbook**.
   2. Name the playbook, and click Save.
   3. Click Create Task and provide a task name.
   4.  In the **Choose Script** field, select **Set** .

       The **Set** script sets a value in context under the key entered.
   5.  In the **key** field, define a context key name for the data. For example, JSONData.

       ![](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-b3b16f5c8e611e52e4d1b53e54a9dc3203c11f09%2F38fe0fa6812d1f708c018e3980afd68fcb6cbc545986a45460e5696ae20a1f8b.png?alt=media)
   6. In the **value** field, set the list you want to extract by clicking the curly brackets.
   7. Click **Filters And Transformers**.
   8. In the **Get** field, click the curly brackets, and in the **Select source for value** section, select the list you created in step 1: **Test1**.
   9. In the **Fetch data** field, select an issue to test the data.
   10. Click **Test**.

       In this example, the test results have found the list data.

       ![](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-9ae84c84914b65b741e20f58379213d7f1bf9e81%2F096ce4f2cadf1185c5bc65456694eddedaa245c9fb9c7249841bf4109a1ff417.png?alt=media)
   11. When the test completes, click **Save**.
   12. Save the task and playbook.
3. Check all the data is stored in the context key you defined by testing the playbook using the debugger:
   1. Click **Run**.
   2.  Open the **Debugger Panel**.

       The key you defined, JSONData, holds the data in context from the JSON object.

       ![](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-775db50288eb61339d47176d086481322e2f74c4%2F3a6a3ed16bb1e081d2ba4d004d0c14c84717bc558c7a5a0ec228bdb146011575.png?alt=media)
