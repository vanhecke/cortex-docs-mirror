# Set up Broker VM on KVM using Ubuntu

Learn set up your Cortex XSIAM Broker virtual machine (VM) on a KVM using Ubuntu.

After you download your Cortex XSIAM Broker virtual machine (VM) QCOW2 image, you need to upload it to a kernel-based Virtual Machine (KVM). The instructions below provide an example of doing this on the latest Ubuntu.

{% hint style="info" %}
#### Prerequisite

Download a Cortex XSIAM Broker VM QCOW2 image. For more information, see the virtual machine compatibility requirements in [Set up and configure Broker VM](..).
{% endhint %}

1. Open KVM on Ubuntu.
2. Click the **New VM** icon.
3. Complete the new virtual machine wizard:
   1. In **Step 1**, select **Import existing disk image**. Click **Forward**.
   2. In **Step 2**, configure the storage:
      * Browse to the downloaded QCOW2 image.
      * Click **Browse Local**, select the image, then click **Open**.
      * Leave **OS type** and **Version** set to **Generic**.
      * Click **Forward**.
   3. In **Step 3**, specify these resources:
      * **Memory (RAM):** `8192` MB (8 GB)
      * **CPUs:** `4`
      * Click **Forward**.
   4. In **Step 4**, enter a name for the VM.
4. Click **Finish**. The VM is listed and ready to use.
