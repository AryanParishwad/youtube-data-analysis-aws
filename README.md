# 📊 YouTube Data Analysis ETL Pipeline on AWS

> This project demonstrates an end-to-end, serverless ETL (Extract, Transform, Load) pipeline built on Amazon Web Services (AWS). The pipeline extracts data from the YouTube Data API, processes it, and loads it into a data lake, where it can be queried and visualized to gain insights into YouTube channel performance.

## ⚙️ Project Overview

The goal of this project is to automate the process of collecting and analyzing YouTube channel statistics. By leveraging a serverless architecture, the pipeline is cost-effective, scalable, and requires minimal operational overhead.

## 🏗️ Architecture

The pipeline follows a standard ETL workflow using various AWS services. The data flows from scheduling to visualization seamlessly.

1.  **Scheduling (`Amazon EventBridge`):** An EventBridge rule is configured to trigger the data extraction process on a recurring schedule (e.g., daily).
2.  **Extraction (`AWS Lambda` & `YouTube Data API`):** The EventBridge rule invokes a Python-based Lambda function. This function calls the YouTube Data API to fetch raw channel statistics (like views, subscribers, and video details) and saves the data as JSON files in a "raw data" S3 bucket.
3.  **Data Cataloging (`AWS Glue Crawler`):** A Glue Crawler runs on the raw data S3 bucket to automatically infer the schema and populate the AWS Glue Data Catalog.
4.  **Transformation (`AWS Glue ETL Job`):** A Glue ETL job, written in PySpark, is triggered after the crawler successfully runs. This job reads the raw JSON data, cleans it, transforms it into a structured format (Parquet), and writes the processed data to a "processed data" S3 bucket.
5.  **Querying (`Amazon Athena`):** Another Glue Crawler updates the Data Catalog with the schema of the processed Parquet files. Amazon Athena is then used to run standard SQL queries directly on the processed data stored in S3.
6.  **Visualization (`Amazon QuickSight`):** Amazon QuickSight is connected to Athena to create interactive dashboards and visualizations, allowing for easy analysis of the YouTube channel data.

## 🛠️ Technologies Used

-   **Data Ingestion:** `YouTube Data API v3`, `Python`
-   **Cloud Platform:** `Amazon Web Services (AWS)`
-   **Services:**
    -   **Compute:** `AWS Lambda`
    -   **Storage:** `Amazon S3`
    -   **ETL:** `AWS Glue (Crawlers and ETL Jobs)`
    -   **Data Querying:** `Amazon Athena`
    -   **Scheduling:** `Amazon EventBridge`
    -   **BI & Visualization:** `Amazon QuickSight`
    -   **Security & Access:** `AWS IAM`

## 🚀 How to Set Up

To replicate this project, you will need an AWS account and a YouTube API key.

1.  **S3 Buckets:** Create two S3 buckets: one for raw data and one for processed data.
2.  **IAM Roles:** Configure the necessary IAM roles with policies that grant permissions for Lambda, Glue, and S3 to interact with each other.
3.  **Lambda Function:** Create a Lambda function with the provided Python script (`lambda_function.py`) and configure its dependencies and environment variables (including your YouTube API key).
4.  **Glue Crawlers & Job:** Set up two Glue Crawlers (one for each S3 bucket) and one Glue ETL job to handle the data transformation.
5.  **EventBridge Trigger:** Create an EventBridge rule to trigger the Lambda function on your desired schedule.
6.  **Athena & QuickSight:** Configure Athena to query the processed data and connect QuickSight to Athena to build your dashboards.

## 📈 Dashboard Preview

*![QuickSight Dashboard Preview](https://github.com/YourUsername/YourRepositoryName/blob/main/dashboard-preview.png?raw=true)*
