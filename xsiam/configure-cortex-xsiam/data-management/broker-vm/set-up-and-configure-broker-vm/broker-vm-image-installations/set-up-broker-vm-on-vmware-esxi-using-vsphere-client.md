---
description: Deploy a Cortex XSIAM Broker VM on VMware ESXi.
---

# Set up Broker VM on VMware ESXi using vSphere Client

Learn more about how to set up you Cortex XSIAM Broker VM on VMware ESXi.

To set up the Broker VM on VMware ESXi, you deploy the OVA image provided in Cortex XSIAM. VMware ESXi 6.5 or later is supported. The instructions below provide an example of doing this using vSphere Client 7.0.3.01400.

{% hint style="info" %}
#### Prerequisite

* Ensure you have a virtualization platform installed that is compatible with an OVA image, and have an authenticated user account.
* Download a Cortex XSIAM Broker VM OVA image. For more information, see the virtual machine compatibility requirements in [Set up and configure Broker VM](..).
{% endhint %}

{% stepper %}
{% step %}
### Deploy the Broker VM OVA image on vSphere Client

1. From vSphere Client, right-click an inventory object for the virtual machine of your broker, and select Deploy OVF Template.
2. In the Select an OVF template page of the wizard, select Local file, click UPLOAD FILES to select the OVA image file that you downloaded, and click NEXT.
3. In the Select a name and folder page, enter a unique name for the virtual machine, select a deployment location, and click NEXT.
4. In the Select a compute resource page, select a resource where to run the deployed VM template, and click NEXT.
5. In the Review details page, verify the OVA template details, and click NEXT.
6. In the Select storage page, define where and how to store the files for the deployed OVA template, and click NEXT. For more information on the options available, see the [VMware vSphere documentation](https://docs.vmware.com/en/VMware-vSphere/7.0/com.vmware.vsphere.vm_admin.doc/GUID-17BEDA21-43F6-41F4-8FB2-E01D275FE9B4.html).
7. In the Select networks page, select a source network and map it to a destination network, and click NEXT. The Source Network column lists all networks that are defined in the OVA template.
8. In the Ready to complete page, review the details and click FINISH. A new task for creating the virtual machine is displayed in the Recent Tasks pane. When the Status of the task reaches 100%, the task is complete, and the new virtual machine is created on the selected resource.
9. Navigate to the resource where the new virual machine is created, right-click the resource, and select Power → Power On.
{% endstep %}
{% endstepper %}
