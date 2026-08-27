---
description: Cortex XSIAM best practices for content pack release notes.
---

# Content pack release notes

Release notes files help users keep track of changes made in specific content entities, such as integrations or playbooks.

To generate a release notes Markdown file, first commit the changes to your branch and then run the following command:

```programlisting
demisto-sdk update-release-notes -i Packs/PACK_NAME -u [major|minor|revision]
```

{% hint style="info" %}
**Note**

Changes that have not been committed are not detected automatically by the `update-release-notes` command.
{% endhint %}

The `update-release-notes` command automatically updates the `currentVersion` found in the `pack_metadata.json` file according to the update version (as denoted by the -u flag). The versioning format is as follows: MAJOR.MINOR.REVISION.

| Versioning Type | Description                                                                                                                                 |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| major           | Use for a new version of the pack, or a new version of one of its integrations. For example, a rewrite of an integration or a large change. |
| minor           | Use for adding new functionality (for example, adding mirroring, fetching incidents, or indicators) or adding many new commands.            |
| revision        | Use when you add new content items or a few commands, or when updating content items or commands.                                           |
| documentation   | Use when adding or updating documentation.                                                                                                  |

In most cases, run the command when you are ready to merge and when you expect no further changes. If you need to make additional changes after running the `update-release-notes` command, remove the `-u` argument. This updates the release notes file for you to fill out.

```programlisting
demisto-sdk update-release-notes -i [Changed pack path]
```

For more information regarding the `update-release-notes` command in the demisto-sdk, please refer to the [command documentation](https://app.gitbook.com/s/nozw5MT5S8KZD2eF8roV/demisto-sdk-guide/demisto-sdk-commands/update-release-notes).

### Locate generated content pack release notes

The release notes file is generated for you and is found in the `ReleaseNotes` folder within each pack. If this folder does not already exist, it is created for you. Do not change the names of the files that are automatically generated, as this can cause potential issues later in the development process.

### Format content pack release notes

After running the `demisto-sdk update-release-notes` command, the release notes file contains a section for each entity changed in the pack as well as a placeholder (`%%UPDATE_RN%%`). This placeholder should be replaced with a line describing what was changed for that specific entity.

For example, if changes are detected in the Cortex XDR pack for the items `IncidentFields`, `Integrations`, and `Playbooks`, the following is created:

```programlisting
#### Incident Fields
##### XDR Alerts
  - %%UPDATE_RN%%

#### Integrations
##### Cortex XDR - IR
  - %%UPDATE_RN%%

#### Playbooks
##### Cortex XDR - Isolate Endpoints
  - %%UPDATE_RN%%

##### Cortex XDR - Port Scan
  - %%UPDATE_RN%%
```

### Use Markdown formatting in release notes

For single line RNs, follow this format:

```programlisting
#### Integrations
##### Cortex XDR - IR
Release note here.
```

For single line RNs with a nested list, follow this format:

```programlisting
#### Integrations
##### Cortex XDR - IR
Release note here.
  - List item 1
  - List item 2
```

For multiline RNs, follow this format:

```programlisting
#### Integrations
##### Cortex XDR - IR
  - Release note 1 here.
  - Release note 2 here.
  - Release note 2 here.
```

For multiline RNs with nested content, follow this format:

```programlisting
#### Integrations
##### Cortex XDR - IR
  - Release note 1 here.
    - List item 1
    - List item 2
  - Release note 2 here.
    - List item 1
    - List item 2
  - Release note 2 here.
```

### Write effective content pack release notes

Log the following in the corresponding release notes file:

* Any change(s) made
* New command(s)
* New or updated parameters
* New or updated arguments
* Updated outputs
* Bug fixes

#### Content pack release note writing guidelines

* Release notes should be simple, informative, and clearly written. Consider the impact of changes on the user and what they need to know about this version. A poorly written release note with inadequate information can lead to a Customer Support ticket. For example, instead of writing `Added a timeout parameter`, we recommend adding additional detail explaining the new parameter, such as `Added a timeout parameter, that enables you to define the amount of time (in minutes) that the integration tries to execute commands before it throws an error`.
* Single line release notes do not need a bullet point.
*   Release notes must start with one of the following prefixes:

    * Added support for
    * Added the
    * Added a
    * Added an
    * Fixed an issue
    * Improved implementation
    * Updated the
    * You can now
    * Deprecated
    * Deprecated the
    * Improved layout
    * Created a new layout
    * Playbook now supports
    * Created a new playbook
    * New:

    Release notes that do not start with one of these prefixes will generate an error when running `demisto-sdk doc-review`: `Line is not using one of our templates, consider changing it to fit our standard`.

#### Format content entity names in release notes

* Command names should be wrapped with three stars - \*\*\*command\_name\*\*\*
* Content pack names, integrations, scripts, playbooks, and other content entities (incident fields, dashboards, etc.) should be wrapped with two stars - \*\*entity\_name\*\*
* Parameters, arguments, functions, and outputs names should be wrapped with one star - \*parameter\_name\*

#### Content pack release note examples

**Enhancement release note example**

````
```programlisting
- **MISP V2**  
You can now filter an event by attribute data fields.

- **WhatIsMyBrowser**  
Added support for the *extend-context* argument in the ***ua-parse*** command.

- **Microsoft Graph Mail**   
Added 3 commands:
    - ***msgraph-mail-list-folders***
    - ***msgraph-mail-list-child-folders***
    - ***msgraph-mail-create-folder***
```
````

**Bug fix release note example**

````
```programlisting
- **Slack v2**  
    - Fixed an issue where mirrored investigations contained mismatched user names.
    - Added the **reporter** and **reporter email** labels to incidents that are created by direct messages.

- **CrowdStrike Falcon**  
Fixed an issue with ***fetch incidents***, which caused incident duplication.

- **IBM QRadar**  
Fixed an issue in which the ***qradar-delete-reference-set-value*** command failed to delete reference sets with the "\" character in their names.

- **GitHub**  
Improved implementation of the default value for the *fetch_time* parameter.
```
````

**Docker update release note example**

````
```programlisting
- Updated the Docker image to: *demisto/python3:3.9.1.15759*.
```
````

**General change release note example**

````
<div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>Use this type only if the change has no clear or visible impact on the user.</p></div>

```programlisting
- Documentation and metadata improvements.
```
````

### Exclude items from generated release notes

Release notes must contain all changed items included in the generated file. Validation fails if detected items are removed from the generated release notes file.

However, you may encounter a scenario where certain changes are not necessary to document in the release notes. In this case, to pass validation, comment out the entries using the following syntax:

```programlisting
<!--
#### Integrations
##### Cortex XDR - IR
  - Renamed an item. Not necessary to document in release notes.
-->
```

### Validate release notes with `demisto-sdk doc-review`

demisto-sdk includes the [doc-review](https://app.gitbook.com/s/nozw5MT5S8KZD2eF8roV/demisto-sdk-guide/demisto-sdk-commands/doc-review) command to assist with the documentation review process. The `doc-review` command checks the spelling of the release notes and provides guidance if you are not using one of our standardized templates. Example usage: `demisto-sdk doc-review -i Packs/Base/ReleaseNotes/1_11_10.md`.

### Create release notes for breaking changes

In some cases, a new version is introduced which breaks backward compatibility. You can mark a new version as a breaking changes version. Marking a version as a breaking changes version provides the user with an alert before installation.

To mark a new version as a breaking changes version, run the `demisto-sdk update-release-notes` command with the `-bc` flag. For example:

```programlisting
demisto-sdk update-release-notes -i Packs/<Pack Name> -u revision -bc
```

The `-bc` flag generates a corresponding configuration JSON file to the new release notes. For example, if the newly created release notes version is `1_1_0.md`, a new configuration file `1_1_0.json` is created in the corresponding `ReleaseNotes` directory.

The configuration JSON file is generated with the following fields:

* `breakingChanges`: Indicates whether the version has breaking changes or not, is created with `true` value when using the `-bc` flag.
*   `breakingChangesNotes`: Contains the text to be displayed to the customer before installation. If `breakingChangesNotes` is not specified, the default is to present the entire release notes text to the user prior to the content pack installation. The field can be in Markdown format. For example, to add a list of changes:

    ```programlisting
    {
        "breakingChanges": true,
        "breakingChangesNotes": "<ul><li>The `ip` command returns a list/array of IPs in the `HelloWorld.IP` context path (instead of a single IP).</li><li>The `ip` command context output paths `HelloWorld.IP.Objects`, `HelloWorld.IP.Names` were stripped of the leading whitespace (e.g. `HelloWorld.IP. Objects` -> `HelloWorld.IP.Objects`).</li><li>The `ip` command will now return a maximum of 50 results.</li></ul>Make sure to check and update any Playbooks/Scripts that use the above context paths."
    }
    ```

### Troubleshoot content pack release notes

#### Excluded item fails release note validation

Remove the `%%UPDATE_RN%%` from the generated file and leave the other generated items intact.

#### `update-release-notes` does not find changes

First check you have committed your files. Then verify that the type of file you changed requires a release notes entry. TestPlaybooks, Images, READMEs, and TestData do not require release notes.

#### Completed release notes fail validation

On rare occasions, it's possible that the pack you are working on has already had the version updated. To resolve this, delete the generated release notes Markdown (.md) file and restore the `currentVersion` in the `pack_metadata.json` file to its original version. Next, pull from the master branch. Lastly, run the `update-release-notes` command again.

#### Release notes for new content packs

The build process automatically creates the initial release notes. You do not need to generate release notes for new content packs.
