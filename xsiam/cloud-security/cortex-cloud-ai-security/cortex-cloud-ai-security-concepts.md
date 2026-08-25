---
description: >-
  Learn Cortex Cloud AI Security concepts in Cortex XSIAM, including AI assets,
  risks, and findings.
---

# Cortex Cloud AI Security concepts

{% hint style="info" %}
This feature is included with a Cortex XSIAM Premium license. It is also included with any other Cortex XSIAM license that has the Cloud Posture Security or Cloud Runtime Security add-on.
{% endhint %}

#### Introduction to AI applications

The AI application ecosystem comprises several critical components that work together to enable the functionality of AI-driven applications. The following explains the main concepts and shows some examples.

<details>

<summary>Model</summary>

The model is the core component of the AI ecosystem. It is the trained machine learning model that takes input data, processes it, and produces output. In the context of large language models (LLMs), this involves understanding and generating human-like text based on the given input.

OpenAI GPT-4 model, which can generate coherent and contextually relevant text, answer questions, and perform various other natural language processing tasks.

</details>

<details>

<summary>Model endpoint</summary>

The model endpoint is the interface through which applications interact with the AI model. It acts as an access point for sending inputs to the model and receiving outputs. The endpoint is responsible for managing requests, routing them to the appropriate model instance, and returning the results to the application.

A Microsoft Azure OpenAI deployment using OpenAI GPT-4, which you can use to integrate natural language processing capabilities into your applications by sending text prompts and receiving generated text in response.

Amazon Web Services (AWS) EC2 instances with GPU acceleration running Llama2 by Meta, which supports an application that communicates with the EC2 instance.

</details>

<details>

<summary>Plugin</summary>

A plugin is an auxiliary but highly capable model or tool that acts as a helper to the primary AI model. Plugins extend the functionality of the main model by providing specialized capabilities, such as accessing inference datasets, performing specific computations, or interfacing with other services. This approach, known as retrieval-augmented generation (RAG), enhances the primary model's ability to generate more accurate and contextually relevant outputs. For more information, see [Inference datasets](#UUID-6e61b890-1b68-9f51-20e6-135d5465d8ee_section-idm234761053923993) and [Retrieval-Augmented Generation](#UUID-6e61b890-1b68-9f51-20e6-135d5465d8ee_section-idm234761105802593).

A weather plugin integrated with an AI chatbot that allows the chatbot to fetch and provide real-time weather updates based on user queries. Another example is a language translation plugin that helps the main model translate text between different languages.

</details>

<details>

<summary>Training datasets</summary>

Training is a fundamental stage in the AI development process where the model learns to perform its tasks by processing large amounts of data. During this phase, the model is exposed to various examples and adjusts its internal parameters to minimize errors in predictions or classifications. The dataset is an integral part of the process, with the insights learned by the model influenced by the training data.

Training a model like GPT-4 involves using vast text corpora from various sources to help the model understand language patterns, context, and nuances, enabling it to generate coherent and contextually relevant text.

</details>

<details>

<summary>Inference datasets</summary>

Inference datasets are specialized collections of data used during the inference phase of AI models, which is the stage where the model makes predictions or generates outputs based on new input data. Unlike training datasets, which are used to teach the model how to understand and process information, inference datasets help improve the model's performance by providing realistic, real-world data inputs for better contextual answering.

When building a chatbot for customers to learn more about their spending habits, financial institutions use customer transactions as inference data to provide contextually accurate answers.

</details>

<details>

<summary>Fine-tuning</summary>

Fine-tuning in machine learning refers to the process of adapting a pre-trained model to perform specific tasks or cater to particular use cases. This technique has become essential in deep learning, especially for training foundation models used in generative AI. Fine-tuning leverages data (similarly to training) to adjust the responses of the model to certain inputs, making it more suitable for the intended business case.

</details>

<details>

<summary>Retrieval-Augmented Generation</summary>

Retrieval-Augmented Generation (RAG) enhances large language model (LLM) responses by incorporating information from knowledge bases and other sources. This allows the model to reference up-to-date inference data before generating a response, improving contextual accuracy. This approach is cost-effective and ensures the output remains relevant, accurate, and useful across different contexts.

</details>

<details>

<summary>Example scenario: AI-powered customer support chatbot</summary>

To illustrate how these components work together, consider an AI-powered customer support chatbot:

![AI\_security\_concepts\_1.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-573734ef610085566019f74fa84c41ca5c1672df%2F1c1f16306c2221ea26e4808e480bb2419acbb6c0bde60c112055c8d3689673a5.png?alt=media)

* **Model endpoint:** The chatbot application interacts with the GPT-4 model through the Azure OpenAI Deployment, which serves as the model endpoint. This endpoint handles user queries, processes them, and directs them to the GPT-4 model to generate responses.
* **Model:** The GPT-4 model receives the user's query, processes it, and generates a relevant and contextually appropriate response based on the information and nuances provided in the query.
* **Plugin:** The chatbot integrates a customer database plugin that allows it to fetch user-specific inference data, such as order status or account details, to provide more personalized and accurate support. The customer database used by the plugin is the Inference Dataset.
* **Training dataset:** The chatbot undergoes fine-tuning using a dataset of previous customer interactions and support tickets, making it adept at handling common inquiries and issues in the specific industry.
* **Application:** The customer support platform integrates the chatbot with a user-friendly interface.

</details>
