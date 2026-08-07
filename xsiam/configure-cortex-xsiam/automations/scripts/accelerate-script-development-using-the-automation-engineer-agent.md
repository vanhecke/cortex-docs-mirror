# Accelerate script development using the Automation Engineer agent

The **Automation Engineer** agent is a conversational AI that simplifies Python script creation and management through an intuitive, interactive experience. It enables you to generate, query, iterate, and refine automation scripts with the **Agentic Assistant** natural language chat prompt.

Automation Engineer agent scripting capabilities include:

*   Initial code generation: Generate a full script from a simple prompt. For example, "Generate a script to change the verdict of a given indicator based on user input, including documentation notes and debug messages."

    The agent uses security best practices and Agentic SDK to generate tailor-made Python scripts.
* Existing script modification: For example, “Add a check to ensure the indicator exists before proceeding with the verdict change, and return an error if it does not.”
* Iterative bug fixing: For example, "Provide specific error messages for the agent to analyze and automatically repair."
* API compatibility updates: For example, "Detect and replace deprecated API calls across an entire script."
* Logic simplification: Ask the agent to refactor complex code to be more readable or to remove redundant conditionals for simple lookups.
* Script explanation: Ask the agent questions about system or custom scripts, including asking how the script works. You can ask the agent to explain the specific script currently open or pose general technical questions regarding script logic and the Agentic SDK.
* Input and error validation: Enhance script robustness by asking the agent to add specific try/except blocks or validate that inputs like username are not empty.
* SDK and command guidance: Ask the agent for technical details on using the Agentic SDK or the proper syntax for running commands within a script.

When you download or update content packs, the new or updated scripts are immediately ready for the Automation Engineer agent to recommend and use.

{% hint style="info" %}
The Automation Engineer agent is available with the Cortex Agentic Assistant for users with script editing permissions. For more information, see [Cortex Agentic Assistant](../../../learn-about-cortex-xsiam/agentic-ai-in-cortex-xsiam) and [Agentic Assistant role-based access control](../../configure-the-cortex-agentic-assistant-1/agentic-assistant-role-based-access-control).
{% endhint %}

<details>

<summary>Search tips</summary>

Use the free text search to find scripts by name, tag, script content, or all fields. Use quotation marks for exact script-name matches. Wildcards are not supported.

</details>

### How to use the Automation Engineer agent

1.  From the **Investigation & Response** → **Automation** → **Scripts** page, either choose an existing script or create a new script.

    #### For a new script

    1. Click **+ New Script**, give the script a name, and click **Save**.
    2. Click ![agentic-assistant-icon.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-3608fe6382bd2f237a643f6293383c881313b349%2F83a46d7b4a89b73f6ad0bd44541cf87fb8d32a7243be84b2d991e221c398c1b4.png?alt=media). The **Agentic Assistant** pane opens with the Automation Engineer agent automatically selected.

    #### For an existing script

    1. In the **Scripts Library**, search for the script you want to use.
    2. Click Edit. The Agentic Assistant pane automatically opens with the Automation Engineer agent selected.\
       If a script is installed from a content pack, by default, the script is locked, which means that it is not editable. To edit a system script, you first need to duplicate it.

    If you are in the middle of a chat with a different agent, you are prompted to start a new chat with the Automation Engineer agent.

    If you start a chat with one script and switch to another script, you are prompted to start a new chat.
2. In the Agentic Assistant pane, enter a natural language prompt describing what you need the agent to do, including:

* Explain what the script does.
* Fix code errors: If there are errors in the script code, you can ask the Automation Engineer agent to suggest a correction.
* Add documentation notes to the script: Ask to include explanations and inline comments.
*   Add arguments to the script: Define the inputs your script should accept. Each argument should include a name, type, whether it is required, and optionally a default value.

    Examples:

    * **`days — number, optional, default: 3`**
    * **`email — string, required`**, **`email="soc@company.com`**
* Add outputs to the script: Describe what the script should return to the context, for example, **`recentIncidentsSummary — string, a human-readable summary of incidents`**.
* Include debug logging: Request to include contextual log messages in the script.
* Include error handling: Ask to include try/except blocks with informative error logs.

{% hint style="info" %}
Use detailed prompts, for example, **`Get failed logins from last 24 hours and return as a table`**.

Clearly define argument names, types, and default values.

Mention if you expect the output in a specific format, such as a table, JSON, or plain text.
{% endhint %}

Example:\
The following are sample prompts

```
Fetch all open incidents from the last 3 days. 
Generate a summary table with ID, name, and severity. 
Email the summary to the given address.

Arguments:
- days (number, default: 3)
- email (string, required)

Output:
- incidentsSummary (string): a human-readable table of incident details
Explain what this script does
How do I use the SDK to execute a search command?
I got this error: <KeyError>: <userId>. Fix it.
```

3\. Click [![ai-script-prompt-go.png](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACYAAAAmCAYAAACoPemuAAAACXBIWXMAABJ0AAASdAHeZh94AAAAB3RJTUUH6QYFCCgXlZyfrQAAAa9JREFUWIXt1r9qwlAUBvAvNjaJIijEwYJIoEMy2kwtOAt9BPsQDn2BQvfSZ+jQ1dnFDpY6iaPdhCw6ZIj/YiRRO8UiGHuPGuuQb8y9l/y4OffkcgBWOMPE/hsQlAhGTQSjJoJRwwyTdA1ytQJBVcL0rMOzTowlREi6BknX4JkWRrUGps1OaLALAE9sMAnJUnEDmSzdYGU7WJgWVq53VBgHwi8p//a89fnSdjCuf2FSb2FpO6eH5V4ewcvpwPGl7WDW7mJUa8AzrYNgzJ8SAERVQfwqGzjOxXlcFnJIle/Ayxm4Rn/vHSTBFsPJus7+ig8UVQWeaWFB3EEazLTgGgNcXucRS4hMa/hsBslSEaKqABzgGgOmdaQa23ihnIagKRBUBZKuMUM904L5+g7X6O+cd7adn7nB+pF0DemH+52nc1vm3R6mnx3mpkyCCaoCuVohg4a1D8y/e6R1JFiqfMs8d9rsHNTPSLB4Ibdz/JgNlgQLqqswfknMsG3XHf+WMWt3jwYiw/js726d4trDDPPrZ1xvkU/YPtm784eds+38EYyaCEZNBKMmglETwaj5AcLUpYoXiOg8AAAAAElFTkSuQmCC)](https://docs-cortex.paloaltonetworks.com/viewer/attachment/5CAbsl8idaK8R43ZLhoTOw/Z0vUNOuMQ3kVCg6tHt4EkA-5CAbsl8idaK8R43ZLhoTOw) or **`Enter`** to submit the prompt.\
The Agentic Assistant then displays:

* The plan describes the steps the Automation Engineer agent took.
* A script preview card that includes the following details:
  * The script name.
  * The script revision number (#).
  * Script metadata: The number of lines, arguments, and outputs.
  * An expand icon that shows the new script code with the option to Use this revision.
  * [![three-dots-dark.png](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACAAAAAjCAYAAAD17ghaAAAACXBIWXMAABJ0AAASdAHeZh94AAAAB3RJTUUH6QsCDQAEL/NOOgAAApxJREFUWIXtVzFrpEAYfXPIoOIMBq1clmUk2N2vuCK/5ur7CYH8lTTpUh6Brba9zkIJi1spBkdUjOAVYWVvV129y7Ep8irRb973+ObNN59ktVq1uCC+XDL5p4APIUCZGmgYBq6ursAYg6ZpUJS3pU3ToCxLSCmRpinyPH9fAaZpwnEcUEqRJAmiKEJRFGia5o1AUaDrOjjnuL6+Rl3X2O12eHl5mSSAjB1DIQQ454iiCHEcTyK0bRuLxQJZliEMw78ToCgKPM9DVVUIwxBtO69VEEIghICqqvB9v6tWH3pN6HkepJQIgmB2cgBo2xZBEEBKCc/zRmNPBAghUFUVttvt7MTH2G63qKoKQohpAkzTBOf87N7d3D1is9lgs9ng8e5mNDYMQ3DOYZrmeQGO4yCKorNltxntnimzR2PbtkUURXAcZ1yAYRiglE5ye33oqaY+Gx/HMSilMAzj5Ft3CpbLJQC8y973YYi/qwBjDFmW/ZfkAJBlGRhjJ+87AZqmoSiKSWRzTLhHURTQNG1YgKIoow3jEHNMuEfTNN390StgDuaacAydpL3C19fXs4vuv3/D/dxEAxXuKlCWJXRdn0k7HbquoyzLYQFSSnDOJ5Hd3D5g/bTG+mmNh9tpJuScQ0o5LCBNU1iWNYnMNhmoRkE1CmZOM6FlWUjTdFhAnueo6xq2fZ5wrglt20Zd173T0h/nYrfbYbVaIUmS0fvg/u4H4q8WKGokv36OJieEYLFY4Pn5uf/78UAihAAhBEEQjBJPheu6aNt28IY96QNhGEJV1a53/wuWyyVUVR293nsbke/7YIzBdV0QQmYnJoTAdV0wxuD7/njshxxKD3E8lmdZNjiWW5b1vmP5IS72Y7JHnuezyafg4v+GnwJ+AxX2QhQiVAHvAAAAAElFTkSuQmCC)](https://docs-cortex.paloaltonetworks.com/viewer/attachment/5CAbsl8idaK8R43ZLhoTOw/thsZ_aCJgLfIxEAgkOeaiQ-5CAbsl8idaK8R43ZLhoTOw) that includes Use this revision or Copy code.

The first line of the generated script indicates it was generated by Cortex XSIAM, with the date and time of the latest update.

4\. Use natural language in the prompt to modify the generated script as needed.\
Example\
For the script generated from the sample prompt above, enter the following modification to add sorting:

````

```
Modify the sorting behavior so that all 1s (threats) come before all 0s (safe events). Keep the rest of the script structure the same.
1 / 1
```
````

{% hint style="info" %}
If you make manual edits in the script and don't save the changes, and then modify the script with the Automation Engineer agent, you are prompted to confirm that you're overwriting the manual edits.
{% endhint %}

5. (Optional) Access an earlier script revision by clicking [![three-dots-dark.png](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACAAAAAjCAYAAAD17ghaAAAACXBIWXMAABJ0AAASdAHeZh94AAAAB3RJTUUH6QsCDQAEL/NOOgAAApxJREFUWIXtVzFrpEAYfXPIoOIMBq1clmUk2N2vuCK/5ur7CYH8lTTpUh6Brba9zkIJi1spBkdUjOAVYWVvV129y7Ep8irRb973+ObNN59ktVq1uCC+XDL5p4APIUCZGmgYBq6ursAYg6ZpUJS3pU3ToCxLSCmRpinyPH9fAaZpwnEcUEqRJAmiKEJRFGia5o1AUaDrOjjnuL6+Rl3X2O12eHl5mSSAjB1DIQQ454iiCHEcTyK0bRuLxQJZliEMw78ToCgKPM9DVVUIwxBtO69VEEIghICqqvB9v6tWH3pN6HkepJQIgmB2cgBo2xZBEEBKCc/zRmNPBAghUFUVttvt7MTH2G63qKoKQohpAkzTBOf87N7d3D1is9lgs9ng8e5mNDYMQ3DOYZrmeQGO4yCKorNltxntnimzR2PbtkUURXAcZ1yAYRiglE5ye33oqaY+Gx/HMSilMAzj5Ft3CpbLJQC8y973YYi/qwBjDFmW/ZfkAJBlGRhjJ+87AZqmoSiKSWRzTLhHURTQNG1YgKIoow3jEHNMuEfTNN390StgDuaacAydpL3C19fXs4vuv3/D/dxEAxXuKlCWJXRdn0k7HbquoyzLYQFSSnDOJ5Hd3D5g/bTG+mmNh9tpJuScQ0o5LCBNU1iWNYnMNhmoRkE1CmZOM6FlWUjTdFhAnueo6xq2fZ5wrglt20Zd173T0h/nYrfbYbVaIUmS0fvg/u4H4q8WKGokv36OJieEYLFY4Pn5uf/78UAihAAhBEEQjBJPheu6aNt28IY96QNhGEJV1a53/wuWyyVUVR293nsbke/7YIzBdV0QQmYnJoTAdV0wxuD7/njshxxKD3E8lmdZNjiWW5b1vmP5IS72Y7JHnuezyafg4v+GnwJ+AxX2QhQiVAHvAAAAAElFTkSuQmCC)](https://docs-cortex.paloaltonetworks.com/viewer/attachment/5CAbsl8idaK8R43ZLhoTOw/thsZ_aCJgLfIxEAgkOeaiQ-5CAbsl8idaK8R43ZLhoTOw) and then Use this revision on the script preview card of the revision you want to use.
6. Continue modifying and submitting prompts until the script works as intended.
7. For a new script, click Save Version. For an existing script that was edited, click Use this revision and then Save Version.
8. (Recommended) Validate your script.
   1. Click Test.
   2.  In the Arguments section, provide values for any inputs your prompt requires. These inputs are used to simulate how the script will behave in a live playbook, or how the script registered as an Action and assigned to an Agent will run as part of an executed plan.

       You can add input values manually.
   3.  Click Run.

       The scripts are executed in the Playground. Review the output generated by the script to validate its behavior and ensure it produces the expected results. The output is typically a text summary or another structured format that you have defined.

       <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>If there is an error, you can copy the error message from the test result into the Agentic Assistant prompt and ask the Automation Engineer agent to correct the error.</p></div>

       In each run result, you can take the following actions:

       | Action                   | Description                                                                                                                                                                                                                                    |
       | ------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
       | Edit                     | Edit the entry, mark it as a note, preview it, or delete it.                                                                                                                                                                                   |
       | Mark as note             | <p>Marks the entry as a note, which can help you understand why certain action was taken and assist future decisions.</p><p>When marked as a note, it is highlighted, so you can easily find it in the War Room or the Issue Overview tab.</p> |
       | View artifact in new tab | Opens a new tab for the artifact.                                                                                                                                                                                                              |
       | Add tags                 | Add any relevant tags to use that help you find relevant information.                                                                                                                                                                          |
