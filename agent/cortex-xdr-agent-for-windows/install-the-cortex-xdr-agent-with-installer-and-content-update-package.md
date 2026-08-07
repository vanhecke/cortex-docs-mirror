---
description: >-
  Deploy the Cortex XDR agent on Windows endpoints using the latest content and
  installer package.
---

# Install the Cortex XDR Agent with Installer and Content Update Package

To reduce the network load and time typically required for the initial roll-out or major upgrades of the Cortex XDR agent, Cortex XDR offers an agent installation and content update distribution package. The distribution package includes the agent installer and the latest supported content available in Cortex XDR, eliminating the content update download phase which is typically required after agent installation. You can deploy the distribution package using a third party tool such as an SCCM, or manually on the endpoint.

To deploy or upgrade agents using the distribution package, you first need to create an agent installation package in Cortex XDR. Then, you can choose to download the distribution package zip along with the latest content zip. The content version included in the package is the latest content available in Cortex XDR at the time of package download. If between the time you created a package and the time you downloaded it a new content version has become available, Cortex XDR will automatically update the content version within the distribution packages available in your tenant. After you download the package, the content version within that zip archive is static and cannot be updated. It is therefore advised to always download a pre-created distribution package only at the time you intend to start the deployment.

The following are prerequisites to use this deployment method:

| Requirement | Description                                                                                                                                                                  |
| ----------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| General     | <ul><li>Requires Windows 7 SP1/Server 2008 R2 SP1 or later.</li><li>When you deploy using the SCCM system, you must have network credentials in your organization.</li></ul> |

<details>

<summary>How to install or update agents using the installer and content package manually</summary>

To deploy the Cortex XDR agent and content manually on the endpoint, first create an agent installation package with the latest content, download and extract it, and then proceed to Install the Cortex XDR Agent for Windows using the CONTENT runtime argument:

1.  Create an agent installation package.

    In Cortex XDR, go to Endpoints → Endpoint Management → **Agent Installations** page, and Create an agent Installation Package.
2.  Download the installation and content distribution package locally.

    In **Agent Installations**, right-click the distribution package you created and according to the endpoint architecture, select 64 bit installer → **Download 64 bit installer + latest content update (zip)**.

    The extracted downloaded distribution package zip includes two files: the msi installer and the content zip.

    ![installer-and-content-package-download-zip.png](https://517755450-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FuBmMrMEHkk0xAv8axZos%2Fuploads%2FFM1ujrAo3mW9tH9c8c0Z%2F013b2b958e575853e0199c50118993adabc0f18057b83a78bf1fee588a524947.png?alt=media\&token=82ec754d-c890-427f-82c3-270c5d51ae0a)
3.  Install the agent on the endpoint.

    Proceed to [Install the Cortex XDR agent for Windows](install-the-cortex-xdr-agent-for-windows) and add the **`CONTENT`** runtime argument as explained. For example,**`CONTENT=\\sccm\share\Traps\Version740\content-181-58641.zip`**.

</details>

<details>

<summary>How to install or update agents using the installer and content package using SCCM</summary>

To deploy the Cortex XDR agent and content on the endpoint using an SCCM, follow these guidelines and fill-in the values as specified.

{% hint style="info" %}
### Note

This high-level workflow refers only to the specific SCCM configurations that you must set for this type of deployment. For the other optional settings that are not included in this workflow, follow the Microsoft official guidelines and your organization needs.
{% endhint %}

1.  Upload the files to your SCCM network Share folder.

    Unpack the Cortex XDR agent installation.zip file, and copy both the installation msi and content-XXX-XXXXX.zip files to the Share folder on your SCCM server under a directory of your choice. For example, `\\SCCM\Share\MyCortexXDRAgentDeploymentFolder\`. To copy files to the Share folder, you must have network credentials in your organization.
2. Create the SCCM application package.
   1.  In SCCM Applications, **Create Application** to launch the **Create Application Wizard** and specify the following settings for this application:

       * Ensure the **Automatically detect information about this application from installation files** option is selected to enable SCCM to pull both msi and content-XXX-XXXXX.zip files from the Share folder on the SCCM server.
       * **Type**—**Windows installer (\*.msi file)**
       * **Location**—Browse to your Share folder and select the installation file.
       * Click **Next** to continue.

       ![sccm-create-package.png](https://517755450-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FuBmMrMEHkk0xAv8axZos%2Fuploads%2FRefMKGHwJjMVTAVsStml%2F06bca115cb260d1b37a436434fbd73e60d74723429f2f1910459d0d9930d8e9e.png?alt=media\&token=d955b494-0404-49ca-9e6d-d4a0eb0588e3)
   2.  In **View imported information**, verify that SCCM detected both files in the Share folder, the msi and the content zip files (Number of files: 2). Click **Next** to continue.

       ![sccm-create-package-2.png](https://517755450-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FuBmMrMEHkk0xAv8axZos%2Fuploads%2FCo95VS3rBAHcROwERZB5%2F74c6cfba57b206925778ec2521951c1cdd33eb7df9a7caf92abb6f622119cfc5.png?alt=media\&token=06800abf-beeb-4a84-acfe-9d9b03a07aae)
   3. In **Specify info about this application**, fill-in the following information:
      * **Name**—Displays the name of your deployment application.
      *   **Installation program**—Enter the Cortex XDR agent installation command line to include the msi and content zip files. For example:

          ```programlisting
          msiexec /i “installer_x64.msi”  CONTENT=\\SCCM\Share\MyCortexXDRAgentDeploymentFolder\content-XXX-XXXXX.zip /qn
          ```

          It is highly recommended to add the `/qn` installation flag for a quiet installation. Other installation flags such as creating a log file are optional and can be added as described in [Install the Cortex XDR agent for Windows](install-the-cortex-xdr-agent-for-windows).
      * **Install behavior**—**Install for system**.
      * Proceed to fill-in other fields as required, and click **Next** to continue.
   4.  Review the **Summary**. To confirm the settings for this application, click **Next**. Wait for the application package to generate and **Close** to exit the wizard.

       ![sccm-application-complete.png](https://517755450-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FuBmMrMEHkk0xAv8axZos%2Fuploads%2F66jt0e3bvYZ4hIQzPeIa%2F5b62fd903b555f33fb6924386905cc8ea8f1bcaba62031ab351a889d74a5a58d.png?alt=media\&token=5b216538-bbf7-41bb-bd94-fe831f06110a)
3.  Set the Working Directory.

    To ensure that SCCM deploys the Cortex XDR agent installation and content files in the correct folders on the endpoint, you must set the application package working directory.

    1.  From the SCCM applications list, right-click your application package and select **Properties**.

        ![properties.png](https://517755450-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FuBmMrMEHkk0xAv8axZos%2Fuploads%2FHwD4OX4Jn3zQCGdLqjOl%2F4fe3580784a0049b39a736752c1ec789f707896d3ca1bf8ce5e40ab16c921090.png?alt=media\&token=34a98dbe-c6eb-42e4-97b1-57562747a116)
    2.  Go to the **Deployment Types** tab, select the msi file, and **Edit**.

        ![sccm-working-dir.png](https://517755450-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FuBmMrMEHkk0xAv8axZos%2Fuploads%2FCwYhH2NAeXQti23an2kF%2Fafd4b9a3efd78a4557db678113e1bc7112f113345b9ddc192dbb690af33e0cf5.png?alt=media\&token=8efdc2a1-956b-4bbf-8da6-65de254de04e)
    3.  Go to the **Programs** tab.

        In the **Installation starts in** field, carefully enter the full path to the Share folder on the SCCM server where the msi and content zip files are and **Apply**. For example, `\\SCCM\Share\MyCortexXDRAgentDeploymentFolder\`

        ![sccm-start-path-highlighted.png](https://517755450-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FuBmMrMEHkk0xAv8axZos%2Fuploads%2Fjt45OIIihxJFzk9AtGZ4%2F597c688c50f08f6a557f0640a8d74465418a765024d1167ac47de8f7fbe13535.png?alt=media\&token=7a955f8c-d0d3-4851-9440-2aadc757f84e)
4. Distribute the application package content.
   1.  To launch the **Distribute Content Wizard** from the SCCM applications list, right-click your application and select **Distribute Content**.

       ![sccm-distribute-content.png](https://517755450-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FuBmMrMEHkk0xAv8axZos%2Fuploads%2FDM7FQLPJLmsssFGyOx9N%2F4f91ae467e2ef71267c1388e11986d3b568e5405503633255ea2335326052be0.png?alt=media\&token=e1db9222-631c-413b-877c-07763e64941f)
   2.  When you **Review selected content**, ensure that the **Detect associated content dependencies and add them to this distribution** option is selected. This ensures that SCCM pulls both the msi and content zip files from the Share folder.

       ![sccm-distribute-content-2.png](https://517755450-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FuBmMrMEHkk0xAv8axZos%2Fuploads%2FBKnZTif8inKsBYDuPTyV%2F0d52233e4cc1bf9e59a1f17954c74030f1ef815e81e95453a6f96048f0a2ee30.png?alt=media\&token=eb1756d0-e43a-4749-94c6-e177b50ec945)
   3. Continue to configure the other settings in this wizard, and when you are done, **Close** the wizard to exit.
5. Proceed to deploy the application package on your endpoints.
   1.  To launch the **Deploy Software Wizard** from the SCCM applications list, right-click your application and select **Deploy**.

       ![sccm-deploy.png](https://517755450-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FuBmMrMEHkk0xAv8axZos%2Fuploads%2FaeUdGKOsdytD6Ly7XyrV%2F648cca03756bb9c062866be15ad057dd05e57f3dbfce1f2ace74950bb411bda4.png?alt=media\&token=0e5a7f3d-a199-40cf-8b5b-b9d3451f2675)
   2.  When you **Specify general information for this deployment**, ensure that the **Automatic distribute content for dependencies** option is selected. This ensures that SCCM pulls both the msi and content zip files from the Share folder.

       ![sccm-deploy-device-collection.png](https://517755450-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FuBmMrMEHkk0xAv8axZos%2Fuploads%2FzPsP78In4wVB33qY0QtB%2F981afb482a3484bbe5d7b20bd15e8a043edb32a59097637a15c8f9d7aa1b0cdf.png?alt=media\&token=43589dbe-0ca1-4642-86f5-aa62020ea68a)
   3.  In **Deployment Settings**, ensure that:

       * **Action** is set to **Install**.
       * **Purpose** is set to **Required**. Otherwise, if it is set to Available, SCCM will only advertise the new Cortex XDR agent application but will not install it on the endpoint.

       ![sccm-deploy-settings.png](https://517755450-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FuBmMrMEHkk0xAv8axZos%2Fuploads%2F1HMpRd91w1owxHqGJaR9%2Fd8e06f943d396d6f603c818b6d1094de2020ece77914cca1b3d6bd4f15275c54.png?alt=media\&token=372940a0-5fde-4257-9fcf-64343ed2e0b0)
6. Continue to configure the other settings in this wizard, and when you are done, **Close** the wizard to exit.

</details>
