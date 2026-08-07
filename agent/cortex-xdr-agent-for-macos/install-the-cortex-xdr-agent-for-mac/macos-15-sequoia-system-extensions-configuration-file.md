# macOS 15 Sequoia system extensions configuration file

This flow details how to deploy the Cortex XDR agent on macOS 15 Sequoia endpoints using the Palo Alto Networks system extensions configuration file.

When applying the configuration profile on older OS versions, and then upgrading to macOS 15 Sequoia, some fields may not be propagated properly due to known macOS issue. We recommend creating a smart/dynamic group of machines running macOS 15 Sequoia, and applying this profile only to this group.

1. If this has not been done previously, follow the instructions for installing the unified configuration profile to your MDM tool. [Install with a unified configuration profile for MDMs](install-with-a-unified-configuration-profile-for-mdms)
2. Download the signed or unsigned system extensions configuration profile.
   *   [Download the signed configuration profile ](#signed-configuration-profile)(CortexXDR\_SystemExtensionsSequoia\_V1\_SignedPANW.mobileconfig)

       SHA256: 35796ab146072f9beef9fc0398d567cba23432244ff38268124b16aa000ab148

       MD5: e354fb7dcf7e17fe21982f3974537e61
   *   [Download the unsigned configuration profile ](#unsigned-configuration-profile)(CortexXDR\_SystemExtensionsSequoia\_V1\_UnsignedPANW.mobileconfig)

       SHA256: f852abf35b525bc4eb25ad05b4590980c72ebfc623eeeda958f4e32cabcf9941

       MD5: 66aaf5535d5eba67ef8df9f2bf28980a
3. Create a smart/dynamic group of machines running macOS 15 Sequoia in your organization.
4. Upload/install the profile, and add this smart group to the profile’s targets.

#### Signed configuration profile

{% file src="https://517755450-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FuBmMrMEHkk0xAv8axZos%2Fuploads%2Fqj3Obx94GKt8IrzJstvm%2FCortexXDR_SystemExtensionsSequoia_V1_SignedPANW.mobileconfig.zip?alt=media&token=57e49f6d-05de-4d62-acbf-cc21330c7a7a" %}

#### Unsigned configuration profile

{% file src="https://517755450-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FuBmMrMEHkk0xAv8axZos%2Fuploads%2FgL2rAbm0eODHwQmQoTi2%2FCortexXDR_SystemExtensionsSequoia_V1_Unsigned.mobileconfig.zip?alt=media&token=3c0dd294-8b5b-4fd9-8ad4-397527d35f87" %}
