# Weather-Data-Analysis-Project
***
## Project Overview
This project is an overview of an Event Driven Sales Data Projection data pipeline that Process the Orders data based on their Status and route towards DynamoDB or SQS as per the Business requirement rules.
An airline daily data ingestion project using S3, S3 Cloudtrail Notification, Event Bridge Pattern Rule, Glue Crawler, Glue Visual ETL, SNS, Redshift, and Step Function

***

## Architectural Diagram
![AirlineProject](https://github.com/yash872/Airline-Data-Ingestion-Project/blob/main/Images/AirlineProject.jpg)

***

## Key Steps
### 1. Create a S3 bucket
- we will create a S3 bucket "airflow-managed-yb" to store the airflow scripts under dags folder and requirement.txt.
![S3](https://github.com/yash872/Weather-Data-Analysis-Project/blob/main/Images/S3_before.JPG)


### 2. Create a Codebuild Project
- we will create a CodeBuild Project "weather-cicd" for the CICD setup which will copy the dags script and othe files to the S3 on the pull merge request.
![S3](https://github.com/yash872/Weather-Data-Analysis-Project/blob/main/Images/CodeBuild.JPG)