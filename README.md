# Spotify-Data-Pipeline-using-AWS
## Project Overview
This project builds an ETL pipeline using AWS services to process and analyze the Spotify Dataset (2023) from Kaggle. The pipeline performs data ingestion, transformation, and visualization using AWS Glue, Athena, and QuickSight.

## Architecture
The pipeline follows the following architecture:

S3 (Staging Area) → AWS Glue (ETL Processing) → S3 (Data Warehouse) → AWS Glue Crawler → AWS Athena (Querying Engine) → Amazon QuickSight (Visualization)
## Steps to Implement
### 1. Data Ingestion
1. Download the Spotify Dataset (2023) from Kaggle.
2. Since the dataset is in raw format, perform preprocessing to split it into three structured files.
### 2. AWS IAM Configuration
1. Log in as a Root User (not recommended for production; use an IAM admin instead).
2. Create an IAM User to securely access AWS services.
3. Assign necessary IAM policies:
AmazonS3FullAccess, 
AWSGlueFullAccess, 
AmazonAthenaFullAccess, 
AmazonQuickSightFullAccess, 
AWSQuickSightDescribeRDS
### 3. S3 Bucket Setup
1. Create an S3 bucket: spotify-aws-project
2. Inside the bucket, create two folders:
3. staging/ (for raw/preprocessed data)
4. datawarehouse/ (for transformed data)
5. Upload the preprocessed data files to the staging folder.
### 4. AWS Glue for ETL Processing
1. Navigate to AWS Glue and create a Visual ETL job.
2. Use drag-and-drop transformations to clean, filter, and merge datasets.
3. Perform inner joins on Artist and Album tables using TrackID.
4. Drop unnecessary fields and add destination tables.
### 5. AWS IAM Role for Glue
1. In IAM, create a role for Glue:
2. Assign S3FullAccess and AWSGlueFullAccess policies.
3. Name the role: glue-access-s3.
4. Attach this role to the Glue job.
### 6. AWS Glue Crawler & Data Catalog
1. Go to AWS Glue > Data Catalog > Crawlers.
2. Create a new crawler:
3. Set the data source as S3 (datawarehouse/ folder).
4. Assign the glue-access-s3 IAM role.
5. Run the crawler to generate table schemas in the Glue Data Catalog.
### 7. AWS Athena for Querying
1. Use AWS Athena to analyze data stored in S3.
2. Write SQL queries using PySpark and Spark SQL.
3. Launch the Notebook Editor in Athena for advanced analysis.
### 8. Data Visualization with QuickSight
1. Connect QuickSight to Athena for interactive dashboards.
2. Create visualizations, trends, and insights from Spotify data.
## Technologies Used
1. Storage: Amazon S3
2. ETL Processing: AWS Glue
3. Data Catalog & Querying: AWS Glue Crawlers, AWS Athena
4. Visualization: Amazon QuickSight
5. Access Management: AWS IAM
## Future Enhancements
1. Automate the pipeline using AWS Step Functions.
2. Implement real-time streaming with AWS Kinesis.
3. Add machine learning-based trend analysis on music genres.
## How to Run the Project
1. Ensure you have an AWS account with necessary permissions.
2. Follow the step-by-step implementation as outlined above.
3. Run Glue ETL jobs and Crawlers to update the Data Catalog.
4. Use Athena to query data and QuickSight for visualizations.
