---
title: "How to connect Watsonx to Watsonx Assistant"
excerpt: "How to connect Watsonx to WatsonX Assistant ?"

header:
  image: "../assets/images/posts/2024-08-12-How-to-connect-Watsonx-Assistant-to-WatsonX/cover.png"
  teaser: "../assets/images/posts/2024-08-12-How-to-connect-Watsonx-Assistant-to-WatsonX/cover.png"
  caption: "A year spent in artificial intelligence is enough to make one believe in God. —Alan Perlis"
  
---
## Introduction
**Watsonx** is IBM's platform that helps businesses use Data and AI. It includes tools for training, testing, and using AI, especially generative AI through Large Language Models (LLMs) in the **watsonx.ai** part of the platform. One of the features of **IBM watsonx Assistant** is how easily it can connect to AI services like **watsonx.ai**. This guide will show you how to set up this connection.

This tutorial gives a simple example of how to integrate these two services. If you want to learn more about all the features of **watsonx Assistant**, check out the [Official documentation](https://cloud.ibm.com/docs/watson-assistant?topic=watson-assistant-welcome-new-assistant).  

If you have questions about connecting a virtual assistant with generative AI, feel free to ask in the [discussion forum](#).

---

## Prerequisites

To follow this tutorial, you'll need:

- An [**IBM watsonx Assistant**](https://cloud.ibm.com/catalog/services/watsonx-assistant) instance on IBM Cloud. Even the free version will work.
- Access to a [**watsonx.ai**](https://eu-de.dataplatform.cloud.ibm.com/registration/stepone?context=wx?cm_sp=ibmdev-_-developer-_-trial&utm_source=ibm_developer&utm_content=in_content_link&utm_id=tutorials_integrate-your-watson-assistant-chatbot-with-watsonxai-for-generative-ai&preselect_region=true) project.

### Estimated Time

This tutorial will take about **20 minutes** to complete.

---

## Steps

### Step 1: Get the OpenAPI Definition for Watsonx.ai

Before connecting **watsonx.ai** to **watsonx Assistant**, you need the OpenAPI file for the **watsonx.ai** service. You can find a sample version in the [assistant toolkit GitHub repository](https://github.com/watson-developer-cloud/assistant-toolkit/tree/master/integrations/extensions/starter-kits/language-model-watsonx). Download the modified version of the **watsonx-openapi.json** file to your computer.

### Step 2: Add an Empty Virtual Assistant

Create a new virtual assistant in **watsonx Assistant** for testing. If you don't already have an assistant, use the **Create Assistant** wizard and name it *Watsonx Integration*. Set the deployment location to *web*.

### Step 3: Create an API Key for Watsonx.ai

If you already have an API key for **watsonx.ai**, you can skip this step.

Otherwise, log in to **watsonx.ai**, ensure you are using the same account as your **Watson Machine Learning** instance, and follow these steps:

1. Go to **Manage access and users > API Keys**.
2. Click **Create**, give it a name like *watsonx-apikey*, and provide a description.

![](../assets/images/posts/2024-08-12-How-to-connect-Watsonx-Assistant-to-WatsonX/1.jpg)

3. Click **Create** and make sure to copy and save the API key, as you won’t be able to see it again.

### Step 4: Get Your Watsonx.ai Project ID

In **watsonx.ai**, open the menu, go to **Projects**, and select your project. Under the **Manage** tab, find and copy your **Project ID**. You can save it in a notepad as it's not sensitive information like the API key.

![](../assets/images/posts/2024-08-12-How-to-connect-Watsonx-Assistant-to-WatsonX/2.jpg)

### Step 5: Add Watsonx.ai to Your Assistant

In **watsonx Assistant**, go to the **Integrations** panel on the left side, scroll down to **Extensions**, and click **Build Custom Extension**.

![](../assets/images/posts/2024-08-12-How-to-connect-Watsonx-Assistant-to-WatsonX/3.jpg)

Follow the steps below:

1. Name the extension *Watsonx* and give it a description (optional).
2. Upload the **watsonx-openapi.json** file that you downloaded earlier.

![](../assets/images/posts/2024-08-12-How-to-connect-Watsonx-Assistant-to-WatsonX/4.jpg)
3. Complete the setup by following the prompts.Add the created Extension

![](../assets/images/posts/2024-08-12-How-to-connect-Watsonx-Assistant-to-WatsonX/5.jpg)
4. You will be using **OAuth 2.0** authentication add your **API key** in custom api key field.

![](../assets/images/posts/2024-08-12-How-to-connect-Watsonx-Assistant-to-WatsonX/6.jpg)

Once the extension is added, you can use it in your assistant.

### Step 6: Create an Action for Watsonx.ai

Now, you can create an action in **watsonx Assistant** to generate AI responses. Here's how to do it:

1. In the **Actions** panel, click **Create Action**.
2. Select **Start from Scratch** and name it *Share Market*.

![](../assets/images/posts/2024-08-12-How-to-connect-Watsonx-Assistant-to-WatsonX/7.jpg)
3. Click the pencil icon to set a step title. Use Prompt for a prompt as the title.

![](../assets/images/posts/2024-08-12-How-to-connect-Watsonx-Assistant-to-WatsonX/8.jpg)
4. Set the user response to **Free Text Input**.

Then Create new step, you'll connect this action to **watsonx.ai**.

5. Use the **watsonx** extension and configure the parameters:

![](../assets/images/posts/2024-08-12-How-to-connect-Watsonx-Assistant-to-WatsonX/9.jpg)
Then configure the extension as Generation and the parameters and optional parameters

![](../assets/images/posts/2024-08-12-How-to-connect-Watsonx-Assistant-to-WatsonX/10.jpg)
![](../assets/images/posts/2024-08-12-How-to-connect-Watsonx-Assistant-to-WatsonX/11.jpg)

   - **Model ID**: `meta-llama/llama-3-405b-instruct`
   - **Project ID**: Use the Project ID you copied earlier.
   - **Temperature**: 0.8
   - **Max Tokens**: 200
   - **Min Tokens**: 50
   - **Repetition Penalty**: 2
   - **Decoding Method**: *sample*

Save your action and move to the next step.
6. In this step, select with conditions. In the with condition, click the first item, and select watsonx + watsonx Assistant  (step 2). and click Ran Successfully

![](../assets/images/posts/2024-08-12-How-to-connect-Watsonx-Assistant-to-WatsonX/12.jpg)

7. After that set new value and add new session variable as result and free text

![](../assets/images/posts/2024-08-12-How-to-connect-Watsonx-Assistant-to-WatsonX/13.jpg)

![](../assets/images/posts/2024-08-12-How-to-connect-Watsonx-Assistant-to-WatsonX/14.jpg)

8. For the variable assignment To, select Expression,a pull-down menu appears. Select watsonx + watsonx Assistant(step 2). and select body.results and append with [0].generated_text finally Its looks like    eg.2.body.results[0].generated_text.    And In Assistant says click fx select session variables and select result

![](../assets/images/posts/2024-08-12-How-to-connect-Watsonx-Assistant-to-WatsonX/15.jpg)


### Step 7: Test the Action

Test the assistant by asking it to generate a  Share market message. Enter a prompt like:

```
Create a 5-sentence for share market message for a company called BSE. Offer: No fees, 2% interest rate, no minimum balance. Tone: Informative.
```

If everything is working correctly, **watsonx.ai** will generate a marketing message based on your input.

![](../assets/images/posts/2024-08-12-How-to-connect-Watsonx-Assistant-to-WatsonX/16.jpg)

---

## Next Steps

You can further experiment with different prompts and parameters to see how the assistant responds. Try adding optional parameters like **random_seed** for more control over the generated responses.

Explore more features of **watsonx Assistant** and **watsonx.ai** to enhance your virtual assistant!
