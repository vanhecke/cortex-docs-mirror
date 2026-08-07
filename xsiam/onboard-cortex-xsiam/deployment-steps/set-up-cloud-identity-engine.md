---
description: Learn how to set up Cloud Identity Engine to use with Cortex XSIAM.
---

# Set up Cloud Identity Engine

The Cloud Identity Engine provides both user identification and user authentication for a centralized cloud-based solution in on-premise, cloud-based, or hybrid network environments. The Cloud Identity Engine allows you to write security policy based on users and groups, not IP addresses, and helps secure your assets by enforcing behavior-based security actions. It also provides the flexibility to adapt to changing security needs and users by making it simpler to configure an identity source or provider in a single unified source of user identity, allowing scalability as needs change. By continually syncing the information from your directories, whether they are on-premise, cloud-based, or hybrid, ensures that your user information is accurate and up to date and policy enforcement continues based on the mappings even if the cloud identity provider is temporarily unavailable.

To provide user, group, and computer information for policy or event context, Palo Alto Networks cloud-based applications and services need access to your directory information. The Cloud Identity Engine, a secure cloud-based infrastructure, provides Palo Alto Networks apps and services with read-only access to your directory information for user visibility and policy enforcement. The components of the Cloud Identity Engine deployment vary based on whether the Cloud Identity Engine is accessing an on-premises directory (such as Active Directory) or a cloud-based directory (such as Microsoft Entra ID).

The authentication component of the Cloud Identity Engine allows you to configure a profile for a SAML 2.0-based identity provider (IdP) that authenticates users by redirecting their access requests through the IdP before granting access. You can also configure a client certificate for user authentication. When you configure an Authentication policy and the Authentication Portal on the Palo Alto Networks firewall, users must log in with their credentials before they can access the resource.

**Guidelines for using Cloud Identity Engine with Cortex XSIAM**

Keep in mind the following guidelines:

* Cloud Identity Engine is an optional service.
* Cloud Identity Engine must be activated in the same region as Cortex XSIAM.
* You can use Active Directory information in policy configuration and endpoint management.
* Cortex XSIAM supports on-premises Active Directory and Microsoft Entra.
* You can use XQL Query to query the data using the `pan_dss_raw` dataset.

<details>

<summary>Activate Cloud Identity Engine</summary>

Activating a Cloud Identity Engine instance on your Cortex XSIAM account will allow you to pair your Cortex XSIAM tenant with the Active Directory information collected by the Cloud Identity Engine instance.

</details>

<details>

<summary>Configure Cortex XSIAM with Cloud Identity Engine</summary>

After you complete the activation steps, wait about ten minutes and do the following:

1. Log in to Cortex XSIAM.
2. Select **Settings** → **Configuration** → **Integrations** → **Cloud Identity Engine**.
3. In the **Add Cloud Identity Engine** dialog box, select the instance name and click **Save**.

</details>

<details>

<summary>Risk sharing between Cortex XSIAM and the Cloud Identity Engine</summary>

Integrate Cortex XSIAM with the Cloud Identity Engine (CIE) to enable dynamic user grouping and access control based on real-time risk assessments. This integration leverages historical events and alerts from Cortex XSIAM to continuously evaluate user and host risk, synchronizing the insights with CIE to support adaptive policy enforcement. When an Okta tenant with an Identity Threat Protection (ITP) license is available, CIE can be connected to Okta to create and apply adaptive policies directly within the Okta environment, based on Cortex Risky users sharing, ensuring responsive and risk-based identity management.

Before you activate the integration, you must complete the onboarding in the Cloud Identity Engine.

1. Configure Cortex XSIAM with Cloud Identity Engine.
2. In the Cloud Identity Engine, onboard the relevant directories, Active Directory, Entra ID, or Okta.
3.  In Cortex XSIAM, go to **Settings** → **Configuration** → **Integrations** → **Cloud Identity Engine** and select **Activate risk signal sharing to CIE**.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>The <strong>Activate risk signal sharing to CIE</strong> checkbox is available only after the second step is completed.</p></div>

</details>
