---
description: "A checklist of all the files you need to\_contribute\_to the Cortex XSIAM content repository."
---

# File checklist

Before contributing and opening a pull request, verify you prepared all the files you need to contribute to the Cortex XSIAM content repository. Note that content packs can contain multiple types of entities, such as integrations, scripts, playbooks, incident types, and incident fields.

### Content pack checklist

All content packs must include the following:

* Pack metadata file. For example, `Packs/YourPackName/pack_metadata.json` contains the information about your content pack. It should be compiled with all the [required information](content-pack-structure).
* Pack README. For example, `Packs/YourPackName/README.md`) - the [README](../documentation/content-pack-metadata-file) of the pack file.

If you are updating an existing content pack, the content pack must include [release notes](../documentation/content-pack-release-notes). For example, `Packs/YourPackName/ReleaseNotes/1_0_1.md`.

{% hint style="info" %}
### Note

Use PascalCase (e.g. YourPackName) for the name of the pack, its directories and its entities (integrations, scripts, playbooks, etc.) For reference, view the tree of the [Hello World](https://github.com/demisto/content/tree/master/Packs/HelloWorld) pack on GitHub.
{% endhint %}

### How do I create these files?

To create a new content pack directory tree and structure, you should use the [demisto-sdk init command](https://app.gitbook.com/s/nozw5MT5S8KZD2eF8roV/demisto-sdk-commands/init) , as described in the tutorial for [setting up your development environment](../readme/content-development-environments/set-up-a-local-development-environment).

Integrations and scripts should be written with your favorite IDE.

All other entity types (playbooks, test playbooks, incident/indicator fields and types, layouts, classifiers and mappers, widgets, and dashboards) should be created in the Cortex XSIAM UI and exported using the [demisto-sdk download command](https://app.gitbook.com/s/nozw5MT5S8KZD2eF8roV/demisto-sdk-commands/download) (using the **`-fmt`** argument). You can also export the files manually via the Cortex XSIAM UI (either individually using the download icons, or using the Export Custom Content feature. If you export the files instead of using [demisto-sdk download command](https://app.gitbook.com/s/nozw5MT5S8KZD2eF8roV/demisto-sdk-commands/download), you'll need to format them using [demisto-sdk format](https://app.gitbook.com/s/nozw5MT5S8KZD2eF8roV/demisto-sdk-commands/format).

### Integrations

If your pack contains an integration, the integration directory must contain the following:

| File                                                         | Sample Path and Description                                                                                                                                                                                                                                                                                                                                                                                                 |
| ------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Code                                                         | <p><code>Packs/YourPackName/Integrations/YourIntegrationName/YourIntegrationName.py</code></p><p>Integration implementation code</p>                                                                                                                                                                                                                                                                                        |
| YAML                                                         | <p><code>Packs/YourPackName/Integrations/YourIntegrationName/YourIntegrationName.yml</code></p><p><a href="../integrations-and-scripts/components/integration-metadata-yaml-file">YAML</a> file with integration metadata.</p>                                                                                                                                                                                              |
| Description                                                  | <p><code>Packs/YourPackName/Integrations/YourIntegrationName/YourIntegrationName_description.md</code></p><p><a href="../integrations-and-scripts/components/integration-description-file">Markdown file</a> with instructions for the customer to configure the integration instance. The Markdown file shows up as a snippet when the user clicks the question mark icon in the integration configuration panel.</p>      |
| Image                                                        | <p><code>Packs/YourPackName/Integrations/YourIntegrationName/YourIntegrationName_image.png</code></p><p>The integration <a href="../integrations-and-scripts/components/integration-logo-requirements">logo</a>.</p>                                                                                                                                                                                                        |
| README                                                       | <p><code>Packs/YourPackName/Integrations/YourIntegrationName/README.md</code></p><p>The integration <a href="../documentation/readme-files-for-content-entities">documentation</a>, mostly autogenerated.</p>                                                                                                                                                                                                               |
| Command Examples                                             | <p><code>Packs/YourPackName/Integrations/YourIntegrationName/command_examples</code></p><p>Required to <a href="../documentation/readme-files-for-content-entities">autogenerate</a> the documentation.</p>                                                                                                                                                                                                                 |
| Unit Tests                                                   | <p><code>Packs/YourPackName/Integrations/YourIntegrationName/YourIntegrationName_test.py</code></p><p>This file must be included to automatically <a href="../testing/unit-testing">test</a> the code during the review phase. Although we encourage extensive testing, we do not enforce testing each and every function in the code. We recommend you focus on the most important functions and the helper functions.</p> |
| Unit Tests Data                                              | <p><code>Packs/YourPackName/Integrations/YourIntegrationName/test_data/*.json</code></p><p>Contains example responses from your product API, to be used in <a href="../testing/unit-testing">unit tests</a>. See <a href="https://github.com/demisto/content/tree/master/Packs/HelloWorld/Integrations/HelloWorld/test_data">examples</a> from Hello World.</p>                                                             |
| Custom Alert Types, Fields, Classifiers, Mappers and Layouts | If your integration has the ability to fetch alerts, you usually need to provide custom alert types and related entities. You should plan for this during the design phase, and speak with your Palo Alto Networks Alliance contact person if you have any questions.                                                                                                                                                       |

{% hint style="info" %}
### Note

If you use PowerShell instead of Python, the code files extension will be .ps1 instead of .py.
{% endhint %}

### Playbooks

| File     | Sample Path and Description                                                                                                                                                                                                                           |
| -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Playbook | <p><code>Packs/YourPackName/Playbooks/playbook-YourPlaybookName.yml</code></p><p>If the file is exported directly from the Cortex XSIAM UI, it must be formatted with <code>demisto-sdk format</code>.</p>                                            |
| README   | <p><code>Packs/YourPackName/Playbooks/playbook-YourPlaybookName_README.md</code></p><p>Documentation file for the playbook, mostly <a href="../documentation/readme-files-for-content-entities">autogenerated</a>.</p>                                |
| Image    | <p><code>Packs/YourPackName/doc_files/YourPlaybookName.png</code></p><p>Image of the playbook as exported from the Cortex XSIAM UI. Its link should be added to the <a href="../documentation/readme-files-for-content-entities">README file</a>.</p> |

{% hint style="info" %}
### Note

The playbook README file must be updated with the correct image link after the pull request is opened, as explained in [README files for content entities](../documentation/readme-files-for-content-entities).
{% endhint %}

### Incident or indicator fields

If your pack contains at least one custom incident or indicator field, it must contain a incident field or indicator field JSON file. For example, `Packs/YourPackName/IncidentTypes/YourIncidentTypeName.json` or `Packs/YourPackName/IndicatorType/YourIndicatorTypeName.json`. If the file is exported directly from the Cortex XSIAM UI, it must be formatted with `demisto-sdk format`.

### Incident or indicator types

If your pack contains at least one custom incident or indicator type, it must contain a incident type or indicator type JSON file. For example, `Packs/YourPackName/IncidentFields/YourIncidentFieldName.json` or `Packs/YourPackName/IndicatorFields/YourIndicatorFieldName.json`. If the file is exported directly from the Cortex XSIAM UI, it must be formatted with `demisto-sdk format`.

If you have a custom incident or indicator type, in most situations you also need to include corresponding classifiers, mappers and layouts.

### Classifiers and mappers

| File       | Sample Path and Description                                                                                                                                                                                                        |
| ---------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Classifier | <p><code>Packs/YourPackName/Classifiers/classifier-YourIntegrationName.json</code></p><p>If the file is exported directly from the Cortex XSIAM UI, it must be formatted with <code>demisto-sdk format</code>.</p>                 |
| Mapper     | <p><code>Packs/YourPackName/Classifiers/classifier-mapper-incoming-YourIntegrationName.json</code></p><p>If the file is exported directly from the Cortex XSIAM UI, it must be formatted with <code>demisto-sdk format</code>.</p> |

### Incident or indicator layouts

If your pack contains at least one custom incident or indicator layout, it must contain a incident layout or indicator layout JSON file. For example, `Packs/YourPackName/Layouts/layoutscontainer-YourIncidentTypeName.json.` If the file is exported directly from the Cortex XSIAM UI, it must be formatted with `demisto-sdk format`.

### Scripts

If your content pack contains at least one automation script, the scripts directory must contain the following:

| File            | Sample Path and Description                                                                                                                                                                                         |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Code            | <p><code>Packs/YourPackName/YourScriptName/Scripts/YourScriptName.py</code></p><p>Script implementation code</p>                                                                                                    |
| YAML            | <p><code>Packs/YourPackName/Scripts/YourScriptName/YourScriptName.yml</code></p><p><a href="../integrations-and-scripts/components/integration-metadata-yaml-file">YAML</a> file with script metadata.</p>          |
| README          | <p><code>Packs/YourPackName/Scripts/YourScriptName/README.md</code></p><p>The script <a href="../documentation/readme-files-for-content-entities">documentation</a>, mostly autogenerated.</p>                      |
| Unit Tests      | <p><code>Packs/YourPackName/Scripts/YourScriptName/YourScriptName_test.py</code></p><p>This file must be included to automatically <a href="../testing/unit-testing">test</a> the code during the review phase.</p> |
| Unit Tests Data | <p><code>Packs/YourPackName/Scripts/YourScriptName/test_data/*.json</code></p><p>Contains example responses from your product API, to be used in <a href="../testing/unit-testing">unit tests</a>.</p>              |

{% hint style="info" %}
### Note

If you use PowerShell instead of Python, the code files extension will be .ps1 instead of .py.
{% endhint %}

{% hint style="info" %}
### Note

If your pack contains both integrations and scripts, you can use a single test playbook to test both.
{% endhint %}

### Widgets

If your pack contains at least one custom widget, it must contain a widget JSON file. For example, `Packs/YourPackName/Widgets/widget-YourWidgetName.json`. If the file is exported directly from the Cortex XSIAM UI, it must be formatted with `demisto-sdk format`.

### Dashboards

If your pack contains at least one custom dashboard, it must contain a dashboard JSON file. For example, `Packs/YourPackName/Dashboard/dashboard-YourDashboardName.json`. If the file is exported directly from the Cortex XSIAM UI, it must be formatted with `demisto-sdk format`.

### Checklist table

The requirements above are also summarized in the following table:

| Entity Type               | All Contributions                                                              | Partner/Cortex XSIAM Only                                                                                                      |
| ------------------------- | ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------ |
| Pack                      | <ul><li>Pack metadata</li><li>Pack README file</li><li>Release notes</li></ul> |                                                                                                                                |
| Design                    |                                                                                | Must follow use case guidelines and review the design document with the Alliances team.                                        |
| Integration               | <ul><li>Code file</li><li>YAML file</li><li>Description file</li></ul>         | <ul><li>Image file</li><li>README file</li><li>Command examples file</li><li>Unit tests file</li><li>Unit tests data</li></ul> |
| Playbook                  | Playbook file                                                                  | <ul><li>README file</li><li>Playbook image file</li></ul>                                                                      |
| Incident/Indicator Field  | Incident and/or indicator field JSON file                                      |                                                                                                                                |
| Incident/Indicator Type   | Incident and/or indicator type JSON file                                       |                                                                                                                                |
| Classifier and Mapper     | <ul><li>Classifier JSON file</li><li>Mapper JSON file</li></ul>                |                                                                                                                                |
| Incident/Indicator Layout | Layout JSON files                                                              |                                                                                                                                |
| Script                    | <ul><li>Code file</li><li>YAML file</li><li>README file</li></ul>              | <ul><li>Unit tests file</li><li>Unit tests data</li></ul>                                                                      |
| Widget                    | Widget JSON file                                                               |                                                                                                                                |
| Dashboard                 | Dashboard JSON file                                                            |                                                                                                                                |
