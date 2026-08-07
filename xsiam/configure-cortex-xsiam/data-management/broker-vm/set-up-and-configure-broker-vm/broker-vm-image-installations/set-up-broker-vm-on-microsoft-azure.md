# Set up Broker VM on Microsoft Azure

Learn how to set up your Cortex XSIAM Broker virtual machine (VM) on Microsoft Azure.

After you download your Cortex XSIAM Broker VHD (Azure) image, you need to upload it to Azure as a storage blob.

{% hint style="info" %}
#### Prerequisite

Download a Cortex XSIAM Broker VM VHD (Azure) image. For more information, see the virtual machine compatibility requirements in [Set up and configure Broker VM](..).
{% endhint %}

Perform the following procedures in the order listed below.

#### Task 1. Extract the downloaded VHD (Azure) image

Make sure you extract the zipped hard disk file on a server that has more then 512 GB of free space.

{% hint style="info" %}
#### Note

Extraction can take up to a few hours.
{% endhint %}

#### Task 2. Create a new storage blob on your Azure account by uploading the VHD file

Upload from Microsoft Windows or Ubuntu.

{% tabs %}
{% tab title="Windows" %}
1. Verify you have:
   * Windows PowerShell version 5.1 or later.
   * .NET Framework 4.7.2 or later.
2.  Open PowerShell and run:

    ```powershell
    Set-ExecutionPolicy unrestricted
    [Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
    Install-PackageProvider -Name NuGet -MinimumVersion 2.8.5.201-Force
    ```
3.  Install `azure cmdlets`.

    ```powershell
    Install-Module -Name Az -AllowClobber
    ```
4.  Connect to your Azure account.

    ```powershell
    Connect-AzAccount
    ```
5. Start the upload.
   *   For Azure PowerShell:

       ```powershell
       Set-AzStorageBlobContent -Container $containerName -File $localFilePath -Context $storageContext -BlobType Page
       ```
   *   For Azure CLI:

       ```bash
       az storage blob upload -f -n -c --account-name
       ```

{% hint style="info" %}
#### Note

Upload can take up to a few hours.
{% endhint %}
{% endtab %}

{% tab title="Linux" %}
1.  Install Azure util. There are two different ways to install the Azure util.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h4>Note</h4><p>For more information, see the <a href="https://learn.microsoft.com/en-us/cli/azure/install-azure-cli-linux?view=azure-cli-latest&#x26;pivots=apt">Azure Documentation</a>.</p></div>

    *   Option 1:

        ```bash
        curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash
        ```
    * Option 2:
      1.  Get the packages needed for the installation process:

          ```bash
          sudo apt-get update
          sudo apt-get install apt-transport-https ca-certificates curl gnupg lsb-release
          ```
      2.  Download and install the Microsoft signing key:

          ```bash
          sudo mkdir -p /etc/apt/keyrings
          curl -sLS https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor | sudo tee /etc/apt/keyrings/microsoft.gpg > /dev/null
          sudo chmod go+r /etc/apt/keyrings/microsoft.gpg
          ```
      3.  Add the Azure CLI software repository:

          ```bash
          AZ_DIST=$(lsb_release -cs)
          echo "Types: deb URIs: https://packages.microsoft.com/repos/azure-cli/ Suites: ${AZ_DIST} Components: main Architectures: $(dpkg --print-architecture) Signed-by: /etc/apt/keyrings/microsoft.gpg" | sudo tee /etc/apt/sources.list.d/azure-cli.sources
          ```
      4.  Update repository information and install the `azure-cli` package:

          ```bash
          sudo apt-get update
          sudo apt-get install azure-cli
          ```
2.  Connect to Azure.

    ```bash
    az login
    ```
3.  Start the upload.

    ```bash
    az storage blob upload -f <vhd to upload> -n <vhd name> -c <container name> --account-name <account name>
    ```
{% endtab %}
{% endtabs %}

#### Task 3. Add and configure a new disk in Azure

1. In the Azure home page, navigate to Azure services → Disks and Add a new disk.
2.  Navigate to the Create a managed disk → Basics page, and define the following information:

    | Heading         | Parameter                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
    | --------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | Project details | Resource group: Select your resource group.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
    | Disk details    | <p>Disk name: Enter a name for the disk object.<br><br>Region: Select your preferred region.<br><br>Source type: Select <strong><code>Storage Blob</code></strong>.<br><br>Additional fields are displayed, which you can define as follows:</p><ul><li><p>Source blob:</p><ul><li>Select Browse. You are directed to the Storage accounts page.</li><li>From the navigation panel, select the bucket and then container to which you uploaded the Cortex XSIAM VHD image.</li><li>In the Container page, Select your VHD image.</li></ul></li><li>OS type: Select Linux</li><li>VM generation: Select Gen 1</li></ul> |
3. Check you settings by clicking Review + create.

#### Task 4. Create the Broker VM disk

1. Create your Broker VM disk, and after deployment is complete, click Go to resource.
2. In your created Disks page, click Create VM.
3.  In the Create a virtual machine page, define the following:

    | Heading           | Parameter                                                                                                                                                                                                                                                                                     |
    | ----------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | Instance details  | <p>(Optional) Virtual machine name: Enter the same name as the disk name you defined.<br><br>Size: Select the size according to your company guidelines. Select Next to navigate to the Networking tab.</p>                                                                                   |
    | Network interface | <p>NIC network security group: Select Advanced.<br><br>Configure network security group: Select HTTPS to be able to access the Broker VM Web UI, and SSH to allow for remote access when troubleshooting. Make sure to allow these connection to the Broker VM from secure networks only.</p> |
4. To check your settings, click Review + create.
5. Create your VM. After deployment is complete, click Go to resource. You are directed to your VM page.

{% hint style="info" %}
#### Note

Creating the VM can take up to 15 minutes. The Broker VM Web UI is not accessible during this time.
{% endhint %}

6.  Ensure that the VM you created contains an Outbound port rule that allows the broker to reach the Azure Instance Metadata Service using the IP address `169.254.169.254` and port `80`. For more information about the Azure Instance Metadata Service, see the [Azure Documentation](https://learn.microsoft.com/en-us/azure/virtual-machines/instance-metadata-service?tabs=windows). To configure an outbound rule on your VM, select Networking → Network settings, and under the Rules → Outbound port rules section, you can either:

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h4>Note</h4><p>For more information on creating a rule in an Azure VM, see <a href="https://learn.microsoft.com/en-us/azure/virtual-network/manage-network-security-group?tabs=network-security-group-portal#create-a-security-rule">Create a Security Rule</a> in the Azure Documentation.</p></div>

    * Configure a new outbound port rule by selecting Create port rule → Outbound port rule and setting the following settings in the Add outbound security rule dialog box:
      * Destination: Select IP Addresses.
      * Destination IP addresses/CIDR ranges: Enter the IP address as `169.254.169.254`.
      * Destination port ranges: Enter the port as `80`.
      * Protocol: Select TCP.
      * Name: Enter a unique name for this new outbound port rule, such as AzureInstanceMetadataService. Click Add to create the new outbound port rule.
    * Edit an existing outbound port rule and ensure that the settings provided above for creating a new outbound port rule match what is already configured in the rule.
