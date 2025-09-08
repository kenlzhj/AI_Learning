# Develop an AI app with the Azure AI Foundry SDK

Use the Azure AI Foundry SDK to develop AI applications with Azure AI Foundry projects.

## Learning objectives

After completing this module, you'll be able to:

- Describe capabilities of the Azure AI Foundry SDK.
- Use the Azure AI Foundry SDK to work with connections in projects.
- Use the Azure AI Foundry SDK to develop an AI chat app.

# Introduction

Developers creating AI solutions with Azure AI Foundry need to work with a combination of services and software frameworks. The Azure AI Foundry SDK is designed to bring together common services and code libraries in an AI project through a central programmatic access point, making it easier for developers to write the code needed to build effective AI apps on Azure.

In this module, you'll learn how to use the Azure AI Foundry SDK to work with resources in an AI project.



# What is the Azure AI Foundry SDK?

Azure AI Foundry provides a REST API that you can use to work with AI Foundry projects and the resources they contain. Additionally, multiple language-specific SDKs are available, enabling developers to write code that uses resources in an Azure AI Foundry project in their preferred development language. With an Azure AI Foundry SDK, developers can create applications that connect to a project, access the resource connections and models in that project, and use them to perform AI operations, such as sending prompts to a generative AI model and processing the responses.

The core package for working with projects is the **Azure AI Projects** library, which enables you to connect to an Azure AI Foundry project and access the resources defined within it. Available language-specific packages the for Azure AI Projects library include:

- [Azure AI Projects for Python](https://pypi.org/project/azure-ai-projects)
- [Azure AI Projects for Microsoft .NET](https://www.nuget.org/packages/Azure.AI.Projects)
- [Azure AI Projects for JavaScript](https://www.npmjs.com/package/@azure/ai-projects)



To use the Azure AI Projects library in Python, you can use the **pip** package installation utility to install the **azure-ai-projects** package from PyPi:

```
pip install azure-ai-projects
```

## Using the SDK to connect to a project

The first task in most Azure AI Foundry SDK code is to connect to an Azure AI Foundry project. Each project has a unique *endpoint*, which you can find on the project's **Overview** page in the Azure AI Foundry portal.



**<font color='red'>Note</font>**

The project provides multiple endpoints and keys, including:

- An endpoint for the project itself; which can be used to access project connections, agents, and models in the Azure AI Foundry resource.
- An endpoint for Azure OpenAI Service APIs in the project's Azure AI Foundry resource.
- An endpoint for Azure AI services APIs (such as Azure AI Vision and Azure AI Language) in the Azure AI Foundry resource.