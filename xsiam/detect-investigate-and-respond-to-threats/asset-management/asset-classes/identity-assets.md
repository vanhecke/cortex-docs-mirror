# Identity assets

Powered by the Identity Security module, the Identity Asset Inventory helps you discover your entire cloud identity estate. It analyzes your environment to determine exactly what actions identities can take and which resources they can access, providing the context needed to trigger security detection rules.

**Identity categories**

The identity inventory is organized into the following categories:

* **All Identity Assets:** Identities originating from all platforms and sources.
* **Human:** All cloud, identity provider (IdP), and platform users.
* **Non-human:** Machine identities that can assume permissions and perform cloud Identity and Access Management (IAM) actions such as VMs and functions.
* **Groups:** Identity and Access Management groups.
* **Policies:** Permission documents, such as AWS policies, Azure roles, and GCP roles.

For each identity category, you can refine the results using the tabs:

* **All Identities**: Identities originating from all platforms and sources.
* **Cloud Identities**: Identities originating from cloud platforms.
* **SaaS Identities**: Identities originating from SaaS data sources.
*   **On-premises Identities**: Identities managed within your on-premises or enterprise directories.\
    For **Human** identities, the **On-premises Identities** tab includes the **Weak Password** widget to filter the users in your organization who are likely to be targeted because they have a weak password.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>Access to the <strong>Weak Password</strong> widget and column requires the ITDR add-on.</p></div>

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>Once a user updates their password to a strong password, they will no longer appear in the filtered weak password results.</p></div>

**Expanded identity details**

Clicking an identity asset in the inventory opens a detailed asset card that provides deep contextual analysis. Because managing identity security requires understanding how assets interact with one another, the information available on these cards helps map the complex web of relationships and permissions within your environment.

While the specific layout changes depending on whether you are viewing a human identity, a machine identity, or a secret, the asset details generally provide an aggregated view of the permissions associated with the asset. By exploring the identity details, you can understand exactly how an identity is granted its permissions by viewing the groups it belongs to, the cloud service accounts it can impersonate, and any policy attachments or inline policies. You can also review an identity's specific access levels to destination assets, which highlights unused permissions, excessive permissions, and the account access type.
