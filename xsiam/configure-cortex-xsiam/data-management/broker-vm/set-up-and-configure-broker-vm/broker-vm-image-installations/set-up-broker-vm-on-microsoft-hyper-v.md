---
description: Deploy a Cortex XSIAM Broker VM on Microsoft Hyper-V.
---

# Set up Broker VM on Microsoft Hyper-V

Learn how to set up your Cortex XSIAM Broker virtual machine (VM) on Microsoft Hyper-V.

To set up a Broker virtual machine (VM) image on Microsoft Hyper-V, you need to download a Cortex XSIAM Broker VM VHD image, and then upload it to your newly created Microsoft Hyper-V VM. Microsoft Hyper-V 2012 or later is supported.

{% hint style="info" %}
#### Prerequisite

Download a Cortex XSIAM Broker VM VHD image. For more information, see the virtual machine compatibility requirements in [Set up and configure Broker VM](..).
{% endhint %}

Perform the following procedures in the order listed below.

{% stepper %}
{% step %}
#### Task 1. Create a new VM in the Hyper-V Manager and upload the VHD image

1. In the Hyper-V Manager, select New → Virtual Machine to open the New Virtual Machine Wizard.
2. In the Specify Name and Location screen, specify a Name for your VM, and click Next.
3. In the Specify Generation screen, select Generation 1, and click Next.
4. In the Assign Memory screen, set the Startup memory to 8192 MB, and click Next.
5. In the Configuring Networking screen, select the network adapter for the Connection, and click Next.
6. In the Connect Virtual Hard Disk screen, select Use an existing virtual hard disk, Browse to the downloaded VHD image file, and click Next.
7. In the Completing the New Virtual Machine Wizard screen, click Finish.
{% endstep %}

{% step %}
#### Task 2. Start the VM that you created for Microsoft Hyper-V

1. From the Virtual Machines list, right-click the VM that you created, and select Start.
2. When the State of the VM updates to Running, right-click the VM, and select Connect. The Broker VM console now displays.
{% endstep %}
{% endstepper %}
