---
description: >-
  Monitor correlation rule executions, audit status, errors, and related health
  issues in Cortex XSIAM
---

# Monitor Correlation rules

Cortex XSIAM audits all correlation executions in the `correlations_auditing` dataset. The dataset records the query initiation times, end times, retry attempts, failure reasons, and other useful metrics. You can use this dataset to monitor your correlation executions. Cortex XSIAM also provides OOTB health issues that are generated when a correlation rule completes with errors. For more information, see [About health issues]().

In the `correlations_auditing` dataset, audit entries are added as follows:

* The rule starts executing. This is audited with the status of Initiated or Initiated Manually.
* The rule completes successfully. This is audited as Completed.
* The rule completes with errors. This is audited as Error.

In the dataset, the Query start time and Query end time indicate the timeframe of the data that was queried. The actual start and end times of the correlation rule execution are recorded in the \_time field for the Initiated and Completed entries.

### Field descriptions for the correlations\_auditing dataset in Cortex XSIAM

The following table describes the fields in the correlations\_auditing dataset:

| Field                   | Description                                                                                                                                                                                                                                          |
| ----------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| \_time                  | <p>Timestamp of the audit.</p><p>For entries with an Initiated or Initiated Manually status, this is the start time of the correlation rule execution. For entries with a Completed or Error status, this is the end time of the rule execution.</p> |
| \_id                    | Unique identifier of the audit entry.                                                                                                                                                                                                                |
| Rule ID                 | Unique identification number for the correlation rule.                                                                                                                                                                                               |
| Name                    | Correlation rule name.                                                                                                                                                                                                                               |
| Status                  | <p>The status of the correlation rule query.</p><p>Possible values are Initiated, Initiated Manually, Completed, and Error.</p>                                                                                                                      |
| Query start time        | The start time of the query timeframe.                                                                                                                                                                                                               |
| Query end time          | The end time of the query timeframe.                                                                                                                                                                                                                 |
| Time frame              | Time frame for the query.                                                                                                                                                                                                                            |
| Failure reason          | For correlation rules with errors, this field displays the error message.                                                                                                                                                                            |
| Retry attempts          | Number of retry attempts before the query initiated or failed to run.                                                                                                                                                                                |
| Schedule                | Scheduled frequency to execute the correlation rule.                                                                                                                                                                                                 |
| Rule creation time      | Date and time that the correlation rule was created.                                                                                                                                                                                                 |
| Rule modification time  | Date and time that the correlation rule was last modified.                                                                                                                                                                                           |
| Description             | Description of the correlation rule.                                                                                                                                                                                                                 |
| Severity                | Defined severity of the correlation rule.                                                                                                                                                                                                            |
| Dataset                 | Target data set, as defined in the correlation rule                                                                                                                                                                                                  |
| Suppression status      | Whether issue suppression is Enabled or Disabled.                                                                                                                                                                                                    |
| Suppression duration    | Duration for which to ignore additional events that match the issue suppression criteria.                                                                                                                                                            |
| Suppression fields      | Fields on which the issue suppression is based.                                                                                                                                                                                                      |
| Timezone                | Timezone on which the scheduled frequency is based.                                                                                                                                                                                                  |
| MITRE ATT\&CK Tactic    | MITRE ATT\&CK tactic that the correlation rule attempted to generate.                                                                                                                                                                                |
| MITRE ATT\&CK Technique | MITRE ATT\&CK technique that the correlation rule attempted to generate.                                                                                                                                                                             |
| Issue category          | Category of issue as configured when creating the rule.                                                                                                                                                                                              |
| Source                  | Source of the correlation rule.                                                                                                                                                                                                                      |
| XQL search              | XQL query for the correlation rule.                                                                                                                                                                                                                  |
| Drill-down query        | XQL query configured for further investigation.                                                                                                                                                                                                      |
| Issue name              | Name of the issue that the correlation rule will generate.                                                                                                                                                                                           |
