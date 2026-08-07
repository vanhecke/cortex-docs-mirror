# Set up Broker VM on Alibaba Cloud

Learn how to set up your Cortex XSIAM Broker virtual machine (VM) on Alibaba Cloud.

After you download your Cortex XSIAM Broker virtual machine (VM) QCOW2 image, you need to upload it to Alibaba Cloud. Since the image file is larger than 5G, you need to download the `ossutil` utility file provided by Alibaba Cloud to upload the image.

{% hint style="info" %}
#### Prerequisite

Download a Cortex XSIAM Broker VM QCOW2 image. For more information, see the virtual machine compatibility requirements in [Set up and configure Broker VM](..).
{% endhint %}

Perform the following procedures in the order listed below.

{% stepper %}
{% step %}
#### Task 1. Download the `ossutil` utility file provided by Alibaba Cloud

The download is dependent on the operating system and infrastructure you are using.

* Alibaba Cloud supports using the following operating systems for the utility file: Windows, Linux, and macOS.
* Supported architectures: x86 (32-bit and 64-bit) and ARM (32-bit and 64-bit)

For more information on downloading the utility, see the [Alibaba Cloud documentation](https://www.alibabacloud.com/help/doc-detail/120075.htm?spm=a2c63.p38356.879954.4.4a3265d0RjYjwJ#concept-303829).
{% endstep %}

{% step %}
#### Task 2. Upload the image file to Alibaba Cloud using the utility file you downloaded

The command is dependent on the operating system and architecture you are using. Below are a few examples of the commands to use based on the different operating systems and architectures, which you may need to modify based on your system requirements.

{% tabs %}
{% tab title="Linux (using CLI)" %}
```
Format ./ossutil64 cp Downloads/ oss:///
Example ./ossutil64 cp Downloads/QCOW2_broker-vm-14.0.1.qcow2 oss://kvm-images-qcow2/Cortex XSIAM -broker-vm-14.0.1.qcow2
```
{% endtab %}

{% tab title="macOS (using CLI)" %}
```
Format ./ossutilmac64 cp Downloads/<name of Broker VM QCOW2 image oss:///
Example ./ossutilmac64 cp Downloads/QCOW2_broker-vm-14.0.1.qcow2 oss://kvm-images-qcow2/Cortex XSIAM -broker-vm-14.0.1.qcow2
```
{% endtab %}

{% tab title="Windows (using CMD)" %}
```
Format for 64-bit D:\ossutil>ossutil64.exe cp Downloads\<name of Broker VM QCOW2 image> oss:///
Example for 64-bit D:\ossutil>ossutil64.exe cp Downloads\QCOW2_broker-vm-14.0.1.qcow2 oss://kvm-images-qcow2/Cortex XSIAM -broker-vm-14.0.1.qcow2
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
#### Note

For Linux and Windows uploads, you can use Alibaba Cloud’s graphical management tool called [ossbrowser](https://partners-intl.aliyun.com/help/doc-detail/209974.htm?spm=a2c63.p38356.b99.270.7ae22454encexz).
{% endhint %}
{% endstep %}

{% step %}
#### Task 3. Create the image file in the Alibaba Cloud format

1. Open the [Alibaba Cloud console](https://homenew-intl.console.aliyun.com/).
2. Select Hamburger menu → Object Storage Service → , where the is the directory you configured when uploading the image. For example, in the step above the used in the examples provided is kvm-images-qcow2.

{% hint style="info" %}
#### Note

The Object Storage Service must be created in the same Region as the image of the virtual machine.
{% endhint %}

3. From the list of images displayed, find the row for the Broker VM QCOW2 image that you uploaded, and click View Details.
4. In the URL field of the View Details right-pane displayed, copy the internal link for the image in Alibaba cloud. The URL that you copy ends with .com and you should not include any of the text displayed after this.
5. Select Hamburger menu → Elastic Compute Service → Instances & Images → Images.
6. In the Import Images area on the Images page, click Import Images.
7. In the Import Images window, set the following parameters:
   * OSS Object Address: This field is a combination of the internal link that you copied for the Broker VM image and the file name for the uploaded image, using this format /. Paste the internal link for the Broker VM QCOW2 image in Alibaba Cloud that you copied, and add the following text after the .com: /.
   * Image Name: Specify a name for the image.
   * Operating System/Platform: Leave Linux configured and change CentOS to Ubuntu.
   * System Architecture: Leave the default x86\_64 selected.
   * Leave the rest of the fields as defined by the default or change them according to your system requirements.
8. Click OK. A notification is displayed indicating that image was imported successfully. Once the Status for the imported image in the Images page changes to Available, you will know the process is complete. This can take a few minutes.
{% endstep %}

{% step %}
#### Task 4. Create a new VM in Alibaba Cloud

1. Select Hamburger menu → Elastic Compute Service → Instances & Images → Instances.
2. Create Instance to open a wizard to define the VM machine.
3. Define the Basic Configurations screen by setting these parameters:
   * Billing Method: Select the applicable billing method according to your system requirements.
   * Region: Ensure the Region selected is the same as the OSS Object Address.
   * Instance Type: Set these settings according to your system requirements.
   * Selected Instance Type Quantity: Set these settings according to your system requirements.
   * Image: Select Custom Image, and in the field select the image that you imported to Alibaba Cloud.
   * Storage (Optional): Set these settings according to your system requirements.
   * Snapshot (Optional): Set these settings according to your system requirements.
4. Click Next.
5. Define the Networking screen by setting these parameters:
   * Network Type: Select the applicable Network Type and update the field according to your system configuration.
   * Public IP Address (Optional): Enable the instance to access the public network.
   * Security Group: You must select a Security Group for setting network access controls for the instance. Ensure that port 22 and port 443 are allowed in the security group rules to access the Broker VM.
   * Elastic Network Interface (Optional): Add an ENI according to you system requirements.
6. Click Next.
7. Define the System Configurations screen by setting these parameters:
   * Logon Credentials: Select Inherit Password From Image.
   * Instance Name: You can either leave the default instance name or specify a new name for the VM instance.
   * Description (Optional): Specify a description for the VM instance.
   * The rest of the fields are optional to configure.
8. Click Next.
9. (Optional) Define the Grouping screen according to your system requirements.
10. Click Next.
11. Review the Preview screen settings, select ECS Terms of Service and Product Terms of Service, and click Create Instance. A dialog box is displayed indicating that the VM instance has been created. Click Console to bring you back to the Instances page, where you can see the IP Address listed to connect to the VM instance.
{% endstep %}

{% step %}
#### Task 5. Reboot the Broker VM

Reboot the Broker VM before logging in for the first time.
{% endstep %}
{% endstepper %}
