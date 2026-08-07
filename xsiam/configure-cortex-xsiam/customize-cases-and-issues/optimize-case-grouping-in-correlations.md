# Optimize case grouping in correlations

When custom detections (such as correlation rules) generate issues, those issues might not group automatically into related cases—even when they appear related from a user perspective.

Case grouping is determined by Cortex XSIAM’s broader grouping and machine learning logic, which evaluates relationships, context, and shared artifacts across issues.

To optimize how Cortex XSIAM groups issues triggered by correlations, you can map specific fields that influence grouping and prioritization.

### **Why field mapping matters in issue grouping**

Cortex XSIAM’s grouping and machine learning models use specific fields to construct grouping artifacts. These artifacts are then used to evaluate whether issues are related to each other or to an ongoing activity.

Not all fields influence grouping. To contribute effectively to grouping and prioritization, your correlation rules must supply one or more of the relevant fields in a supported format that Cortex XSIAM can interpret. In addition, ensure that the mapped fields adhere to the correct field structure, and expected formatting requirements.

If these fields are missing, incorrectly mapped, or improperly formatted, Cortex XSIAM may be unable to correlate related issues accurately. This can reduce grouping effectiveness and lead to unnecessary issue fragmentation across multiple cases.

Benefits of proper grouping configuration:

* Correlate related custom issues into a single investigative workflow
* Reduce issue and case fragmentation
* Reduce over grouping of issues in cases
* Improve investigation efficiency
* Strengthen ML-based prioritization and correlation
* Align custom detections with organizational context

{% hint style="info" %}
Field mapping does not guarantee grouping.

Cortex XSIAM grouping uses machine learning and platform logic that evaluates confidence, context, relationships, and additional case signals. Field mapping helps influence grouping by contributing relevant artifacts, but final grouping decisions are determined by the platform’s overall grouping logic.

For more information about case grouping behavior, see [Case grouping](../../detect-investigate-and-respond-to-threats/investigation-and-response/case-concepts/case-grouping).
{% endhint %}
