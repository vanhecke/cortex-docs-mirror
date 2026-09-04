---
description: Retrieve the Cortex XSIAM support file password for endpoint troubleshooting.
---

# Retrieve support file password

The Cortex XDR agent generates the Tech Support File (TSF) as a password-protected zip archive. The TSF is packaged inside an outer archive that also contains a metadata file with the encrypted token used to retrieve the password. Follow the steps below to retrieve the password and unzip the file.

The TSF is generated in either of two ways:

* **Remotely from Cortex XSIAM -** The **Retrieve Support File** action is initiated from the **Action Center** or from an endpoint's page. The resulting archive is downloaded from the Action Center.
* **Locally from the endpoint** - The `cytool log collect` command is run on the endpoint's command line. The resulting archive is saved on the endpoint's local filesystem.

{% stepper %}
{% step %}
### Locate the token

Find the encrypted token inside the archive.

1. Open the outer archive that contains the TSF. This is either the file you downloaded from the **Action Center** or the file saved locally on the endpoint.
2. Locate and open the metadata file (typically named `_CRYPTO-INFO`).
3. Copy the encrypted token string it contains.
{% endstep %}

{% step %}
### Retrieve the TSF file password

The next steps depend on how the TSF was generated.&#x20;

<details>

<summary>From the Action Center</summary>

Follow these steps if the TSF was downloaded from the **Action Center**.

1. Go to **Action Center** → **All Actions**.
2. Locate your **Support File Retrieval** action.
3. Right-click the action and select **Retrieve Support File Password**.
4. In the **Retrieve Support File Password** dialog box, in the **Encrypted Password** field, paste the token that you copied in Step 1.
5. Click the copy button to copy the displayed password and then click **Ok**. Use the password to unzip the TSF file.

</details>

<details>

<summary>From the endpoint</summary>

Follow these steps if the TSF was collected locally by running the `cytool log collect` command on the endpoint's command line.&#x20;

1. Go to **Inventory** → **Endpoints** → **All Endpoints**.
2. At the top of the page, click the key icon <img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-e6a03305250c113a69f127e31e02e2d623fdac04%2F48eece5124cdca27f9a7a4ee50ae57b15cd6e3a3e056df865cf847c10efd7ae9.png?alt=media" alt="Screenshot_2025-08-04_at_15_40_52.png" data-size="line"> (**Tokens and Passwords**) and select **Retrieve Support File Password**.
3. In the **Retrieve Support File Password** dialog box, in the **Encrypted Password** field, paste the token that you copied in Step 1.
4. Click the copy button to copy the password displayed and then click **Ok**. Use the password to unzip the TSF file.

</details>
{% endstep %}
{% endstepper %}
