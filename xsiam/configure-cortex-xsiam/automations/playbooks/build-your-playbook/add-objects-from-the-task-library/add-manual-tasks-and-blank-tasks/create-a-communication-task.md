---
description: >-
  Create communication tasks in Cortex XSIAM playbooks for notifications and
  collaboration.
---

# Create a communication task

Communication tasks enable you to send surveys to users, both internal and external, to collect data for an issue. The collected data can be used for issue analysis, and also as input for subsequent playbook tasks. For example, you can send a scheduled survey requesting analysts to send specific issue updates or send a single (stand-alone) question survey to determine how an issue was handled.

There are two types of communication tasks:

* **Ask tasks**: A conditional task that sends a single question survey. The answer is used to determine how the playbook proceeds.
* **Data collection tasks**: A data collection task sends a survey of one or more questions. The answers are recorded in context data and can be used as input for subsequent tasks.

<details>

<summary>Create an ask task in Cortex XSIAM</summary>

An ask task is a type of conditional task that sends a single question survey, the answer to which determines how a playbook proceeds. If you send the survey to multiple users, the first answer received is used, and subsequent responses are disregarded. For more information about ask task settings, see [Create a conditional task](create-a-conditional-task).

Because this is a conditional task, you need to create a condition for each of the answers. For example, if the survey answers include, **`Yes, No, and Maybe`**, there should be a corresponding condition (path) in the playbook for each of these answers.

Users interact with the survey directly from the message, meaning the question appears in the message and they click an answer from the message.

The survey question and the first response is recorded in the issue context data. This enables you to use this response as the input for subsequent playbook tasks.

For all ask conditional tasks, a link is generated for each possible answer the recipient can select. If the survey is sent to more than one user, a unique link is created for each possible answer for each individual recipient. These links are visible in the context data of the issue's Work Plan. The links appear under Ask.Links in the context data.

In this example, the message and survey will be sent to recipients every hour for six hours, until a reply is received (it is repeated every 60 minutes, 6 times). The SLA is six hours. If the SLA is breached, the playbook will proceed according to the Yes condition.

The SLA is six hours. If the SLA is breached, the playbook will proceed

![ask-timer.png](https://paloaltonetworks.fluidtopics.net/api/khub/maps/5CAbsl8idaK8R43ZLhoTOw/resources/yeqUDjXQYR7A1CLYidWTZA-5CAbsl8idaK8R43ZLhoTOw/content?v=1a7ca3cd9c24b294\&Ft-Calling-App=ft/turnkey-portal)<br>

In this example, a message and survey are sent by email to all users with the Analyst role. We are not including a message body because the message subject is the survey question we want recipients to answer. There are three reply options, Yes, No, and Not sure. In the playbook, we will only add conditions for the Yes and No replies. We require recipient authentication, which first involves setting up authentication.

We require recipient authentication, which first involves setting up authentication.

![ask-task-example-email-8-4.png](https://paloaltonetworks.fluidtopics.net/api/khub/maps/5CAbsl8idaK8R43ZLhoTOw/resources/loHWMiMUko2aguwYgiuPRQ-5CAbsl8idaK8R43ZLhoTOw/content?v=fd28f60fe02fcbad\&Ft-Calling-App=ft/turnkey-portal)

</details>

<details>

<summary>Create a data collection task in Cortex XSIAM</summary>

The data collection task is a multi-question survey (form) that survey recipients access from a link in the message. Users do not need to log in to access the survey, which is located on a separate site.

All responses are collected and recorded in the issue context data, whether you receive responses from a single user or multiple users. This enables you to use the survey questions and answers as input for subsequent playbook tasks. If responses are received from multiple users, data for multi-select fields and grid fields are aggregated. For all other field types, the response received most recently will override previous responses as it displays in the field. All responses are always available in the context data.

For all data collection tasks, a single link is generated for each recipient of the survey. These links are visible in the context data of the issue's Work Plan. The links appear in the context data under the Links section of that survey.

You can include the following types of questions in the survey.

* Stand alone questions. These are presented to users directly in the message, and from which users answer directly in the message (not an external survey).
* Field-based questions. These are based on a specific issue field (either system or custom), for example, an Asset ID field. The response (data) received for these fields automatically populates the field for this issue. For single-select field based questions, the default option is taken from the field’s defined default.

How to create a Data Collection task

1. From the Task Library pane, click the task you want, for example Blank Task.
2. In the Task Details pane, select the Data Collection Task Type.
3. Enter a meaningful name in the Task Name field for the task that corresponds to the data you are collecting.
4.  Select the communication options you want to use to collect the data.

    Tabs and configuration fields

    | Tab       | Configuration fields in the tab                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
    | --------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | Message   | <ul><li><p>Ask by: The method for sending the message and survey. Options are:</p><ul><li>Task (can always be completed directly in the Workplan)</li><li>Generated link (appears in the context data): A link to the data collection survey is available in the context data of the task.</li><li>Email: If you select this option, enter below the subject and message of the email and the email addresses of the users who should receive this message or survey.</li></ul></li><li><p>To: The message and survey recipients. You can define by:</p><ul><li>Selecting from a predefined drop down list.</li><li>Manually typing email addresses for users and/or external users.</li><li>Clicking the context icon to define recipients from a context data source.</li></ul></li><li>CC of the email: A CC email address.</li><li>Subject of the email: The message subject that displays to message recipients. You can write the survey question in the subject field or in the message body field.</li><li>Message body: The message question body to be used in the notification sent to the given users along with the reply options.</li><li>Require users to authenticate: Enable this option to have your SAML or AD authenticate the recipient before allowing them to answer. You must first set up an authentication integration instance and check Use this instance for external users authentication only in the integration instance settings.</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
    | Questions | <ul><li>Web Survey Title: The title displayed for the web survey.</li><li>Short Description: A description displayed above the questions on the web survey. Click Preview to see how it displays.</li><li>Question: A question to ask recipients.</li><li><p>Answer Type: The field type for the answer field. Options are:</p><ul><li>Short text</li><li>Long text</li><li>Number</li><li>Single Select (requires you to define a reply option)</li><li>Multi select/Array (requires you to define a reply option)</li><li>Date picker</li><li>Attachments</li></ul></li><li>Mandatory: If this checkbox is selected for a question, survey recipients will not be able to submit the survey until they answer this question.</li><li>Help Message: The message that displays when users hover over the question mark help button for the survey question.</li><li>Placeholder: A sample value displayed until a real value is entered.</li></ul><p>You can drag questions to rearrange the order in which they display in the survey.</p>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
    | Timing    | <ul><li>Retry interval (minutes): Determines the wait time between each execution of a command. For example, the frequency (in minutes) that a message and survey are resent to recipients before the response is received.</li><li><p>Number of retries: Determines how many times a command attempts to run before generating an error. For example, the maximum number of times a message is sent. If a reply is received, no additional retry messages will be sent.</p><p>Retries are not supported for data collection tasks that have errors sending emails (indicated by a server timeout). This is because retries only work on automation execution failures, not on email delivery issues.</p></li><li>Task SLA: Set the SLA in granularity of weeks, days, and hours.</li><li>Set task Reminder at: Set a task reminder in granularity of weeks, days, and hours.</li><li><p>Complete automatically if:</p><ul><li>Reached task SLA (with or without a reply): This option is grayed out.</li><li>Received &#x3C;enter a number> reply</li></ul></li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
    | Details   | <ul><li>Tag the result with: Add a tag to the task result. You can use the tag to filter entries in the War Room.</li><li>Task description (Markdown supported): Describe what this task does. You can enter objects from the context data in the description. For example, in a communication task, you can use the recipient’s email address. The value for the object is based on what appears in the context every time the task runs.</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
    | Advanced  | <ul><li><strong>Register as case timeline record</strong>: If enabled, the results of the task execution appear as a record in the case timeline. If enabled, you must enter a <strong>Record name.</strong> You have the option of adding an <strong>Effective time</strong>, <strong>Description</strong>, <strong>Tags</strong>, and marking the record as evidence and adding an evidence comment.<br><strong>NOTE</strong>: Only enter an <strong>Effective time</strong> if you want the same exact time recorded every time the playbook task executes.</li><li><strong>Using</strong>: Choose which integration instance will execute the command, or leave empty to use all integration instances.</li><li><strong>Extend context</strong>: Append the extracted results of the action to the context. For example, "newContextKey1=path1::newContextKey2=path2" returns "[path1:'aaa',path2: 'bbb', newContexKey1: 'aaa',newContextKey2:'bbb']"</li><li><strong>Ignore outputs:</strong> If set to true, will not store outputs into the context (besides the extended outputs).</li><li><strong>Execution timeout (seconds):</strong> Sets the command execution timeout in seconds.</li><li><p><strong>Indicator Extraction mode:</strong> Choose when to extract indicators:</p><ul><li>None: Do not perform indicator extraction</li><li>Inline: Before other playbook tasks</li><li>Out of band: While other tasks are running</li></ul></li><li><strong>Mark results as note</strong></li><li><strong>Mark results as evidence</strong></li><li><strong>Run without a worker</strong></li><li><strong>Skip this branch if this script/playbook is unavailable</strong></li><li><strong>Quiet Mode:</strong> When in quiet mode, tasks do not display inputs and outputs or extract indicators. Errors and warnings are still documented. You can turn quiet mode on or off at the task or playbook level.</li></ul> |
5.  (Optional) To customize the look and feel of your email message, click Preview.

    You can determine the color scheme and how the text in the message header and body appear, as well as the appearance and text of the button the user clicks to submit the survey.

    If you configured a custom logo in server settings, it will appear in the preview.

    When customizing HTML for data collection emails, do not apply CSS styles directly to the **`<body>`** tag. Cortex XSIAM injects your HTML as a fragment into an existing email template and removes the **`<body>`** tag to ensure valid HTML structure. Any styles applied to the **`<body>`** tag will be lost. To ensure your formatting renders correctly, wrap your content in a container element such as a **`<div>`** or **`<span>`** and apply your styles to that container.

    ```
    <body>
        <div style="font-family: sans-serif;">Content</div>
    </body>
    ```
6.  Click Save.

    The task is added in the playbook editor.

    A user icon ( [![user\_icon.png](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABUAAAAUCAYAAABiS3YzAAAACXBIWXMAAA7EAAAOxAGVKw4bAAAAB3RJTUUH6QEcCjYkYrjRDwAAAAd0RVh0QXV0aG9yAKmuzEgAAAAMdEVYdERlc2NyaXB0aW9uABMJISMAAAAKdEVYdENvcHlyaWdodACsD8w6AAAADnRFWHRDcmVhdGlvbiB0aW1lADX3DwkAAAAJdEVYdFNvZnR3YXJlAF1w/zoAAAALdEVYdERpc2NsYWltZXIAt8C0jwAAAAh0RVh0V2FybmluZwDAG+aHAAAAB3RFWHRTb3VyY2UA9f+D6wAAAAh0RVh0Q29tbWVudAD2zJa/AAAABnRFWHRUaXRsZQCo7tInAAACw0lEQVQ4ja2Tz29UVRTHP+fe9+6bEehMW4hI1IRMW4YU40JDIMbEhSt3JEYXIq7cuHbBhiVhZViY8C8Q/wJNXLGAoEL9kWjCggabaqcj1A5lZvre3HePizdl5nVaY8CTvJdzc879fr/nm3NFVTWEHEKGyTugKaA8a3S6hiiEACHF+PZzge2Ecw6jwSN5538BBMjznAgU0XT/Lg0FoQJC8RPZOewHyt4qNaDpJv6vJfzaLUKvjbgp7Owp4pfOYg6+AibaE1SytK9xWNtVyfAPf6K/9AX5+h2wMWIcaI7mKebAMdzJC7i59zFJvXT14UZajF8WOMC3btO7dRHttpDqYZLmeVzzE8LGr2z/eBXfvkv685fo9iMqr32GuEMjPctfYUIYB1X0ySrpL9fQbgsAW2uQnDiPSWpEL57GNc4VndkWgwdfM/j9m6HvQwRVjOoIVH2Kby/h178f8RiH7IxoIrCVp6WwtYJfu0notcZkgSnN7rv49t2yv75H6K0PSftotlm2f2uF0FkeU8oupWFA6LZKl8KTPxisfFvknfsMVm+U6pptEdIRkQJGdq+bsaPcVpDKzHAvgZCD2MIOMU8tEROP02DGhCK2gq3PF3l8kPjVd6mevUzS/LjgOPI6L7x1heTUp8WeimAqs0j1yBiolD2V+ADR0TOIq2FmmlTfvIidXii8HH7ipkjmP8QtfIDEU9j6PLZ2vDRs+UmYGDvdJD7+Hvnf9xj8eROZ8AfQQHj8ADtzkujld5Bk+l9AAVM9TNK8QP/OFbZ/uIxmjydBbYKtz+FOfER09MxEefLxisHW56ievkR27zp+/Ts07aB5iohB3CFMfQHXOEd87G2w7j+AAojF1hpU3vicsHmffOM3wvYGEiXYWgM7s1hsxYQtCqpEe1k2wq5gZxexs4v7N42Fz7oE3y+v1HOFKv1Hy2SdVf4BnlIpDjqxOdoAAAAASUVORK5CYII=)](https://docs-cortex.paloaltonetworks.com/viewer/attachment/5CAbsl8idaK8R43ZLhoTOw/pGUex5j8fb50MJRq0seibw-5CAbsl8idaK8R43ZLhoTOw)) indicates the task requires manual input.
7. Connect the tasks you've added in their logical order by dragging and dropping a wire from one task to another.
8. Save the playbook.

<br>

</details>

<details>

<summary>View Cortex XSIAM data collection task examples</summary>

Stand-alone question with a single-select answer

In this example, we create a stand-alone question with a single-select answer. This question is not mandatory. If we select the **First option is default** checkbox, the reply option "0" is the default value in the answer field.

![data-collection-eg.png](https://paloaltonetworks.fluidtopics.net/api/khub/maps/5CAbsl8idaK8R43ZLhoTOw/resources/htceTUvEISzoCM_GHAJ0wQ-5CAbsl8idaK8R43ZLhoTOw/content?v=5d88ad644d2dee03\&Ft-Calling-App=ft/turnkey-portal)

In this example, create a question based on a custom issue field that is marked as mandatory. You can add a question based on a field. To add a field, click the **Add Question based on field**

</details>

<details>

<summary>Configure Cortex XSIAM communication task authentication</summary>

When sending a form in a communication task, you can configure user authentication to ensure only authorized users gain access to the form.

The authorized users are usually external users not in Cortex XSIAM, and they will not be able to access anything else in Cortex XSIAM.

Set up playbook communication task authentication

1. Set up your SSO if it is not already configured. See [Authenticate users using SSO](../../../../../../onboard-cortex-xsiam/deployment-steps/set-up-authentication/authenticate-users-using-sso) for more details.
2.  In the Task details of your playbook communication task, check **Require users to authenticate** to have your SAML or AD authenticate the recipient before allowing them access to the form.

    ![playbook-comm-task-authenticate-2.png](https://paloaltonetworks.fluidtopics.net/api/khub/maps/5CAbsl8idaK8R43ZLhoTOw/resources/5BYS3karytnXCEKur3S59w-5CAbsl8idaK8R43ZLhoTOw/content?v=d913ac2050c4b630\&Ft-Calling-App=ft/turnkey-portal)

    [![playbook-comm-task-authenticate-2.png](https://docs-cortex.paloaltonetworks.com/api/khub/maps/5CAbsl8idaK8R43ZLhoTOw/resources/5BYS3karytnXCEKur3S59w-5CAbsl8idaK8R43ZLhoTOw/content?v=d913ac2050c4b630\&Ft-Calling-App=ft/turnkey-portal)](https://docs-cortex.paloaltonetworks.com/viewer/attachment/5CAbsl8idaK8R43ZLhoTOw/5BYS3karytnXCEKur3S59w-5CAbsl8idaK8R43ZLhoTOw)

</details>

<details>

<summary>Configure NGINX for Cortex XSIAM data collection email links</summary>

If you are using NGINX as a reverse proxy with SSL termination, configure the NGINX configuration file to enable accessing data collection links in emails.

1. Navigate to `/etc/nginx/sites-available/` and open the NGINX configuration file.
2.  Update the file with the following configurations:

    ```
    server {
    	listen 443 ssl;
    	server_name <PROXY DOMAIN>;


    	ssl_certificate <path to CRT file>;
    	ssl_certificate_key <path to KEY file>;
    	ssl_protocols TLSv1.2 TLSv1.3;
    	ssl_ciphers 'ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384';
    	ssl_prefer_server_ciphers on;


    	location / {
    		proxy_pass https://<XSOAR DOMAIN>;
    		proxy_cookie_domain <XSOAR DOMAIN> <PROXY DOMAIN>;
    		proxy_pass_header Set-Cookie;
    		proxy_set_header X-Real-IP $remote_addr;
    		proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    		proxy_set_header X-Forwarded-Proto $scheme;
    		}

    	} 
    ```

</details>
