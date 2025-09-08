## <font color='red'>Learning objectives</font>

By the end of this module, you'll be able to:

- Select a language model from the model catalog.
- Deploy a model to an endpoint.
- Test a model and improve the performance of the model.



# Introduction

Generative AI applications are built on *language models*. The development process usually starts with an exploration and comparison of available *foundation* models to find the one that best suits the particular needs of your application. After selecting a suitable model, you deploy it to an endpoint where it can be consumed by a client application or AI agent.

Foundation models, such as the GPT family of models, are state-of-the-art language models designed to understand, generate, and interact with natural language. Some common use cases for models are:

- Speech-to-text and text-to-speech conversion. For example, generate subtitles for videos.
- Machine translation. For example, translate text from English to Japanese.
- Text classification. For example, label an email as spam or not spam.
- Entity extraction. For example, extract keywords or names from a document.
- Text summarization. For example, generate a short one-paragraph summary from a multi-page document.
- Question answering. For example, provide answers to questions like "What is the capital of France?"
- Reasoning. For example, solve a mathematical problem.



**<font color='blue'>Note</font>**

The latest breakthrough in generative AI models is owed to the development of the **Transformer** architecture. Transformers were introduced in the [*Attention is all you need* paper by Vaswani, et al. from 2017](https://arxiv.org/abs/1706.03762). The Transformer architecture provided two innovations to NLP that resulted in the emergence of foundation models:

- Instead of processing words sequentially, Transformers process each word independently and in parallel by using **attention**.
- Next to the semantic similarity between words, Transformers use **positional encoding** to include the information about the position of a word in a sentence.





# Explore the model catalog

The *model catalog* in Azure AI Foundry provides a central repository of models that you can browse to find the right language model for your particular generative AI use case.



## Can AI *solve* my use case?

To start answering this question, you need to discover, filter, and deploy a model. You can explore the available language models through three different catalogs:

- [**Hugging Face**](https://huggingface.co/models): Vast catalog of open-source models across various domains.
- [**GitHub**](https://github.com/marketplace/models-github): Access to diverse models via GitHub Marketplace and GitHub Copilot.
- [**Azure AI Foundry**](https://ai.azure.com/explore/models): Comprehensive catalog with robust tools for deployment.

### Choose between large and small language models

First of all, you have a choice between <font color='blue'>Large Language Models (LLMs)</font> and <font color='blue'>Small Language Models (SLMs)</font>.

- <font color='red'>LLMs</font> like GPT-4, Mistral Large, Llama3 70B, Llama 405B, and Command R+ are powerful AI models designed for tasks that require deep reasoning, complex content generation, and extensive context understanding.
- <font color='red'>SLMs</font> like Phi3, Mistral OSS models, and Llama3 8B are efficient and cost-effective, while still handling many common Natural Language Processing (NLP) tasks. They're perfect for running on lower-end hardware or edge devices, where cost and speed are more important than model complexity.



### Focus on a modality, task, or tool

Language models like GPT-4 and Mistral Large are also known as **chat completion** models, designed to generate coherent and contextually appropriate text-based responses. When you need higher levels of performance in complex tasks like math, coding, science, strategy, and logistics, you can also use **reasoning** models like DeepSeek-R1 and o1.

Beyond text-based AI, some models are **multi-modal**, meaning they can process images, audio, and other data types alongside text. Models like GPT-4o and Phi3-vision are capable of analyzing and generating both text and images. Multi-modal models are useful when your application needs to process and understand images, such as in computer vision or document analysis. Or when you want to build an AI app that interacts with visual content, such as a digital tutor explaining images or charts.

If your use case involves **generating images**, tools like DALL·E 3 and Stability AI can create realistic visuals from text prompts. Image generation models are great for designing marketing materials, illustrations, or digital art.

Another group of task-specific models are **embedding models** like Ada and Cohere. Embeddings models convert text into numerical representations and are used to improve search relevance by understanding semantic meaning. These models are often implemented in **Retrieval Augmented Generation** (**RAG**) scenarios to enhance recommendation engines by linking similar content.

When you want to build an application that interacts with other software tools dynamically, you can add **function calling** and **JSON support**. These capabilities allow AI models to work efficiently with structured data, making them useful for automating API calls, database queries, and structured data processing.3

### Specialize with regional and domain-specific models

Certain models are designed for specific languages, regions, or industries. These models can outperform general-purpose generative AI in their respective domains. For example:

- <font color='red'>Core42 JAIS</font> is an Arabic language LLM, making it the best choice for applications targeting Arabic-speaking users.
- <font color='red'>Mistral Large </font>has a strong focus on European languages, ensuring better linguistic accuracy for multilingual applications.
- <font color='red'>Nixtla TimeGEN-1</font> specializes in time-series forecasting, making it ideal for financial predictions, supply chain optimization, and demand forecasting.

If your project has regional, linguistic, or industry-specific needs, these models can provide more relevant results than general-purpose AI.



### Balance flexibility and performance with open versus proprietary models

You also need to decide whether to use open-source models or proprietary models, each with its own advantages.

**Proprietary models** are best for cutting-edge performance and enterprise use. Azure offers models like OpenAI’s GPT-4, Mistral Large, and Cohere Command R+, which deliver industry-leading AI capabilities. These models are ideal for businesses needing enterprise-level security, support, and high accuracy.

**Open-source models** are best for flexibility and cost-efficiency. There are hundreds of open-source models available in the Azure AI Foundry model catalog from Hugging Face, and models from Meta, Databricks, Snowflake, and Nvidia. Open models give developers more control, allowing fine-tuning, customization, and local deployment.

Whatever model you choose, you can use the Azure AI Foundry model catalog. Using models through the model catalog meets the key enterprise requirements for usage:

- **Data and privacy**: you get to decide what happens with your data.
- **Security and compliance**: built-in security.
- **Responsible AI and content safety**: evaluations and content safety.

Now you know the language models that are available to you, you should have an understanding of whether AI can indeed solve your use case. If you think a language model would enrich your application, you then need to select the specific model that you want to deploy and integrate.

## How do I *select* the best model for my use case?

To select the best language model for you use case, you need to decide on what criteria you're using to filter the models. The criteria are the necessary characteristics you identify for a model. Four characteristics you can consider are:

- **Task type**: What type of task do you need the model to perform? Does it include the understanding of only text, or also audio, or video, or multiple modalities?
- **Precision**: Is the base model good enough or do you need a fine-tuned model that is trained on a specific skill or dataset?
- **Openness**: Do you want to be able to fine-tune the model yourself?
- **Deployment**: Do you want to deploy the model locally, on a serverless endpoint, or do you want to manage the deployment infrastructure?

You already explored the various types of models available in the previous section. Now, let's explore in more detail how precision and performance can be important filters when choosing a model.



### Filter models for precision

In generative AI, precision refers to the accuracy of the model in generating correct and relevant outputs. It measures the proportion of true positive results (correct outputs) among all generated outputs. High precision means fewer irrelevant or incorrect results, making the model more reliable.

When integrating a language model into an app, you can choose between a base model or a fine-tuned model. A base model, like GPT-4, is pretrained on a large dataset and can handle various tasks but can lack precision for specific domains. Techniques like prompt engineering can improve this, but sometimes fine-tuning is necessary.

A fine-tuned model is trained further on a smaller, task-specific dataset to improve its precision and ability to generate relevant outputs for specific applications. You can either use a fine-tuned model or fine-tune a model yourself.



### Filter models for performance

You can evaluate your model performance at different phases, using various evaluation approaches.

| Benchmark          | Description                                                  |
| :----------------- | :----------------------------------------------------------- |
| **Accuracy**       | Compares model-generated text with correct answer according to the dataset. Result is one if generated text matches the answer exactly, and zero otherwise. |
| **Coherence**      | Measures whether the model output flows smoothly, reads naturally, and resembles human-like language. |
| **Fluency**        | Assesses how well the generated text adheres to grammatical rules, syntactic structures, and appropriate usage of vocabulary, resulting in linguistically correct and natural-sounding responses. |
| **Groundedness**   | Measures alignment between the model's generated answers and the input data. |
| **GPT Similarity** | Quantifies the semantic similarity between a ground truth sentence (or document) and the prediction sentence generated by an AI model. |
| **Quality index**  | A comparative aggregate score between 0 and 1, with better-performing models scoring a higher value |
| **Cost**           | The cost of using the model based on a price-per-token. Cost is a useful metric with which to compare quality, enabling you to determine an appropriate tradeoff for your needs. |



To evaluate how a selected model performs regarding your specific requirements, you can consider **manual** or **automated** evaluations. 

<font color='red'>Manual evaluations</font> allow you to rate your model's responses. 

<font color='red'>Automated evaluations</font> include traditional machine learning metrics and AI-assisted metrics that are calculated and generated for you.

When you evaluate a model’s performance, it's common to start with <font color='red'>manual evaluations</font>, **as they quickly assess the quality of the model’s responses**. For more systematic comparisons, automated evaluations using metrics like precision, recall, and F1 score based on your own ground truth offer a faster, scalable, and more objective approach.



## Can I *scale* for real-world workloads?

You selected a model for your use case and have successfully built a prototype. Now, you need to understand how to scale for real-world workloads.

Considerations for scaling a generative AI solution include:

- **Model deployment**: Where will you deploy the model for the best balance of performance and cost?
- **Model monitoring and optimization**: How will you monitor, evaluate, and optimize model performance?
- **Prompt management**: How will you orchestrate and optimize prompts to maximize the accuracy and relevance of generated responses?
- **Model lifecycle**: How will you manage model, data, and code updates as part of an ongoing *Generative AI Operations* (GenAIOps) lifecycle?

<font color='red'>**Azure AI Foundry**</font> provides visual and code-first tools that can help you build and maintain a scalable generative AI solution.



# Deploy a model to an endpoint

## Why deploy a model?

1. An API request is sent to the endpoint.

2. The endpoint specifies the model that processes the request.

3. The result is sent back to the app through an API response.

   

## Deploy a language model with Azure AI Foundry

The associated cost depends on the type of model you deploy, which deployment option you choose, and what you are doing with the model:

|                  | Standard deployment                                          | Serverless compute                        | Managed compute              |
| :--------------- | :----------------------------------------------------------- | :---------------------------------------- | :--------------------------- |
| Supported models | Azure AI Foundry models (including Azure OpenAI models and Models-as-a-service models) | Foundry Models with pay-as-you-go billing | Open and custom models       |
| Hosting service  | Azure AI Foundry resource                                    | AI Project resource in a hub              | AI Project resource in a hub |
| Billing basis    | Token-based billing                                          | Token-based billing                       | Compute-based billing        |



# Optimize model performance

Let's explore how you can use prompt engineering techniques to optimize your model's performance.

## Apply prompt patterns to optimize your model's output

The quality of the questions you send to the language model, directly influences the quality of the responses you get back. You can carefully construct your question, or **prompt**, to receive better and more interesting responses. The process of designing and optimizing prompts to improve the model's performance is also known as **prompt engineering**.

**Prompt engineering requires users to ask relevant, specific, unambiguous, and well-structured questions, instructing the model to generate more accurate responses.** 

To understand how to create well-defined prompts, let's explore some patterns that help you improve the output of a model:

- Instruct the model to act as a persona.
- Guide the model to suggest better questions.
- Provide a template to generate output in a specific format.
- Understand how a model reasons by asking it to reflect.
- Add context to improve the accuracy of the model's output.

### Instruct the model to act as a persona

| No persona specified | With persona specified                                       |                                                              |
| :------------------- | :----------------------------------------------------------- | ------------------------------------------------------------ |
| System prompt        | *None*                                                       | You're a seasoned marketing professional that writes advertising copy for an audience of technical customers. |
| User prompt          | Write a one-sentence description of a CRM product.           | Write a one-sentence description of a CRM product.           |
| Model response       | A CRM product is a software tool designed to manage a company's interactions with current and potential customers, encompassing sales, marketing, customer service, and technical support. | Experience seamless customer relationship management with our CRM product, designed to streamline your business operations, enhance customer interactions, and drive sales growth with its intuitive interface and robust analytics tools. |

You can **create different personas for various business roles.** Think of roles like a product manager, data analyst, customer service expert, or teacher. Define the persona and add more detail to what you expect that persona to know or do to get tailored, context-driven responses.

### Ask for better question suggestions

|                | No suggestions given                                         | With suggestions given                                       |
| :------------- | :----------------------------------------------------------- | ------------------------------------------------------------ |
| System prompt  | You're an AI chef who can advise on menus.                   | You're an AI chef who can advise on menus. <font color='red'>You're approachable and always want to provide the best advice you can.</font> |
| User prompt    | I have to host a dinner party for four people. What should I cook? | I have to host a dinner party for four people. What should I cook? <font color='red'>What other information do you need to help me plan a great meal for my guests?</font> |
| Model response | Hosting a dinner party for four is a wonderful opportunity to showcase your culinary skills. Here's a suggested three-course menu that balances flavors and provides a pleasant dining experience: <br /> <br />*Appetizer* <br />**Caprese Salad Skewers** <br />- *Ingredients*: Cherry tomatoes, fresh mozzarella balls, fresh basil leaves, balsamic glaze, olive oil, salt, and pepper. - *Instructions*: Thread a cherry tomato, a basil leaf, and a mozzarella ball onto small skewers. Drizzle with olive oil and balsamic glaze, then season with salt and pepper. This dish is light, refreshing, and easy to prepare ahead of time.  <br /><br />*Main Course* <br />**Herb-Crusted Salmon with Lemon Asparagus** <br />- *Ingredients*: Salmon fillets, fresh herbs (such as parsley, dill, and thyme), breadcrumbs, lemon, asparagus, olive oil, salt, and pepper. - *Instructions*: Preheat your oven to 400°F (200°C). Mix breadcrumbs with chopped fresh herbs and a bit of olive oil to form a paste. Press this mixture onto the salmon fillets and season with salt and pepper. Place salmon on a baking sheet and bake for about 15-20 minutes, or until cooked through. In the last 10 minutes of cooking, toss asparagus with olive oil, lemon zest, salt, and pepper, and roast alongside the salmon. Serve with a squeeze of fresh lemon juice over the salmon and asparagus.  <br /><br />*Dessert* <br />**Chocolate Mousse with Fresh Berries** <br />-*Ingredients*: Dark chocolate, eggs, sugar, heavy cream, vanilla extract, and mixed berries (such as strawberries, blueberries, and raspberries). - *Instructions*: Melt the chocolate over a double boiler, then let it cool slightly. Separate egg yolks and whites. Whip the egg whites to soft peaks, then gradually add sugar to make a meringue. Whip the heavy cream until soft peaks form and mix in vanilla extract. Fold the melted chocolate into the egg yolks, then gently fold in the whipped cream and meringue until combined. Spoon the mousse into serving dishes and refrigerate for at least 2 hours. Serve topped with fresh berries for a burst of color and freshness.  <br /><br />**Additional Tips** - *Pairings*: Consider serving a light white wine with the appetizer and main course, and perhaps a dessert wine with the chocolate mousse. - *Timing*: Prepare the appetizer and dessert in advance to minimize last-minute stress. <br /><br />The main course will take the most time in the oven, so plan accordingly.  This menu is designed to be elegant yet approachable, ensuring your guests enjoy both the food and the experience. Enjoy your dinner party! | Hosting a dinner party is a wonderful opportunity to showcase your culinary skills and create memorable experiences for your guests. To help you plan a great meal, here are a few questions that can guide you in choosing the perfect menu: <br /><br />**Dietary Preferences/Restrictions**:<br />Are any of your guests vegetarian, vegan, gluten-free, or have any food allergies or intolerances? Knowing this will help in selecting dishes that everyone can enjoy.<br />**Flavor Preferences**: Do your guests have any favorite cuisines or flavors? For example, do they enjoy Italian, Mexican, Mediterranean, or perhaps something more adventurous like Thai or Indian?<br />**Time and Skill Level**: How much time do you have to prepare the meal, and what is your comfort level in the kitchen? Are you looking for a simple meal or are you up for something more elaborate?<br />**Occasion**: Is this a casual get-together, a celebration, or something more formal? The nature of the event might influence the menu style.<br />**Seasonal Ingredients**: Are you interested in using seasonal ingredients? This can help in choosing fresh and flavorful produce.<br />**Drinks Pairing**: Would you like to include alcoholic or non-alcoholic beverages to pair with the meal? With this information, I can suggest a tailored menu. Here’s a general idea that can be adapted based on your answers:  <br /><br />**Starter**<br />Garden Salad with Citrus Vinaigrette**: Fresh greens, seasonal vegetables, and a light citrus dressing.**<br />Stuffed Mushrooms**: For a vegetarian option, filled with herbs and cheese. **<br /><br />**Main Course** <br />**Herb-Crusted Chicken Breast**: Served with roasted vegetables.<br />**Quinoa Stuffed Bell Peppers**: A flavorful vegetarian or vegan option. <br /><br />**Side Dishes** <br />**Garlic Butter Roasted Potatoes**: Classic and comforting.<br />**Steamed Green Beans with Almonds**: A simple, healthy side. <br /><br />**Dessert** <br />**Chocolate Lava Cake**: A decadent treat to end the meal.<br />**Fruit Tart**: A lighter, refreshing option. <br /><br />**Drinks** <br />**Wine Pairing**: A versatile white wine like Sauvignon Blanc or a light red like Pinot Noir.<br />**Mocktail Option**: A refreshing citrus mocktail or sparkling water with herbs.  <br /><br /><br />Feel free to share more details, and I can help refine the menu further! |

When you encourage the model to suggest clarifications or extra details can help you ask the right questions and achieve better, more accurate answers in fewer interactions.

### Specify the desired format for responses

When you want the model to generate output in a specific format, you can provide a template or structure in your prompt.

For example, if you're a sports reporting composing a historical article, you can request that the model follow a specific template, which includes headings, bullet points, and data breakdowns.

![Snipaste_08-08-44](C:\Users\c\Desktop\备份\Snipaste_08-08-44.png)



### Ask for an explanation of reasoning

When you want the model to explain the reasoning behind its answers, you can ask the model to automatically reflect on its rationale and assumptions after providing a response.

For example, if you're working on a mathematical problem, you can ask the model to explain the reasoning behind specific calculations.

![Snipaste_08-10-12](C:\Users\c\Desktop\备份\Snipaste_08-10-12.png)



### Add context

When you want the model to focus on specific topics, you can specify the context to consider. You can also tell the model to ignore irrelevant information.

For example, if you're planning a trip, you can provide the model with more context to help improve the relevance of its response.

![Snipaste_08-17-15](C:\Users\c\Desktop\备份\Snipaste_08-17-15.png)

By defining what the model should focus on or disregard, you can ensure the conversation stays on track and generate more relevant, tailored responses.

You can specify the context by describing what it should or shouldn't include, and by connecting the model to data sources it should retrieve context from before generating an answer.

## Apply model optimization strategies

Prompt engineering can be an effective way to optimize model responses, but in some cases it may not provide sufficient context or guidance to always meet your exact needs. As a developer, you can consider the following additional optimization strategies to improve the relevance of your generative AI application's responses:

- **Retrieval Augmented Generation (RAG)**: A technique that involves using a data source to provide *grounding* context to prompts. RAG can be a useful approach when you need the model to answer questions based on a specific knowledge domain or when you need the model to consider information related to events that occurred after the training data on which the model is based.

  一种通过数据源为提示提供背景信息的技术。当需要模型基于特定知识领域回答问题，或需要模型考虑其训练数据之外发生的事件相关信息时，RAG技术可以成为一种有效的方法。

- **Fine-tuning**: A technique that involves extending the training of a foundation model by providing example prompts and responses that reflect the desired output format and style.

Both of these approaches involve additional cost, complexity, and maintainability challenges, so as a general rule it's best to start your optimization efforts through prompt engineering, and then consider additional strategies if necessary.

The strategy you should choose as a developer depends on your requirements:

![](https://learn.microsoft.com/en-us/training/wwl-data-ai/explore-models-azure-ai-studio/media/model-optimization.png)

- **Optimize for context**: When the model lacks contextual knowledge and you want to **maximize responses accuracy**.
- **Optimize the model**: When you want to improve the response format, style, or speech by **maximizing consistency of behavior**.

To optimize for context, you can apply a **Retrieval Augmented Generation** (**RAG**) pattern. With RAG, you *ground* your data by first retrieving context from a data source before generating a response. For example, you want employees to ask questions about expense claim processes and limits based on your own corporation's expenses policy documentation.

When you want the model to respond in a specific style or format, you can instruct the model to do so by adding guidelines in the system message. When you notice the model's behavior isn't consistent, you can further enforce consistency in behavior by **fine-tuning** a model. With fine-tuning, you train a base language model on a dataset of example prompts and responses before integrating it in your application, with the result that the fine-tuned model will produce responses that are consistent with the examples in the fine-tuning training dataset.

You can use any combination of optimization strategies, for example prompt engineering, RAG *and* a fine-tuned model, to improve your language application.