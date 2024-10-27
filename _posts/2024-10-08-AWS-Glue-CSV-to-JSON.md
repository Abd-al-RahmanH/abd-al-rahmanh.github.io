---
title: "AWS Glue: Convert CSV to JSON using Lambda - A Practical Guide"
excerpt: "Explore AWS Glue components and implement a real-world project that converts CSV to JSON using AWS Lambda and S3."
date: 2024-10-08
header:
  image: "../assets/images/posts/2024-10-08-AWS-Glue-CSV-to-JSON/cover.jpg"
  teaser: "../assets/images/posts/2024-10-08-AWS-Glue-CSV-to-JSON/cover.jpg"
  caption: "Effortlessly transform your data with AWS Glue and Lambda. - Abdul Rahman"
  categories: [AWS, Big Data, AWS Glue, Lambda, S3]
---

## 🌟 Introduction to AWS Glue

AWS Glue is a fully managed ETL (Extract, Transform, Load) service provided by Amazon Web Services. It simplifies the process of discovering, preparing, and combining data for analytics, machine learning, and application development.

### Key Components of AWS Glue

1. **AWS Glue Data Catalog** 📚  
   - Acts as a centralized repository to store metadata about your datasets.
    
2. **Crawlers** 🕵️‍♂️  
   - Automatically scan data sources and store metadata in the Data Catalog.
  
3. **ETL Jobs** 🔧  
   - Allow transformation of raw data into structured formats, such as CSV to JSON.

4. **Triggers** ⏲️  
   - Automate the execution of ETL jobs based on schedules or events.

5. **Development Endpoints** 💻  
   - Provide an environment for testing and developing ETL scripts.

---

## 💡 AWS Glue Project: Convert CSV to JSON in S3 using Lambda

In this project, we’ll build an automated pipeline to convert CSV files stored in an S3 bucket into JSON format using **AWS Glue** and trigger the ETL process using **AWS Lambda**.

### 🗺️ Overview of the Process

1. **S3 Buckets** 🪣: Set up source, destination, and script buckets.
2. **AWS Glue Job** 🛠️: Create a Glue job to handle the conversion of CSV to JSON.
3. **AWS Lambda Function** ⚡: Trigger the job based on file uploads.
4. **Monitoring** 📊: Track the process with CloudWatch logs.

---

### 📂 Step 1: Set Up S3 Buckets

1. Go to the **S3 Console**.
2. Create three buckets:
   - `source-csv-bucket`
   - `destination-json-bucket`
   - `glue-script-bucket`

![S3 Icon](https://github.com/Abd-al-RahmanH/AWS-Data-Engineering/blob/main/Projects/AWS%20Glue%20Convert%20CSV%20to%20JSON%20in%20S3%20using%20Lambda/assets/images/1.jpg?raw=true)

---

### 🛠️ Step 2: Create AWS Glue ETL Job

1. Navigate to the **AWS Glue Console**.
2. Create a new job:
   - **Source**: `source-csv-bucket`, format CSV.
   - **Target**: `destination-json-bucket`, format JSON.
   - **Script Path**: Stored in the `glue-script-bucket`.

![glue](https://github.com/Abd-al-RahmanH/AWS-Data-Engineering/blob/main/Projects/AWS%20Glue%20Convert%20CSV%20to%20JSON%20in%20S3%20using%20Lambda/assets/images/2.jpg?raw=true)

---

### ⚡ Step 3: Set Up AWS Lambda Trigger

1. Go to **AWS Lambda Console**.
2. Create a function named `csv_to_json` and add an **S3 Trigger** for `source-csv-bucket` with event type as `PUT` for `.csv` files.
3. Use this Python code to start the Glue job:

   ```python
   import boto3
   glueClient = boto3.client('glue')

   def lambda_handler(event, context):
       glueClient.start_job_run(JobName="csv_to_json")
       return "Job started"
   ```

![Lambda Icon](https://github.com/Abd-al-RahmanH/AWS-Data-Engineering/blob/main/Projects/AWS%20Glue%20Convert%20CSV%20to%20JSON%20in%20S3%20using%20Lambda/assets/images/3.jpg?raw=true)

---

**IAM Permissions**:
   - Ensure that the Lambda IAM role has the following permissions:
     - `AWSGlueConsoleFullAccess`
     - `AmazonS3FullAccess`
     - `AWSLambdaBasicExecutionRole`

![AWS IAM Permissions](https://github.com/Abd-al-RahmanH/AWS-Data-Engineering/blob/main/Projects/AWS%20Glue%20Convert%20CSV%20to%20JSON%20in%20S3%20using%20Lambda/assets/images/4.jpg?raw=true)

### 🔍 Step 4: Monitor the Pipeline

- Use **CloudWatch Logs** to monitor the Lambda execution and Glue job status.
- AWS Glue Console will provide job status updates.

![CloudWatch Icon](https://github.com/Abd-al-RahmanH/AWS-Data-Engineering/blob/main/Projects/AWS%20Glue%20Convert%20CSV%20to%20JSON%20in%20S3%20using%20Lambda/assets/images/5.jpg?raw=true)

---

## 🎉 Conclusion

By following this guide, you’ve successfully set up an automated ETL pipeline using **AWS Glue**, **Lambda**, and **S3**. This architecture ensures that every CSV file uploaded to the source bucket is automatically converted into JSON, providing seamless data transformation. Expand this project by adding more complex ETL tasks or integrating AWS Step Functions for advanced workflows.

---
