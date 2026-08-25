---
description: Configure Cloud Identity Security settings in Cortex XSIAM.
---

# Configure Cloud Identity Security

{% hint style="info" %}
Requires a Cloud Posture Security, Cloud Runtime Security, or Cortex XSIAM Premium license.
{% endhint %}

You can configure how you want Cloud Identity Security to behave across your identities.

## Trusted domains

Users may be sharing data across SaaS, Cloud, and on-premises environments externally. In order to highlight untrusted data sharing, this feature allows you to define which domains your organization trusts.

When non-internal identities are discovered, Cloud Identity Security flags them as **External**, and their domain is checked against your configuration as follows:

* **Match found:** The asset is designated as **Trusted**.
* **No match found:** The asset is designated as **Untrusted**.

#### Required roles

* **Identity Security Administrator:** Can view and manage trusted domains.
* **Identity Security Reader:** Can view trusted domains.

### Manage domains

#### **View existing domains**

To see all the existing domains, do the following:

1. Click **Settings** > **Configurations**.
2. Open **Identity Configuration**.\
   The **Allowed Domains** list is displayed.

#### **Add a domain**

To add a domain to the **Trusted Domains** list, do the following:

1. Click **Settings > Configurations > Identity Configuration**.
2. On the **Trusted Domains** screen, click **Add Domain**.
3. In the **Add Domain** dialog box, enter a domain that you want to designate as trusted, for example [domain.com](http://domain.com), and click **Add**.

{% hint style="info" %}
**Note**

To successfully add a domain to your trusted domains list, it must meet the following criteria:

* **Valid format:** The domain must contain at least one period (.), cannot contain spaces or empty sections, and must end with a valid top-level domain, such as `.com` or `.org`.
* **No duplicates:** Cloud Identity Security does not support duplicate domain entries.
* **Limits:** You can configure a maximum of 1,000 domains per tenant.
{% endhint %}

4. The domain you added now appears in the **Trusted Domains** list.

#### **Delete or edit a domain**

If you want to delete or edit a domain, do the following:

1. Click **Settings** > **Configurations** > **Identity Configuration**.
2. On the **Trusted Domains** screen, click the More menu (three dots) for the domain you want to delete or edit, and select either **Delete** or **Edit**.
