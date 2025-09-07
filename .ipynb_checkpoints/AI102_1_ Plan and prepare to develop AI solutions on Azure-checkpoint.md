# Unit 1

# 1. Introduction

- [ ] ###### <font color='red'>comprehensive AI solutions need to combine </font>

1. ###### machine learning models

2. ###### AI services

3. ###### prompt engineering solutions

4. ###### custom code



- [ ] **Azure AI Foundry**; a comprehensive platform for AI development on Microsoft Azure.



# 2.What is AI?

- [ ] The term "Artificial Intelligence" (AI) covers a wide range of software capabilities that enable applications to exhibit human-like behaviour.

| Capability                                                   | Description                                                  |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| ![Diagram of speech bubbles.](https://learn.microsoft.com/en-us/training/wwl-data-ai/prepare-azure-ai-development/media/generative-ai.png) **Generative AI** | The ability to generate original responses to natural language *<font color='blue'><u>prompts</u></font>*. For example, software for a real estate business might be used to automatically generate property descriptions and advertising copy for a property listing. |
| ![Diagram of a human head with a cog for a brain.](https://learn.microsoft.com/en-us/training/wwl-data-ai/prepare-azure-ai-development/media/agent.png) **Agents** | Generative AI applications that can <u><font color='blue'>respond to user input or assess situations autonomously, and take appropriate actions.</font></u> For example, an "executive assistant" agent could provide details about the location of a meeting on your calendar, or even attach a map or automate the booking of a taxi or rideshare service to help you get there. |
| ![Diagram of an eye being scanned.](https://learn.microsoft.com/en-us/training/wwl-data-ai/prepare-azure-ai-development/media/computer-vision.png) **Computer vision** | The ability <font color='blue'><u>to accept, interpret, and process visual input from images, videos, and live camera streams</u></font>. For example, an automated checkout in a grocery store might use computer vision to identify which products a customer has in their shopping basket, eliminating the need to scan a barcode or manually enter the product and quantity. |
| ![Diagram of a speech bubble and a sound wave.](https://learn.microsoft.com/en-us/training/wwl-data-ai/prepare-azure-ai-development/media/speech.png) **Speech** | The ability <font color='blue'>to recognize and synthesize speech</font>. For example, a digital assistant might enable users to ask questions or provide audible instructions by speaking into a microphone, and generate spoken output to provide answers or confirmations. |
| ![Diagram of a text document.](https://learn.microsoft.com/en-us/training/wwl-data-ai/prepare-azure-ai-development/media/natural-language.png) **Natural language processing** | The ability<font color='blue'> to process natural language in written or spoken form, analyse it, identify key points, and generate summaries or categorizations</font>. For example, a marketing application might analyse social media messages that mention a particular company, translate them to a specific language, and categorize them as positive or negative based on sentiment analysis. |
| ![Diagram of a form containing information.](https://learn.microsoft.com/en-us/training/wwl-data-ai/prepare-azure-ai-development/media/information-extraction.png) **Information extraction** | The ability <font color='blue'>to use computer vision, speech, and natural language processing to extract key information from documents, forms, images, recordings, and other kinds of content</font>. For example, an automated expense claims processing application might extract purchase dates, individual line item details, and total costs from a scanned receipt. |
| ![Diagram of a chart showing an upward trend.](https://learn.microsoft.com/en-us/training/wwl-data-ai/prepare-azure-ai-development/media/prediction.png) **Decision support** | The ability <font color='blue'>to use historic data and learned correlations to make predictions that support business decision making. </font>For example, analysing demographic and economic factors in a city to predict real estate market trends that inform property pricing decisions. |



## A closer look at generative AI

<font color='red'>Generative AI </font>represents the latest advance in artificial intelligence, and deserves some extra attention. Generative AI uses language models to respond <u>to natural language prompts, enabling you to build conversational apps and agents</u> that support research, content creation, and task automation in ways that were previously unimaginable.

![Diagram of a prompt, a language model, and a response.](https://learn.microsoft.com/en-us/training/wwl-data-ai/prepare-azure-ai-development/media/prompt.png)

The language models used in generative AI solutions can be <font color='red'>large language models (LLMs) </font>that have been trained on huge volumes of data and include many <font color='blue'>millions of parameters</font>; or they can be <font color='red'>small language models (SLMs)</font> that are optimized for specific scenarios with lower overhead. <u>Language models commonly respond to text-based prompts with natural language text</u>; though increasingly new *multi-modal* models are able to handle image or speech prompts and respond by generating text, code, speech, or images.





# 3. Azure AI services

Microsoft Azure provides a wide range of <font color='red'>cloud services</font> that you can use to develop, deploy, and manage an AI solution. The most obvious starting point for considering AI development on Azure is Azure AI services; a set of <font color='red'>out-of-the-box prebuilt APIs and models </font> that you can integrate into your applications. The following table lists some commonly used Azure AI services (for a full list of all available Azure AI services, see [Available Azure AI services](https://learn.microsoft.com/en-us/azure/ai-services/what-are-ai-services#available-azure-ai-services?azure-portal=true)).

| Service                                                      | Description                                                  |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| ![Azure OpenAI service icon.](https://learn.microsoft.com/en-us/training/wwl-data-ai/prepare-azure-ai-development/media/open-ai.png) <br>**Azure OpenAI** | <font color='red'>Azure OpenAI</font> in Foundry Models provides access to OpenAI generative AI models including the GPT family of <font color='blue'>large and small language models and DALL-E image-generation models</font> within a scalable and securable cloud service on Azure. |
| ![Azure AI Vision service icon.](https://learn.microsoft.com/en-us/training/wwl-data-ai/prepare-azure-ai-development/media/vision.png) <br/>**Azure AI Vision** | The Azure AI Vision service provides a set of models and APIs that you can use to implement common computer vision functionality in an application. With the AI Vision service, you can <font color='blue'>detect common objects in images, generate captions, descriptions, and tags based on image contents, and read text in images.</font> |
| ![Azure AI Speech service icon.](https://learn.microsoft.com/en-us/training/wwl-data-ai/prepare-azure-ai-development/media/speech-service.png) <br/>**Azure AI Speech** | The Azure AI Speech service provides APIs that you can use **to implement *text to speech* and *speech to text* transformation**, as well as specialized speech-based capabilities like <font color='red'>speaker recognition and translation.</font> |
| ![Azure AI Language service icon.](https://learn.microsoft.com/en-us/training/wwl-data-ai/prepare-azure-ai-development/media/language.png) <br/>**Azure AI Language** | The Azure AI Language service provides models and APIs that you can use to analyze natural language text and perform tasks such as **entity extraction, sentiment analysis, and summarization**. The AI Language service also provides functionality to help you <font color='blue'>build conversational language models and question answering solutions.</font> |
| ![Azure AI Foundry Content Safety service icon.](https://learn.microsoft.com/en-us/training/wwl-data-ai/prepare-azure-ai-development/media/content-safety.png) <br/>**Azure AI Foundry Content Safety** | **Azure AI Foundry Content Safety** provides developers with access to advanced algorithms for <font color='blue'>processing images and text </font>and <font color='blue'>flagging content</font> that is potentially <font color='red'>offensive, risky, or otherwise undesirable.</font> |
| ![Azure AI Translator service icon.](https://learn.microsoft.com/en-us/training/wwl-data-ai/prepare-azure-ai-development/media/translator.png) <br/>**Azure AI Translator** | The Azure AI Translator service uses state-of-the-art language models to translate text between a large number of languages. |
| ![Azure AI Face service icon.](https://learn.microsoft.com/en-us/training/wwl-data-ai/prepare-azure-ai-development/media/face.png) <br/>**Azure AI Face** | The Azure AI Face service is a specialist computer vision implementation that can detect, analyze, and recognize human faces. Because of the potential risks associated with personal identification and misuse of this capability, access to some features of the AI Face service are restricted to approved customers. |
| ![Azure AI Custom Vision service icon.](https://learn.microsoft.com/en-us/training/wwl-data-ai/prepare-azure-ai-development/media/custom-vision.png) <br/>**Azure AI Custom Vision** | The Azure AI Custom Vision service enables you to train and use custom computer vision models for image classification and object detection. |
| ![Azure AI Document Intelligence service icon.](https://learn.microsoft.com/en-us/training/wwl-data-ai/prepare-azure-ai-development/media/document-intelligence.png) <br/>**Azure AI Document Intelligence** | With Azure AI Document Intelligence, you can <font color='blue'>use pre-built or custom models to extract fields from complex documents</font> such as <font color='red'>invoices, receipts, and forms.</font> |
| ![Azure AI Content Understanding service icon.](https://learn.microsoft.com/en-us/training/wwl-data-ai/prepare-azure-ai-development/media/content-understanding.png) <br/>**Azure AI Content Understanding** | **The Azure AI Content Understanding service** provides multi-modal content analysis capabilities that enable you to build models to <font color='red'>extract data from forms and documents, images, videos, and audio streams.</font> |
| ![Azure AI Search service icon.](https://learn.microsoft.com/en-us/training/wwl-data-ai/prepare-azure-ai-development/media/search.png) <br/>**Azure AI Search** | The Azure AI Search service uses a pipeline of AI skills based on other Azure AI Services and custom code to extract information from content and create a searchable index. AI Search is commonly used to create vector indexes for data that can then be used to *ground* prompts submitted to generative AI language models, such as those provided in Azure OpenAI. |



## Single service or multi-service resource?

Most Azure AI services, such as **Azure AI Vision**, **Azure AI Language**, and so on, can be provisioned as standalone resources, enabling you to create only the Azure resources you specifically need. Additionally, standalone Azure AI services often include a free-tier SKU with limited functionality, enabling you to evaluate and develop with the service at no cost. Each standalone Azure AI resource provides an endpoint and authorization keys that you can use to access it securely from a client application.

Alternatively, you can provision a multi-service resource that encapsulates multiple AI services in a single Azure resource. Using a multi-service resource can make it easier to manage applications that use multiple AI capabilities. There are two multi-service resource types you can use:



![Azure AI service icon.](https://learn.microsoft.com/en-us/training/wwl-data-ai/prepare-azure-ai-development/media/cognitive-services.png)
**Azure AI services**

The Azure AI Services resource type includes the following services, making them available from a single endpoint:

- Azure AI Speech
- Azure AI Language
- Azure AI Translator
- Azure AI Vision
- Azure AI Face
- <font color='red'>Azure AI Custom Vision</font>
- Azure AI Document Intelligence



![Azure AI Foundry icon.](https://learn.microsoft.com/en-us/training/wwl-data-ai/prepare-azure-ai-development/media/ai-services.png)
**Azure AI Foundry**

The Azure AI Foundry resource type includes the following services, and supports working with them through an Azure AI Foundry project:

- <font color='blue'>Azure OpenAI</font>
- Azure AI Speech
- Azure AI Language
- <font color='blue'>Azure AI Foundry Content Safety</font>
- Azure AI Translator
- Azure AI Vision
- Azure AI Face
- Azure AI Document Intelligence
- <font color='blue'>Azure AI Content Understanding</font>

# 4. Azure AI Foundry

**Azure AI Foundry is a platform for AI development on Microsoft Azure**. While you *can* provision individual Azure AI services resources and build applications that consume them without it, the project organization, resource management, and AI development capabilities of Azure AI Foundry makes it the recommended way to build all but the most simple solutions.

Azure AI Foundry provides the ***Azure AI Foundry portal***, a web-based visual interface for working with AI projects. It also provides the ***Azure AI Foundry SDK***, which you can use to build AI solutions programmatically.

## Azure AI Foundry projects

In Azure AI Foundry, you manage the resource connections, data, code, and other elements of the AI solution in *projects*. There are two kinds of project:

- [ ] ### Foundry projects

![Diagram of a Foundry project.](https://learn.microsoft.com/en-us/training/wwl-data-ai/prepare-azure-ai-development/media/foundry-project.png)

*Foundry projects* are associated with an **Azure AI Foundry** resource in an Azure subscription. Foundry projects provide support for Azure AI Foundry models (including OpenAI models), Azure AI Foundry Agent Service, Azure AI services, and tools for evaluation and responsible AI development.

An Azure AI Foundry resource supports the most common AI development tasks to develop generative AI chat apps and agents. In most cases, using a Foundry project provides the right level of resource centralization and capabilities with a minimal amount of administrative resource management. You can use Azure AI Foundry portal to work in projects that are based in Azure AI Foundry resources, making it easy to add connected resources and manage model and agent deployments.

- [ ] ### Hub-based projects

![Diagram of a hub-based project.](https://learn.microsoft.com/en-us/training/wwl-data-ai/prepare-azure-ai-development/media/hub-project.png)

*Hub-based projects* are associated with an **Azure AI hub** resource in an Azure subscription. Hub-based projects include an Azure AI Foundry resource, as well as managed compute, support for Prompt Flow development, and connected **Azure storage** and **Azure key vault** resources for secure data storage.

Azure AI hub resources support advanced AI development scenarios, like developing Prompt Flow based applications or fine-tuning models. You can also use Azure AI hub resources in both Azure AI Foundry portal and Azure Machine learning portal, making it easier to work on collaborative projects that involve data scientists and machine learning specialists as well as developers and AI software engineers



# 5.Developer tools and SDKs

While you can perform many of the tasks needed to develop an AI solution directly in the Azure AI Foundry portal, developers also need to write, test, and deploy code.



## Development tools and environments

There are many development tools and environments available, and developers should choose one that supports the languages, SDKs, and APIs they need to work with and with which they're most comfortable. For example, a developer who focuses strongly on building applications for Windows using the .NET Framework might prefer to work in an integrated development environment (IDE) like <font color='red'>Microsoft Visual Studio</font>. Conversely, a web application developer who works with a wide range of open-source languages and libraries might prefer to use a code editor like <font color='red'>Visual Studio Code (VS Code)</font>. Both of these products are suitable for developing AI applications on Azure.



## The Azure AI Foundry for Visual Studio Code extension

When developing Azure AI Foundry based generative AI applications in Visual Studio Code, you can use the Azure AI Foundry for Visual Studio Code extension to simplify key tasks in the workflow, including:

- Creating a project.
- Selecting and deploying a model.
- Testing a model in the playground.
- Creating an agent.



GitHub and GitHub Copilot

<font color='blue'>GitHub</font> is the world's most popular platform for source control and DevOps management, and can be a critical element of any team development effort. Visual Studio and VS Code both provide native integration with GitHub, and access to <font color='blue'>GitHub Copilot</font>; an AI assistant that can significantly improve developer productivity and effectiveness.

## Programming languages, APIs, and SDKs

You can develop AI applications using many common programming languages and frameworks, including Microsoft C#, Python, Node, TypeScript, Java, and others. When building AI solutions on Azure, some common SDKs you should plan to install and use include:

- The **[Azure AI Foundry SDK](https://learn.microsoft.com/en-us/azure/ai-studio/how-to/develop/sdk-overview)**, which enables you to write code to connect to Azure AI Foundry projects and access resource connections, which you can then work with using service-specific SDKs.
- The **[Azure AI Foundry Models API](https://learn.microsoft.com/en-us/rest/api/aifoundry/modelinference/)**, which provides an interface for working with generative AI model endpoints hosted in Azure AI Foundry.
- The **[Azure OpenAI in Azure AI Foundry Models API](https://learn.microsoft.com/en-us/azure/ai-services/openai/reference)**, which enables you to build chat applications based on OpenAI models hosted in Azure AI Foundry.
- **[Azure AI Services SDKs](https://learn.microsoft.com/en-us/azure/ai-services/reference/sdk-package-resources)** - AI service-specific libraries for multiple programming languages and frameworks that enable you to consume Azure AI Services resources in your subscription. You can also use Azure AI Services through their [REST APIs](https://learn.microsoft.com/en-us/azure/ai-services/reference/rest-api-resources).
- The **[Azure AI Foundry Agent Service](https://learn.microsoft.com/en-us/azure/ai-services/agents/overview)**, which is accessed through the Azure AI Foundry SDK and can be integrated with frameworks like [Semantic Kernel](https://learn.microsoft.com/en-us/semantic-kernel/overview) to build comprehensive AI agent solutions.

# 6.Responsible AI

It's important for software engineers to consider the impact of their software on users, and society in general; including considerations for its responsible use. When the application is imbued with artificial intelligence, these considerations are particularly important due to the nature of how AI systems work and inform decisions; often based on probabilistic models, which are in turn dependent on the data with which they were trained.

The human-like nature of AI solutions is a significant benefit in making applications user-friendly, but it can also lead users to place a great deal of trust in the application's ability to make correct decisions. The potential for harm to individuals or groups through incorrect predictions or misuse of AI capabilities is a major concern, and software engineers building AI-enabled solutions should apply due consideration to mitigate risks and ensure <font color='red'>fairness, reliability, and adequate protection from harm or discrimination</font>.

Let's discuss some core principles for responsible AI that have been adopted at Microsoft.

## Reliability and safety

![A diagram of a shield.](https://learn.microsoft.com/en-us/training/wwl-data-ai/prepare-azure-ai-development/media/reliability-safety.png)

<font color='red'>AI systems should perform reliably and safely.</font> For example, consider an AI-based software system for an autonomous vehicle; or a machine learning model that diagnoses patient symptoms and recommends prescriptions. Unreliability in these kinds of system can result in substantial risk to human life.

As with any software, AI-based software application development must be subjected to rigorous testing and deployment management processes to ensure that they work as expected before release. Additionally, software engineers need to take into account the probabilistic nature of machine learning models, and apply appropriate thresholds when evaluating confidence scores for predictions.

## Privacy and security

![A diagram of a padlock.](https://learn.microsoft.com/en-us/training/wwl-data-ai/prepare-azure-ai-development/media/privacy-security.png)

<font color='red'>AI systems should be secure and respect privacy. </font>The machine learning models on which AI systems are based rely on large volumes of data, which may contain personal details that must be kept private. Even after models are trained and the system is in production, they use new data to make predictions or take action that may be subject to privacy or security concerns; so appropriate safeguards to protect data and customer content must be implemented.

## Inclusiveness

![A diagram of a diverse group of people.](https://learn.microsoft.com/en-us/training/wwl-data-ai/prepare-azure-ai-development/media/inclusiveness.png)

<font color='red'>AI systems should empower everyone and engage people.</font> AI should bring benefits to all parts of society, regardless of physical ability, gender, sexual orientation, ethnicity, or other factors.

One way to optimize for inclusiveness is to ensure that the design, development, and testing of your application includes input from as diverse a group of people as possible.

## Transparency

![A diagram of an eye.](https://learn.microsoft.com/en-us/training/wwl-data-ai/prepare-azure-ai-development/media/transparency.png)

<font color='red'>AI systems should be understandable. </font>Users should be made fully aware of the purpose of the system, how it works, and what limitations may be expected.

For example, when an AI system is based on a machine learning model, you should generally make users aware of factors that may affect the accuracy of its predictions, such as the number of cases used to train the model, or the specific features that have the most influence over its predictions. You should also share information about the confidence score for predictions.

When an AI application relies on personal data, such as a facial recognition system that takes images of people to recognize them; you should make it clear to the user how their data is used and retained, and who has access to it.

## Accountability

![A diagram of a handshake.](https://learn.microsoft.com/en-us/training/wwl-data-ai/prepare-azure-ai-development/media/accountability.png)

<font color='red'>People should be accountable for AI systems. </font>Although many AI systems seem to operate autonomously, ultimately it's the responsibility of the developers who trained and validated the models they use, and defined the logic that bases decisions on model predictions to ensure that the overall system meets responsibility requirements. To help meet this goal, designers and developers of AI-based solution should work within a framework of governance and organizational principles that ensure the solution meets responsible and legal standards that are clearly defined.
