# Add an IOC or BIOC rule exception

If you want to create a rule to take action on specific behaviors but also want to exclude one or more indicators from the rule, you can create an IOC or BIOC rule exception. An indicator can include the SHA256 hash of a process, process name, process path, vendor name, user name, causality group owner (CGO) full path, or process command-line arguments. For more information about these indicators, see [What are detection rules?](../../../../../../detect-investigate-and-respond-to-threats/threat-management/detection-rules/what-are-detection-rules). For each exception, you also specify the rule scope to which the exception applies.

In case you need to map fields returned in an XQL process query to your exception configuration, the following table provides a matrix for the criteria mentioned in this procedure to the fields returned in a process query.

| IOC/BIOC suppression rule conditions | Process query result fields            |
| ------------------------------------ | -------------------------------------- |
| Process Sha256                       | actor\_process\_image\_sha256          |
| Process Name                         | actor\_process\_image\_name            |
| Process Path                         | actor\_process\_image\_path            |
| Signed By Vendor                     | actor\_process\_signature\_vendor      |
| User Name                            | actor\_effective\_username             |
| Cgo Full Path                        | actor\_process\_command\_line          |
| Process Cmd                          | causality\_actor\_process\_image\_path |

{% hint style="info" %}
### Note

Cortex XSIAM only supports exceptions with one attribute. See [Add an issue exclusion rule](issue-exclusions/add-an-issue-exclusion-rule) to create advanced exceptions based on your filtered criteria.
{% endhint %}

1. Select **Settings** → **Exceptions Configuration** → **IOC/BIOC Suppression Rules**.
2. Click **+ New Exception**.
3. Specify a rule name and an optional description.
4.  Configure the indicators and conditions that define the exception.

    You can use wildcards to match the command line.
5.  Select the scope of the exception, whether the exception applies to IOCs, BIOCs, or both.

    By default, all BIOC rules that match the criteria are excluded. To exclude only specific BIOC rules, select them from the provided rule list. You can add multiple rules.
6.  **Save** the exception rule.

    By default, activity matching the indicators does not trigger any rule. As an alternative, you can select one or more rules. After you save the exception, the **Exceptions** count for the rule increments. If you edit the rule later, you will also see the exception defined in the rule summary.

**Export a rule exception**

You can choose to export a BIOC rule exception.

1. Select **Settings** → **Exceptions Configuration** → **IOC/BIOC Suppression Rules**.
2. In the **Exceptions** table, locate the exception rule you want to export. You can select multiple rules.
3.  Right-click the rule or rules, and select **Export**.

    If one or more of the selected exceptions are applied to a specific BIOC rule, select one of the following options:

    * **Export anyway**
    * **Export only non-specific Exceptions:** Only export exceptions are applied on all BIOC rules
    * **Export all Exceptions as non-specific:** Export and apply specific exceptions to BIOC rules
