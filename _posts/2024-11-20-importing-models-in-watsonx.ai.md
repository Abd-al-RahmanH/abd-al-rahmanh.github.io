---
title: "Importing Models and Creating Batch Deployments in IBM watsonx.ai "
excerpt: "A step-by-step guide to importing machine learning models and creating batch deployments using IBM watsonx.ai."
date: 2024-11-20
header:
  image: "../assets/images/posts/2024-11-20-importing-models-in-watsonx.ai/cover.png"
  teaser: "../assets/images/posts/2024-11-20-importing-models-in-watsonx.ai/cover.png"
  caption: "Simplify AI deployment with IBM watsonx.ai."
  categories: [AI, IBM Watson, Machine Learning]
  tags: [IBM Watson, AI Deployment, Machine Learning, Batch Processing]
---

# Introduction

IBM watsonx.ai  enables you to import machine learning models trained outside of its environment. The models can be stored in the watsonx.ai  repository (a Cloud Object Storage bucket) and optionally deployed for testing.

## Ways to Import Models

1. **Directly through the UI**
2. **By using a path to a file**
3. **By using a path to a directory**

### Steps to Import a Model Using the UI

1. Navigate to the **Assets** tab in your watsonx.ai  space.
2. Click **Import assets**.

![](../assets/images/posts/2024-11-20-importing-models-in-watsonx.ai/1.jpg)

3. Select **Local file**, then **Model**.

![](../assets/images/posts/2024-11-20-importing-models-in-watsonx.ai/2.jpg)

4. Choose the model file and click **Import**.
   - The system will automatically select a matching model type based on the version string in the file.

![](../assets/images/posts/2024-11-20-importing-models-in-watsonx.ai/3.jpg)   

### Supported Frameworks and Import Options

| Import Option                        | Spark MLlib | Scikit-learn | XGBoost | TensorFlow | PyTorch |
|--------------------------------------|-------------|--------------|---------|------------|---------|
| Importing a model object             | ✓           | ✓            | ✓       |            |         |
| Importing a model via a file path    |             | ✓            | ✓       | ✓          | ✓       |
| Importing a model via a directory    |             | ✓            | ✓       | ✓          | ✓       |

**Note:** Models in PMML format can be imported directly by uploading the `.xml` file.

---

# Creating Batch Deployments

Batch deployments process input data from files or data connections and write the output to a specified destination. Unlike online deployments, batch deployments are designed for asynchronous processing.

## Steps to Create a Batch Deployment from UI

1. Organize resources in a deployment space, adding deployable assets and data files.
2. Deploy the asset (e.g., machine learning model) with **Batch** as the deployment type.

![](../assets/images/posts/2024-11-20-importing-models-in-watsonx.ai/4.jpg)

3. Configure the batch deployment job by specifying the above in **new job**:

![](../assets/images/posts/2024-11-20-importing-models-in-watsonx.ai/5.jpg)

   - Input data location
   - Output data destination
     
   ![](../assets/images/posts/2024-11-20-importing-models-in-watsonx.ai/8.jpg)

   - Scheduling details (if needed)

   ![](../assets/images/posts/2024-11-20-importing-models-in-watsonx.ai/9.jpg)

4. Click **Create**. The status will change to **Deployed** upon successful creation.   

 ![](../assets/images/posts/2024-11-20-importing-models-in-watsonx.ai/11.jpg)

5. Run the job, which processes the input data and writes the output to the specified location.

### Supported Asset Types for Batch Deployment

- **Models**: AutoAI, Scikit-learn, TensorFlow, XGBoost, Spark MLlib, PyTorch-ONNX, PMML, SPSS Modeler
- **Scripts**: Python scripts
- **Functions**: Python functions, Decision Optimization models


### Testing Batch Deployments

1. Create a batch job from the deployment space.
2. Define the job, including input data and run schedule.
3. Run the job manually or as per the schedule.
4. View or download the output from the **Assets** page.

 ![](../assets/images/posts/2024-11-20-importing-models-in-watsonx.ai/13.jpg)

---
 
# Conclusion

IBM watsonx.ai provides powerful tools for managing AI workflows, from importing models to executing batch deployments. Use this guide to streamline your AI model deployment and processing tasks.

Happy Deploying! 🎉
