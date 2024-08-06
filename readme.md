# YouTube Data Engineering and Analysis Pipeline

## Project Overview

This project aims to analyze YouTube data to help a client optimize their social media advertising strategy. The goals are to identify popular video categories, understand factors affecting video popularity, and provide actionable insights through data-driven decisions.

## Table of Contents

1. [Project Goals and Success Criteria](#project-goals-and-success-criteria)
2. [AWS Services Used](#aws-services-used)
3. [Step-by-Step Process](#step-by-step-process)
    - [IAM Setup](#iam-setup)
    - [S3 Setup and Data Upload](#s3-setup-and-data-upload)
    - [Data Processing with AWS Glue](#data-processing-with-aws-glue)
    - [Automated Data Processing with AWS Lambda](#automated-data-processing-with-aws-lambda)
    - [Data Analysis with AWS QuickSight](#data-analysis-with-aws-quicksight)
4. [Conclusion](#conclusion)
5. [License](#license)

## Project Goals and Success Criteria

- **Goals**:
  - Identify top video categories on YouTube.
  - Understand factors influencing video popularity.
  - Provide actionable insights for strategic decision-making.
- **Success Criteria**:
  - Efficient data ingestion.
  - Robust ETL processes.
  - Scalable data infrastructure.
  - Insightful reporting.

## AWS Services Used

- **Amazon S3**: Scalable and secure data storage.
- **AWS IAM**: Access and permissions management.
- **AWS Glue**: Automated data discovery, ETL processes, and data cataloging.
- **AWS Lambda**: Serverless data processing and automation.
- **AWS QuickSight**: Interactive dashboards and visualizations.

## Step-by-Step Process

### IAM Setup

1. **Create IAM User**:
    - Log in to AWS Management Console with root credentials.
    - Navigate to IAM service, create a new IAM user with specific permissions.
    - Assign the user to an appropriate group (e.g., Administrators) and attach necessary policies.
    - Generate access keys for programmatic access if required.

2. **Best Practices**:
    - Use IAM users instead of the root account for everyday tasks to enhance security.

### S3 Setup and Data Upload

1. **Create S3 Bucket**:
    - Create an S3 bucket to store raw data.
    - Enable server-side encryption for security.
    - Attach necessary bucket policies to control access.

2. **Upload Data**:
    - Use AWS CLI to upload data to S3:
    ```bash
    aws s3 cp . s3://YOUR_BUCKET_NAME/youtube/raw_statistics_reference_data/ --recursive --exclude "*" --include "*.json"
    aws s3 cp CAvideos.csv s3://YOUR_BUCKET_NAME/youtube/raw_statistics/region=ca/
    aws s3 cp DEvideos.csv s3://YOUR_BUCKET_NAME/youtube/raw_statistics/region=de/
    # Repeat for other regions
    ```

### Data Processing with AWS Glue

1. **Set Up Glue Crawlers**:
    - Create a crawler to discover data in S3 and populate the Glue Data Catalog.
    - Configure the crawler to run on a schedule.

2. **Create ETL Jobs**:
    - Use AWS Glue Studio to create ETL jobs.
    - Join DataFrames on `category_id` and `id` columns.
    - Save the transformed data back to S3 in a structured format.

### Automated Data Processing with AWS Lambda

1. **Create Lambda Function**:
    - Write a Python script to process new incoming data and store it in cleansed S3 buckets.
    - Set up IAM roles with permissions to access AWS Glue and S3.

2. **Invoke Lambda Function**:
    - Configure triggers to invoke the Lambda function on new data uploads to S3.

### Data Analysis with AWS QuickSight

1. **Set Up QuickSight**:
    - Connect to the processed data in S3.
    - Prepare and import the data set into QuickSight.

2. **Create Dashboard**:
    - Build various visualizations to answer key questions:
        - Bar charts for top video categories.
        - Line charts for trend analysis.
        - Heat maps and geospatial charts for regional insights.
        - Tables for detailed engagement metrics.

3. **Share Dashboard**:
    - Save and publish the dashboard.
    - Share with stakeholders for data-driven decision-making.

## Conclusion

This end-to-end YouTube data engineering project demonstrates how to leverage AWS services to build a scalable, automated, and insightful data pipeline. By integrating various AWS tools, we efficiently ingested, processed, and analyzed large datasets, providing actionable insights to optimize social media advertising strategies.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
