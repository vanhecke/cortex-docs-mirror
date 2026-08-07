# Bring your own keys

### What is Cortex BYOK?

Cortex self-managed BYOK (bring your own keys) offers a comprehensive data encryption solution, empowering enterprises to assert complete authority over their encryption key management, while ensuring platform reliability, availability, and responsiveness. It enables you to securely import and manage your own encryption keys via Cortex Gateway. This provides you with enhanced control over your tenant data encryption and accessibility, eliminates reliance on default CSP encryption or third-party key management, and enables you to comply with stringent regulatory requirements.

Unlike self-hosted solutions, Cortex BYOK minimizes exposure to external risks, such as downtime, breaches, or operational disruptions, by reducing dependency on external environments, ensuring availability and responsiveness of your Cortex products.

By default, Google Cloud encrypts customer data at rest using envelope encryption, where randomly generated Data Encryption Keys (DEKs) encrypt the data, and Google-managed Key Encryption Keys (KEKs) wrap the DEKs, all protected within Google's multi-layered key hierarchy. Cortex BYOK enhances this model by allowing customers to generate and supply their own KEK, which is securely imported into PANW's tenant-specific Key Management Service (KMS) environment on Google Cloud. The customer-provided KEK is used to encrypt the DEKs that protect tenant data, giving customers control over key management through the Cortex Gateway. While PANW securely manages encryption operations within its cloud environment, customers retain authority over the KEK, achieving greater control and auditability.

### Cortex BYOK architecture

Cortex BYOK leverages a dedicated Key Management Service (KMS) deployed per tenant within PANW's GCP-based infrastructure. Each tenant has its own isolated KMS instance, ensuring complete separation of key material.

In multitenant environments, each tenant has its own isolated KMS instance and keys, and each one is managed independently.

Two separate keys are used for encrypting tenant data: one for the Data lake BigQuery and another for other services.

### Security measures

Cortex BYOK ensures key material is wrapped for protection in transit, and access to the wrapping key is limited solely to the scope of the import job.

The key material is unwrapped solely within the tenant’s KMS using the import job's private key and is inserted as a new version of the target key on the target key ring through an atomic operation. This ensures that no key material is left exposed or in an untrusted state, keeping it secure and preventing potential vulnerabilities, while maintaining its integrity and consistency.

Cortex also provides detailed audit logs within the tenant on all key management operations.

Email notifications are sent for any key management operations, allowing tenant administrators to monitor and review all activities and detect and mitigate any unauthorized access attempts.

### BYOK key management operations

BYOK supports the following key management operations. Cortex XSIAM provides detailed audit logs and email notifications on all key management operations.

<details>

<summary>Set up new tenant with BYOK</summary>

Generate your own encryption keys and import them via Cortex Gateway to retain greater control over your tenant data and encryption. This control enables you to implement customized security measures tailored to your organization’s needs and compliance requirements for encrypting your tenant data at rest.

Cortex BYOK uses two keys for encrypting your tenant data at rest: one for the Data lake BigQuery and another for all other tenant services. You can generate a single key for both or create two separate keys.

*   If you're doing the activation for the first time, in the Cortex Gateway, follow the Tenant Activation wizard. In **Tenant Activation → Define Tenant Settings**, under **Advanced**, select **BYOK (Bring Your Own Keys)** and click **Create Tenant and Set Up Keys**.

    The tenant is now initialized, which may take a few minutes. You can set up your keys now, or return at a later stage and click **Set Up Encryption Keys** next to the tenant in the gateway to continue the process.
* If you've already started the activation process and paused, locate your tenant in the Available Tenants list in the Cortex gateway, click **Set Up Encryption Keys** next to your tenant and set up your keys.

</details>

<details>

<summary>Rotate encryption keys</summary>

To rotate your encryption keys, in the Cortex gateway, open the more options menu next to the tenant, select **Rotate Encryption Key**, and follow the Bring your own keys (BYOK) setup.

To resume the process, in the main gateway, open the more menu next to the tenant, select **Continue Rotation**, and follow the Bring your own keys (BYOK) setup.

As long as the rotation hasn't been completed, you can cancel the rotation process from the three dot menu next to the tenant.

{% hint style="success" %}
**NOTE:**

The new keys you import will serve as primary encryption keys for newly generated data.
{% endhint %}

{% hint style="success" %}
**NOTE:**

For BYOK key rotation, you can select your preferred key import method, replacing the previously fixed default RSA\_OAEP\_3072\_SHA256.

The new recommended default is RSA\_OAEP\_3072\_SHA256\_AES\_256. To use the previous default method, select it manually.
{% endhint %}

</details>

<details>

<summary>Disable encryption keys</summary>

To disable your encryption keys, in the main gateway, open the three dot menu next to the tenant, select **Disable All Keys & Deactivate Tenant**.

{% hint style="info" %}
**PREREQUISITE:**

To disable your encryption keys and deactivate a tenant, you must have an Account Admin role.
{% endhint %}

{% hint style="warning" %}
**CAUTION:**

Disabling all encryption keys and deactivating the tenant renders the tenant inaccessible and non-operational.

Disabling the keys affects the communication with the agents, may prevent the agents from receiving updates to policies, configurations, and crucial information, and may result in loss of data.

To secure your tenant data and to prevent unauthorized access, re-enabling the keys and re-activating the tenant are strictly controlled and require manual intervention by the Cortex XSIAM Customer Success team.
{% endhint %}

</details>

To import a new encryption key, whether for initial tenant setup or key rotation, use the Bring your own keys (BYOK) setup.

### Bring your own keys (BYOK) setup

Cortex BYOK uses two keys for encrypting your data at rest. One key is for the Data lake and the other is for all the other services within the tenant. You can generate a single key for both or create two separate keys for each service.

You can select your preferred key wrapping algorithm to meet regulatory or compliance requirements.

After completing the process, the imported keys become the primary keys used for encrypting any newly generated data stored within the tenant.

Import new keys for encrypting your tenant data at rest:

1.  The **Generate Key** screen helps you generate an encryption key.

    Generate a key that meets these requirements using your preferred method or use the provided OpenSSL command:

    When your encryption key is ready, select **I have a 32-byte symmetric encryption key ready** and click **Next**.
2. In the **Wrap & Upload** screen, repeat the following procedure for both **Data lake wrapping key** and **Services wrapping key**.
   1.  Select your import method and download the wrapping key. You can only select your import method the first time you download your key.

       Available import methods are:

       * RSA\_OAEP\_3072\_SHA256\_AES\_256 (default)
       * RSA\_OAEP\_4096\_SHA256\_AES\_256
       * RSA\_OAEP\_3072\_SHA256
       * RSA\_OAEP\_4096\_SHA256

       The wrapping key is valid for up to three days. After three days, you need to download a new wrapping key.
   2. Use an OpenSSL editor to wrap your encryption key using the following procedure:
      *   For RSA\_OAEP\_3072\_SHA256 and RSA\_OAEP\_4096\_SHA256:

          Wrap the target key using the wrapping public key:<br>

          ```
          openssl pkeyutl \  
          -encrypt \  
          -pubin \  
          -inkey <full path to the public wrapping key file that ends with .pem> \  
          -in <full path to your target encryption key> \  
          -out  <full path where you want to save the wrapped target key that is ready for import> \  
          -pkeyopt rsa_padding_mode:oaep \  
          -pkeyopt rsa_oaep_md:sha256 \  
          -pkeyopt rsa_mgf1_md:sha256
          ```
      * For RSA\_OAEP\_3072\_SHA256\_AES\_256 and RSA\_OAEP\_4096\_SHA256\_AES\_256:
        1. Patch and recompile OpenSSL. For more details, see [Configuring Open SSL for manual key wrapping](https://docs.cloud.google.com/kms/docs/configuring-openssl-for-manual-key-wrapping).
        2.  Generate a temporary random AES key:<br>

            ```
            openssl rand 32 > <full path where you want to save the temporary AES key>
            ```
        3.  Wrap the temporary AES key with the wrapping public key:<br>

            ```
            openssl pkeyutl \  
            -encrypt \  
            -pubin \  
            -inkey  <full path to the public wrapping key file that ends with .pem>  \  
            -in <full path to your temporary AES key> \ 
            -out <full path where you want to save the wrapped key> \  
            -pkeyopt rsa_padding_mode:oaep \  
            -pkeyopt rsa_oaep_md:sha256 \  
            -pkeyopt rsa_mgf1_md:sha256
            ```
        4.  Wrap the target key with the temporary AES key and append it to the wrapped key:<br>

            ```
            "<full path to your patched and recompiled (OpenSSL) openssl.sh script>" enc \  
            -id-aes256-wrap-pad \  
            -iv A65959A6 \  
            -K $( hexdump -v -e '/1 "%02x"' < "<full path to your temporary AES key> " ) \  
            -in "<full path to your target encryption key>" >> " <full path to the wrapped key that is now ready for import>"
            ```
   3. Upload the wrapped key and click **Complete Activation**.
