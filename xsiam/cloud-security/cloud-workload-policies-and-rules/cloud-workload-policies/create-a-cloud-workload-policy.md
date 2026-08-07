# Create a cloud workload policy

You can create policies to address specific types of security risks or compliance requirements.

To create a cloud workload policy:

Navigate to **Posture Management** → **Rules & Policies** → **Policies** → **Cloud Workload**.

In the **Cloud Workload Policy** page, click **Create Policy** and select the type of policy you want to create:

{% tabs %}
{% tab title="Misconfiguration Policy" %}
1. Enter a unique name and description. Note that these are mandatory fields.
2.  The **Evaluation Stage** will be selected as **Runtime**.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>The Evaluation stage for Misconfiguration policies is supported only in the Runtime SDLC stage and is enforceable through the Kubernetes Admission Controller for clusters onboarded using the Posture Management (KSPM) Connector.</p></div>
3. Click **Next**
4. The **Summary** section on the right displays a real-time, interactive view of all policy configurations as users progress through the wizard. It **automatically updates** to reflect the current selections and settings, enabling seamless navigation between fields from any step in the wizard. It includes the following sections:
   * **General** – Policy name and description.
   * **Rules** – No. of selected rules and the asset types relevant to the selected rules.
   * **Scope** - The defined scopes included in the policy and SDLC stage.
5. In the **Rules** section:
   *   Click on **Add Rules** to select the rules that identify the violations that you want to track.

       A new window opens, displaying a list of all the existing predefined OOTB rules.

       <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>Use <a href="../cloud-workload-rules/create-a-new-custom-detection-rule">Create a new Custom Detection Rule</a> to define and add new custom rules as required.</p></div>
   * After completing your selection, click **Select** to confirm. The chosen rules are displayed in the **Rules** section, where you can toggle between the **Cards** and **Grid** view to display the rules in your preferred layout.
   *   In the **Rules** section, you can select one or more rules to modify the **Severity**, **Policy Action** and **Remediation** values, either individually or in bulk.

       <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>Each rule may support different actions. While some include both <strong>Create an Issue</strong> and <strong>Prevent and Create an Issue</strong>, others provide only the <strong>Create an Issue option.</strong></p></div>
6.  In the Scope section, for the Scope Selection Method, select Asset Groups or Default Asset Scopes, depending on your preference.

    1. If you select Asset Groups, you can choose between the following options:

    **Select existing Asset groups**

    The displayed list shows all Asset Groups available in the Runtime SDLC stage. You can select the asset group to which you want this policy to apply.

    Click Preview Selection to view all relevant Compute Assets associated with the selected asset groups.

    All non-relevant (non-compute) assets are automatically excluded from the included asset list.<br>

    **Add Group**

    Click on Add Group. A new window opens to create a new **Compute Asset group**.

    * Enter a unique Group name and Description.
    *   The displayed list of **Compute Assets** in the table is **pre-filtered** to show only the **relevant assets** based on the **rules selected in the previous section**. The **asset list is dynamically updated** and restricted to the applicable asset types of the selected rules, ensuring that users can select only valid and compatible assets for the new Compute Asset Group.

        You can filter these assets using the Show Filter Panel button based on the fields Asset ID, Name, Provider, and more.
    * When only an **asset filter** is defined, the system creates a **dynamic asset group** that automatically includes assets that meet the specified filter criteria.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>Dynamic asset groups for Kubernetes Prevent Policies support these attributes:</p><ul><li><strong>Kubernetes Resource Cluster</strong>: The cloud identifier for the cluster.</li><li><strong>Kubernetes Resource Namespace</strong>: The namespace where the resource is located.</li><li><strong>Kubernetes Resource Labels</strong>: The labels assigned to the resource.</li><li><strong>Kubernetes Resource Category</strong>: The category of the resource (Identity, Workload, Configuration, or Network).</li><li><strong>Kubernetes Resource Creation Time</strong>: The time the resource was created.</li><li><strong>Kubernetes Resource Name</strong>: The name of the resource.</li></ul><p>When <strong>specific assets are manually selected</strong> from the asset list, a <strong>static asset group is created</strong>, containing only the explicitly chosen assets.</p></div>

    b. On selecting Default Asset Scopes, you can further select the Assets Scope from the predefined **Asset Scopes** that are filtered based on the **selected rules in the previous section** and their applicable **Asset Types**. The Scope options are dynamically updated and limited to the applicable asset types of the selected rules, ensuring that users can select only valid and compatible scopes.
7. Click Done to complete the process and create the new Misconfiguration Workload Policy.
{% endtab %}

{% tab title="Malware Policy" %}
1. Enter a unique name and description. Note that these are mandatory fields.
2. Select an **SDLC Evaluation Stage**. The following options are available.
   * **CI**
   * **Runtime**
   * **Deploy**
3. Click **Next**.
4. The **Summary** section on the right provides a real-time, readable view of all policy configurations as users progress through the wizard. It automatically updates to reflect current selections and settings. It includes the following sections:
   * **General** – Policy name and description.
   * **Conditions** – Selected rule filter and exclusion criteria.
   * **Scope** - The defined scopes included in the policy and SDLC stage.
   * **Actions** - Selected action type.
5. Configure the settings specific to the evaluation stage you select.

<details>

<summary>CI</summary>

* In the **Conditions** section, define the detection rule by specifying the criteria to identify relevant malware findings. You may also include exclusion criteria to filter out any malware findings that meet specific conditions you wish to exclude from this policy.
* Click **Next**.
* In the **Scope** section, select the checkbox to confirm that this selection applies the policy and its detection rules to **All Cloud Workload Build Container Image** asset types available at the CI SDLC stage.
* Click **Next**.
* In the **Action** section:
  *   For **Select an action**, choose the option to **Create an issue** to log an issue if the policy is violated or **Prevent and create an issue** to prevent and create an issue.

      <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h4>Note</h4><p>See Cloud Workload Preventive Action, to learn more about the Prevent action behavior and prerequisites.</p><p>If the <strong>Prevent and create an issue</strong> action is selected, the preventive actions in the CI pipeline will trigger a Fail Pipeline by returning an exit code of 2 in the CI tool.</p></div>
  * Under **Issue Severity**, choose **Critical, High, Medium or Low** to define the issue severity.
  * In the **Remediation Guidance** field, enter the optional remediation instructions.
* Click **Done** to complete the process and create the new Cloud Malware Workload Policy.

</details>

<details>

<summary>Runtime</summary>

* In the Conditions section, define the detection rule by specifying the criteria to identify relevant malware findings. You may also include exclusion criteria to filter out any malware findings that meet specific conditions you wish to exclude from this policy.
* Click Next.
* In the Scope section, for the Scope Selection Method, select Asset Groups or Default Asset Scopes, depending on your requirement.
  *   If you select Asset Groups, you can choose between the following options:<br>

      **Select existing Asset groups**

      The displayed list contains all the asset groups for the Cloud Workload Container Images, Container Instances, Hosts (VM Instances), Serverless Functions or Kubernetes Workloads asset types that are available at the Runtime SDLC stage.<br>

      **Add Group**

      * Click on Add Group. A new window opens to create a new **Compute Asset group**.
      *   The displayed list of **Compute Assets** in the table is **pre-filtered** to show only the **Compute asset types** as Cloud Workload Container Images, Container Instances, Hosts (VM Instances), Serverless Functions or Kubernetes Workloads asset types, ensuring that users can select only valid and compatible assets for the new Compute Asset Group.

          You can filter these assets using the Show filter Panel button based on the fields Asset ID, Name, Provider and more.
      *   When only an **asset filter** is defined, the system creates a **dynamic asset group**, that automatically includes assets that meet the specified filter criteria.

          When **specific assets are manually selected** from the asset list, a **static asset group is created**, containing only the explicitly chosen assets.

      You can then select the asset group to which you want this policy to apply.
  * On selecting Default Asset Scopes, you can further select the Asset Scopes as:
    *   All Cloud Workload Assets

        Choosing this option results in the automatic selection of all other asset scopes in the list.
    * All Cloud Workload Hosts(VM Instances)
    * All Cloud Workload Container Images
    * All Cloud Workload Container Instances
    * All Cloud Workload Kubernetes Workloads
    * All Cloud Workload Serverless Functions
* Click Next.
* In the Action section:
  *   For Select an Action, choose the option to Create an issue to log an issue if the policy is violated or Prevent and create an issue to prevent and create an issue.

      See [Cloud Workload Preventive Action](cloud-workload-preventive-action) to learn more about the Prevent action behavior and prerequisites.
  * Under Issue Severity, choose **Critical, High, Medium or Low** to define the issue severity.
  * In the Remediation Guidance field, enter the optional remediation instructions.
* Click Done to complete the process and create the new Cloud Malware Workload Policy.

<br>

</details>

<details>

<summary>Deploy</summary>

* In the Conditions section, define the detection rule by specifying the criteria to identify relevant malware findings. You may also include exclusion criteria to filter out any malware findings that meet specific conditions you wish to exclude from this policy.
* Click Next.
* In the Scope section, for the Scope Selection Method select Registry Images in Cloud Workload Asset Groups or the All Cloud Workload Registry Images, depending on your requirement.
  * If you select Registry Images in Cloud Workload Asset Groups ,this policy applies only to Cloud Workload Container Registry Images asset types in those groups that are available at the Deploy SDLC stage. A list of all these available asset groups is displayed. You can then select the asset group to which you want this policy to apply.
  * On selecting All Cloud Workload Registry Images, the policy and its detection rules will apply to All Cloud Workload Container Registry Images asset types available at Deploy SDLC Stage.
* Click Next.
* In the Action section:
  * For Select an Action, the default option is Create an issue to log an issue if the policy is violated.
  * Under Issue Severity, choose **Critical, High, Medium or Low** to define the issue severity.
  * In the Remediation Guidance field, enter the optional remediation instructions.
* Click Done to complete the process and create the new Cloud Malware Workload Policy.

</details>
{% endtab %}

{% tab title="Secret Policy" %}
* Enter a unique name and description. Note that these are mandatory fields.
* Select an **SDLC Evaluation Stage**. The following options are available.
  * **CI**
  * **Runtime**
  * **Deploy**
* Click **Next**.
* The **Summary** section on the right provides a real-time, readable view of all policy configurations as users progress through the wizard. It automatically updates to reflect current selections and settings. It includes the following sections:
  * **General** – Policy name and description.
  * **Conditions** – Selected rule filter and exclusion criteria.
  * **Scope** - The defined scopes included in the policy and SDLC stage.
  * **Actions** - Selected action type.
* Configure the settings specific to the evaluation stage you select.

<details>

<summary>CI</summary>

* In the **Conditions** section, define the detection rule by specifying the criteria to identify relevant malware findings. You may also include exclusion criteria to filter out any malware findings that meet specific conditions you wish to exclude from this policy.
* Click **Next**.
* In the **Scope** section, select the checkbox to confirm that this selection applies the policy and its detection rules to **All Cloud Workload Build Container Images** asset types available at the CI SDLC stage.
* Click **Next**.
* In the **Action** section:
  * For **Select an action**, choose the option to **Create an issue** to log an issue if the policy is violated or **Prevent and create an issue** to prevent and create an issue.
  * Under **Issue Severity**, choose **Critical, High, Medium or Low** to define the issue severity.
  * In the **Remediation Guidance** field, enter the optional remediation instructions.
* Click **Done** to complete the process and create the new Cloud Malware Workload Policy.

</details>

<details>

<summary>Runtime</summary>

* In the **Conditions** section, define the detection rule by specifying the criteria to identify relevant malware findings. You may also include exclusion criteria to filter out any malware findings that meet specific conditions you wish to exclude from this policy.
* Click **Next**.
*   In the **Scope** section, for the **Scope Selection Method**, select **Asset Groups** or **Default Asset Scopes**, depending on your requirement.

    * If you select **Asset Groups**, you can choose between the following options:

    **Select existing Asset groups**

    The displayed list contains all the asset groups for the **Cloud Workload Container Images, Container Instances, Hosts (VM Instances), Serverless Functions or Kubernetes Workloads** asset types that are available at the Runtime SDLC stage.<br>

    **Add Group**

    * Click on **Add Group**. A new window opens to create a new Compute Asset group.
    *   The displayed list contains all the asset groups for only the **Compute asset types** as **Cloud Workload Container Images, Container Instances, Hosts (VM Instances), Serverless Functions or Kubernetes Workloads**, ensuring that users can select only valid and compatible assets for the new Compute Asset Group.

        You can filter these assets using the Show filter Panel button based on the fields Asset ID, Name, Provider and more.
    *   When only an asset filter is defined, the system creates a **dynamic asset group** that automatically includes assets that meet the specified filter criteria.

        When **specific assets are manually selected** from the asset list, **a static asset group is created,** containing only the explicitly chosen assets.

    You can then select the asset group to which you want this policy to apply.

    * On selecting **Default Asset Scope**, you can further select the **Asset Scopes** as
      *   **All Cloud Workload Assets**

          <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>Choosing this option results in the automatic selection of all other asset scopes in the list.</p></div>
      * **All Cloud Workload Hosts(VM Instances)**
      * **All Cloud Workload Container Images**
      * **All Cloud Workload Container Instances**
      * **All Cloud Workload Kubernetes Workloads**
      * **All Cloud Workload Serverless Functions**
    * Click **Next**.
* In the **Action** section:
  *   For **Select an action**, choose the option to **Create an issue** to log an issue if the policy is violated or **Prevent and create an issue** to prevent and create an issue.

      <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>See <a href="cloud-workload-preventive-action">Cloud Workload Preventive Action</a> to learn more about the Prevent action behavior and prerequisites.</p></div>
  * Under **Issue Severity**, choose **Critical, High, Medium or Low** to define the issue severity.
  * In the **Remediation Guidance** field, enter the optional remediation instructions.
* Click **Done** to complete the process and create the new Cloud Malware Workload Policy.

</details>

<details>

<summary>Deploy</summary>

* In the **Conditions** section, define the detection rule by specifying the criteria to identify relevant malware findings. You may also include exclusion criteria to filter out any malware findings that meet specific conditions you wish to exclude from this policy.
* Click **Next**.
* In the **Scope** section, for the **Scope Selection Method** select **Registry Images in Cloud Workload Asset Groups** or the **All Cloud Workload Registry Images**, depending on your requirement.
  * If you select **Registry Images in Cloud Workload Asset Groups** ,this policy applies only to Cloud Workload Container Registry Images asset types in those groups that are available at the Deploy SDLC stage. A list of all these available asset groups is displayed. You can then select the asset group to which you want this policy to apply.
  * On selecting **All Cloud Workload Registry Images**, the policy and its detection rules will apply to All Cloud Workload Container Registry Images asset types available at Deploy SDLC Stage.
* Click **Next**.
* In the **Action** section:
  * For **Select an Action**, the default option is **Create an issue** to log an issue if the policy is violated.
  * Under **Issue Severity**, choose **Critical, High, Medium or Low** to define the issue severity.
  * In the **Remediation Guidance** field, enter the optional remediation instructions.
* Click **Done** to complete the process and create the new Cloud Malware Workload Policy.

</details>
{% endtab %}

{% tab title="Trusted Images" %}
1. Enter a unique name and description. Note that these are mandatory fields. The **SDLC Evaluation Stage** is preset to **Runtime**.
2. Click **Next**.
3. Configure the policy's condition settings.
   1.  In the **Conditions** section, specify the criteria to identify relevant images.

       You can specify criteria to define both broad policies and strict policies, for example: `Trust images (from registryX or registryY) OR (digestA or digestB)`. An example of criteria for a broad policy could be `all images from gcr.io/myorg/` while an example of criteria for a strict policy could be: `gcr.io/myorg/app@sha256:abc123`.

       You can also include exclusion criteria to filter out any images that meet specific conditions for exclusion from this policy.

       Because trust is subjective, context-dependent, and scope-based, we recommend you create finely-tuned criteria. For example, an image might be trusted in a low-risk demo environment because it has relaxed patching requirements, but it would be instantly blocked as untrusted in a production environment. For more information, see [Trusted Image Policies](types-of-cloud-workload-policies/types-of-cloud-workload-policies).

<details>

<summary>Considerations for specifying criteria for the policy's conditions</summary>

* If you include a base image as a criterion in your trusted image policy, ensure that the base image itself is successfully scanned and pre-ingested into the system.
* Do not use Scanned by CLI = Yes as the sole criterion for establishing image trust. The CLI scanning status is generally used as an indicator that contributes to overall trustworthiness. Instead, combine the CLI scanning status with stronger, verifiable identifiers like the image registry, signature, and/or base image.
* Define trust criteria only using metadata that is consistently and explicitly included in your deployment files. The policy cannot establish trust if the required metadata (for example, a specific tag or label) is missing from the image definition.
* Avoid using mutable tags as criteria for establishing image trust. Because the underlying image associated with a mutable tag can change without warning, basing trust on it can lead to unexpected outcomes. We strongly recommend enforcing immutable tags—a hallmark of secure, mature CI/CD pipelines—which is supported by all major registries (such as Docker Hub, ACR, ECR, GAR).
* When using trust criteria that rely on image metadata, such as the base layer information or specific tags, we recommend that you pre-ingest the images into Cortex Cloud. While it is possible to base trust on an image that has not been pre-ingested, omitting this step can significantly impact the performance of your policy evaluation, slowing down critical CI/CD workflows.

</details>

2. Click **Next**.

4\. Configure the policy's scope settings.

1. In the **Scope** section, for the **Scope Selection Method** select **Asset Groups** or **Default Asset Scopes**.
   *   **Asset Groups**. The policy applies only to Cloud workload container images, container instances, hosts (VM instances), serverless functions or Kubernetes workload asset types in those groups that are available at the Runtime SDLC stage. A list of available asset groups is displayed. You can then select the asset group to which you want this policy to apply.

       \
       We recommend narrowing the asset group scope to ensure that a policy only checks relevant assets. For more information, see Trusted Images Policies.<br>

       Consider the following when specifying criteria for the policy's scope:

       * Exclude system-critical Kubernetes namespaces, such as **kube-system**, from the policy scope to avoid interfering with core cluster operations.
       * If you select an asset group that contains a specific namespace, the policy will apply only to resources in that namespace—not the entire cluster.
   * **Default Asset Scopes**. On selecting **Default Asset Scopes**, you can further select the **Asset Types**:
     * **All Cloud Workload Assets**
     * **All Cloud Workload Container Images**
     * **All Cloud Workload Kubernetes Workloads**
     * **All Cloud Workload Serverless Functions**
     * **All Cloud Workload Hosts (VM Instances)**
2. Click **Next**.

5\. Configure the policy's action settings. In the Action section:

1. For **Select an Action**, choose either **Create an issue** to log an issue if the policy is violated or **Prevent and create an issue** to prevent and create an issue. For more information, see Preventative action.
2. If you select **Prevent and create an issue** as the policy's action, an additional **Action when trust verdict is unavailable** option becomes available. This is for situations where there is insufficient information available for determining if the image is trusted. The default is **Prevent and create an issue**.
3. Under **Issue Severity**, choose **Critical**, **High**, **Medium**, or **Low** to define the issue severity.
4. In the **Remediation Guidance** field, enter optional remediation instructions.

Issues are automatically closed when the affected asset is removed from the inventory or when the policy is deleted. You can manually close issues at any time.

6\. Click **Done** to complete the process and create the new policy.
{% endtab %}
{% endtabs %}
