# Create a section header

Section headers are used to manage the flow of your playbook and help you organize your tasks efficiently. You create a section header to group a number of related tasks.

1. From the **Task Library** pane, click **Header** or **Blank Task**.
2. In the **Task Details** pane, for Task Type, select the Section Header icon.
3. Enter a meaningful name in the **Task Name** field for the section header.
4. In the **Details** tab, configure the following.
   * **Tag the result with**: Add a tag to the task result. You can use the tag to filter entries in the War Room.
   * **Sub Section**: If selected, this section becomes a subsection of the parent section above it, and it collapses when its parent section collapses.
   * **Response action**: Select this checkbox to mark the section as containing impactful remediation or response steps. These actions are surfaced in the Resolution tab of an issue and the Possible Response section in the playbook's high-level visual structure. Use this for autonomous playbooks to highlight key results for analysts.
   * **Requires manual intervention**: Select this checkbox to pause the playbook at this section. The playbook will remain in a pending state until an analyst provides manual approval or performs the required action in the Pending tab of the Resolution Center. Use this to ensure relevant autonomous actions only proceed with human oversight.
   * **Display label**: Enter a short, human-readable name for the action. This label is displayed in the UI (such as the Resolution tab or Case screen) to help analysts identify the task's intent during an investigation. This enables autonomous playbooks to provide a clear summary of automated findings.
   * **Task description (Markdown supported)**: Provide a description of what this task does. In the Playbooks page, click [![playbook-info-icon.png](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABwAAAAiCAYAAABMfblJAAAACXBIWXMAABJ0AAASdAHeZh94AAAAB3RJTUUH6QEPCiAUGlWsBQAAAXRJREFUSIljjK1u+s9AQ8DEyMiQFxXKYKSpDuHT0jIGBgaGf///M0xYuorh/I1b9LEQBiavWMNw78kz+ln4589fhllrN9LPQgYGBoZnr9/Q10IGBjrG4YBZyIJLQliAnyKDf/3+zfD56zfiLWRgYGDg5eIi28K3Hz9iFScrSJ3MjBnifDwYuDk5SNZLloX2JoYMKnIyDKpysvSxkBKANw5xgVU79zLISYozXL17nz4WXr17nyzLSLaQnZWVIT86jIGHi5Ph/afPDDPXbGT49uMHSRaSFIdcnBwM3FycDAwMDAyCfLwMavI0TjTvP31mmLpiLZzPzMxMWwsZGBgYXr97D2czkmwdGRYit0eEBfgZmJhIM4KifGhtoMtgqadNewtvPXwMZ3/9TloqJSsfLtm6k0FaTJTh5+/fDG/ef6C9hQwMDAxPX70mSx9OC3/9/o2ziqEE4LQQW+VJDTD82zSjFo5aSBKQEhWhn4UsLMwMacH+DAAFHVwMu415lgAAAABJRU5ErkJggg==)](https://docs-cortex.paloaltonetworks.com/viewer/attachment/5CAbsl8idaK8R43ZLhoTOw/GTMaqKJ4g8wTHm17qoJxmA-5CAbsl8idaK8R43ZLhoTOw) on the section header to display the description.
5. In the **Timers** tab, for a time tracking header, select the action to take when the timer is triggered (start, stop, or pause).
   * **Timer.start**: The trigger for starting to send a message or survey to recipients. You can change this trigger or add a trigger for Timer.stop or Timer.pause. Select the trigger timer field from the drop down.
   * **Add Trigger**: You can add other trigger timer fields from the drop down.
6. Click **Save**.
