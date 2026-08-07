# Case thresholds

To keep cases manageable, Cortex XSIAM implements case grouping thresholds. When the case reaches a threshold, it stops accepting issues and groups subsequent related issues in a new case.

* 30 days have passed since case creation.
* 14 days have passed since the last issue was detected.
* A case reaches the 1,000 issue limit.

You can track the threshold status in the `Issues Grouping Status` field in the cases table.

**Auto-resolved cases**

If a case is resolved with the status `Resolved - Auto Resolved`, Cortex XSIAM reopens the case within a six-hour window if a matching issue occurs. The six-hour period is defined by the timestamp of the last issue that was grouped into the case. After the six-hour period, any new issues are linked to a new case for a new investigation.
