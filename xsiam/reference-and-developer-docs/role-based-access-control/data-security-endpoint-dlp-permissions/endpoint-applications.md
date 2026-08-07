# Endpoint Applications

Endpoint Applications is a catalog of applications that can be referenced in Data-in-motion Rules. It includes predefined applications (web applications, local file-sharing applications, cloud storage applications, USB devices) and allows creation of custom local and web applications. Each application entry defines process names, URLs/domains, and application type that the DLP engine uses to identify data movement channels.

Users access Endpoint Applications by going to **Modules** → **Data Security** → **Endpoint Data-in-Motion Rules** → **Endpoint Applications**.

{% hint style="warning" %}
### Caution

Predefined (system) applications cannot be edited or deleted regardless of permissions.
{% endhint %}

| Permission | Description                                                                                                                                                                                                                                          | Recommended Roles                                                                                                                                                                                                       |
| ---------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| None       | Users cannot access the **Endpoint Applications** page. Users cannot see the application catalog, custom applications, or any application definitions. Any attempt to directly access the URL will result in an access denied error.                 | <ul><li>SOC Tier-1 Analyst: Application catalog management is outside the Tier-1 scope.</li><li>IT Admin: Application catalog management is outside the IT infrastructure administration scope.</li></ul>               |
| View       | Users can navigate to the Endpoint Applications page and see all applications in the grid view. They can view application names, types (Web Application, Local Application), process names, URLs/domains, and whether they are predefined or custom. | <ul><li>SOC Tier-2 and 3 Analysts: May need to review application definitions when investigating DLP issues.</li><li>Threat Hunter: May need to understand monitored applications for threat hunting context.</li></ul> |
| View/Edit  | Users have full control over Endpoint Applications. They can create new local applications and web applications, edit custom application definitions, and delete custom applications.                                                                | <ul><li>Security Engineer: Responsible for defining custom applications for DLP rule targeting.</li><li>Security Admin: Full administrative access to all DLP configurations.</li></ul>                                 |

**Required and recommended permissions**

Endpoint Applications act as the building blocks for your DLP rules. To effectively manage the application catalog, administrators must understand how these applications are grouped and enforced.

| Permission                  | Permission Level | Reason                                                                                                                                                                                                                      |
| --------------------------- | ---------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Endpoint Application Groups | View             | Strongly recommended. Groups contain applications; viewing the application catalog helps when managing groups.                                                                                                              |
| Data-in-Motion Rules        | View             | Strongly Recommended. DLP rules directly reference the applications defined in this catalog. Viewing these rules provides essential context on where and how specific applications are actively being monitored or blocked. |
