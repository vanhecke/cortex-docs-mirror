# Attack Surface Testing

{% hint style="info" %}
### Note

Requires the ASM add-on.
{% endhint %}

Attack Surface Testing confirms vulnerabilities and misconfigurations on your external attack surface, enabling you to quickly and confidently prioritize risks. With your approval, Cortex XSIAM runs daily, controlled exploits against externally facing assets to confirm the presence or absence of vulnerabilities, eliminating the need to manually verify every inferred CVE. Issues are created for positive attack surface test results, so you can address these vulnerabilities as part of your existing remediation workflows.

## **Attack surface tests**

Cortex XSIAM has an extensive set of attack surface tests for CVEs and other risks that affect externally-facing services and can be confirmed with controlled testing. Our attack surface testing is layered on top of our existing attack surface management (ASM) global scanning infrastructure, which distributes requests across a broad time range to minimize the impact to scanned and tested services.

We perform external scans only, which means we only test directly-discovered services accessible from the public internet and that you selected for testing. To further decrease test load and the possibility of impacting a service, we map attack surface tests to service classifications, enabling us to run tests only on the relevant services in your approved set of targets. For example, we only run Apache attack surface tests against your Apache services.

{% hint style="info" %}
### Note

Attack surface testing scans are typically not CFAA compliant, meaning that they may attempt more extensive fuzzing to confirm or deny the presence of a CVE. Additionally, some attack surface tests are more intrusive than others. Tests are labeled with the level of intrusiveness, so you can decide whether to run more intrusive tests.
{% endhint %}

New attack surface tests are added at the discretion of the Cortex XSIAM Security Research Team when new vulnerabilities are announced.

## **Attack surface tests for default credentials**

Attack Surface Testing does not perform authenticated tests; however, we do have attack surface tests focused on the detection of applications that are using manufacturer default credentials. These attack surface tests attempt to log in to specific business operations systems, IT, and networking devices with default credentials, but don't perform any operations if login is successful and will never change the state or configuration of a tested service.

You can identify attack surface tests for default credentials by looking at the test Name field, which typically includes **Default Credentials** , and the Vulnerability ID field, which uses the prefix **DEFAULT-CRED-**.

**Attack Surface Testing intrusivity**

Attack surface tests are classified by their level of intrusivity. While most tests are benign, some vulnerabilities require more intrusive methods for confirmation. You can choose whether to enable these more intrusive tests, with the various levels of intrusiveness described in the table below.

| Intrusivity level               | Description                                                                                                                                                                                     | Examples                                                                                                                                                                                                                                                                              |
| ------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Level 0: Non-intrusive          | No interaction with the target system beyond passive information gathering. The system remains completely unaffected by any tests.                                                              | <ul><li>Default credential login tests</li><li>Basic HTTP GET / POST requests</li></ul>                                                                                                                                                                                               |
| Level 1: Minimal interaction    | Basic interactions that involve standard requests without altering the system state or data. Any changes are confined to volatile memory and do not persist.                                    | <ul><li>Dropping a small, benign file in a temporary directory, such as <code>/tmp</code>, that the system deletes on reboot.</li></ul>                                                                                                                                               |
| Level 2: Temporary modification | Makes temporary and fully reversible changes to the system. Modifications do not impact normal operations and can be undone without lasting effects. Cleanup is not necessary, but can be done. | <ul><li>Dropping files with benign content in non-temporary directories and that can be removed afterward</li><li>Modifying service configurations that revert after a restart</li><li>Creating a temporary database user that is deleted upon restart</li></ul>                      |
| Level 3: Reversible changes     | Introduces changes that persist but can be reversed with your actions. These changes may slightly impact normal operations, but are recoverable.                                                | <ul><li>Dropping a file containing controlled code that is removed afterward</li><li>Modifying application data (such as UI elements or database entries) that can be corrected</li><li>Executing commands that alter system state but can be undone</li></ul>                        |
| Level 4: Significant impact     | Makes significant changes that are not easily reversible. These actions may disrupt services or alter system data.                                                                              | <ul><li>Injecting data into a database that cannot be fully removed</li><li>Causing temporary service unavailability (for example, a brief Denial of Service lasting a few seconds)</li><li>Creating users or projects within the application that cannot be deleted</li></ul>        |
| Level 5: Full compromise        | Actions that fully compromise the system, leading to irreversible damage, persistent backdoors, or extensive disruption.                                                                        | <ul><li>Executing commands that install persistent backdoors or webshells that cannot be removed</li><li>Modifying critical system files or settings leading to system instability</li><li>Performing Denial of Service attacks that render services completely unavailable</li></ul> |

## **Set up Attack Surface Testing**

To set up Attack Surface Testing for the first time, complete the following tasks:

* [Task 1: Verify that you have edit permission for Vulnerability Testing](#UUID-afc5809d-f703-b7b0-82dc-85e85bb14fa6_section-id235175053282886)
* [Task 2: Accept the End-User Licensing Agreement (EULA)](#UUID-afc5809d-f703-b7b0-82dc-85e85bb14fa6_section-id235175051846476)
* [Task 3: Select targets for attack surface testing](#UUID-afc5809d-f703-b7b0-82dc-85e85bb14fa6_section-id235175050244242)
* [Task 4: Configure the default enablement of new attack surface tests](#UUID-afc5809d-f703-b7b0-82dc-85e85bb14fa6_section-id235174946165067)

**Task 1: Verify that you have edit permission for Vulnerability Testing**

To set up Attack Surface Testing, you must have a role that includes edit permission for Vulnerability Testing. To check your role-based permissions go to **Settings** → **Configurations** → **Access Management** → **Roles**, and select the role. Select the Components tab, and find **Vulnerability Testing** under **Attack Surface**.

**Task 2: Accept the End-User Licensing Agreement (EULA)**

The EULA gives Cortex XSIAM permission to conduct attack surface testing scans. You only need to accept the EULA once. After accepting the EULA the Vulnerability Testing Configuration page opens automatically so you can select the targets for testing.

You only need to accept the EULA once, before you enable attack surface testing for the first time.

1. Navigate to **Modules** → **Attack Surface** → **Policies** → **Attack Surface Tests**.
2. On the Welcome to Vulnerability Testing page, click **Next**.
3. Read the End-User Licensing Agreement and click **Accept Terms**.

After accepting the terms of the EULA, the **Vulnerability Testing Configuration** page opens and you can select the set of services to be tested.

**Task 3: Select targets for attack surface testing**

Attack surface testing targets are directly-discovered services, which are definitively associated with an asset that belongs to your organization. You can choose to run attack surface tests on all your relevant directly-discovered services or you can specify a subset of services.

Specify the directly-discovered services upon which Cortex XSIAM will run attack surface tests. After the initial set-up, you can update this set of targets anytime.

1. Navigate to **Settings** → **Configurations** → **Attack Surface** → **Attack Surface Testing**.
2.  To select specific targets, in the **Target Testing** section, make sure the toggle is set to **Selected Targets**, and click **Edit Targets** (or **Add Targets** if this is the first time you are selecting targets.)

    To select all the targets, set the toggle to **All Targets**. This overrides your target selection.
3. Use the filter to define a set of targets from your list of services.
4. Click **Save Targets**.

**Task 4: Configure the default enablement of new attack surface tests**

When you first enable Attack Surface Testing, all existing attack surface tests with intrusiveness level 0 or level 1 are enabled by default. Moving forward, all new tests that are introduced, for all intrusiveness levels, are disabled by default. To configure Cortex XSIAM to automatically enable new attack surface tests and to specify the intrusiveness level of those default tests, perform the steps below. After the initial set-up, you can update this set of defaults anytime.

1. Navigate to **Settings** → **Configurations** → **Attack Surface** → **Attack Surface Testing**.
2.  In the **Default Attack Surface Test Enablement** section, select the intrusiveness level for the new tests you want to be enabled by default moving forward.

    The intrusiveness level you select will include the tests for the levels below it. For example, if you select Level 2, then new level 0, level 1, and level 2 tests will be enabled moving forward.

After you complete the initial set-up tasks, Cortex XSIAM begins daily attack surface testing scans using the default set of attack surface tests. The default set of tests consists of existing tests with level 0 and level 1 intrusiveness levels.

You can now view details about attack surface tests and enable or disable them and view issues that were triggered by positive attack surface testing scans.

## **Manage attack surface tests**

View information about the available attack surface tests, and enable or disable tests on the **Vulnerability Testing** page. By default all tests are enabled.

1. Navigate to **Modules** → **Attack Surface** → **Policies** → **Attack Surface Tests**.
2. Filter and sort the list of tests as needed to identify the tests you want to enable or disable.
3. Select one or more tests using the check boxes, and right click to **Enable** or **Disable** them.

<details>

<summary>Attack surface test field descriptions</summary>

<table><thead><tr><th width="250">Field</th><th>Description</th></tr></thead><tbody><tr><td>Affected Software</td><td>Software names and versions impacted by this vulnerability.</td></tr><tr><td>CWE IDs</td><td>Common Weakness Enumeration ID as defined by MITRE.</td></tr><tr><td>Created</td><td>When Cortex XSIAM released this test.</td></tr><tr><td>EPSS Score Description</td><td>The Exploit Prediction Scoring System (EPSS) score indicates the likelihood that a vulnerability will be exploited in the wild. Possible values are 0 -100%.the higher the score, the greater the probability that a vulnerability will be exploited.</td></tr><tr><td>References</td><td>Research references and supporting documentation.</td></tr><tr><td>Remediation Guidance</td><td>Recommended steps for remediating or mitigating the vulnerability.</td></tr><tr><td>Severity Score</td><td>The CVE severity score is based on the NIST Common Vulnerability Scoring System (CVSS).</td></tr><tr><td>Services Found Vulnerable</td><td>The number of directly-discovered services owned by your organization that Cortex XSIAM has confirmed vulnerable with this test.</td></tr><tr><td>Status</td><td>Indicates whether the test is <strong>Enabled</strong> or <strong>Disabled</strong>.</td></tr><tr><td>Vendor Names</td><td>Name of the vendor whose product is impacted by the vulnerability.</td></tr><tr><td>Vulnerability IDs</td><td>CVE number or other public identifier for the vulnerability.</td></tr></tbody></table>

</details>

## **View issues created from Attack Surface Testing results**

Cortex XSIAM creates issues for confirmed positive attack surface test results, for both vulnerabilities and misconfigurations. To view those issues and attack surface testing details, perform the following steps.

1. Navigate to **Modules** → **Attack Surface** → **Attack Surface Issues**.
2. Filter the issues list with **Finding Sources** **=** **Cortex Attack Surface Testing**.
3. To view AST scan details, click on an issue, and then select the **Overview** tab of the issue details panel. The AST scan details appear in the **Attack Surface Testing** section.

## **Source IP addresses for Attack Surface Testing scans**

To view the IP address range Cortex XSIAM uses for vulnerability tests, navigate to **Settings** → **Configurations** → **Attack Surface** → **Attack Surface Testing** and refer to the **Source IP Addresses** section. We recommend adding this range to your organization's security tooling allow lists to avoid unnecessary alerting; however, we do not recommend modifying the configuration of your perimeter security controls to allow this traffic to pass. The aim of Attack Surface Testing is to confirm the exploitability of vulnerabilities from an attacker perspective.
