# Change the Docker image in an integration or script

Docker enables you to run scripts and integrations from an image in a controlled environment that isolates and safeguards the tenant. It also simplifies environment setup by packaging dependencies and configurations within an image, ensuring consistent execution across different systems. By default, Cortex XSIAM pulls images from the `Demisto` Docker image registry in GitHub, which are used in scripts and integrations as needed. Cortex XSIAM integrations and scripts have the relevant Docker image already selected. For example, the Rasterize integration uses the `demisto/python.3.3.11.9.1079` Docker image.

You may want to select a different Docker image for your integration or script. In Cortex XSIAM, you can select a different Docker image from a dropdown that is pulled from the `Demisto` Docker image registry. In GitHub, the [dockerfiles-info branch](https://github.com/demisto/dockerfiles-info/tree/master) contains information about each image to help you find one that is relevant.

{% hint style="info" %}
You can access publicly available Docker images from the Cortex XSIAM tenant even if there is no external connection to the `Demisto` registry, for example, if due to firewall constraints, your engine cannot access the `Demisto` registry.
{% endhint %}

Change the Docker image for a script

1. Edit the script.
2.  Under ADVANCED, in the Docker image name field, click X to clear the current selection and then select a Docker image name from the dropdown menu.

    For more information about changing the Docker image for a script, see the Advanced tab in [Create a script](create-a-script).
3. Save your changes.

Change the Docker image for an integration

1.  Navigate to Settings → Data Sources & Integrations, find and select your integration and edit the integration’s source.

    For an out-of-the-box content pack integration, you first need to duplicate the integration to edit it.
2. In the Integration Settings, expand the Script section.
3.  Click X to clear the current selection and select a Docker image name from the dropdown menu.

    For more information about changing the Docker image, see the Advanced tab in [Create a script](create-a-script).
4. Save your changes.
